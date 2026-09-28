# 5. Aplicação em projetos legados

[Índice](README.md) · [Exemplo preenchido](exemplos/02-projeto-legado.md) · [Template de diagnóstico](templates/apoio/legacy-assessment.md)

Legado é um sistema que já tem comportamento, dependências e usuários a preservar. A adoção de SDD começa descrevendo a realidade e delimitando a próxima mudança. Não exige reescrever o sistema nem especificar retroativamente cada funcionalidade.

## 1. Escolher uma fronteira de investigação

Selecione um fluxo relacionado à mudança desejada: uma operação, módulo, endpoint, job ou integração. Identifique entrada, regras, persistência e saída. Se a alteração atravessar vários componentes, expanda a investigação para essas dependências.

Levante README, configurações, testes, código, migrações, contratos, exemplos de payload e histórico relevante. Documentos antigos são pistas; confirme sua correspondência com a revisão atual.

## 2. Registrar fatos, hipóteses e intenção separadamente

| Categoria | Exemplo | Como tratar |
|---|---|---|
| Fato observado | A operação atual aceita quantidade zero no teste reproduzido | Registrar revisão, entrada e saída |
| Hipótese | Talvez uma integração use zero para cancelar | Investigar consumidores e consultar responsável |
| Intenção confirmada | Novas solicitações devem ter quantidade positiva | Registrar decisão e impacto em compatibilidade |
| Desconhecido | Não há inventário completo dos consumidores | Tratar como risco e definir investigação necessária |

Essa separação impede que engenharia reversa transforme bugs em regras de produto, ou que uma especificação nova apague contratos usados na prática.

## 3. Estabelecer uma baseline

Antes de alterar código:

1. Identifique a revisão e o estado local do repositório.
2. Prepare um ambiente isolado e dados adequados ao teste.
3. Execute as verificações disponíveis e registre os resultados.
4. Reproduza o fluxo relevante, incluindo erros conhecidos.
5. Documente falhas preexistentes, limitações e verificações impossíveis naquele ambiente.

Uma baseline pode conter falhas. Ela serve para distinguir o estado anterior do efeito da mudança. Não declare aprovação se a verificação não rodou. Quando uma falha conhecida impede avaliar o comportamento alterado, resolva o bloqueio ou produza evidência adicional confiável antes de concluir.

## 4. Criar testes de caracterização

Testes de caracterização registram o comportamento atual em uma fronteira estável. Eles são úteis quando faltam especificações e você precisa refatorar ou acrescentar uma regra com controle de regressão.

Escolha casos reais representativos, com dados sintéticos ou adequadamente preparados: entradas válidas, rejeições, formato de saída e efeitos relevantes. Evite congelar timestamps, IDs aleatórios ou detalhes internos irrelevantes. Quando o comportamento atual for um defeito que será corrigido, identifique o teste correspondente e a mudança de expectativa pretendida.

Exemplo: antes de adicionar um campo opcional a uma resposta, registre status, campos antigos, tipos e erros existentes. Depois acrescente verificações do novo campo. Assim fica explícito o que deve continuar compatível.

## 5. Reconstruir a constituição

Escreva a missão com base no objetivo atual confirmado. Em `tech-stack.md`, registre o que existe e separe propostas futuras. No roadmap, descreva as próximas mudanças; não transforme toda a aplicação já existente em um plano a executar novamente.

O curso usa README e TODO como entradas para essa reconstrução. No seu projeto, acrescente evidências do código e da execução. Um TODO desatualizado não deve prevalecer automaticamente sobre uma funcionalidade já entregue.

## 6. Especificar o delta

O requisito de legado deve explicar **antes, depois e o que precisa ser preservado**.

| Aspecto | Antes | Depois | Evidência necessária |
|---|---|---|---|
| Contrato | Resposta com campos A e B | A e B mantidos; C opcional | Testes dos consumidores relevantes |
| Dados | Registros antigos sem C | Leitura antiga continua válida | Teste com amostra representativa |
| Regra | Duplicatas possíveis | Novas duplicatas impedidas | Teste concorrente e política para duplicatas históricas |
| Operação | Uma versão do serviço | Versões podem coexistir na publicação | Ensaio de compatibilidade durante transição |

Uma adição de campo pode quebrar consumidores estritos. Uma mudança “interna” pode alterar ordenação, tempo de resposta ou tratamento de erro. Determine o impacto a partir dos contratos reais.

## 7. Preparar migração e recuperação quando necessário

Para mudanças persistentes, descreva formato antigo e novo, tratamento de registros existentes, duração esperada do trabalho, reexecução e efeitos de uma interrupção. Valide em ambiente representativo antes de produção.

Uma sequência possível é: ampliar o esquema de modo compatível → disponibilizar código compatível com ambos → migrar dados → verificar consumidores → retirar o formato antigo. Essa sequência deve ser adaptada ao sistema; não é necessária para toda mudança.

Rollback de aplicação não implica rollback de dados. Se a versão anterior não conseguir interpretar novos registros, reverter apenas o binário pode piorar o incidente. Especifique se a recuperação será rollback, correção adiante, restauração com reconciliação ou outra ação ensaiada. Use o [template operacional](templates/apoio/rollout-rollback.md).

## 8. Entregar incrementalmente

Prefira uma mudança de comportamento por vez, com refatorações limitadas ao que viabiliza e torna segura a entrega. Se uma refatoração maior for necessária, separe objetivos e evidências: primeiro preservar comportamento, depois alterá-lo.

Depois da entrega, atualize somente a documentação afetada e os conhecimentos transversais úteis. A cobertura documental do legado cresce com o trabalho real, não com uma iniciativa interminável de catalogação.

## Sinais de adoção saudável

- Uma nova pessoa identifica o contrato afetado e consegue reproduzir a baseline.
- Regras confirmadas e suposições estão distinguíveis.
- A feature define compatibilidade e testes de regressão relevantes.
- Dados históricos e consumidores conhecidos foram considerados.
- A equipe consegue explicar o que acontecerá se a publicação falhar.

## Armadilhas

Não use o diagnóstico como justificativa automática para reescrever. Não elimine uma convenção antiga antes de entender seus consumidores. Não marque falhas preexistentes como resolvidas sem evidência. Não promova testes que apenas confirmam a implementação atual a requisitos imutáveis de negócio.
