---
name: code-review
description: 'Review pull requests for documentation coverage on two levels (isis-saude/docs and <project>-docs), contract/endpoint inventory, and that linked docs PRs actually describe the diff. Use when reviewing a pull request, doing a code review, or checking docs and inventory coverage. Skip Dependabot and docs-only PRs.'
---

# Code review — documentation source of truth

Follow this skill and `reference-docs-sot.md` in this directory.

GitHub Copilot code review on github.com only sees files **in this repository**. Use the **GitHub MCP** (enabled by default for Copilot review) to read sibling repos in org `isis-saude`: `get_file_contents`, search pull requests, search code. Do not guess inventory lines or hostnames.

## 0. Every code change needs docs on two levels (hard gate)

The required workflow **`docs-sync-gate`** (org ruleset, `.github-governance`) blocks merge of any PR that changes code unless the PR body links, for the same delivery:

1. **General** — an open or merged PR on `isis-saude/docs` (repo page under `docs/arquitetura/repos/`, catalog, inventory when an endpoint changes).
2. **Detail** — an open or merged PR on the sibling `<project>-docs` repo (table in `reference-docs-sot.md`). Only when no sibling exists, local `README*.md` / `docs/**` / `*.md` changes in this PR satisfy this level.

Job `docs-sync` checks that the links exist and point to open/merged PRs. Job `copilot-docs-review` (Copilot CLI, same workflow) reads the diff and the linked docs PRs and fails on `REPROVADO`. In the native code review you repeat that semantic check with the GitHub MCP: open the linked docs PRs with the GitHub MCP and confirm they describe **this** diff (new env var, endpoint, flag, job, chart value, Terraform output…). A docs PR that does not cover the change is a finding, even though the gate is green.

Exempt from the gate: Dependabot and other bots, docs-only PRs, repos `docs` / `*-docs` / `.github` / `.github-governance`, and break-glass label `docs-exempt` + body line `Sem impacto em docs: <justificativa>`. Flag a `docs-exempt` whose justification does not hold.

## 1. Classify the diff

**Contract / visible endpoint / consumer-facing behavior** includes any of:

- New, changed, or removed FQDN, hostname, IP, JDBC, bootstrap, Ingress, RDS, MSK, blob/DFS URL, platform `*.svc.cluster.local`, Terraform output consumed by apps
- New chart/values surface that exposes a connection (hostname, port, connection env)

**Exempt from the inventory row** (not from section 0) when the change is only:

- Dependabot (dependency bump)
- Internal chore with no contract impact
- Docs-only with no new/changed endpoint

If exempt, the PR body must include one line stating **no contract impact** (or that it is Dependabot). Comment in pt-BR only if that justification is missing.

## 2. If contract: the `isis-saude/docs` PR must carry the inventory

The general-level PR from section 0 must update `docs/arquitetura/inventario-recursos.md` (and the repo page under `docs/arquitetura/` when the catalog applies). If **this** repository **is** `isis-saude/docs`, this PR **is** the MkDocs side: verify table format, taxonomy, and that no host is invented; still require the code-repo and `<project>-docs` sides linked in the body unless it explains why they do not apply.

Apply the inventory gate in `reference-docs-sot.md` (literal / `PENDING_<FONTE>` / **BLOQUEADO**). Closing with "see TFC / cluster / dynamic" is a finding.

## 3. How to comment

- Write review comments in **Brazilian Portuguese (pt-BR)**.
- Point to **file and line**.
- Never invent FQDNs, IPs, JDBC strings, or claim an inventory row exists without reading it via MCP.
- Copilot review is a **Comment** (approval is opt-in since 2026-09; never Request changes) — it does not block merge. The block comes from `docs-sync-gate`; your review adds the semantic check on top.
