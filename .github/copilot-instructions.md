# Copilot — repository instructions

On **pull request review**, use the skill `code-review` at `.github/skills/code-review/` (`SKILL.md` and `reference-docs-sot.md`).

Use the GitHub MCP (`get_file_contents`, search pull requests, search code) in org `isis-saude`. Do not invent hostnames, FQDNs, JDBC strings, or inventory rows.

Write review comments in **Brazilian Portuguese (pt-BR)**, pointing to file and line.

Ponto de partida para qualquer repositório da org: `isis-saude/docs` é a única fonte de verdade (site <https://symmetrical-bassoon-4qv51go.pages.github.io/>); consulte o MCP graphify (`docs/arquitetura/graphify.md`) antes de qualquer decisão.

PRs must cite a Linear issue: `Fixes <ID>` when the PR closes the card, `Part of <ID>` when it delivers only part of it, plus the line `**Linear:** [<ID>](https://linear.app/iasis/issue/<ID>)` (teams `INFRA`, `IAS`; see `isis-saude/docs` → `docs/arquitetura/linear.md`). Every PR with code changes must link a PR on `isis-saude/docs` (general) **and** on the sibling `<project>-docs` (detail; local README/`docs/` only when no sibling exists), enforced by the required workflow `docs-sync-gate`. Exempt: bot authors, docs-only PRs and the repos `docs`, `*-docs`, `.github`, `.github-governance`. Contract/endpoint changes additionally require the inventory row in `isis-saude/docs`.

Two required workflows run Copilot CLI on every PR to the default branch and, through the `integration-branch-gates` ruleset (enforcement `evaluate`: never blocks), on every PR to `develop` when it is not the default branch: `docs-sync-gate` (job `copilot-docs-review`: do the linked docs PRs describe the diff?) and `rules-review-gate` (does the PR follow the documented platform rules?). On the default branch they block only when their org variable is `block`; on `develop` they do not block. Your native review is an extra read on top of them.

GitHub Copilot code review leaves a Comment (approval is opt-in since 2026-09; never Request changes); it does not block merge. Custom instructions for review are on by default (*Use custom instructions when reviewing PRs*); there is no Terraform resource for that toggle.
