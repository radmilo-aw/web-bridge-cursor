# Bridge Project — Development

Internal development repo for the SPS Commerce web team bridge workflow system. This is where the system is designed, built, and maintained.

Full project context and current status: `CLAUDE.md`

---

## Setup

- **Editor:** Cursor — Claude Code CLI runs in the integrated terminal
- **AI:** Claude Code CLI (`claude` command) — Cursor's built-in AI is not used
- **CU data:** fetched live via CU MCP (no scripts, no local JSON)
- **Context:** `CLAUDE.md` at root — Claude Code CLI reads this automatically

---

## Folder structure

```
Bridge_Project/
├── CLAUDE.md               ← full project context for Claude Code CLI
├── docs/                   ← system design, team profiles, scenarios, design history
├── tasks_pm/               ← PM reference files — not bridge workflow
└── n8n-workflows/          ← n8n workflow JSON (when built)
```


