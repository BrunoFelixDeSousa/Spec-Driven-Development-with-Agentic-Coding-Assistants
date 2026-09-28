# Exemplo completo: evoluir uma consulta em um legado

[Índice](../README.md) · [Guia de legado](../05-projetos-legados.md) · [Templates](../templates/README.md)

Este caso é fictício. Considere um serviço que já lista reservas e possui consumidores conhecidos. A mudança adiciona um filtro opcional por estado. Não há repositório executável nem baseline coletada neste exemplo; os contratos abaixo são premissas didáticas a confirmar no projeto real.

## Pedido inicial

“O dashboard precisa listar somente reservas ativas. Hoje recebe todas e filtra localmente. Queremos poder solicitar apenas as ativas sem quebrar as consultas existentes.”

O objetivo não é reescrever o serviço nem trocar persistência. É acrescentar um comportamento optativo, mantendo o contrato quando o filtro não é usado.

## Arquivo: `specs/legacy-assessment.md`

### Fronteira

Operação `GET /reservations`, parsing de parâmetros, consulta de persistência e dois consumidores: dashboard interno e exportação. O serviço usa o controle de acesso existente. Não serão alteradas criação, cancelamento ou regras de autorização.

### Contrato assumido para estudo

- Sem filtro, retorna uma coleção JSON de reservas com `id`, `room_id`, `status` e `starts_at`.
- Estados persistidos: `active` e `cancelled`.
- Ordenação: `id` crescente.
- Resultado sem registros: coleção vazia com status 200.
- Erro de persistência: status 503 e corpo `{"error":"service_unavailable"}`.
- A consulta não modifica registros.

### Inventário a confirmar

| Item | Premissa do caso | Evidência necessária no projeto real |
|---|---|---|
| Dashboard | Pode adotar o novo filtro | Código da chamada e teste de consumo |
| Exportação | Precisa continuar recebendo todos os estados | Teste do consumidor e execução com fixture |
| Persistência | Coluna `status` já existe | Esquema/migrações e amostra preparada |
| Valores históricos | Somente `active` e `cancelled` | Perfil dos dados e restrições existentes |
| Parâmetros desconhecidos | Comportamento existente deve ser preservado | Caracterização do parser atual |

Nenhuma linha é tratada como descoberta de um sistema real. No projeto de destino, substitua as premissas por fatos observados e registre divergências antes de implementar.

### Baseline planejada

Executar a consulta sem filtro, consulta vazia, falha de persistência, fluxo de exportação e controles de acesso existentes. Registrar revisão, comandos, ambiente e resultado. Estado: **não executado**.

Se já houver uso de `status` com significado diferente, a solução proposta exige revisão; adicionar o novo parâmetro deixaria de ser uma mudança puramente optativa.

## Arquivo: `specs/mission.md`

O serviço permite que aplicações internas consultem e gerenciem reservas. A prioridade desta evolução é reduzir filtragem duplicada no dashboard, preservando integrações existentes.

O público afetado é formado pelos usuários do dashboard e responsáveis pela exportação. O sucesso desta entrega será demonstrado pela consulta filtrada correta e pela manutenção do comportamento antigo quando não há filtro.

## Arquivo: `specs/tech-stack.md`

Manter linguagem, framework, banco e padrões atuais. A camada de entrada interpreta o parâmetro; a regra de consulta aplica o filtro; a persistência usa o mecanismo de parâmetros do projeto, sem concatenar entrada em consultas.

**Comandos:** copiar os comandos reais de baseline e testes após investigar o repositório. Nenhum comando específico é fornecido como existente neste caso fictício.

**Decisão:** não alterar esquema; a coluna `status` é uma premissa a verificar. Se precisar de migração, interromper essa suposição e revisar plano e rollout. Reutilizar convenções existentes de logs e erros, confirmando se o novo erro proposto abaixo é compatível com elas.

## Arquivo: `specs/roadmap.md`

| Fase | Resultado | Estado | Dependências |
|---|---|---|---|
| F01 | Baseline e caracterização da listagem | pendente | Acesso ao repositório e ambiente |
| F02 | Filtro opcional de estado, contrato antigo preservado | pendente | F01 e confirmação das premissas |
| F03 | Dashboard passa a enviar o filtro | pendente | Serviço publicado com suporte ao filtro |

A feature deste exemplo engloba o diagnóstico F01 e a mudança F02. A adoção pelo dashboard é uma entrega posterior. Publicar o consumidor antes do serviço poderia produzir comportamento inesperado.

## Arquivo: `specs/2026-09-28-filtrar-reservas/requirements.md`

### Objetivo e escopo

Adicionar o parâmetro opcional `status` à listagem existente. Aceitar exatamente `active` e `cancelled`. Sem o parâmetro, preservar o comportamento anterior. Não mudar corpo de sucesso, ordenação, autorização, paginação eventualmente existente ou esquema de dados. Se a investigação revelar paginação, especificar a interação entre filtro e paginação antes de implementar.

### Antes e depois

| Chamada | Antes, conforme premissa | Depois esperado |
|---|---|---|
| `GET /reservations` | Todas as reservas, ordem por ID | Mesmo contrato e conteúdo para o mesmo estado de dados |
| `GET /reservations?status=active` | Sem contrato definido para este parâmetro | Somente reservas ativas |
| `GET /reservations?status=cancelled` | Sem contrato definido para este parâmetro | Somente reservas canceladas |
| `GET /reservations?status=other` | Sem contrato definido para este parâmetro | 400, `{"error":"invalid_status"}` |

### Requisitos

| ID | Comportamento |
|---|---|
| REQ-01 | Ausência de `status` preserva a resposta anterior, incluindo ordem, campos e tipos |
| REQ-02 | Um único `status=active` ou `status=cancelled` restringe os resultados ao estado exato, mantendo ordenação e formato |
| REQ-03 | Valor vazio, desconhecido, com espaços, caixa diferente ou parâmetro repetido retorna 400 com `invalid_status`, sem executar a consulta de dados |
| REQ-04 | Um filtro válido sem correspondências retorna 200 e coleção vazia |
| REQ-05 | A falha de persistência mantém 503 e `service_unavailable`, com ou sem filtro válido |
| REQ-06 | Nenhuma dessas consultas altera registros, e os controles de acesso existentes são preservados |

### Critérios de aceite

- **AC-01 / REQ-01:** com fixture contendo ambos os estados, comparar resposta sem filtro antes e depois; mesmos campos, tipos, registros e ordenação.
- **AC-02 / REQ-02:** para cada um dos dois valores permitidos, obter somente registros correspondentes, com o mesmo formato de item e IDs crescentes.
- **AC-03 / REQ-03:** testar `status=`, `other`, `ACTIVE`, espaço codificado antes/depois e dois parâmetros `status`, inclusive valores iguais. Todos retornam o erro definido; a consulta de dados não é acionada.
- **AC-04 / REQ-04:** executar filtro válido sem correspondências e verificar status 200 com `[]`.
- **AC-05 / REQ-05:** simular falha na leitura e verificar o erro anterior nas chamadas sem filtro e com cada filtro válido.
- **AC-06 / REQ-06:** comparar dados antes/depois dos cenários e reexecutar os testes dos controles de acesso existentes, sem ampliar acesso.

### Decisões e limites

Valores exatos evitam normalização implícita. Parâmetros repetidos são rejeitados para eliminar diferenças de interpretação entre camadas. Outros parâmetros seguem a regra anterior, que deve ser caracterizada.

Não acrescentar índice preventivamente. Se a consulta filtrada revelar um problema de desempenho relevante na baseline representativa, medir e especificar a otimização e eventual migração. Nenhuma meta numérica de desempenho foi inventada neste exemplo.

## Arquivo: `specs/2026-09-28-filtrar-reservas/plan.md`

### Grupo 1 — Reconhecimento e preservação

- [ ] **T-01:** confirmar contratos, esquema, consumidores e comandos; registrar baseline com falhas preexistentes, se houver.
- [ ] **T-02:** criar ou ajustar caracterização da resposta sem filtro, erros e controles de acesso.

**Condição de saída:** premissas confirmadas ou requisitos revisados. Se a resposta real for um envelope paginado, manter esse envelope e atualizar todos os cenários; não mudar para coleção simples por causa do exemplo.

### Grupo 2 — Filtro optativo

- [ ] **T-03:** interpretar presença, multiplicidade e valor exato de `status`, atendendo REQ-03.
- [ ] **T-04:** acrescentar filtro na leitura para valores válidos; manter caminho sem filtro, formato e ordem, atendendo REQ-01, REQ-02 e REQ-04.
- [ ] **T-05:** preservar propagação do erro de persistência e ausência de efeitos, atendendo REQ-05 e REQ-06.

### Grupo 3 — Validação e transição

- [ ] **T-06:** executar matriz de casos, testes da exportação e regressões dos controles de acesso; registrar resultados.
- [ ] **T-07:** documentar contrato, preparar publicação do serviço e posterior adoção pelo dashboard.

## Arquivo: `specs/2026-09-28-filtrar-reservas/validation.md`

### Fixture

| ID | Sala | Estado | Início |
|---|---|---|---|
| 1 | 10 | active | 2026-10-01T10:00:00Z |
| 2 | 20 | cancelled | 2026-10-01T11:00:00Z |
| 3 | 10 | active | 2026-10-01T12:00:00Z |

Preparar também uma fixture sem correspondências. Cada execução deve isolar seu estado. Os controles de acesso usam os atores de teste já definidos no projeto real.

### Matriz de validação

| Requisito | Critério | Tarefas | Verificação | Resultado esperado | Estado |
|---|---|---|---|---|---|
| REQ-01 | AC-01 | T-02, T-04 | VAL-01: comparação de contrato e consumidor de exportação | IDs 1, 2, 3 e contrato anterior preservado | não executado |
| REQ-02 | AC-02 | T-04 | VAL-02: integração dos dois filtros | `active`: 1, 3; `cancelled`: 2 | não executado |
| REQ-03 | AC-03 | T-03 | VAL-03: parsing, resposta e ausência de chamada ao repositório | 400 e `invalid_status` em todos os casos inválidos | não executado |
| REQ-04 | AC-04 | T-04 | VAL-04: consulta sem correspondência | 200 e `[]` | não executado |
| REQ-05 | AC-05 | T-05 | VAL-05: indisponibilidade simulada na fronteira de leitura | 503 e `service_unavailable` | não executado |
| REQ-06 | AC-06 | T-05, T-06 | VAL-06: estado persistido e regressão de acesso | Nenhuma escrita; mesmas permissões | não executado |

### Evidências a coletar

Antes da alteração, registrar a baseline. Depois, registrar revisão candidata, comandos reais, ambiente, resultado de cada VAL e diferenças observadas. Uma verificação com mock de persistência serve para conferir que o parser bloqueia a chamada; o teste de integração deve usar a persistência apropriada ao projeto para validar a consulta real.

**Parecer atual:** não pronto. A especificação didática está preenchida, mas baseline, implementação e testes não foram executados.

## Arquivo: `specs/2026-09-28-filtrar-reservas/rollout.md`

1. Confirmar que clientes atuais não usam `status` com outro significado e que os contratos caracterizados passam na versão candidata.
2. Publicar o serviço mantendo consumidores atuais sem filtro.
3. Executar smoke tests sem filtro, com cada filtro e com entrada inválida, em dados adequados ao ambiente.
4. Observar erros de consulta e fluxo de exportação durante a janela definida pela equipe.
5. Só depois promover a entrega de adoção do parâmetro pelo dashboard.

**Gatilho de recuperação:** regressão do contrato sem filtro, falha de exportação causada pela versão nova ou divergência dos cenários de smoke test.

**Recuperação:** antes da adoção pelo dashboard, retornar o serviço à versão anterior conforme o mecanismo de publicação existente. Depois da adoção, primeiro desativar o envio do filtro pelo dashboard e restaurar sua filtragem local, verificar o comportamento e então considerar reverter o serviço. Comandos, responsáveis e janela precisam ser preenchidos no ambiente real antes da publicação.

**Dados:** nenhuma migração é esperada, pois a coluna já existe como premissa. Se isso não for confirmado, o plano operacional deve ser refeito. Não há execução operacional registrada neste exemplo.

## O que este exemplo ensina

A especificação do legado descreve a diferença desejada e o contrato a preservar. Um parâmetro opcional ainda exige investigar consumidores e valores existentes. A sequência de publicação é parte da compatibilidade: um serviço antigo pode não entender o parâmetro que um consumidor novo passou a enviar.
