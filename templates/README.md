# Templates: como copiar e preencher

[Índice dos guias](../README.md)

Este kit contém modelos de documentação, sem dependência de linguagem, framework ou assistente. Copie somente os arquivos aplicáveis. Os arquivos dentro de `projeto/`, `feature/` e `apoio/` não dependem de links para este curso e podem ser usados separadamente.

## Catálogo

| Modelo | Destino sugerido | Quando usar |
|---|---|---|
| [Missão](projeto/mission.md) | `specs/mission.md` | Em qualquer projeto que adote o kit |
| [Decisões técnicas](projeto/tech-stack.md) | `specs/tech-stack.md` | Em qualquer projeto que adote o kit |
| [Roadmap](projeto/roadmap.md) | `specs/roadmap.md` | Para organizar resultados e dependências |
| [Requisitos](feature/requirements.md) | `specs/AAAA-MM-DD-feature/requirements.md` | Para cada entrega relevante |
| [Plano](feature/plan.md) | `specs/AAAA-MM-DD-feature/plan.md` | Para cada entrega relevante |
| [Validação](feature/validation.md) | `specs/AAAA-MM-DD-feature/validation.md` | Para cada entrega relevante |
| [Diagnóstico de legado](apoio/legacy-assessment.md) | `specs/legacy-assessment.md` | Ao iniciar adoção ou investigar área desconhecida |
| [ADR](apoio/adr.md) | `specs/decisions/ADR-NNN-titulo.md` | Quando uma decisão duradoura precisa de justificativa |
| [Handoff](apoio/handoff.md) | Pasta da feature, `handoff.md` | Para retomar trabalho entre sessões ou responsáveis |
| [Rollout e rollback](apoio/rollout-rollback.md) | Pasta da feature, `rollout.md` | Para publicação com risco operacional ou migração |
| [Rastreabilidade ampliada](apoio/rastreabilidade.md) | Pasta da feature, `traceability.md` | Se a matriz do trio ficar extensa |
| [Backlog e pesquisa](apoio/backlog-item.md) | `backlog/assunto.md` | Para hipóteses e trabalho fora do escopo atual |
| [Descrição de entrega/PR](apoio/pr-description.md) | Descrição da revisão de código | Para apresentar problema, mudança e evidências |

## Copiar manualmente

1. Crie `specs/` na raiz do projeto de destino.
2. Copie os três arquivos de `projeto/` para `specs/`.
3. Crie uma pasta de feature com data e nome descritivo em kebab-case.
4. Copie os três arquivos de `feature/` para ela.
5. Acrescente modelos de apoio somente conforme a necessidade.

Não é necessário copiar os diretórios chamados `projeto`, `feature` ou `apoio` para o destino. Eles apenas organizam o kit.

## Exemplo de cópia via shell

Os comandos abaixo são opcionais, para shells compatíveis com Bash. Ajuste caminhos, data e nome. Use em um destino onde os arquivos ainda não existam; as condições evitam sobrescrever documentos existentes e avisam os arquivos preservados.

```bash
COURSE_DOCS_SOURCE='/caminho/para/sc-spec-driven-development-files/docs'
SDD_PROJECT_DEST='/caminho/para/seu-projeto'
SDD_FEATURE_NAME='AAAA-MM-DD-nome-da-entrega'

mkdir -p "$SDD_PROJECT_DEST/specs/$SDD_FEATURE_NAME"

for file in mission.md tech-stack.md roadmap.md; do
  if test -e "$SDD_PROJECT_DEST/specs/$file"; then
    printf 'Já existe, revisar manualmente: %s\n' "$SDD_PROJECT_DEST/specs/$file"
  else
    cp "$COURSE_DOCS_SOURCE/templates/projeto/$file" "$SDD_PROJECT_DEST/specs/$file"
  fi
done

for file in requirements.md plan.md validation.md; do
  if test -e "$SDD_PROJECT_DEST/specs/$SDD_FEATURE_NAME/$file"; then
    printf 'Já existe, revisar manualmente: %s\n' "$SDD_PROJECT_DEST/specs/$SDD_FEATURE_NAME/$file"
  else
    cp "$COURSE_DOCS_SOURCE/templates/feature/$file" "$SDD_PROJECT_DEST/specs/$SDD_FEATURE_NAME/$file"
  fi
done
```

Se algum comando falhar, corrija o caminho ou a permissão antes de continuar. Confirme os seis arquivos no destino; executar a cópia não significa que os documentos estejam preenchidos.

## Ordem de preenchimento

Em projeto novo: missão → decisões técnicas → roadmap → requisitos e validação → plano.

Em legado: diagnóstico e baseline → constituição mínima → requisitos do delta e validação → plano. Você pode refinar a constituição durante a investigação, mantendo fatos separados de propostas.

Em ambos, faça uma leitura cruzada do trio antes de implementar. Cada `REQ` precisa de critério e verificação; cada tarefa precisa de uma finalidade justificada.

## Personalização

- Substitua `[PREENCHER: ...]` por informações verificadas.
- Remova orientações editoriais quando terminar o preenchimento.
- Marque seções não aplicáveis com justificativa ou remova-as quando não forem úteis.
- Use comandos reais do projeto, indicando diretório e pré-requisitos. Não copie comandos da stack do curso para outra stack.
- Resolva perguntas bloqueadoras antes do trabalho dependente; registre as demais com responsável.
- Adicione links internos após definir os caminhos no destino.
- Mantenha o idioma e os termos do domínio consistentes.

Os exemplos [projeto novo](../exemplos/01-projeto-novo.md) e [legado](../exemplos/02-projeto-legado.md) mostram o nível de preenchimento esperado.
