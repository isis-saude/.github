---
name: code-review
description: 'Review pull requests for contract, endpoint, and inventory documentation. Use when reviewing a pull request, doing a code review, or checking docs and inventory coverage. Skip Dependabot and internal chore with no contract impact when the PR body states that exemption.'
---

# Code review — documentation source of truth

Follow this skill and `reference-docs-sot.md` in this directory.

GitHub Copilot code review on github.com only sees files **in this repository**. Use the **GitHub MCP** (enabled by default for Copilot review) to read sibling repos in org `isis-saude`: `get_file_contents`, search pull requests, search code. Do not guess inventory lines or hostnames.

## 1. Classify the diff

**Contract / visible endpoint / consumer-facing behavior** includes any of:

- New, changed, or removed FQDN, hostname, IP, JDBC, bootstrap, Ingress, RDS, MSK, blob/DFS URL, platform `*.svc.cluster.local`, Terraform output consumed by apps
- New chart/values surface that exposes a connection (hostname, port, connection env)

**Exempt** (do not require docs PRs) when the change is only:

- Dependabot (dependency bump)
- Internal chore with no contract impact
- Docs-only with no new/changed endpoint

If exempt, the PR body must include one line stating **no contract impact** (or that it is Dependabot). Comment in pt-BR only if that justification is missing.

## 2. If contract: require both documentation sides

1. **Project docs** — README and/or `docs/` **in this repo**, or a sibling `*-docs` repo (table in `reference-docs-sot.md`). The PR body must link a PR or commit there (same Linear ID or explicit URL). If this PR already updates those local docs, that side is satisfied.
2. **MkDocs source of truth** — `isis-saude/docs` file `docs/arquitetura/inventario-recursos.md` (and the repo page under `docs/arquitetura/` when the catalog applies). The PR body must link a PR on `isis-saude/docs`. If **this** repository **is** `isis-saude/docs`, this PR **is** the MkDocs side: verify table format, taxonomy, and that no host is invented; still require the project-docs side in the code repo unless the body explains why it does not apply.

Apply the inventory gate in `reference-docs-sot.md` (literal / `PENDING_<FONTE>` / **BLOQUEADO**). Closing with “see TFC / cluster / dynamic” is a finding.

## 3. How to comment

- Write review comments in **Brazilian Portuguese (pt-BR)**.
- Point to **file and line**.
- Never invent FQDNs, IPs, JDBC strings, or claim an inventory row exists without reading it via MCP.
- Copilot review is always a **Comment** — it does not block merge. Still flag missing docs as required follow-up before merge.
