## Contexto

Descreva o problema e por que esta mudança é necessária.

## Linear

- [ ] Issue Linear atribuída (sub-issue `PR: <repo> — …`)
- [ ] Body com magic word de fechamento (`Fixes INF-xx` / `Fixes INFRA-xx`) **e** `**Linear:** [id](url)`

## Mudanças

- [ ] Mudança 1
- [ ] Mudança 2

## Documentação (required workflow `docs-sync-gate` — bloqueia merge)

Toda PR com código precisa das **duas** PRs de docs da mesma entrega, linkadas aqui (`https://github.com/isis-saude/<repo>/pull/N` ou `isis-saude/<repo>#N`):

- Geral — PR em **`isis-saude/docs`** (página do repo em `docs/arquitetura/repos/`; inventário se criar/alterar endpoint):
- Detalhe — PR no irmão **`<projeto>-docs`** (se o repo não tem irmão, basta alterar `README.md` / `docs/**` nesta PR):

Dispensa só com label `docs-exempt` **e** a linha abaixo preenchida (break-glass, auditável):

`Sem impacto em docs:` <!-- justificativa em uma linha, ou apagar -->

## Contrato / endpoint

Esta PR cria, altera ou remove contrato, endpoint ou comportamento visível para consumidores?

- [ ] **Não** — sem impacto de contrato (Dependabot, chore interno ou docs-only). Justificativa em uma linha:
- [ ] **Sim** — a PR em `isis-saude/docs` acima atualiza o **inventário** (`docs/arquitetura/inventario-recursos.md`) com valor literal / `PENDING_<FONTE>` / **BLOQUEADO**

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
- [ ] Variável nova está no lugar do consumidor que a lê (`envMap` só config; segredo no store do consumidor) — `docs/ses-mg/onde-cada-env-vive.md`
- [ ] Merge gate de segurança: sem Dependabot **critical/high** abertos nem secret scanning **open** no repo (ver *Security*; inclui alertas “generic”/password quando o workflow central está atualizado)
