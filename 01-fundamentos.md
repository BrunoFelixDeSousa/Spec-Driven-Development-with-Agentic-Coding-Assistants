# 1. Fundamentos: pensar em comportamento antes de implementar

[Índice](README.md) · Próximo: [Artefatos](02-artefatos-e-organizacao.md)

## O que é SDD neste material

SDD é organizar o desenvolvimento em torno de especificações versionadas, revisáveis e verificáveis. A especificação conecta a necessidade do produto à mudança no código e às evidências de funcionamento. Ela permanece útil depois da implementação, como referência para manutenção e próximas entregas.

Uma conversa pode iniciar uma decisão. Um documento no repositório permite que outra pessoa a encontre, examine e questione sem reconstruir toda a conversa. Isso reduz a dependência da memória de quem trabalhou e do contexto de uma sessão de IA.

SDD não exige que todo o sistema seja definido antecipadamente. Neste curso, o desenvolvimento acontece em fases; a especificação de cada fase amadurece com feedback e implementação. A missão tende a ser estável; o roadmap e o plano mudam com mais frequência.

## Quatro perguntas diferentes

| Pergunta | Exemplo em um sistema de reservas | Onde registrar |
|---|---|---|
| Por que existe? | Pessoas precisam reservar um recurso sem depender de uma planilha compartilhada | `mission.md` |
| O que deve acontecer? | Duas solicitações concorrentes não podem reservar o mesmo recurso no mesmo intervalo | `requirements.md` |
| Como vamos fazer? | Usar o mecanismo transacional disponível e verificar o conflito na gravação | `plan.md`, com referência às decisões técnicas |
| Como saberemos? | Disparar duas solicitações concorrentes e verificar uma reserva persistida e uma rejeição | `validation.md` |

Misturar essas perguntas produz falhas comuns. “Criar uma tabela” é uma tarefa, mas não explica o valor para o usuário. “Funcionar bem” é uma intenção, mas não fornece um critério de aceite. “Usar framework X” é uma escolha técnica, mas não define o comportamento do produto.

## Especificações como acordos que evoluem

Uma boa especificação registra:

- Contexto suficiente para entender o problema sem a conversa original.
- Escopo incluído e excluído, para impedir expansão acidental.
- Regras e exemplos, inclusive rejeições e casos de fronteira.
- Decisões relevantes e suas razões, não somente o resultado final.
- Dúvidas com impacto, responsável e próximo passo.
- Critérios observáveis de sucesso e a forma de coletar evidências.

Ela não precisa antecipar cada função ou classe. Detalhe a implementação quando há um contrato, risco, padrão existente ou restrição que torne essa decisão relevante. Deixe decisões locais de baixo impacto para a implementação.

## Uma melhoria de requisito, passo a passo

Versão inicial: “O usuário pode fazer uma reserva.”

Versão delimitada: “Um operador interno pode reservar um recurso ativo para uma data e hora.”

Versão verificável: “Para um recurso ativo, um operador autorizado pode reservar um intervalo futuro com início menor que fim. Intervalos que se sobrepõem a uma reserva ativa são rejeitados, sem gravar uma segunda reserva. Intervalos adjacentes são permitidos.”

Agora surgem perguntas úteis: quem é autorizado? Qual é o fuso? O que significa ativo? A concorrência deve ser garantida? Como o chamador reconhece a rejeição? Essas respostas devem ser adequadas ao domínio; não precisam ser idênticas em todos os projetos.

Um critério de aceite poderia ser:

> Dado um recurso reservado das 10:00 às 11:00, quando um operador tenta reservar das 10:30 às 11:30, então a solicitação é rejeitada por conflito e a quantidade de reservas permanece inalterada.

O exemplo revela que rejeitar uma resposta e impedir uma gravação são verificações distintas.

## O papel do humano e do assistente

O responsável pelo produto esclarece intenção, prioridades e regras que o repositório não pode revelar. Quem implementa investiga o sistema, propõe alternativas e entrega a mudança. O assistente pode apoiar ambos, mas precisa distinguir fatos observados de hipóteses.

Se um agente encontra uma regra de desconto no código, isso comprova a implementação atual. Não comprova que a regra é a desejada. Se um stakeholder pede alterar essa regra, isso expressa intenção; não comprova que os consumidores existentes estão preparados para a alteração.

Registre as duas perspectivas. Em legado, a diferença entre comportamento atual e desejado é parte central da especificação.

## Quanto documentar

| Mudança | Documentação proporcional |
|---|---|
| Correção de texto sem lógica | Contexto, texto esperado e inspeção; uma nota curta pode bastar |
| Nova regra de negócio | Trio de feature, exemplos, testes de fronteira e impacto |
| Alteração de contrato usado por terceiros | Trio, inventário de consumidores, compatibilidade e estratégia de transição |
| Migração de dados ou mudança operacional relevante | Acrescentar diagnóstico, ensaio de migração e rollout/rollback |

Evite criar documentos somente para cumprir uma estrutura. Também evite reduzir a documentação de uma mudança arriscada porque o diff é pequeno: uma linha pode alterar cobrança, acesso ou integridade de dados.

## Erros frequentes

| Sintoma | Problema | Ajuste |
|---|---|---|
| Especificação enorme e sem prioridades | Não há uma entrega claramente delimitada | Dividir em resultados pequenos e colocar o restante no backlog |
| Plano diz algo diferente dos requisitos | A decisão mudou em apenas um lugar | Revisar o trio antes de implementar |
| Todos os testes passam, mas o usuário não consegue concluir a tarefa | Testes não cobrem o critério de aceite | Validar o fluxo observável e seus efeitos |
| “O agente sabe porque conversamos” | Decisão depende de contexto temporário | Registrar a decisão e sua justificativa |
| Copiar a stack do exemplo sem avaliar o destino | Confundir método com tecnologia | Preencher decisões técnicas a partir do projeto real |
| Documentar tudo apenas depois | Perde-se a oportunidade de encontrar ambiguidades cedo | Especificar o comportamento e a validação antes da implementação |

Você entendeu o fundamento quando consegue explicar por que cada tarefa existe e qual evidência demonstrará que ela entregou o resultado esperado.
