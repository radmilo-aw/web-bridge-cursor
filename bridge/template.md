# Bridge Project Doc — Template

_This doc covers all web work for [product area] — not just the initial request. When new work comes in for the same area, add it here. Do not create a new doc._

**At intake: always check the CU Projects folder first.** If a doc exists for this product area, update it — add the new task to Connected Tasks, update What's Missing, create a new Jira task under the existing epic.

---

## Document structure

```
Main doc (= Jira epic)
├── Header
├── Connected Tasks          ← bridge fills on creation
├── What's Missing           ← auto + bridge adds manual items
├── Problem                  ← auto on first run, bridge edits
├── Decision                 ← bridge fills when ready
├── Bridge To-Dos            ← auto from blockers + bridge adds manual
├── Inputs & Decisions       ← auto from CU comments + bridge adds Slack/call notes
└── Bridge Checklist         ← bridge ticks off before each dev handoff

Subdoc — created at start
└── Learnings                ← empty until project closes

Subdoc — created only when solution is unclear
└── Research                 ← bridge works here during Defining
    └── [Recommendation]     ← becomes stakeholder-facing page when ready to share

Subdoc — created per dev handoff for complex/phased work only (= Jira task)
└── Dev Brief — [name]       ← one per phase, created only when that phase is ready
                             ← NOT needed for straightforward work (content swap,
                                simple build) — bridge writes task description
                                directly in Jira instead
```

**Jira epic:** always created — long-lived, future changes to the same product area land here.
**Jira task:** always created — bridge writes the task description at handoff (from Dev Brief if one exists, or directly if work is straightforward).

---

## Main page

---

**Type** ~~Single task~~ / ~~Multi-task~~  ← delete the one that does not apply, do this first

**CU Task** [MO-XXXXX](https://app.clickup.com/t/{task_id})  ← Single task only — remove this line for Multi-task
**Bridge Status** Defining / Ready for Dev / Dev in Progress / Parked  ← delete all but one
**Last AI run** —

**Requestor** —
**PM** —
**Accountable** —
**Reviewer** —
**Designer** —
**Content** —
**Priority** Tier 1 / 2 / 3 / 4

**Campaign Brief** —
**SharePoint** —
**Design** —

---

## Connected Tasks

_Bridge adds all dev tasks and subtasks that belong to this project. One line per task. This section is never auto-updated._

- [MO-XXXXX](https://app.clickup.com/t/{task_id}) — Task name

---

## What's Missing

_Live view of current active gaps only. Auto-populated from CU subtask statuses — Cursor reads each connected task's subtasks and checks status. Build and SEO/Metadata run in parallel — Launch is blocked until both are done. Bridge adds anything that arrived outside CU (e.g. design link shared on Slack but not in CU)._

_When a wave of work is fully complete, move its status block to Learnings (Completed Work section) and remove it here. This keeps the main doc focused on what needs action now._

_Note: for Single task projects this section can be a simple flat list. For Multi-task, use one block per task as shown below._

### [Task name (MO-XXXXX)](https://app.clickup.com/t/{task_id}) · Dev: [name or "not assigned"]
- [ ] Design — [status] ([owner])
- [ ] Copy — [status] ([owner])
- [ ] Build & QA — [status]
- [ ] Bridge QA — internal review (QA Excel)
- [ ] Metadata / SEO Review — [status] ([owner])
- [ ] Launch

_Note: for phased projects (e.g. Industry Pages), each phase has its own Bridge QA — template QA, pages QA, nav QA are separate events with separate checklists._

---

## Problem

_What is broken, missing, or being requested for the current active wave. Pulled from task descriptions on first run. Bridge edits to add context that is not in CU. When a wave closes, move this to Learnings and replace with the next wave's problem._

---

## Decision

_Bridge fills this when the path forward is agreed for the current active wave. When a wave closes, move this to Learnings and replace with the next wave's decision._

**What we're building:** —
**Decided by:** —
**Date decided:** —
**Reason:** —

---

## Bridge To-Dos

_Generated from unresolved blockers in What's Missing. Each item assigned to a bridge person via @mention — not a CU task. Bridge assigns who handles each item. Bridge can add manual items._

- [ ] @[bridge person] — Chase [PM/owner name]: [blocking task] is blocking [dev task] and not started
- [ ] @[bridge person] — [manual item added by bridge]

---

## Inputs & Decisions

_Running log. Auto-populated from CU comments on connected tasks. Bridge adds Slack messages, call notes, and email decisions manually._

**YYYY-MM-DD · Person · Source (CU comment / Slack / call / email)**
Entry.

---

## Bridge Checklist — before Ready for Dev

- [ ] All blockers in What's Missing resolved
- [ ] Problem confirmed with requestor or PM
- [ ] Decision documented above
- [ ] All open questions answered
- [ ] Dev person assigned in CU
- [ ] Jira epic created (long-lived — future changes to this product area land here)

**If straightforward work (content swap, simple build — no Dev Brief needed):**
- [ ] Jira task created with description: what to build, template/reference, content links, QA expectations

**If complex or phased work:**
- [ ] Dev Brief subdoc generated and reviewed with Radmilo
- [ ] Jira task created from Dev Brief

_Jira task description must always include the CU task link and the instruction: "When build is complete, post 'ready for QA' comment on the CU task." This is how bridge knows to start the Bridge QA._

- [ ] Bridge QA completed (QA Excel reviewed) — one per page for simple projects, one per phase for phased projects
- [ ] Task moved to Ready for Dev list

---

## Subdoc: Dev Brief — [name]

_One subdoc per dev handoff. Name reflects what it covers (e.g. Dev Brief — Template, Dev Brief — Pages). Created only when that phase is ready — not at project start. Cursor reads this subdoc to create the Jira task._

_Not generated until Decision section on main page is complete._

- **Objective** —
- **Technical approach** —
- **Scope** —
- **Out of scope** —
- **Open questions for dev** —
- **Acceptance criteria** —

---

## Subpage: Research

_Created only when solution is unclear at intake. Bridge works here during Defining. When ready to share with stakeholders for sign-off or budget approval, this page is shared directly._

- **Background** — why this research was needed
- **Constraints** — non-negotiable technical or business requirements any solution must meet
- **Research Questions** — what bridge needed to answer before recommending
- **Solutions Evaluated** — one block per option: what it is / pros / cons / estimated effort / cost
- **Recommendation** — chosen solution with reasoning
- **Why not the others** — brief rationale for ruling out alternatives
- **Cost and timeline** —
- **Proposed next steps** —

---

## Subpage: Learnings

_When a wave closes, move Problem, Decision, and What's Missing for that wave here. Main doc stays clean and current. Bridge fills the reflection questions per wave._

## Wave 1 — [description] · Closed [date]

**Problem:**
_Paste from main doc Problem section when wave closes._

**Decision:**
_Paste from main doc Decision section when wave closes._

**What shipped:**
- [Page / task name] — Live ✓ · Dev: [name]

**What went well:**

**What slowed us down:**

**What bridge should do differently next time:**

**Anything to add to the scenarios doc:**

---

_Add a new block above for each future wave._
