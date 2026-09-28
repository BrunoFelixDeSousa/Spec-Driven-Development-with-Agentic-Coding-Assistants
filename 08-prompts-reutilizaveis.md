# 8. Prompts reutilizáveis

[Índice](README.md) · [Templates](templates/README.md)

Substitua os marcadores e forneça acesso aos arquivos relevantes. Os prompts funcionam como instruções de trabalho em diferentes assistentes; não dependem de slash commands ou ferramentas proprietárias. Use somente a etapa necessária.

Não envie credenciais nem dados reais desnecessários ao contexto. Em um ambiente com regras próprias, os comandos e ações devem seguir as permissões do projeto. Produzir uma especificação não implica autorização automática para publicar uma aplicação.

## 1. Descobrir um projeto novo

```text
Quero estruturar [PRODUTO] com desenvolvimento orientado por especificações.
Leia [BRIEFING/README] e as instruções locais disponíveis.
Identifique problema, público, resultado desejado e restrições confirmadas.
Separe fatos, hipóteses e perguntas em aberto.

Faça perguntas sobre escopo, decisões e contexto somente onde a resposta
alterar materialmente a solução. Use as informações já disponíveis.
Produza specs/mission.md, specs/tech-stack.md e specs/roadmap.md.
Proponha fases pequenas com resultados observáveis e dependências explícitas.
Registre escolhas técnicas com motivo; não invente comandos existentes.
Não trate hipóteses como decisões confirmadas.
```

## 2. Diagnosticar um legado

```text
Quero adotar SDD no sistema existente, começando por [FLUXO/MÓDULO].
Leia documentação, testes, código, contratos e migrações dessa área.
Faça um diagnóstico antes de alterar comportamento.

Registre: fluxo atual, pontos de entrada, persistência, consumidores,
comandos de verificação, falhas conhecidas e lacunas de conhecimento.
Vincule descobertas a arquivos, revisão ou execução observada.
Separe comportamento atual de comportamento desejado.
Proponha uma baseline e testes de caracterização proporcionais ao risco.
Produza specs/legacy-assessment.md e proponha a constituição mínima.
Não proponha reescrita como premissa da adoção do método.
```

## 3. Especificar uma feature

```text
Leia specs/mission.md, specs/tech-stack.md e specs/roadmap.md.
Considere fases parcialmente implementadas, dependências e bloqueios.
A entrega escolhida é [ENTREGA], ou justifique qual é a próxima fase elegível.
Inspecione os padrões e contratos existentes na área afetada.

Esclareça dúvidas relevantes sobre escopo, decisões e contexto.
Crie specs/[DATA]-[NOME]/requirements.md, plan.md e validation.md.
Inclua objetivo, fora de escopo, regras, critérios de aceite e casos de erro.
Relacione requisitos a tarefas e verificações com IDs estáveis.
Mantenha resultados de execução como não executados até haver evidência.
No legado, registre antes/depois, compatibilidade e baseline.
Não implemente nesta etapa; entregue os documentos prontos para revisão.
```

## 4. Revisar antes de implementar

```text
Revise a feature em [CAMINHO] contra a constituição e o código existente.
Procure contradições, termos vagos, lacunas de aceitação, dependências
escondidas, tarefas fora de escopo e riscos sem verificação.
Para cada achado, indique arquivo/seção, impacto e correção sugerida.
Separe bloqueadores de melhorias opcionais.
Informe se a especificação permite começar e quais dúvidas impedem partes dela.
```

## 5. Implementar um grupo

```text
Implemente o próximo grupo elegível de [CAMINHO]/plan.md.
Leia requisitos e validação antes de editar.
Respeite os contratos e as convenções do repositório.
Execute as verificações necessárias para o comportamento alterado.
Registre tarefas, arquivos afetados, resultados e limitações.

Se descobrir uma decisão de produto ausente, registre a dúvida e resolva-a
antes de implementar o comportamento dependente. Continue tarefas independentes.
Se surgir trabalho fora de escopo, proponha seu registro no backlog.
Não marque a feature inteira concluída apenas por concluir este grupo.
```

## 6. Validar uma entrega

```text
Valide [CAMINHO DA FEATURE] na revisão atual.
Relacione cada critério de aceite à evidência correspondente.
Execute comandos disponíveis e procedimentos aplicáveis ao ambiente.
Registre contexto, preparação, esperado, obtido e limitações.
Se um teste manual não puder ser realizado, marque como pendente ou bloqueado.
Inspecione os efeitos relevantes, além das respostas visíveis.
Informe falhas novas, falhas preexistentes e critérios sem cobertura.
Conclua se está pronta para integração, com base nos critérios vigentes.
```

## 7. Replanejar após uma descoberta

```text
Descobrimos [FATO/RESTRIÇÃO] durante [FEATURE].
Avalie o impacto em missão, decisões técnicas, roadmap e feature ativa.
Proponha a menor mudança coerente de escopo e sequência.
Registre motivo, decisões substituídas, tarefas afetadas e destino do trabalho parcial.
Atualize os documentos acordados e identifique o que precisa ser revalidado.
Preserve a distinção entre evidência histórica e validação da nova versão.
```

## 8. Revisar a entrega por perspectivas

```text
Revise o diff de [REFERÊNCIA INICIAL] até [REFERÊNCIA FINAL] e a feature [CAMINHO].
Avalie produto, engenharia e suficiência das evidências.
Procure problemas concretos, com referência e cenário de falha.
Separe defeitos, dúvidas e sugestões; não trate preferência estética como defeito.
Verifique se há requisitos sem implementação ou sem validação.
Resuma bloqueios e condições para concluir a entrega.
```

## 9. Preparar uma retomada

```text
Crie ou atualize [CAMINHO]/handoff.md para outra pessoa ou assistente continuar.
Registre objetivo, branch/revisão, mudanças locais, leituras prioritárias,
tarefas concluídas, pendências, decisões, testes executados e bloqueios.
Indique a próxima ação concreta e como verificar seu resultado.
Referencie os documentos oficiais em vez de duplicar regras do produto.
Não apresente como executadas verificações apenas planejadas.
```

## 10. Atualizar o histórico

```text
Prepare entradas de changelog para [INTERVALO DE COMMITS OU ENTREGA].
Confira o diff e os requisitos, além dos títulos dos commits.
Descreva mudanças relevantes para usuários e operadores.
Identifique incompatibilidades e procedimentos de migração, quando existirem.
Evite duplicar entradas ou omitir commits por terem a mesma data de uma entrada anterior.
Siga o formato de histórico já adotado pelo projeto.
```

## Como avaliar a resposta do assistente

Uma resposta útil aponta para arquivos e evidências, explicita dúvidas e produz um próximo passo verificável. Uma resposta fraca apenas repete o prompt, inventa comandos, atribui regras ao produto sem fonte ou declara sucesso sem execução. Revise esses pontos antes de usar o resultado como base para implementar.
