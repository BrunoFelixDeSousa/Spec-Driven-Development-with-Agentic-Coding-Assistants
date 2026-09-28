# 4. Aplicação em projetos novos

[Índice](README.md) · [Exemplo preenchido](exemplos/01-projeto-novo.md) · [Templates](templates/README.md)

Em um projeto novo, a principal dificuldade é transformar uma ideia ampla em uma primeira entrega útil sem inventar infraestrutura e regras desnecessárias. Comece pela intenção e por uma fatia pequena do comportamento.

## 1. Descobrir o produto

Reúna objetivo, usuários, problemas atuais, restrições e sinais de sucesso. As respostas podem vir de uma conversa, briefing ou README. Diferencie necessidade de sugestão de solução.

“Precisamos de um dashboard” ainda não informa qual decisão ele ajuda a tomar. Pergunte quais informações o usuário precisa, quando e para agir de que maneira. A missão deve registrar esse resultado.

Preencha [mission.md](templates/projeto/mission.md) com:

- Problema e público principal.
- Resultado desejado e como observá-lo.
- Fluxos centrais e vocabulário do domínio.
- Limites, inclusive o que não pertence ao produto agora.
- Premissas ainda não confirmadas.

**Critério de saída:** alguém consegue explicar o propósito sem mencionar uma linguagem ou framework.

## 2. Definir a base técnica suficiente

Preencha [tech-stack.md](templates/projeto/tech-stack.md) com as escolhas necessárias para a primeira entrega. Registre o motivo: experiência da equipe, integração existente, ambiente de execução ou restrição operacional. Não trate preferências como requisitos inevitáveis.

Uma seleção técnica útil considera onde o sistema roda, como os dados sobrevivem a reinicializações, como erros são diagnosticados e como a equipe testa. Não é necessário definir uma arquitetura distribuída quando um componente atende ao problema inicial.

Quando uma escolha depender de evidência, crie uma investigação com pergunta e critério de conclusão. Exemplo: “Confirmar se a biblioteca existente oferece a operação transacional necessária; produzir um teste mínimo e registrar a limitação.” Evite pesquisas sem decisão a tomar.

**Critério de saída:** existe um caminho concreto para executar e verificar a primeira fase; o que ainda não existe está explicitado no plano.

## 3. Criar um roadmap por resultados

Um roadmap inicial de reservas poderia ser:

| Fase | Resultado utilizável | Fora desta fase |
|---|---|---|
| 1 | Consultar recursos ativos com dados persistidos | Reservar e cancelar |
| 2 | Criar reserva sem sobreposição | Recorrência e lista de espera |
| 3 | Cancelar conforme regras do domínio | Notificações externas |

As fases podem ser reordenadas. Se o maior risco for a exclusão concorrente, investigue essa capacidade antes de investir na interface. Uma fase técnica é justificável quando reduz um risco necessário; registre qual risco e como saber que ele foi reduzido.

**Critério de saída:** a primeira fase tem uma fronteira clara e dependências compreendidas.

## 4. Especificar a primeira fatia

Copie o trio de feature. Para “consultar recursos ativos”, defina quais campos aparecem, como ordenar, o que fazer sem resultados e como lidar com falha da fonte de dados. Esses detalhes evitam que a implementação invente silenciosamente o produto.

Não transforme a especificação em um catálogo de futuras funcionalidades. Relacione ideias futuras ao roadmap ou backlog. Concentre o plano em uma entrega que possa ser examinada de ponta a ponta.

## 5. Preparar execução reproduzível

Documente pré-requisitos e comandos reais. Identifique o diretório de execução, configuração mínima e dados sintéticos. Se testes, build ou análise estática ainda não estiverem disponíveis, planeje sua configuração conforme a necessidade da entrega.

Um comando com saída zero pode não executar nenhuma verificação. Confirme descoberta dos testes e quais cenários foram exercitados. Se a fase for uma prova técnica manual, descreva exatamente a observação que a valida e seus limites.

## 6. Executar uma entrega completa

Siga o [ciclo de trabalho](03-ciclo-de-trabalho.md). Após a primeira fase, confira se outra pessoa conseguiria reproduzir o resultado lendo os arquivos. Use essa dificuldade como feedback para os templates: adicione informações ausentes e remova burocracia que não ajudou.

## Como adaptar para outros tipos de sistema

| Tipo | Comportamento a especificar | Evidências possíveis |
|---|---|---|
| Aplicação web/mobile | Fluxos, estados, navegação, permissões e falhas | Testes de domínio e integração; inspeção de interface |
| API | Contratos, autorização, efeitos e erros | Testes de contrato e integração com persistência |
| CLI | Argumentos, entrada padrão, saída e códigos de retorno | Execuções reproduzíveis e verificações de arquivos |
| Biblioteca | API pública, compatibilidade e casos de uso | Testes da API e exemplos executáveis |
| Pipeline de dados | Esquema, qualidade, reprocessamento e deduplicação | Fixtures, contagens, invariantes e reconciliação |
| Serviço assíncrono | Eventos, entrega repetida, ordenação e falhas | Cenários com repetição, atraso e recuperação |

Os nomes dos arquivos permanecem úteis; o conteúdo muda. Um serviço sem interface não precisa de checklist visual. Uma CLI pode precisar detalhar códigos de saída que uma aplicação web não usa.
