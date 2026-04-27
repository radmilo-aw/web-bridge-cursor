# Bridge Team — Project Context for Claude

## What this project is

A workflow design and implementation project for a web team inside a Marketing COE at SPS Commerce. Three goals: reduce Radmilo and Katie's bridge admin; reduce Joe's admin and make him better at his role; keep the dev team efficient without growing headcount.

This is a test project to prove the concept works. Once validated, a new project will be set up with the real client Jira and ClickUp.

Doc generation for bridge people runs via **Cursor + CU MCP** — all 3 bridge people have Cursor licences, not all have Claude. Cursor connects to CU API via MCP so bridge can generate project docs without scripts.

**Working setup (Radmilo):** Cursor is the single editor for this project — replaces VS Code, one folder (`Bridge_Project`), one git repo. Claude Code CLI runs in Cursor's integrated terminal. Cursor's built-in AI is not used — all AI work goes through Claude Code CLI.

---

## Reference docs — read these when relevant

| File | Contents |
|------|----------|
| `docs/team-and-roles.md` | All team profiles, org context, external stakeholders |
| `docs/scenarios-and-edge-cases.md` | 10 real scenarios with CU evidence — rebuilt 2026-04-19 from full 187-task pull |
| `docs/diagrams/01-industry-pages-reality.md` | Industry Pages timeline and gap analysis — real failure evidence |
| `docs/session-log.md` | Full history of what was done and decided each session |
| `bridge/template.md` | Project doc template — structure for all CU project docs bridge creates |
| `bridge/examples/` | Filled-in examples per project (industry-pages/, new-search/) — one file per CU doc page |

**Archived docs** (old design — do not use as reference): `docs/archive/`

---

## Project folder structure

```
bridge-team/
├── CLAUDE.md                    ← you are here — always in root
├── bridge/                      ← bridge people's source files (template, examples)
│   ├── template.md              ← project doc template for CU docs
│   └── examples/                ← filled-in examples per project type
├── docs/                        ← system design, team profiles, session log (dev only)
├── n8n-workflows/               ← workflow JSON files, numbered prefix (e.g. 01-name.json)
├── runbooks/                    ← setup and operational notes
└── scripts/                     ← Jira API scripts (pilot testing)
```

**CU data — use MCP directly:** CU tasks, comments, and status are fetched live via CU MCP in Cursor. No scripts or local JSON snapshots needed.

**Rules for Claude when creating new files:**
- n8n workflow JSON → `n8n-workflows/`, numbered prefix
- Operational runbooks and pilot notes → `runbooks/`
- System design updates → `docs/`
- Bridge people's working files (template, examples) → `bridge/`
- Never create files in the root except `CLAUDE.md`
- Create folders when the first file is needed — do not create empty folders

---

## Current status — where we are

**April 24, 2026 — Bridge team stays in CU, dev team stays in Jira**

New development: bridge team has a dedicated Web folder in SPS Marketing CU space with edit permission. Bridge workflow lives entirely in CU — Jira is for dev team only (not parked, just not bridge's tool).

**Design decided:**

**Structure:**
- 5 lists in SPS Web folder as bridge stage buckets: New Intake → Defining → Ready for Dev → Dev in Progress → Parked
- No board view grouped by list (not supported in this CU plan) — bridge works within each list individually
- Each list has columns customized in CU UI to show only relevant existing fields — no new custom fields added
- Marketing tasks (Web Team Work) untouched — bridge works their own tasks, links back as needed

**Intake flow:**
- PMs create tasks anywhere in the Marketing space (Web Team Work is just a collector, not the only source)
- PM assigns Web Team Admin group → triggers automation → task moves to New Intake list
- Web Team Admin assignment is the exclusive signal for bridge work — nothing reaches the web team without going through bridge first
- Space-level automation needed (Marketing space, not just Web folder): task assigned to Web Team Admin → move to New Intake

**Assignment lifecycle:**
1. Task created → PM assigns Web Team Admin group
2. Bridge picks up → Web Team Admin removed, bridge person added via Web Bridge Assignment field
3. Defining → bridge works it, creates Project doc for complex tasks, dev brief written before moving forward
4. Ready for Dev → Jira ticket created automatically (automation TBD) — no dev assignee in CU yet
5. Dev picks up Jira ticket → dev assignee added in CU, task moves to Dev in Progress
6. Dev in Progress — CU tracks who's working it; dev works in Jira, CU reflects reality

**Grouping & readiness:**
- Multiple related tasks (e.g. 6 Industry Pages) → 1 Jira epic + tasks; parent task in CU = epic unit
- Bridge manually confirms all subtasks defined before moving parent to Ready for Dev
- Dev brief is a CU doc attached to the parent task — Jira ticket links back to CU for dev context

**Dev tracking & reporting:**
- Assignee field always reflects who owns the task — CU is source of truth for dev workload
- PMs can see what dev X is working on without going into Jira

**Jira:**
- Dev team's tool only — bridge doesn't work in Jira
- Jira epic/ticket created automatically at Ready for Dev handoff (n8n — mechanism TBD, field mapping TBD)
- Testing target: askonweb.atlassian.net BTP project

**SPS Web folder IDs (for reference):**
- Folder: `90117842910` | Web Team Work list: `901112557134` | Site Bug & Updates list: `901113645407`
- Web Team Admin group ID: `e5f4f415-15d5-4f9c-8f5f-3f06d61bacbd`

**Bridge lists in SPS Web folder (created 2026-04-24):**
- New Intake: `901113657903`
- Defining: `901113657911`
- Ready for Dev: `901113657913`
- Dev in Progress: `901113657914`
- Parked: `901113657916`

**Personal workspace prototype: skipped** — MCP access to SPS CU means we build directly in SPS Web folder where all 3 bridge people already have access.

**CU field changes — admin request drafted (pending send):**
- Rename "Web Team Assignment" (people field) → `Web Bridge Assignment`
- Rename "Web Team Assignment" (text field) → `Web Bridge Status` + convert to dropdown
- Dropdown values (in order): To Review / No Brief / No Design / No Content / Clarifying / Researching / Blocked / Ready
- Once converted: Defining list will group by Web Bridge Status

**Project doc — when to create:**
- Not all tasks get a doc — bug fixes and small updates go straight to Jira ticket, no doc
- Complex tasks (new feature, new page, research needed, multi-task project): bridge creates Project doc at Defining stage
- Signal that doc exists: paste CU doc link into the `Project Brief` field on the task

**Cursor + CU MCP setup (Radmilo next — immediate):**
- Cursor opened on `Bridge_Project` folder — single editor, one git repo, Claude Code CLI in integrated terminal
- CU MCP config needed in Cursor settings (`.cursor/mcp.json`) with Radmilo's CU API key
- All 3 bridge people use Cursor for doc generation (claude-sonnet-4-6 model via CU MCP)
- Radmilo + Katie share Cursor budget with other dev work; Joe's budget mostly free — Joe handles heavy batch doc generation
- Each person configures CU MCP once in Cursor settings with their own CU API key
- Set up Radmilo first, validate, then write `BRIDGE.md` setup instructions for Katie and Joe

**Automation vision — post-pilot only, do not build yet:**

Bridge workflow has three layers — pilot proves the process manually first, automation added after.

| Layer | Tool | When |
|---|---|---|
| Bridge creates project doc, adds connected tasks | Manual | Always — bridge judgment |
| Cursor populates/re-runs project doc from CU data | Cursor + CU MCP | Bridge-triggered |
| Cursor generates Dev Brief | Cursor + CU MCP | Bridge-triggered when phase is ready |
| n8n generates daily standup subdoc in CU | n8n | Automated, every morning |
| n8n re-runs all active project docs (new CU comments, subtask statuses) | n8n | Automated, every morning |
| CU Notetaker captures standup decisions → n8n appends to project docs | n8n + CU Notetaker | Triggered when notetaker output lands |
| n8n creates Jira epic + tasks when Dev Brief marked Ready | n8n | Triggered by Dev Brief status change |
| n8n updates/adds Jira tasks when Dev Brief updated or new phase added | n8n | Triggered by Dev Brief change |

CU Doc structure for standup: Web folder → Bridge Standup (parent doc) → one subdoc per day (generated by n8n).

**What to do next:**
1. ✅ Create 5 bridge lists in SPS Web folder
2. ✅ New Intake columns configured
3. ✅ Defining columns configured (Web Bridge Status as text field interim — values typed manually until admin converts)
4. ✅ Project doc template designed (`docs/bridge-doc-template.md`) + examples (`docs/examples/`)
5. Send admin request to rename/convert Web Team Assignment fields (request drafted above)
6. **BLOCKED: Ready for Dev, Dev in Progress, Parked columns — do not configure until Dev Brief template done**
7. Finish Dev Brief template + example
8. **NEXT: Set up CU MCP in Cursor (Radmilo first)** — open Bridge_Project in Cursor, configure `.cursor/mcp.json` with CU API key, validate
9. Write `BRIDGE.md` — Cursor instructions for bridge people (populate doc, re-run, generate Dev Brief) — after Radmilo's setup validated
10. Set up CU MCP for Katie and Joe (after BRIDGE.md written)
11. Set up space-level automation in CU UI: task assigned to Web Team Admin → move to New Intake list
12. Pilot with real tasks

---

## Overall project progress

1. ✅ Set up Jira pilot environment (BTP at askonweb.atlassian.net) — clean slate
2. ✅ Built scripting infrastructure (`scripts/`) — working against live SPS CU API
3. ✅ Built real evidence base — full 187-task CU pull, scenarios doc, team profiles
4. ✅ Built data pipeline — pull → enrich → filtered markdown (no re-pulling for filters)
5. ✅ Designed the system — bridge CU workflow confirmed, 5 lists created in SPS Web folder
6. ✅ New Intake + Defining columns configured in CU UI
7. **Now: Build templates (Dev Brief → project doc → Jira ticket mapping) before configuring remaining lists**
7. Pilot the new design manually
8. Document pilot findings
9. Build automation — only after pilot proves the process
10. Present to bridge team (Joe, Radmilo, Katie)
11. Present to head of COE
