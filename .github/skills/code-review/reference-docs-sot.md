# Inventory and project-docs gate (operational)

MkDocs in **`isis-saude/docs`** is the source of truth for consumable endpoints and contracts. Git, Terraform Cloud state, and the cluster **feed** the inventory — they do not replace it.

Canonical page: `docs/arquitetura/inventario-recursos.md` in repo `isis-saude/docs`.

## Hard stop

Any change that **creates, alters, or removes** a consumable endpoint/contract must update the correct inventory section in the **same delivery**, with a **literal** value, or `PENDING_<FONTE>`, or **BLOQUEADO**.

Forbidden as a substitute for the row: “see TFC”, “see cluster”, “dynamic”.

## What counts as an endpoint

- FQDN / hostname (Ingress, ALB, Argo, ECR, RDS, MSK, Blob, DFS, Postgres, Databricks, Key Vault)
- IP (private endpoint, Tailscale, NAT egress, inbound DNS resolver)
- bootstrap / JDBC / `https://` / `s3://` / `abfss://` / `jdbc:`
- Stable in-cluster Service (`*.svc.cluster.local`) when it is a platform contract
- Port and protocol when not obvious (MSK `9098`, OTLP `4317`/`4318`, Postgres `5432`)

## Required row format

| Column | Content |
|--------|---------|
| Endpoint | literal **or** `PENDING_<FONTE>` (never “see output”) |
| Tipo | ingress / rds / msk / ecr / pe / blob / dfs / eks-api / argo / nat / k8s-svc / … |
| Hub | SESMG \| InternalApps \| Azure RMDS \| Azure AKS \| … |
| Env | staging \| production \| hml \| prd |
| Porta | number or `—` |
| Consumidor | who calls it |
| Fonte | Git path and/or TFC workspace + output name **and** read date |

## Taxonomy (where to record)

| Scope | Section | Includes | Does not include |
|-------|---------|----------|------------------|
| **ISIS Saude** | §2 AWS / GitOps / Azure ISIS | AWS accounts InternalApps **and** SESMG; Ingress/RDS/S3/MSK/k8s-svc GitOps; Azure ISIS EOL | Azure of the SES-MG **client** |
| **SES-MG** | §3 Azure only | Databricks RMDS + AKS/Postgres (client subscription) | EKS / MSK / vaccination / apps on EKS |

SES-MG apps on EKS (vaccination, Druid, MSK, …) → **ISIS Saude → AWS/GitOps** with `hub=sesmg`.

## Extra gates

1. `REPLACE_WITH_*` in **endpoint / host / URL / JDBC** → row **BLOQUEADO**. No exception.
2. Narrow exception — **password/token** overwritten at runtime: `REPLACE_WITH_*` in a password/token field does **not** block the row when a Job/controller overwrites it at runtime **and** that mechanism is documented in column Fonte (manifest + what it patches + where the secret comes from). Without a documented mechanism → **BLOQUEADO**. The exception covers only the credential: the endpoint on the same row still requires a literal.
3. Resource removal → strike or delete the row in the same delivery.
4. Do not invent FQDN/IP/JDBC — only a value read now or `PENDING_*`.

## Project docs (in addition to MkDocs)

| Kind | What to require |
|------|-----------------|
| Repo **with** sibling `*-docs` | PR in the sibling repo linked in the body (checked by `docs-sync-gate`); local README/`docs/` changes do **not** replace it |
| Repo **without** sibling | README and/or `docs/` **in this repo** updated in this PR (example: `gitops/docs/platform-gitops-rules.md`) |

Sibling docs repos (org listing read 2026-10-16; the gate derives the sibling by stripping `-backend -frontend -rpa -data -api -iac -indexer` from the repo name, `_` → `-`, plus `-docs`):

| Code repo(s) | Sibling docs repo |
|--------------|-------------------|
| `vacinacao-backend`, `vacinacao-frontend`, `vacinacao-data` | `vacinacao-docs` |
| `cancer-mama`, `cancer-mama-backend`, `cancer-mama-rpa`, `cancer-mama-data` | `cancer-mama-docs` |
| `cancer-mama-apuracao-eixo3-data` | none derived — link `cancer-mama-docs` (gate warns, accepts) |
| `mamografia-backend`, `mamografia-frontend`, `mamografia-data` | `mamografia-docs` |
| `mamografia-profissional-integrador-backend`, `-frontend`, `-data` | `mamografia-profissional-integrador-docs` |
| `gestao-backend`, `gestao-frontend` | `gestao-docs` |
| `isis-platform-frontend` | `isis-platform-frontend-docs` |
| `isis_platform_api` | `isis-platform-api-docs` |
| `isis-ingestion` | `isis-ingestion-docs` |
| `luminai-backend`, `luminai-frontend` | `luminai-docs` |
| `portal-rmds-backend`, `portal-rmds-frontend` | `portal-rmds-docs` |
| `operation-center-backend`, `operation-center-frontend` | `operation-center-docs` |
| `gitops`, `helm-charts`, `aws-sesmg-iac`, `graphify-indexer`, `azure-internalapps-iac`, landing pages, `prototipos-frontend`, `trensrj`, `kafka-logger`, `renovatio-backend`, `operations-center`, `linear_agente`, `template-ecs`, `rmds-gestao-projetos`, `codigo-fonte-sesmg` | none — local README/`docs/` |

Catalog: `isis-saude/docs` → `docs/arquitetura/repos/index.md` and the repo page `docs/arquitetura/repos/<repo>.md` or `docs/arquitetura/<tema>.md`.

## Forbidden vs expected

```
BAD: bootstrap = TFC output without the broker string
BAD: inventory of stacks only, no endpoint table
BAD: EKS/MSK under SES-MG Azure
BAD: Crossplane Claim / XRD Claim for RDS in this contract
BAD: REPLACE_WITH_* on host/JDBC “because a Job fills it later”
BAD: password placeholder without citing the Job/controller that overwrites it
GOOD: host from Secret `*-connection` key `host` + date + hub=sesmg under ISIS Saude → GitOps
GOOD: literal broker string + TFC workspace + date
```
