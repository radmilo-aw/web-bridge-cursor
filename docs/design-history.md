# Bridge Project — Design History

What we tried, why we changed direction, and what we landed on.

---

## Direction 1 — Jira as control center (April 17–18)

**What we built:**
- Jira pilot project (BTP) at askonweb.atlassian.net with two boards: Bridge Board and Dev Board
- 9 shared statuses across both boards
- Plan: CU webhook fires on assignee change → n8n checks prerequisites → Claude API drafts brief → Jira ticket created with brief pre-filled
- Confluence as the living project doc per Epic (replacing CU Documents)
- Personal CU test environment with 8 mirror tasks from real SPS data

**Why we dropped it:**
- The CU → Jira auto-trigger was the wrong model. Industry Pages evidence proved it: 6 separate CU tasks are one web project. Firing on each task creates 6 Jira intake items for what is 1 Epic — bridge people have more admin than before.
- Grouping is a human judgment call (same creation date, naming pattern, same list) — it cannot be automated.
- Confluence adds another tool. Developers should not be in CU; bridge and dev sharing context in Confluence means a third context layer on top of CU and Jira.
- Key finding from Industry Pages chaos: build approach was never confirmed before dev started. Template task created March 4, due March 5 (next day), while dev work was already underway. Katie was coordinating timelines, QA sheets, and Figma across 5 separate CU tasks on the same day. One missing gate caused 6 weeks of confusion — the bridge system must enforce that gate, not just route tasks.

**What we salvaged:**
- The 5-bucket standup model (New Intake, Defining, Ready for Dev, Dev in Progress, Parked) — kept in the CU design.
- The intake rules: first assignee must be a bridge person; dev assignee blocks Jira push; new tasks only.
- The standup card format and intake assessment criteria — documented in `docs/standup-design.md`.

---

## Direction 2 — CU-only bridge workflow (April 22–24)

**What we built:**
- Bridge team stays entirely in CU — no Jira for bridge, Jira for dev team only.
- 5 lists in SPS Web folder as stage buckets: New Intake → Defining → Ready for Dev → Dev in Progress → Parked.
- PM assigns Web Team Admin group → space-level automation → task moves to New Intake.
- Web Team Admin assignment is the exclusive intake signal.
- Columns configured for New Intake and Defining lists.
- Personal workspace prototype built (New Intake list with 7 Industry Pages tasks) — then skipped in favour of building directly in SPS Web folder since bridge team already had edit access.

**Key decision — board view dropped:**
CU board view supports columns = lists, but this CU plan does not support grouping by list on a board view. Bridge works within each list individually.

**Key decision — n8n deferred:**
n8n is only needed once the process is proven manually. All routing can start with native CU automations and manual steps. Automation added after pilot validates the process.

**What we built for doc generation at this stage:**
- Project doc template designed from scratch using real CU data (Industry Pages, New Search, Retailer Pages).
- Template structure: Header, Connected Tasks, What's Missing, Problem, Decision, Bridge To-Dos, Inputs & Decisions, Bridge Checklist.
- Examples created for three project types: multi-task (Industry Pages), phased (Retailer Pages), single-task/research (New Search).
- CU AI dropped at this stage — too slow, not controllable.

**This direction is current — CU workflow design is locked.**

---

## Direction 3 — Cursor + CU MCP for doc generation (April 26 – May 1)

**What we tried:**
- Bridge people use Cursor AI with CU MCP to generate and update project docs.
- Two MCP packages: `clickup-mcp-server` (doc reads) + `@taazkareem/clickup-mcp-server` (task reads/writes).
- Prompt files written for create, update, and re-run operations.
- Setup docs written for sharing the repo with Katie and Joe via git.

**Why we dropped it:**
- Cursor MCP packages (`clickup-mcp-server`, `@taazkareem/clickup-mcp-server`) can read CU tasks and docs but **cannot create CU docs**.
- Doc creation requires the `claude.ai` ClickUp MCP integration, which is account-level and only available in Claude Code CLI — not available as an npm package for Cursor.
- The git sharing concept (Katie and Joe clone the repo, use Cursor for doc work) is paused until they have Claude licences.

---

## What we landed on

**Bridge workflow:** CU-only, 5 lists in SPS Web folder. Bridge works entirely in CU; Jira is dev team's tool only. Design is locked — lists created April 24.

**Doc generation:** Claude Code CLI only. Radmilo runs Claude Code CLI in Cursor's integrated terminal. Claude connects to CU via `claude.ai` ClickUp MCP (creates docs) and `@taazkareem/clickup-mcp-server` (reads/writes tasks). Both connected and working.

**Automation:** Post-pilot only. Pilot proves the process manually first. n8n, standup doc generation, CU Notetaker integration — all deferred.

**Next:** When Katie and Joe have Claude licences, a new co-work project will be set up based on this one. The current project is Radmilo's development environment only.
