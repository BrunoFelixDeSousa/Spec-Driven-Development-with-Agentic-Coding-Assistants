# 6. Validação, rastreabilidade e qualidade

[Índice](README.md) · [Template de validação](templates/feature/validation.md)

Validação responde se a entrega satisfaz o comportamento esperado. O documento começa como plano de verificação e termina com resultados observados. Uma lista de comandos sem critérios e sem resultados não demonstra conclusão.

## Do requisito à evidência

Considere: “Uma solicitação inválida não pode criar uma reserva.” Há pelo menos três observações relevantes: o chamador recebe a rejeição correta, não há reserva persistida e o erro permite corrigir a entrada. Testar apenas a mensagem não comprova ausência de gravação.

Para cada requisito, registre:

1. Critério de aceite, em termos observáveis.
2. Cenário e dados necessários.
3. Tipo de verificação e comando ou procedimento.
4. Resultado esperado.
5. Resultado obtido, revisão, ambiente e evidência.

## Escolher a verificação pelo risco

| Verificação | Pergunta respondida | Limite |
|---|---|---|
| Estática: tipos, lint, análise | A estrutura atende às regras configuradas? | Não demonstra o comportamento em execução |
| Unitária | Uma regra isolada responde aos casos definidos? | Pode não cobrir configuração e integrações |
| Integração | Componentes colaboram e persistem corretamente? | Pode usar infraestrutura diferente da produção |
| Contrato | Um consumidor recebe a interface acordada? | Contrato incompleto pode omitir efeitos importantes |
| Ponta a ponta | O usuário conclui o fluxo no sistema integrado? | Custo e fragilidade podem limitar os cenários |
| Manual exploratória | Há problemas de uso, conteúdo ou interação não previstos? | Exige registro para ser reproduzível |
| Operacional | A mudança publica, observa e recupera como previsto? | Depende da representatividade do ambiente |

Não é obrigatório criar todas essas categorias para cada feature. Escolha as que detectam os riscos concretos. Uma alteração de texto pode pedir inspeção simples; uma regra concorrente exige exercitar concorrência na fronteira onde a garantia deve existir.

## Matriz de cenários

| Categoria | Pergunta orientadora | Exemplo |
|---|---|---|
| Caminho feliz | O fluxo principal entrega valor? | Reserva válida recebe identificação |
| Obrigatoriedade | O que falta e como é informado? | Ausência de recurso é rejeitada |
| Fronteira | O que acontece nos limites? | Fim igual ao início é inválido |
| Estado vazio | Sem dados, o resultado faz sentido? | Consulta retorna coleção vazia |
| Conflito | O estado já existente muda a decisão? | Horários sobrepostos são rejeitados |
| Repetição | Reexecutar altera indevidamente o efeito? | Retry não duplica uma operação quando isso é exigido |
| Concorrência | Duas execuções preservam a invariante? | Somente uma reserva ocupa o intervalo |
| Falha de dependência | O sistema falha de forma definida? | Erro de persistência não gera confirmação falsa |
| Compatibilidade | Consumidores antigos continuam funcionando? | Campos anteriores mantêm tipo e significado |
| Permissão | A ação respeita o ator autorizado? | Usuário sem permissão não acessa dados restritos |

Escolha cenários aplicáveis. Caso um risco relevante fique sem teste automatizado, declare a alternativa de verificação e sua limitação.

## Evidência reproduzível

Uma boa entrada de validação contém, por exemplo:

```text
Verificação: VAL-03 — conflito concorrente
Revisão: [hash ou referência do snapshot de código testado]
Ambiente: [runtime, banco e configuração relevante, sem segredos]
Preparação: [dados sintéticos e estado inicial]
Comando/procedimento: [execução exata]
Esperado: uma confirmação, uma rejeição e uma reserva persistida
Obtido: [preencher após executar]
Estado: não executado | passou | falhou | bloqueado
Evidência: [log, relatório ou registro observacional reproduzível]
Limitação: [diferenças relevantes em relação ao ambiente de destino]
```

Se houver alterações locais fora de um commit, descreva também o diff ou snapshot testado. Um hash sozinho não identifica código ainda não commitado. Depois de corrigir uma falha, registre a nova execução e preserve a informação necessária para entender a resolução.

## O que saída zero não garante

Um runner configurado para aceitar ausência de testes pode terminar com sucesso sem validar uma regra. Uma requisição que imprime HTML pode não exibir o status HTTP. Um mock pode aceitar uma operação que o banco real rejeita.

Confirme que os testes certos foram descobertos e que as asserções correspondem aos requisitos. Confira status e efeitos, não apenas texto. No curso, a fase inicial é uma prova mínima e a automação é adicionada depois; isso ensina evolução do processo, não uma dispensa universal de testes.

## Revisão em três perspectivas

- **Produto:** o fluxo atende à intenção, o escopo está correto e os erros são compreensíveis?
- **Engenharia:** regras e integrações estão corretas, as mudanças são sustentáveis e os contratos preservados?
- **Validação:** os cenários cobrem os riscos, os resultados foram registrados e as alegações correspondem às evidências?

Essas perspectivas podem ser avaliadas por uma pessoa, por colegas ou por assistentes, conforme a equipe. A quantidade de revisores não substitui critérios claros.

## Definição de concluído

Uma feature está concluída quando seus critérios foram atendidos, a regressão relevante foi avaliada e não há bloqueios escondidos. Testes manuais pendentes devem permanecer pendentes. Um problema conhecido pode ser aceito somente se não contrariar os critérios vigentes ou se houver decisão documentada que altere esses critérios, com responsável e impacto claros.

Ao mudar um requisito, atualize tarefa, cenário e evidência necessária. Ao mudar código após a validação, reexecute as verificações afetadas. Evite repetir indiscriminadamente verificações sem relação com a alteração, mas não reutilize uma evidência que já não descreve a versão candidata.
