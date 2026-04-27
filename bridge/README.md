# Bridge Team — Cursor Setup & Usage

This folder contains everything you need to create, update, and re-run project docs in ClickUp using Cursor AI + CU MCP.

Run `git pull` before starting a session to get the latest updates.

---

## One-time setup

### 1. Clone this repo

```
git clone https://github.com/radmilo-aw/web-bridge-cursor
```

Open the **root folder** (`web-bridge-cursor`) in Cursor — not a subfolder. Cursor needs the root to load the AI context automatically.

### 2. Add ClickUp MCP to Cursor

Open **Cursor Settings → MCP → + Add new MCP server** and replace the contents with:

```json
{
  "mcpServers": {
    "clickup": {
      "url": "https://mcp.clickup.com/mcp"
    }
  }
}
```

Save and restart Cursor.

### 3. Authorise ClickUp

Open Cursor chat (Cmd+L) and type any CU request — for example:

```
Fetch task MO-34679 and tell me its title and status.
```

On first use Cursor opens a browser window. Log in with your SPS ClickUp account and click Authorise. Done — all CU fetches work automatically after that.

---

## Before every session

Check if a doc already exists for the product area you're working on:

**CU Projects folder:** `https://app.clickup.com/9003000798/v/dc/8c9xryy-117351`

If a doc exists — update it. Never create a duplicate.

---

## Daily use

1. Open Cursor Agent (Cmd+I)
2. Attach the prompt file for what you need
3. Add the CU task URL or doc URL and send

| What you need | When | Prompt file |
|---|---|---|
| Create a new project doc | New CU task, no doc exists yet | `prompts/01-create-doc.md` |
| Update with new information | New info from standup, Slack, or email | `prompts/02-update-doc.md` |
| Re-run from latest CU data | Refresh everything from current CU state | `prompts/03-rerun-doc.md` |

---

## Reference

| File | What it is |
|---|---|
| `template.md` | Master doc template — all docs follow this structure |
| `examples/retailer-pages/` | Multi-task example |
| `examples/industry-pages/` | Phased project example |
| `examples/new-search/` | Single task / research phase example |

**Key rules:**
- One doc per product area — update the existing doc, never create a duplicate
- What's Missing is a live view — move completed waves to Learnings
- Inputs & Decisions is append-only — never delete existing entries
- Bridge To-Dos are not CU tasks — @mentions in the doc only
