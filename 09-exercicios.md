# 9. Exercícios e autoavaliação

[Índice](README.md)

Use um projeto de estudo ou um fluxo pequeno do seu trabalho. Os exercícios são incrementais: cada um produz material usado no seguinte. Não é necessário adotar a stack do curso.

## Exercício 1 — Separar as perguntas

Parta de “quero um sistema de reservas”. Escreva um parágrafo de missão, três requisitos observáveis, três tarefas e três verificações. Classifique cada frase pela pergunta que responde: por quê, o quê, como ou como comprovar.

**Autoavaliação:** uma tarefa como “criar tabela” não aparece como necessidade do usuário; um critério como “funcionar corretamente” foi substituído por entrada, resultado e efeito verificáveis.

## Exercício 2 — Criar uma constituição mínima

Preencha os três templates globais. Registre pelo menos uma incerteza de produto e uma técnica. Faça um roadmap com três resultados pequenos e suas dependências.

**Autoavaliação:** a primeira fase cabe em uma explicação curta; decisões confirmadas estão separadas de propostas; comandos não existentes não aparecem como prontos.

## Exercício 3 — Especificar e revisar

Crie o trio da primeira fase. Para cada requisito, escreva um caso de sucesso e um caso de limite ou falha relevante. Preencha a matriz de rastreabilidade.

Peça a alguém para explicar o comportamento apenas lendo os documentos. Se estiver estudando sozinho, retome a leitura em outra sessão e anote perguntas que a especificação não responde.

**Autoavaliação:** nenhuma tarefa implementa algo sem justificativa; nenhum requisito essencial fica sem verificação; as respostas não dependem de lembrar a conversa original.

## Exercício 4 — Implementar e coletar evidência

Implemente um grupo por vez. Execute as verificações e preencha resultados reais. Introduza, em ambiente de estudo, uma falha deliberada em uma regra e confira se a verificação correspondente a detecta; depois remova a falha e reexecute.

**Autoavaliação:** os testes verificam o comportamento pretendido; “passou” tem evidência; a execução aponta qual versão foi testada. Uma falha deliberada não detectada revela um teste insuficiente, mesmo que a execução termine com sucesso.

## Exercício 5 — Introduzir uma mudança de escopo

Após especificar, acrescente: “recursos inativos não devem ser exibidos”. Atualize requisito, plano e validação. Registre por que mudou e qual resultado anterior deixou de ser suficiente.

**Autoavaliação:** os três documentos concordam, há cenário com recurso inativo e a evidência anterior não é reutilizada como prova da nova regra.

## Exercício 6 — Adotar em legado

Escolha uma operação existente. Produza um diagnóstico limitado à área, registre uma baseline e escreva testes de caracterização. Proponha uma alteração pequena e descreva antes/depois e consumidores afetados.

**Autoavaliação:** fatos têm referência; hipóteses continuam identificadas; o plano preserva contratos definidos; falhas preexistentes não foram escondidas.

## Exercício 7 — Trocar de contexto

Escreva um handoff e encerre a sessão. Retome usando somente o repositório e o handoff, ou peça a outra pessoa para fazê-lo. Anote o que faltou: comando, dado de teste, decisão, tarefa ou bloqueio.

**Autoavaliação:** a próxima ação é concreta; decisões duradouras estão nos documentos próprios; o resumo não afirma que o repositório continua inalterado sem conferir.

## Rubrica de revisão

Use `0` para ausente, `1` para parcial e `2` para claro e verificável. A pontuação serve para comparar suas próprias revisões, sem substituir avaliação de risco.

| Dimensão | O que observar |
|---|---|
| Intenção | Problema, público e valor estão explícitos |
| Escopo | Incluído e excluído permitem decidir o que implementar |
| Comportamento | Regras, limites e erros são observáveis |
| Execução | Tarefas têm dependências e resultado verificável |
| Evidência | Cada critério tem verificação e resultado honesto |
| Continuidade | Outra pessoa consegue retomar sem reconstruir o chat |
| Legado, quando aplicável | Baseline, compatibilidade e transição foram consideradas |

Independentemente do total, uma dúvida que impeça definir o comportamento principal precisa ser resolvida antes da implementação dependente.
