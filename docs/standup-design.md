# Bridge Standup Design

## Purpose

Morning prep tool for the bridge person on duty (Radmilo, Katie, or Joe — anyone can run it). Reviews new and in-flight tasks before standup. Output is a structured agenda the team works through together.

---

## Two Task Origins

### CU Tasks
Created by marketing PMs in ClickUp, assigned to a bridge person first. Flow: **CU → Jira**.

### Web Team Tasks
Created by the web team directly in Jira. Pushed to CU for visibility so all web work appears in one place for PMs and stakeholders. Flow: **Jira → CU**.

---

## Intake Rules — CU Tasks

**Rule 1 — First assignee must be a bridge person**
Only tasks where the first assignee is Radmilo, Katie, or Joe enter the system. Agreement with PMs required before go-live: all new web tasks must be assigned to a bridge person first.

**Rule 2 — Dev assignee blocks Jira push**
If a dev is added as assignee, the system does not push the task to Jira again. Bridge adds devs after intake is complete.

**Rule 3 — New tasks only**
System applies to tasks created on or after go-live date. Existing tasks are handled manually and run out naturally.

---

## Standup Agenda — 5 Buckets

### 1. New Bridge Task — Intake
Tasks newly assigned to a bridge person since last standup (CU tasks) or newly created by the web team (Jira tasks).

For each CU task:
- What information do we have? (description, requestor, PM, brief, SharePoint folder)
- Is the task a MAIN or SUB? If SUB — check parent MAIN for additional context
- If SUB — what sibling tasks exist before this one, and are they done?
- Does anyone on the bridge team already know context for this task?
- If nobody knows → assign one bridge person to chase the PM/creator

For each Web Team task:
- Do we need approval from someone outside web to start?
- Do we need input from another team (OPS, Ads, etc)?
- If neither — task is self-contained, can go straight to dev

### 2. Existing Bridge Tasks — Defining
Tasks bridge is already chasing for missing information.

For each task:
- Has the assigned bridge person resolved the missing info?
- If stuck — do we need to escalate or push the due date?

### 3. Ready for Dev
Tasks fully qualified and ready to hand to the web team.

For each task:
- Does it belong to an existing Epic in Jira, or does it need a new Epic?
- Which dev picks it up?

### 4. Dev in Progress — Status Check
Tasks currently being worked on by the web team.

For each task:
- Are we on track for the due date?
- Does the dev need more time?
- Any new questions that need bridge involvement?

### 5. Parked
Tasks on hold or waiting on external dependencies.

For each task:
- Is any bridge person or dev free to pick up a parked task?
- Is any unqualified parked task now actionable?

---

## Intake Card — CU Task

Fields pulled from CU at the moment a task is first assigned to a bridge person:

| Field | Source |
|-------|--------|
| Task name | CU task |
| Type (MAIN / SUB) | CU task |
| Parent name + ID | CU task (if SUB) |
| Created date | CU task |
| Due date | CU task |
| Web assignee | CU task (current) |
| Creator | CU task |
| Requestor | CU custom field |
| PM | CU custom field |
| Campaign Brief | CU custom field (URL) |
| SharePoint Folder | CU custom field (URL) |
| Description | CU task |

If SUB task — also pull from parent MAIN:
- Requestor, PM, Campaign Brief, SharePoint Folder, Description

---

## Intake Card — Web Team Task

Fields filled by the web team when creating the task in Jira:

| Field | Notes |
|-------|-------|
| Task name | What needs to be done |
| Description | Full context — what, why, expected output |
| Created by | Web team member who initiated it |
| Due date | |
| Approval needed | Yes / No — if yes, who |
| External input needed | Yes / No — if yes, which team (OPS, Ads, etc) |

After standup bridge decides: self-contained → assign to dev. Needs approval or input → moves to Defining bucket.

---

## Intake Assessment — CU Tasks

**Minimum to pass to dev:**
- Description explains what web needs to build
- Requestor or PM identified (someone to go back to)
- Copy/brief exists — Campaign Brief URL, SharePoint Folder, or content subtask is done

**If minimum not met → Bridge task (Defining)**
Bridge assigns one person to chase missing info. Task does not go to Jira as a web task until qualified.

---

## What Is Not In Scope

- Existing tasks (pre go-live) — handled manually
- Tasks assigned directly to devs — bypass bridge, not tracked by this system
- Watchers — change over time, not used
- Project Brief attachment field in CU — never populated, not used
