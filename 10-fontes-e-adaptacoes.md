# 10. Fontes locais, adaptações e limites

[Índice](README.md)

Esta documentação foi elaborada a partir dos arquivos disponíveis neste repositório. Não pressupõe acesso às gravações nem transcreve aulas. O [README original](../README.md) informa que cada pasta `VideoNN_*` contém um snapshot de início da respectiva aula, e que as aulas conceituais 2–4 não possuem código inicial.

## Mapa de conceitos e fontes

| Conceito | Fontes locais | Uso neste guia |
|---|---|---|
| Organização e progressão do curso | [README](../README.md) | Separar snapshots de etapas de uma única implementação |
| Constituição: missão, stack e roadmap | [Lesson 04](../prompts/Lesson_04_prompts.md), [missão reconstruída](../Video14_Agents_replaceability/specs/mission.md), [stack](../Video14_Agents_replaceability/specs/tech-stack.md) | Guias de fundamentos e templates globais |
| Trio de feature e entrevista | [Lesson 05](../prompts/Lesson_05_prompts.md) | Requisitos, plano e validação por entrega |
| Implementação por grupos | [Lesson 06](../prompts/Lesson_06_prompts.md), [plano inicial](../Video07_Feature_Implementation/specs/2026-03-30-hello-hono/plan.md) | Ciclo incremental |
| Ajustes e integração | [Lesson 07](../prompts/Lesson_07_prompts.md) | Sincronização entre documentos e implementação |
| Testes, responsividade e replanejamento | [Lesson 08](../prompts/Lesson_08_prompts.md) | Evolução dos acordos globais e critérios |
| Revisão por perspectivas | [Lesson 09](../prompts/Lesson_09_prompts.md) | Revisão de produto, engenharia e evidências |
| Agrupar funcionalidades para MVP | [Lesson 10](../prompts/Lesson_10_prompts.md), [requisitos do MVP](../Video12_Legacy_support/specs/2026-04-06-mvp/requirements.md) | Discutir escopo, dependências e tamanho de entrega |
| Adoção em legado | [Lesson 11](../prompts/Lesson_11_prompts.md), [entradas de stakeholders](../Video12_Legacy_support/README.md) | Reconstrução de contexto, acrescida de baseline neste guia |
| Rotina de especificação | [Lesson 12](../prompts/Lesson_12_prompts.md), [skill original](../skills/feature-spec/SKILL.md) | Prompts portáveis e rotina documentada |
| Continuidade e avaliação de testes | [Lesson 13](../prompts/Lesson_13_prompts.md), [snapshot Video14](../Video14_Agents_replaceability/README.md), [visão das aulas](../README.md) | Retomada baseada em artefatos; handoff é extensão do guia |
| Feature completa com decisões de UX e persistência | [Feedback: requisitos](../Video14_Agents_replaceability/specs/2026-04-06-feedback-form/requirements.md), [plano](../Video14_Agents_replaceability/specs/2026-04-06-feedback-form/plan.md), [validação](../Video14_Agents_replaceability/specs/2026-04-06-feedback-form/validation.md) | Exemplo concreto do papel de cada arquivo |
| Feature estática e fronteira de escopo | [About: requisitos](../Video14_Agents_replaceability/specs/2026-04-07-about-us-content/requirements.md), [roadmap](../Video14_Agents_replaceability/specs/roadmap.md) | Separar conteúdo, mapa e entregas posteriores |
| Histórico automatizado | [Skill de changelog](../skills/changelog/SKILL.md), [script](../skills/changelog/scripts/changelog.py) | Registrar mudanças com revisão das entradas |
| Pesquisa fora da feature | [Nota de opções de banco](../Video14_Agents_replaceability/backlog/2026-04-07-vercel-database-options.md) | Distinguir pesquisa, decisão e execução |

Os nomes `Lesson_XX` e `VideoNN` não correspondem sempre ao mesmo número. Os links acima identificam os arquivos pelo conteúdo, sem presumir equivalência numérica.

## O que é específico do AgentClinic

O projeto didático usa TypeScript, Hono, renderização no servidor, SQLite e, em etapas posteriores, Vitest. Tem conteúdo satírico, componentes web e decisões próprias sobre formulários. Essas escolhas ajudam a demonstrar o método, mas não são requisitos para adotar SDD.

Os arquivos em `example_specs/` apresentam uma visão mais ampla de AgentClinic, incluindo uma API de clínica para agentes. A [missão de exemplo](../example_specs/AgentClinic-Mission.md) não deve ser combinada automaticamente com a [missão do snapshot final](../Video14_Agents_replaceability/specs/mission.md), que descreve uma aplicação satírica de ensino. São contextos documentais diferentes.

## Inconsistências e limites úteis para aprender

1. **Escopo versus plano no snapshot inicial.** Os [requisitos Hello Hono](../Video07_Feature_Implementation/specs/2026-03-30-hello-hono/requirements.md) excluem layout compartilhado, mas o [plano da mesma pasta](../Video07_Feature_Implementation/specs/2026-03-30-hello-hono/plan.md) inclui um grupo de layout. Isso exemplifica a necessidade de revisar coerência, sem assumir que um snapshot está totalmente sincronizado.
2. **Validação inicial limitada.** A [validação inicial](../Video07_Feature_Implementation/specs/2026-03-30-hello-hono/validation.md) dispensa testes automatizados e inspeção no navegador para aquela fase. A sequência depois incorpora testes. O guia trata a escolha como proporcional à entrega, sem generalizar a dispensa.
3. **Sucesso sem testes.** A [stack posterior](../Video14_Agents_replaceability/specs/tech-stack.md) documenta um runner com `--passWithNoTests`. O guia acrescenta a verificação de descoberta e cobertura dos cenários, além do código de saída.
4. **Escolha da próxima fase.** A skill original procura uma fase cujos itens estejam todos desmarcados. Isso pode ignorar uma fase parcialmente implementada. Os prompts deste guia consideram estado, prioridade, bloqueios e dependências.
5. **Changelog por data.** O script remove do conjunto novo a data mais recente já registrada. Isso pode omitir commits posteriores do mesmo dia. O guia recomenda intervalos por referência e revisão de duplicatas/omissões, sem alterar o script original.
6. **TODO e roadmap podem divergir.** O [TODO do Video14](../Video14_Agents_replaceability/TODO.md) ainda lista feedback em “Now”, enquanto o roadmap registra a fase como completa. No legado, reconcilie essas fontes antes de planejar.
7. **Pesquisa de ferramentas envelhece.** A nota de bancos é usada apenas como exemplo de backlog. Suas afirmações sobre serviços e fornecedores não foram verificadas como recomendações atuais.

Essas observações derivam da leitura dos documentos e do script indicado. Não constituem uma auditoria de execução de todos os snapshots.

## Extensões propostas neste diretório

IDs de requisitos e critérios, matriz de rastreabilidade, diagnóstico estruturado de legado, testes de caracterização, ADR, handoff, estados de evidência e rollout/rollback foram detalhados aqui para facilitar aplicação em outros projetos. Não se afirma que todos esses mecanismos foram ensinados nas gravações.

As perguntas dos prompts originais foram adaptadas para linguagem neutra de ferramenta. Instruções contidas nas skills do curso foram tratadas como objeto de estudo; este trabalho não instalou nem executou essas skills.

## Como verificar esta documentação

Percorra os links das fontes, compare os papéis dos documentos e preencha um template usando um projeto real. Os exemplos preenchidos são simulações didáticas; resultados de testes permanecem não executados. A revisão deste diretório deve conferir navegação, completude dos modelos e coerência interna, sem alegar execução das aplicações do curso.
