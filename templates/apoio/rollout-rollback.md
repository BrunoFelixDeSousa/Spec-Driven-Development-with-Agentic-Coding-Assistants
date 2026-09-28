# Publicação e recuperação — [PREENCHER: entrega]

- Responsável operacional: [PREENCHER]
- Ambiente e versão candidata: [PREENCHER]
- Janela/condições de execução: [PREENCHER]
- Estado: rascunho, não executado

## Impacto

- Componentes e consumidores: [PREENCHER]
- Dados alterados e reversibilidade: [PREENCHER]
- Compatibilidade entre versões: [PREENCHER]
- Indisponibilidade ou limitação esperada: [PREENCHER]

## Pré-condições

- [ ] Validação da versão candidata concluída.
- [ ] Procedimento ensaiado em ambiente adequado ao risco.
- [ ] Recursos de recuperação disponíveis e verificados, quando necessários.
- [ ] Responsáveis, acesso e condições de início confirmados conforme o processo do projeto.

## Sequência de publicação

| Ordem | Ação concreta/comando e ambiente | Resultado esperado | Responsável | Condição de parada |
|---|---|---|---|---|
| 1 | [PREENCHER] | [PREENCHER] | [PREENCHER] | [PREENCHER] |
| 2 | [PREENCHER] | [PREENCHER] | [PREENCHER] | [PREENCHER] |

## Migração de dados, se aplicável

- Transformação e volume: [PREENCHER]
- Duração/limites operacionais: [PREENCHER]
- Reexecução e interrupção: [PREENCHER]
- Reconciliação e verificação de integridade: [PREENCHER]
- Compatibilidade de leitura/escrita durante a transição: [PREENCHER]

## Observação após publicar

| Sinal | Baseline | Limite de sucesso/falha | Janela | Ação se falhar |
|---|---|---|---|---|
| [PREENCHER: métrica, log ou fluxo] | [PREENCHER] | [PREENCHER: limite acordado] | [PREENCHER] | [PREENCHER] |

## Recuperação

- Gatilhos objetivos: [PREENCHER]
- Responsável pela decisão: [PREENCHER]
- Procedimento: [PREENCHER: rollback de aplicação, correção adiante, restauração ou outro]
- Tratamento de dados escritos após publicar: [PREENCHER]
- Compatibilidade da versão anterior com o estado atual dos dados: [PREENCHER]
- Como verificar recuperação: [PREENCHER]
- Limites: [PREENCHER: irreversibilidade, perda potencial e ações de reconciliação]

## Registro de execução

| Horário | Ação | Resultado real | Evidência | Responsável |
|---|---|---|---|---|
| não executado | [PREENCHER] | não executado | não coletada | [PREENCHER] |

Não presuma que reverter o código reverte os dados. Não execute restauração destrutiva sem o procedimento e as autorizações aplicáveis ao ambiente.
