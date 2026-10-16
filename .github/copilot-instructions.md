# Copilot — repository instructions

On **pull request review**, use the skill `code-review` at `.github/skills/code-review/` (`SKILL.md` and `reference-docs-sot.md`).

Use the GitHub MCP (`get_file_contents`, search pull requests, search code) in org `isis-saude`. Do not invent hostnames, FQDNs, JDBC strings, or inventory rows.

Write review comments in **Brazilian Portuguese (pt-BR)**, pointing to file and line.

Ponto de partida para qualquer repositório da org: `isis-saude/docs` é a única fonte de verdade (site <https://symmetrical-bassoon-4qv51go.pages.github.io/>); consulte o MCP graphify (`docs/arquitetura/graphify.md`) antes de qualquer decisão.

PRs must cite a Linear issue (`Fixes INF-xx` / `Fixes INFRA-xx` and `**Linear:**`). Every PR with code changes must link a PR on `isis-saude/docs` (general) **and** on the sibling `<project>-docs` (detail; local README/`docs/` only when no sibling exists) — enforced by the required workflow `docs-sync-gate` (job `docs-sync` checks the links; job `copilot-docs-review` runs Copilot CLI over the diff and the linked docs PRs and blocks on `REPROVADO`). Your native review repeats the semantic check. Contract/endpoint changes additionally require the inventory row in `isis-saude/docs`. Dependabot and docs-only PRs are exempt.

GitHub Copilot code review leaves a Comment (approval is opt-in since 2026-09; never Request changes) — it does not block merge; `docs-sync-gate` does. Custom instructions for review are on by default (*Use custom instructions when reviewing PRs*); there is no Terraform resource for that toggle.
