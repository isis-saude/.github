# Copilot — repository instructions

On **pull request review**, use the skill `code-review` at `.github/skills/code-review/` (`SKILL.md` and `reference-docs-sot.md`).

Use the GitHub MCP (`get_file_contents`, search pull requests, search code) in org `isis-saude`. Do not invent hostnames, FQDNs, JDBC strings, or inventory rows.

Write review comments in **Brazilian Portuguese (pt-BR)**, pointing to file and line.

PRs must cite a Linear issue (`Fixes INF-xx` / `Fixes INFRA-xx` and `**Linear:**`). Contract/endpoint changes require project docs (local or `*-docs`) **and** a PR on `isis-saude/docs` (inventory). Dependabot and internal chore with no contract impact are exempt when the body says so.

GitHub Copilot code review always leaves a Comment (it does not block merge). Custom instructions for review are on by default (*Use custom instructions when reviewing PRs*); there is no Terraform resource for that toggle.

Agent rule for this repo: `.claude/rules/ponto-de-partida.md` (isis-saude/docs is the single source of truth; start from the docs site and the graphify MCP before any decision).
