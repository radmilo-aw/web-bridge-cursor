# Bridge Team — Project Context for Claude

## What this project is

A workflow design and implementation project for a web team inside a Marketing COE at SPS Commerce. Three goals: reduce Radmilo and Katie's bridge admin; reduce Joe's admin and make him better at his role; keep the dev team efficient without growing headcount.

This is a test project to prove the concept works. Once validated, a new project will be set up with the real client Jira and ClickUp.

**Working setup (Radmilo):** Cursor is the single editor — one folder (`Bridge_Project`), one git repo. Claude Code CLI runs in Cursor's integrated terminal. Cursor's built-in AI is not used — all AI work goes through Claude Code CLI.

**Doc creation:** Claude Code CLI only. Cursor MCP packages can read CU tasks/docs but cannot create docs — doc creation requires the `claude.ai` ClickUp MCP, which is account-level and only available in Claude Code CLI. Katie and Joe take on doc creation once they have Claude licences; a new co-work project will be set up at that point based on this one.

**CU MCP — Claude Code CLI connections:**
- `@taazkareem/clickup-mcp-server` → task reads/writes — **✅ Connected**
- `claude.ai` ClickUp MCP → doc creation (`clickup_create_document`, `clickup_create_document_page`) — **✅ Connected**
- Google Drive MCP: claude.ai account-level integration, not used here — shows as "needs auth" in `claude mcp list`, ignore it

---

## Reference docs — read these when relevant

**Local:**
| File | Contents |
|------|----------|
| `docs/team-and-roles.md` | All team profiles, org context, external stakeholders |
| `docs/scenarios-and-edge-cases.md` | 10 real scenarios with CU evidence — why the bridge system must exist |
| `docs/standup-design.md` | Standup structure, 5 agenda buckets, intake assessment rules |
| `docs/design-history.md` | What we tried before landing on the current design — key pivots and why |

**CU — read live via MCP when needed:**
| What | Where |
|------|-------|
| Project doc examples (structure, sections, real content) | CU Projects folder: `https://app.clickup.com/9003000798/v/dc/8c9xryy-117351` |
| Standup call doc examples (structure, Overview, Decisions) | CU Bridge Standup doc — parent doc ID `8c9xryy-118171` |

---

## Project folder structure

```
Bridge_Project/
├── CLAUDE.md                    ← you are here — always in root
├── docs/                        ← system design, team profiles, scenarios, design history
├── standup/                     ← local standup doc copies, one MD per working day (YYYY-MM-DD.md)
├── tasks_pm/                    ← PM reference files (SEO migration, press center, etc.) — not bridge workflow
└── n8n-workflows/               ← workflow JSON files, numbered prefix (e.g. 01-name.json)
```

**CU data — use MCP directly:** CU tasks, comments, and status are fetched live via CU MCP. No scripts or local JSON snapshots needed.

**Rules for Claude when creating new files:**
- n8n workflow JSON → `n8n-workflows/`, numbered prefix
- System design updates → `docs/`
- Standup docs → `standup/YYYY-MM-DD.md`
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

**Claude Code CLI setup:**
- ✅ Radmilo: `@taazkareem/clickup-mcp-server` + `claude.ai` ClickUp MCP both connected
- ⏳ Katie and Joe: pending Claude licences — co-work project set up when licences land

**Standup doc workflow:**

Two commands Radmilo runs each working day (Mon–Fri only):

1. **Morning — generate standup:**
   - Check today is a working day (Mon–Fri) — stop if not
   - Find the most recent page in Bridge Standup doc (`8c9xryy-118171`)
   - Carry forward any unchecked `- [ ]` questions per person (Joe, Katie, Radmilo) from that page
   - Query New Intake (`901113657903`) and Site Bug & Updates (`901113645407`) for tasks created after that page's date
   - Query Defining (`901113657911`) for tasks due within 3 days (overdue or upcoming) — show only those; if none, write "Nothing due within 3 days"
   - Save to `standup/YYYY-MM-DD.md` — Radmilo reviews
   - On approval: create new CU page in doc `8c9xryy-118171` with today's date as title

**New Intake section format — each task is an H4 heading (collapsible in CU), grouped by status:**
- **Exclude** tasks with these statuses: `live / launched`, `complete`, `closed`, `done`, `approved`
- Status group order (most actionable first): Ready for Review → Dev in Progress → In Progress → Queued → New Intake → Backlog → Stuck / Blocked
- Within each status group: sort overdue first (ascending by date), then upcoming (ascending), then no due date
- Omit groups that have no tasks

Per-task block structure:
```
#### [MO-XXXXX](url) — Task Name
- **Due:** [date] · [X days overdue / in X days]   ← omit Due line if no due date
- **Status:** [status]
- **Owner:** [name or —]
- **Requestor:** [creator name]

> One-sentence overview of what the task is asking for.
```
Overview is a blockquote (`>`), not a bullet — keeps it visually distinct.

2. **After call — sync:**
   - Read the CU page for today's date from doc `8c9xryy-118171`
   - Overwrite `standup/YYYY-MM-DD.md` with the final version (includes decisions filled during call)

**IMPORTANT — how to query bridge lists via API:**
Bridge lists use **secondary list membership** — tasks originate in "All Marketing Requests" (primary list) and are added to bridge lists as secondary lists. `get_tasks` by list ID only returns primary-list tasks and will return 0 for all bridge lists.

**Always use `clickup_search` with `filters.location.subcategories`:**
```
filters: {
  asset_types: ["task"],
  location: { subcategories: ["<list_id>"] },
  created_date_from: "YYYY-MM-DD"   ← optional, for "new since" queries
}
```
This applies to all 5 bridge lists and Site Bug & Updates. The `@taazkareem` `get_tasks` tool and `clickup_filter_tasks` both fail for these lists.

**Local standup files (`standup/`) accumulate over time** — use them to spot patterns: tasks sitting in New Intake across multiple days, recurring question types, questions carried forward repeatedly.

**n8n will automate the morning generation** once the Claude Code CLI flow is validated. The local copy remains even after n8n takes over.

---

**Automation vision — post-pilot only, do not build yet:**

Bridge workflow has three layers — pilot proves the process manually first, automation added after.

| Layer | Tool | When |
|---|---|---|
| Bridge creates project doc, adds connected tasks | Manual | Always — bridge judgment |
| Claude Code CLI populates/re-runs project doc from CU data | Claude Code CLI | Bridge-triggered |
| Claude Code CLI generates Dev Brief | Claude Code CLI | Bridge-triggered when phase is ready |
| Claude Code CLI generates daily standup page → local MD + CU | Claude Code CLI | Manual now — n8n automates once flow is validated |
| n8n re-runs all active project docs (new CU comments, subtask statuses) | n8n | Automated, every morning |
| CU Notetaker captures standup decisions → n8n appends to project docs | n8n + CU Notetaker | Triggered when notetaker output lands |
| n8n creates Jira epic + tasks when Dev Brief marked Ready | n8n | Triggered by Dev Brief status change |
| n8n updates/adds Jira tasks when Dev Brief updated or new phase added | n8n | Triggered by Dev Brief change |

CU Doc structure for standup: Web folder → Bridge Standup (parent doc) → one subdoc per day (generated by n8n).

**What to do next:**
1. Build and validate standup doc generation via Claude Code CLI — use existing CU Bridge Standup docs as reference; n8n automates this post-pilot
2. Build Dev Brief template — read existing CU project docs as reference
3. **BLOCKED: Configure Ready for Dev, Dev in Progress, Parked columns** — do not configure until Dev Brief template is done
4. Send admin request to rename/convert Web Team Assignment fields — send once workflow is validated
5. Set up space-level automation in CU UI: task assigned to Web Team Admin → move to New Intake list
6. Pilot with real tasks

---

## Overall project progress

1. ✅ Set up Jira pilot environment (BTP at askonweb.atlassian.net) — clean slate
2. ✅ Built scripting infrastructure (`scripts/`) — working against live SPS CU API
3. ✅ Built real evidence base — full 187-task CU pull, scenarios doc, team profiles
4. ✅ Built data pipeline — pull → enrich → filtered markdown (no re-pulling for filters)
5. ✅ Designed the system — bridge CU workflow confirmed, 5 lists created in SPS Web folder
6. ✅ New Intake + Defining columns configured in CU UI
7. **Now: Build templates (Dev Brief → project doc → Jira ticket mapping) before configuring remaining lists**
8. Pilot the new design manually
9. Document pilot findings
10. Build automation — only after pilot proves the process
11. Present to bridge team (Joe, Radmilo, Katie)
12. Present to head of COE
