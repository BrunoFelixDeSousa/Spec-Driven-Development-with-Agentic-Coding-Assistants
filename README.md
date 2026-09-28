# Desenvolvimento orientado por especificações: guia e kit reutilizável

Este material transforma os arquivos do curso **Spec-Driven Development with Agentic Coding Assistants** em um guia prático, em português, para aprender e aplicar desenvolvimento orientado por especificações (*Spec-Driven Development*, ou SDD). Serve para projetos novos e legados, com ou sem assistentes de IA.

O objetivo é conseguir responder, antes e durante uma mudança: **qual problema estamos resolvendo, quais comportamentos esperamos, como vamos implementar e que evidências demonstram que funcionou?**

Os guias são independentes de linguagem, framework e fornecedor de agente. Nos projetos reais, os documentos devem registrar a stack e os comandos concretos daquele repositório. Independência de stack não significa deixar a execução vaga.

## Comece por aqui

| Sua situação | Caminho sugerido | Resultado esperado |
|---|---|---|
| Quero entender o método | [Fundamentos](01-fundamentos.md) → [Artefatos e organização](02-artefatos-e-organizacao.md) → [Ciclo de trabalho](03-ciclo-de-trabalho.md) | Entender a função de cada documento e quando atualizá-lo |
| Vou começar um projeto | [Projetos novos](04-projetos-novos.md) → [Exemplo completo](exemplos/01-projeto-novo.md) | Constituição inicial e primeira entrega pequena especificada |
| Vou mudar um sistema existente | [Projetos legados](05-projetos-legados.md) → [Exemplo completo](exemplos/02-projeto-legado.md) | Diagnóstico, baseline e mudança com compatibilidade definida |
| Quero usar imediatamente | [Guia dos templates](templates/README.md) → [Prompts](08-prompts-reutilizaveis.md) | Arquivos preenchidos no projeto de destino |
| Já uso SDD e quero melhorar | [Validação](06-validacao-e-qualidade.md) → [Evolução e continuidade](07-evolucao-e-continuidade.md) | Evidências melhores e documentação que acompanha o código |
| Quero praticar | [Exercícios e autoavaliação](09-exercicios.md) | Aprender por entregas verificáveis |

## O conjunto mínimo

```text
projeto/
  specs/
    mission.md
    tech-stack.md
    roadmap.md
    AAAA-MM-DD-nome-da-entrega/
      requirements.md
      plan.md
      validation.md
```

Os três arquivos globais formam a **constituição do projeto**, nome usado pelo curso. Os três arquivos de cada entrega descrevem comportamento, execução e comprovação. Para uma correção muito pequena, essas seções podem viver em um único arquivo; preserve as perguntas, ajuste a quantidade de arquivos ao risco.

## Primeiro uso em sete passos

1. Leia a missão do seu produto e o código existente, quando houver. Liste o que sabe e o que ainda precisa confirmar.
2. Copie os [templates globais](templates/README.md) para `specs/` no projeto de destino.
3. Preencha missão, decisões técnicas e a próxima fase do roadmap. Não tente prever todo o futuro.
4. Copie o trio de feature para uma pasta datada. Especifique um resultado pequeno e observável.
5. Relacione cada requisito a uma tarefa e a uma verificação. Resolva dúvidas que impedem definir o comportamento.
6. Implemente em grupos pequenos; registre alterações de decisão e execute a validação apropriada.
7. Atualize o resultado observado, revise o diff e conclua a fase somente com evidências.

## O que vem do curso e o que foi acrescentado

O núcleo deriva dos prompts e snapshots locais: constituição, trio de feature, implementação por grupos, validação, replanejamento, legado, rotinas repetíveis e troca de agente. Acrescentamos mecanismos de aplicação prática: IDs de requisitos, matriz de rastreabilidade, inventário de legado, ADR, registro de evidências, rollout/rollback e exercícios.

Essas extensões são sugestões deste guia, não requisitos atribuídos ao curso. Os exemplos de reservas são fictícios e não representam testes executados. Consulte o [mapa de fontes e limites](10-fontes-e-adaptacoes.md) para acompanhar a origem das ideias e as inconsistências didáticas encontradas.

## Convenções de leitura e manutenção

- `[PREENCHER: ...]` indica uma informação que precisa ser substituída no projeto de destino.
- `Não se aplica — motivo` é melhor que uma seção vazia; não use isso para esconder uma decisão pendente.
- Uma caixa marcada significa trabalho efetivamente concluído. Um resultado esperado não é evidência de execução.
- `specs/` guarda decisões específicas do projeto; este `docs/` ensina o método e fornece os modelos.
- Caminhos e comandos de implementação nos exemplos são ilustrativos, a menos que explicitamente identificados como fontes do curso.
- Atualize especificação e código na mesma mudança quando o comportamento mudar. Registre por que houve mudança.

Não é necessário copiar o curso, o AgentClinic ou estes guias inteiros para cada produto. Copie os templates relevantes e mantenha somente documentos que ajudem a decidir, implementar, validar ou retomar o trabalho.
