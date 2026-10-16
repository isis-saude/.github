---
description: Ponto de partida de qualquer tarefa ou decisão — isis-saude/docs é a única fonte de verdade; MCP graphify antes de código
alwaysApply: true
---

# Ponto de partida: docs + graphify (CRÍTICO)

Cópia idêntica em `.claude/rules/ponto-de-partida.md` de todos os repositórios da org `isis-saude`. Origem: `isis-saude/docs`. Mudou lá, muda em todos.

Quem carrega: Claude Code lê este arquivo; Cursor pelo symlink `.cursor/rules/ponto-de-partida.mdc` → este arquivo; Copilot pelo `.github/copilot-instructions.md` do repo.

## Antes de qualquer decisão

1. **`isis-saude/docs` é a única fonte de verdade.** Site: <https://symmetrical-bassoon-4qv51go.pages.github.io/> (Pages privado). Arquitetura, contratos, inventário, runbooks, acesso e onde cada coisa vive estão lá. README, `CLAUDE.md` e comentário de código não substituem o docs; se divergem, o docs vence e a divergência vira PR no `docs`.
2. **Consulte o MCP graphify** (`https://graphify.isissaude.com.br/mcp`) antes de grep ou de afirmar como as partes se ligam. Toda tool recebe `project_path="/data/<repo>"`; sem repositório em mente, comece por `/data/docs`. Conexão (Tailscale com `--accept-routes` + chave no 1Password `Shared`) e regra do agente: `docs/arquitetura/graphify.md` § "Como usar (devs)".
3. O grafo é do branch padrão no último índice (até ~24 h). Para mudança local ou outro branch, leia os arquivos.
4. Não afirme que regra, doc ou processo não existe sem ter lido o `docs`. Lacuna no `docs` se registra no `docs`; não se preenche de memória nem de suposição.
