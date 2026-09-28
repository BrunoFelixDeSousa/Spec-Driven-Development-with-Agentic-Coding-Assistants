# 2. Artefatos e organização do repositório

[Índice](README.md) · Anterior: [Fundamentos](01-fundamentos.md) · Próximo: [Ciclo](03-ciclo-de-trabalho.md)

## Organização sugerida

```text
projeto/
  README.md
  CHANGELOG.md                      # quando houver histórico de entregas
  specs/
    mission.md
    tech-stack.md
    roadmap.md
    AAAA-MM-DD-primeira-entrega/
      requirements.md
      plan.md
      validation.md
      handoff.md                    # se houver trabalho a retomar
      rollout.md                    # se a entrega exigir transição operacional
    legacy-assessment.md            # ao adotar SDD em legado
    decisions/
      ADR-001-titulo.md              # decisões duradouras relevantes
  backlog/
    assunto-em-investigacao.md      # ideias e pesquisa ainda sem compromisso
```

A organização é uma convenção, não uma exigência de ferramenta. Em monorepos, pode haver uma missão global e decisões técnicas por componente. Cada feature deve apontar quais componentes afeta e qual documento prevalece em seu escopo. Evite copiar a mesma regra em vários serviços.

## Responsabilidade de cada documento

| Artefato | Pergunta principal | Atualizar quando | Evitar |
|---|---|---|---|
| Missão | Para quem, por quê e com qual resultado? | Mudar público, objetivo ou limite do produto | Inventário de dependências |
| Decisões técnicas | Como este repositório funciona e quais restrições seguem vigentes? | Mudar stack, comando, arquitetura ou padrão transversal | Lista de tecnologias sem motivo ou referência |
| Roadmap | Qual sequência de resultados vamos buscar? | Entregar, bloquear ou repriorizar uma fase | Checklist detalhado de cada arquivo |
| Requisitos | O que esta entrega inclui e como deve se comportar? | Mudar regra, contrato ou escopo | Prescrever detalhes técnicos sem necessidade |
| Plano | Qual caminho executável atende aos requisitos? | Descobrir dependências ou mudar a abordagem | Marcar tarefas concluídas antes de verificar |
| Validação | O que comprova os critérios e o que foi observado? | Definir critérios e executar verificações | Confundir “esperado” com “passou” |
| ADR | Por que escolhemos esta alternativa relevante? | Tomar ou substituir decisão duradoura | Registrar toda escolha trivial |
| Diagnóstico de legado | O que existe e o que pode quebrar? | Investigar a área afetada e confirmar descobertas | Declarar intenção a partir do código sem confirmação |
| Handoff | Onde o trabalho parou e como continuar? | Encerrar uma sessão ou trocar responsável | Substituir especificações por um resumo de chat |
| Changelog | O que mudou para usuários e operadores? | Preparar uma entrega | Colar todos os commits sem revisar significado |

## Fonte de verdade e conflitos

Cada documento tem uma função, mas nenhum arquivo torna uma afirmação automaticamente verdadeira. A especificação é referência da intenção acordada; o código e a execução são evidências do comportamento implementado. Os dois precisam convergir.

Ao encontrar conflito:

1. Aponte os documentos e comportamentos divergentes.
2. Classifique: documentação desatualizada, defeito, decisão ainda aberta ou mudança intencional.
3. Verifique contratos e dependências antes de escolher uma resolução.
4. Registre a decisão; atualize requisitos, plano e validação afetados.
5. Implemente ou corrija o documento conforme a resolução.

Não adote silenciosamente a versão que torna a tarefa mais fácil.

## Identificadores e rastreabilidade

Use IDs estáveis dentro de uma feature: `REQ-01` para requisito, `AC-01` para critério, `T-01` para tarefa e `VAL-01` para verificação. Em referências entre features, inclua o caminho da feature; `REQ-01` isolado não é globalmente único.

| Requisito | Critério | Tarefa | Verificação | Evidência |
|---|---|---|---|---|
| REQ-01: rejeitar sobreposição | AC-01: nenhuma gravação em conflito | T-02: proteção de gravação | VAL-02: integração de conflito | Execução, revisão e resultado |

A matriz é uma extensão deste guia. Use-a para encontrar requisitos sem validação e tarefas que não atendem ao escopo. Em features pequenas, uma tabela em `validation.md` basta. O template separado só é necessário quando centralizar a matriz ajudar.

## Estados e responsáveis

Para documentos de feature, use: **rascunho → pronta → em implementação → em validação → concluída**. “Bloqueada” deve registrar causa e condição de desbloqueio. “Cancelada” deve registrar motivo e destino do trabalho parcial.

“Pronta” significa comportamento suficientemente definido para começar, e não certeza absoluta sobre toda a implementação. “Concluída” significa critérios atendidos com evidências e pendências tratadas. A prontidão para publicar pode exigir uma etapa operacional adicional.

Registre quem pode esclarecer o produto e quem responde pela implementação. Em trabalho individual, a mesma pessoa pode exercer ambos os papéis. Revisões e aprovações seguem as regras reais da equipe; o método não exige criar uma nova hierarquia.

## Histórico sem perder contexto

Use o controle de versão para preservar revisões. Atualize a documentação global quando a realidade atual mudar. Mantenha o resultado de uma feature entregue como registro daquela entrega; se uma mudança futura a substituir, acrescente referência à nova especificação.

Evite reescrever evidências antigas como se testes da versão passada tivessem validado a versão atual. Uma mudança transversal pode atualizar a orientação vigente, mas exige novas verificações para comprovar o comportamento modificado.
