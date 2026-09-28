# Exemplo completo: primeira entrega de um projeto novo

[Índice](../README.md) · [Guia de projetos novos](../04-projetos-novos.md) · [Templates](../templates/README.md)

Este exemplo é fictício e preenchido para estudo. Ele define um catálogo inicial de salas de uma empresa. Não há aplicação implementada neste diretório nem testes executados. A data da feature é apenas ilustrativa.

As seções a seguir representam o conteúdo que ficaria em arquivos distintos. Ao aplicar em um projeto real, separe-os nos caminhos indicados e acrescente a stack, os comandos e as referências reais.

## Briefing e decisões da conversa

“Hoje as pessoas perguntam à recepção quais salas existem. Queremos um catálogo para consultar nome e capacidade; reservas virão depois.”

| Pergunta | Resposta assumida no exemplo |
|---|---|
| Quem consulta? | Colaboradores, por uma interface interna já acessível na rede corporativa |
| Qual informação mostrar? | Identificador, nome e capacidade das salas ativas |
| Inativas aparecem? | Não; ausência de salas ativas deve ser um resultado vazio válido |
| Como ordenar? | Identificador numérico crescente, por ser determinístico nesta primeira fase |
| Quem cadastra? | A carga inicial é controlada pela equipe; edição pela interface fica fora |
| Precisa de busca ou paginação? | Não nesta fase; o limite de negócio acordado é de até 50 salas cadastradas |
| Há autenticação a desenvolver? | Não nesta fase; acesso externo está fora do escopo e o controle de acesso existente deve ser confirmado antes de publicar |

Essas respostas são decisões do exemplo, não padrões universais. O limite de 50 salas impede tratar uma lista sem paginação como adequada para qualquer volume.

## Arquivo: `specs/mission.md`

### Missão — Catálogo de salas

**Problema:** colaboradores dependem da recepção para descobrir salas e respectivas capacidades.

**Público principal:** colaboradores que precisam escolher uma sala para uma reunião.

**Proposta:** oferecer uma consulta simples e confiável às salas disponíveis no cadastro. “Ativa” significa elegível para uso, e não livre em determinado horário.

**Sucesso da primeira entrega:** em uma demonstração com dados sintéticos, um colaborador identifica o nome e a capacidade de uma sala ativa sem consultar a recepção. Um cadastro sem salas ativas apresenta um estado vazio compreensível.

**Limites:** a primeira entrega não informa agenda, não reserva, não cancela e não permite administrar salas pela interface. O produto poderá acrescentar reservas em fases posteriores.

**Princípios:** informação simples, nomenclatura consistente e ausência de confirmação enganosa quando a fonte de dados falha.

### Vocabulário

| Termo | Significado |
|---|---|
| Sala | Recurso físico identificado por um número estável |
| Ativa | Sala que deve aparecer no catálogo |
| Capacidade | Número inteiro positivo de pessoas comportadas |
| Disponibilidade | Agenda livre em um intervalo; fora da primeira fase |

## Arquivo: `specs/tech-stack.md`

### Decisões técnicas iniciais

**Arquitetura pretendida:** uma aplicação consulta um repositório persistente de salas e apresenta o resultado. A seleção de salas ativas é uma regra testável. A interface traduz resultado vazio e falha em estados diferentes.

**Persistência:** dados devem sobreviver ao reinício. A fonte persistente concreta ainda precisa ser escolhida e preparada. A interface de consulta retorna registros com `id`, `name`, `capacity` e `active` internamente; `active` controla seleção e não precisa aparecer para o usuário.

**Restrições confirmadas:** até 50 salas no cadastro; capacidade inteira positiva; IDs únicos e estáveis; nomes tratados como texto; dados sintéticos para testes.

**Stack:** ainda não escolhida neste exemplo neutro. Isso bloqueia execução e decisões de arquivos concretos, mas não impede revisar os requisitos de produto.

### Preparação técnica obrigatória

| Item | Estado | Critério para resolver |
|---|---|---|
| Runtime e ferramenta de execução | pendente | Escolher conforme ambiente da equipe e registrar versão |
| Persistência local e de destino | pendente | Comprovar leitura e persistência após reinício |
| Runner de testes | pendente | Descobrir e executar um teste que falha e depois passa |
| Comandos de executar/testar/build | não definidos | Registrar comandos reais e diretórios após scaffold |
| Controle de acesso do ambiente interno | a confirmar | Responsável operacional confirmar limite de exposição antes de publicar |

Não há comandos fictícios como `npm test` ou `make test` declarados como existentes. No projeto real, o grupo de preparação abaixo substitui essas pendências por informações executáveis.

## Arquivo: `specs/roadmap.md`

| Fase | Resultado | Estado | Dependências |
|---|---|---|---|
| F01 | Consultar salas ativas e capacidades | pendente | Preparação técnica no primeiro grupo |
| F02 | Reservar um intervalo sem conflito | pendente | F01; regras de horário e autorização a especificar |
| F03 | Cancelar uma reserva conforme regras | pendente | F02; política de cancelamento a definir |

F01 está pronta para especificação de comportamento e preparação técnica. F02 e F03 são intenções de roadmap, sem detalhes suficientes para implementar. Seus contratos serão definidos quando forem priorizadas.

## Arquivo: `specs/2026-09-28-consultar-salas/requirements.md`

### Contexto e escopo

**Estado:** rascunho de implementação; regras de produto definidas no exemplo, preparação técnica pendente.

Entregar uma consulta ao catálogo de salas ativas com nome e capacidade. A carga inicial conterá dados sintéticos. Administração, agenda, busca, paginação e reservas ficam fora desta fase.

### Dados de entrada do repositório

| Campo | Regra |
|---|---|
| `id` | Inteiro positivo único |
| `name` | Texto não vazio, preparado na carga inicial |
| `capacity` | Inteiro positivo |
| `active` | Booleano |

Dados inválidos na carga devem ser detectados durante preparação. Definir uma interface de edição e seus erros é trabalho futuro.

### Regras

| ID | Regra |
|---|---|
| REQ-01 | A consulta mostra somente salas ativas, com identificador, nome e capacidade, ordenadas por ID crescente |
| REQ-02 | Sem salas ativas, mostra o estado “Nenhuma sala disponível no catálogo”, sem tratar isso como erro |
| REQ-03 | Se a fonte falhar, informa que não foi possível carregar o catálogo e permite uma nova tentativa; não apresenta a falha como lista vazia |
| REQ-04 | A consulta não cria nem altera salas |
| NFR-01 | Os registros cadastrados permanecem disponíveis após reiniciar a aplicação |

### Critérios de aceite

- **AC-01 / REQ-01:** dados os registros 20 ativo, 10 ativo e 30 inativo, ao consultar, mostrar somente 10 e 20, nessa ordem, com os valores corretos de nome e capacidade.
- **AC-02 / REQ-02:** dado um cadastro sem salas ativas, ao consultar, mostrar o estado vazio sem sinalização de falha.
- **AC-03 / REQ-03:** dada uma falha de leitura, ao consultar, mostrar erro de carregamento; após restaurar a fonte e tentar novamente, mostrar o catálogo.
- **AC-04 / REQ-04:** comparar os registros antes e depois de duas consultas; o estado persistido deve permanecer igual.
- **AC-05 / NFR-01:** após carregar os registros sintéticos, encerrar e iniciar novamente a aplicação sem refazer a carga; a consulta deve retornar os mesmos registros ativos.

### Decisões

Ordenar por ID simplifica o primeiro contrato e evita assumir regras de comparação textual. Estado vazio e erro são distintos para impedir informação enganosa. Não adicionar cache nesta fase; a consulta deve refletir a fonte utilizada.

## Arquivo: `specs/2026-09-28-consultar-salas/plan.md`

### Grupo 1 — Preparação

- [ ] **T-01:** selecionar stack e persistência adequadas ao ambiente, preparar o scaffold e registrar comandos reais em `tech-stack.md`.
- [ ] **T-02:** criar mecanismo de carga sintética e isolamento dos dados de teste; preparar o runner e confirmar descoberta dos testes.

**Saída:** ambiente executável, fonte persistente e comandos reproduzíveis. Nenhuma execução posterior é considerada concluída antes desse grupo.

### Grupo 2 — Consulta

- [ ] **T-03:** implementar seleção de salas ativas e ordenação, atendendo REQ-01 sem operações de escrita, conforme REQ-04.
- [ ] **T-04:** apresentar nome e capacidade, estado vazio e erro com nova tentativa, atendendo REQ-01 a REQ-03.

**Dependência:** grupo 1. **Saída:** cenários AC-01 a AC-04 verificáveis na aplicação.

### Grupo 3 — Comprovação e entrega

- [ ] **T-05:** verificar persistência após reinício, AC-05.
- [ ] **T-06:** executar as verificações da matriz, inspecionar o fluxo e registrar evidências.
- [ ] **T-07:** confirmar configuração de acesso para o ambiente de publicação, atualizar documentação e concluir F01 somente após validação.

## Arquivo: `specs/2026-09-28-consultar-salas/validation.md`

### Estado

Não executado. Revisão de código, stack, comandos e ambiente ainda não existem neste exemplo. Os procedimentos são especificações de testes; não são resultados.

### Dados sintéticos

| ID | Nome | Capacidade | Ativa |
|---|---|---|---|
| 20 | Sala Azul | 8 | sim |
| 10 | Sala Verde | 4 | sim |
| 30 | Sala Cinza | 6 | não |

Para estado vazio, usar um conjunto separado sem registros ativos. Para falha, simular indisponibilidade na fronteira de leitura sem alterar os dados reais do ambiente.

### Matriz

| Requisito | Critério | Tarefas | Verificação | Esperado | Estado |
|---|---|---|---|---|---|
| REQ-01 | AC-01 | T-03, T-04 | VAL-01: integração da consulta e inspeção da apresentação | Somente 10 e 20, ordenados, campos corretos | não executado |
| REQ-02 | AC-02 | T-04 | VAL-02: conjunto sem ativos | Mensagem de catálogo vazio | não executado |
| REQ-03 | AC-03 | T-04 | VAL-03: falha e recuperação da leitura | Erro distinto de vazio; nova tentativa funciona | não executado |
| REQ-04 | AC-04 | T-03 | VAL-04: comparar estado antes/depois | Nenhuma modificação após consultas repetidas | não executado |
| NFR-01 | AC-05 | T-01, T-05 | VAL-05: reiniciar sem recarregar dados | Registros persistem | não executado |

### Procedimento de execução

Após concluir T-01 e T-02, registrar aqui comandos, diretórios e ambiente. Preparar os conjuntos isolados, executar cada cenário e registrar a revisão e os resultados. A inspeção da apresentação deve confirmar a leitura de nome e capacidade e a distinção entre vazio e erro; o teste de integração deve conferir o conteúdo retornado e a ausência de escrita.

**Critério de conclusão:** todos os cinco critérios atendidos, comandos documentados, fluxo demonstrável e pendências de acesso resolvidas antes da publicação. Resultado atual: ainda não pronto para integração ou publicação, pois nenhuma implementação foi realizada.

## O que este exemplo ensina

É possível especificar um resultado sem escolher uma stack arbitrária. Para executar, porém, a escolha e os comandos reais precisam existir. O primeiro grupo transforma decisões abertas em uma base concreta. Os demais grupos implementam exatamente os comportamentos e verificações definidos, sem antecipar reservas e cancelamentos.
