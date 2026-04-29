# Runbook — Bridge Project Git & Cursor Setup

Single repo for everyone. Bridge people clone it, open the root in Cursor, and work in `bridge/`. Radmilo uses the full project for development.

---

## Phase 1 — Push Bridge Project to GitHub ✅ (Radmilo only)

**Step 1 — Create repo on GitHub**

1. Log in to GitHub
2. New repository → name it (e.g. `web-bridge-cursor`) → set to **Private** → do NOT add README or .gitignore
3. Copy the repo URL

**Step 2 — Connect and push**

```bash
cd /Users/mac/Documents/Bridge_Project
git remote add origin https://github.com/[username]/web-bridge-cursor
git push -u origin master
```

Done. The repo is live.

---

## Phase 2 — Add ClickUp MCP to Cursor (one time per person)

1. Open Cursor → **Cursor Settings → MCP → + Add new MCP server**
2. Replace the contents with:

```json
{
  "mcpServers": {
    "clickup": {
      "url": "https://mcp.clickup.com/mcp"
    }
  }
}
```

3. Save (Cmd+S) and restart Cursor
4. On first CU fetch a browser window opens — log in with your SPS ClickUp account and click Authorise

---

## Phase 3 — Validate MCP is working

Open Cursor Agent (Cmd+I) and type:

```
Use the CU MCP to fetch task MO-34679 and tell me its title and status.
```

Expected: returns the task title and current status from CU.

---

## Phase 4 — Validate a full doc operation

Open `bridge/prompts/03-rerun-doc.md` in Cursor, attach it to the Agent, paste a CU doc URL, and confirm the output matches current CU state.

---

## Phase 5 — Share with Katie and Joe

Send them the GitHub repo link. Their setup:

1. Clone the repo:
   ```bash
   git clone https://github.com/radmilo-aw/web-bridge-cursor
   ```
2. Open the **root folder** in Cursor (not a subfolder)
3. Add ClickUp MCP — follow Phase 2 above (one time only)
4. On first CU fetch, authorise via browser

That's it. `bridge/README.md` has day-to-day usage instructions.

---

## Keeping it up to date

When Radmilo updates templates, examples, or prompts in `bridge/`:

```bash
git add .
git commit -m "[describe what changed]"
git push
```

Katie and Joe run `git pull` before starting a session.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| MCP not showing after adding | Restart Cursor |
| Browser auth window doesn't open | Remove the clickup block from `~/.cursor/mcp.json`, restart, re-add |
| CU fetch returns "not found" | Use `MO-XXXXX` format, not raw task ID |
| Auth window timed out | Try the fetch again — it will re-open the auth window |
| Cursor AI has no project context | Make sure you opened the root folder, not a subfolder |
