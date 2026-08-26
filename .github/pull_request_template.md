## Contexto

Descreva o problema e por que esta mudança é necessária.

## Linear

- [ ] Issue Linear atribuída (sub-issue `PR: <repo> — …`)
- [ ] Body com magic word de fechamento (`Fixes INF-xx` / `Fixes INFRA-xx`) **e** `**Linear:** [id](url)`

## Mudanças

- [ ] Mudança 1
- [ ] Mudança 2

## Contrato / endpoint

Esta PR cria, altera ou remove contrato, endpoint ou comportamento visível para consumidores?

- [ ] **Não** — sem impacto de contrato (Dependabot, chore interno ou docs-only). Justificativa em uma linha:
- [ ] **Sim** — as duas URLs abaixo são obrigatórias:
  - PR ou commit em **docs locais** deste repo ou no irmão `*-docs`:
  - PR em **`isis-saude/docs`** (inventário / página do repo):

## Testes

- [ ] Teste local
- [ ] Evidência anexada (log/print)

## Risco e rollback

- Risco:
- Plano de rollback:

## Checklist

- [ ] Nome da branch conforme política da org (ex.: `<tipo>/<slug>`, `main`/`develop`, `release/…` — ver CONTRIBUTING)
- [ ] Título e commits alinhados a Conventional Commits quando possível (recomendado; não há check central obrigatório)
- [ ] Sem segredos/tokens em arquivos versionados
- [ ] Merge gate de segurança: sem Dependabot **critical/high** abertos nem secret scanning **open** no repo (ver *Security*; inclui alertas “generic”/password quando o workflow central está atualizado)
