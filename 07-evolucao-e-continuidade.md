# 7. Evolução, manutenção e continuidade entre pessoas e agentes

[Índice](README.md) · [Handoff](templates/apoio/handoff.md) · [ADR](templates/apoio/adr.md)

## Replanejamento faz parte do método

No curso, testes e responsividade entram ao longo do desenvolvimento, e fases do roadmap são reorganizadas. A lição é atualizar os acordos quando o entendimento muda. A documentação deve descrever o trabalho vigente, sem fingir que as novas decisões já existiam desde o início.

Para uma mudança transversal, como adotar um padrão de erros:

1. Registre a regra vigente em decisões técnicas.
2. Identifique componentes e features em andamento afetados.
3. Planeje a adaptação do comportamento existente, se necessário.
4. Atualize critérios de validação e execute as verificações relevantes.
5. Preserve evidências históricas e registre a entrega que introduz a nova regra.

## Roadmap, backlog e pesquisa

O roadmap contém a sequência pretendida de entregas. O backlog guarda ideias, problemas e pesquisas que ainda precisam de decisão. Um arquivo de pesquisa deve identificar pergunta, alternativas, evidências, incertezas e próximo passo.

Uma comparação de fornecedores não equivale a uma decisão de migração. Preços, disponibilidade e integrações envelhecem; antes de executar uma escolha dependente dessas informações, verifique as fontes atuais. As notas locais de pesquisa do curso são registros históricos, não recomendações atualizadas deste guia.

Quando uma pesquisa resultar em decisão duradoura, resuma a escolha e os motivos em um ADR. Não obrigue a pessoa que implementa a reler toda a exploração para descobrir o que vale agora.

## Registrar decisões duradouras

Use ADR para escolhas com alternativas e consequências relevantes: mudança de contrato, padrão de persistência, estratégia de compatibilidade ou arquitetura. Escreva contexto, alternativas, decisão, justificativa e efeitos.

Se uma decisão for substituída, mantenha o registro antigo e aponte para o novo. “Usamos isso porque já estava assim” pode descrever a situação, mas não esclarece se preservar o padrão é uma restrição ou apenas uma opção inicial.

## Changelog com significado

O curso automatiza um rascunho a partir de commits e o revisa antes da integração. A ideia reutilizável é registrar entregas e manter o histórico próximo do trabalho.

Para o projeto de destino, decida se a organização será por versão ou data. Descreva efeitos relevantes, correções e mudanças de compatibilidade. Mensagens como “fix”, “ajustes” e “WIP” não ajudam o leitor final.

Se automatizar, use uma referência inequívoca do intervalo já processado, como commit ou tag, e revise duplicatas e omissões. O script didático do curso elimina entradas da data mais recente já registrada; commits novos no mesmo dia podem ficar de fora. Portanto, não copie a regra de corte por data sem adaptação.

## Continuidade entre agentes e sessões

O trabalho deve poder continuar a partir do repositório. Um handoff registra:

- Objetivo e feature ativa.
- Revisão, branch e alterações locais relevantes.
- Documentos que devem ser lidos primeiro.
- Tarefas concluídas, próximas e bloqueadas.
- Verificações executadas e seus resultados.
- Decisões e dúvidas ainda abertas.
- Próxima ação concreta, com dependências.

O handoff é um índice de retomada; regras duradouras permanecem nos documentos próprios. Não duplique longas especificações no resumo da sessão.

Ao retomar, confira o estado real do repositório antes de confiar no handoff. Outro colaborador pode ter alterado código ou documentação depois de sua criação.

## Transformar prompts em rotinas

Primeiro repita o processo manualmente e observe o que se estabilizou. Depois transforme passos recorrentes em checklist, comando ou mecanismo de automação do assistente usado pela equipe.

Uma rotina portável precisa declarar entradas, passos, saídas, limites de atuação e critérios de conclusão. “Criar a próxima feature” deve explicar como escolher uma fase, quais dúvidas esclarecer e quais arquivos produzir. Não deve depender de um nome de ferramenta de perguntas específico.

Os [prompts deste guia](08-prompts-reutilizaveis.md) são texto reutilizável; não são skills instaladas. A instalação e o formato de automações dependem da ferramenta escolhida. As skills originais são analisadas como material do curso, sem exigir sua execução para usar estes templates.

## Manter os documentos úteis

Faça uma revisão rápida da documentação quando um PR mudar comportamento, comandos ou arquitetura. Pergunte: “Alguém seguindo o documento atual chegaria ao resultado esperado?” Se a resposta for não, atualize-o junto com o código.

Sinais simples de qualidade: menos dúvidas repetidas, menor dificuldade de retomar trabalho, critérios mais claros e menos divergências entre escopo e implementação. Use esses sinais para ajustar o processo; volume de páginas e quantidade de caixas marcadas não medem sucesso.
