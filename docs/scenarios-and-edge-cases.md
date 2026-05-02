# Bridge Team — Scenarios & Edge Cases

_Rebuilt 2026-04-19 from complete CU pull (181 open tasks, all 11 Marketing folders)._
_Reference data: `docs/cu-full-task-breakdown.md`_

---

## How to use this doc

Each scenario describes a real pattern visible in CU data. For each: what the situation looks like, why it breaks without a bridge system, and what the bridge system must handle. These are inputs to system design — not solutions.

---

## Scenario 1 — The batch-pages project

**What it looks like in CU:**
11 separate parent tasks in New Navigation 2026 | Big Rocks, all created on the same date (2026-02-09), all assigned to Katie as the web person. Examples: MO-31313 through MO-31327. Each task = one page (Retail, Grocery, Fashion, Beauty, Auto Parts, Industrial Supplies, AI Commerce, Streaming Commerce, Social Commerce, International Commerce, Partner Onboarding).

**What web actually sees:**
One project — one template, one build approach, 11 deliverables. Nikoleta built one "Your Industry" template (MO-33281) that all 6 industry pages use. The template task arrived March 4, nearly a month after the page tasks were already in dev.

**Why it breaks:**
Marketing creates 11 CU tasks because they track each page by campaign, content owner, and SEO. Web has no automated signal that these 11 tasks are one project. Without a bridge person making that judgment, devs get 11 separate briefs (or 11 separate asks) for what is one build.

**What bridge must handle:**
When a cluster of tasks arrives with the same structure (same list, same creation date, naming pattern), a bridge person must group them into one Epic before any dev work starts. This grouping decision cannot be automated — it requires judgment. The system must surface the cluster clearly so the bridge person can make the call in standup.

**CU evidence:** MO-31313 to MO-31327, MO-33281 (template), MO-34942 (Nav section subtask added Apr 1)

---

## Scenario 2 — The tradeshow repeat pattern

**What it looks like in CU:**
18 tasks in Tradeshows / 2026 Events & Tradeshows, all assigned to Joe. Every event creates 2 subtasks automatically: "Build + Prep" and "Launch." All 16 of Joe's tradeshow subtasks are at "new intake" status. No due dates on most. Created between Feb 10 and Apr 2. None have progressed.

**Why it breaks:**
These are not requests with briefs — they are organizational templates. Someone (an events PM or automation) assigns Joe to tradeshow web subtasks as soon as an event is created in CU. Joe has 16 of these sitting at "new intake" doing nothing. They inflate his task count, create noise, and will eventually become urgent when an event deadline approaches.

**What bridge must handle:**
The system needs a way to distinguish stub tasks (organizational stubs with no brief, no movement) from real requests. Tradeshow tasks should not trigger an Epic until a specific event has a real brief and a real deadline. Bridge needs a parking mechanism — or a rule that "new intake with no due date and no description = park until deadline is visible."

**CU evidence:** MO-31488, MO-31489, MO-32566, MO-32567, MO-32603, MO-32604, MO-33380, MO-33381, MO-33528, MO-33529, MO-34028, MO-34029, MO-34064, MO-34066, MO-35047, MO-35048

---

## Scenario 3 — The ghost task (never cleaned up)

**What it looks like in CU:**
Tasks that are technically "in progress" or "backlog" but have been open for months or years with no movement.

Real examples:
- MO-17509 (FormAssembly) — created 2024-07-05, status "in progress", no due date. Joe. Open for 9+ months.
- MO-17647 (Server-side GTM) — created 2024-08-05, status "backlog". Radmilo. 8+ months.
- MO-17682, MO-17687 (Meta pixel audit/implementation) — created Aug–Dec 2024, status "design in progress". Joe.
- Multiple "live / launched" tasks still open: MO-27512, MO-24149, MO-24001 etc.

**Why it breaks:**
Ghost tasks inflate everyone's counts. Joe has 115 tasks but a significant portion are ghosts. Any bridge system that reads "all open tasks assigned to Joe" as a proxy for Joe's load will get a false picture. Automation that triggers on CU assignment change will fire on months-old tasks if they are ever touched.

**What bridge must handle:**
The system cannot rely on CU task count as a proxy for workload. Ghost tasks need a cleanup pass before the bridge system goes live. After go-live, bridge needs a periodic hygiene check (or a rule for marking tasks as parked if untouched for N days with no due date).

**CU evidence:** MO-17509, MO-17647, MO-17682, MO-17687, all "live / launched" tasks still open in Web folder

---

## Scenario 4 — The stuck task with no unblock owner

**What it looks like in CU:**
Tasks at "stuck / blocked" status with no visible driver pushing to resolve the block.

Real examples:
- MO-27813 (Update code live on SPS Commerce) — stuck, was due 2026-04-09. Radmilo. Part of RR Rebrand.
- MO-27106 (Organization schema code snippet) — stuck, due 2026-04-17. Radmilo. RR Rebrand.
- MO-34446 (Remove Korpak Case Study) — stuck. Joe.
- MO-31325 (Social Commerce page) — stuck, Katie. Part of Nav Phase 3, was due 2026-04-16.

**Why it breaks:**
"Stuck" in CU is a dead-end status. The task has a problem but CU has no escalation path. Nobody is formally responsible for unblocking it. Tasks can sit at "stuck" indefinitely.

**What bridge must handle:**
Stuck tasks must have a named unblock owner (a bridge person). When a dev task goes stuck, the bridge system must route it to the responsible bridge person, not leave it in a status queue. The bridge person owns getting it unstuck — whether that means getting a decision from a stakeholder, retrieving missing assets, or escalating to Joe/Radmilo.

**CU evidence:** MO-27813, MO-27106, MO-34446, MO-31325

---

## Scenario 5 — The invisible dev (Predrag and Lazar)

**What it looks like in CU:**
Predrag: 1 open task (MO-26904, Social Poster subtask, dev in progress). Lazar: 1 open task (MO-32299, RR+A analytics page, approved). Both do real work that is not tracked in CU — or not assigned to them in CU.

**Why it breaks:**
Predrag's primary work (AI features, Social Poster, backend) lives mostly in Radmilo's personal Jira, not in SPS CU. Lazar gets content work and dev work through informal assignment (Slack, direct conversation) with no CU trail. The bridge system cannot see their load. A bridge person making a work assignment decision based on CU data will think Predrag and Lazar are free.

**What bridge must handle:**
Jira (the bridge's control layer) must be the source of truth for dev load — not CU. When Predrag or Lazar is assigned a task in Jira, that is the record. CU data cannot be used to assess whether either is available. The bridge system must also have a way to surface Predrag's work from Radmilo's personal Jira — or migrate it into the bridge Jira during the pilot.

**CU evidence:** Predrag: only MO-26904. Lazar: only MO-32299. Both confirmed doing real work beyond what CU shows.

---

## Scenario 6 — The solo contractor (Marc with no bridge)

**What it looks like in CU:**
Marc has 39 open tasks spread across 6 folders: Nav 2026, Retail Pod, Core Pod, RR+A, Tradeshows, Content Team. Almost every task is a subtask (Build & Prep, Launch, QA) assigned directly by marketing pods. Radmilo or Katie are not co-assigned on the majority. Task names: "Build & QA - NEW page", "Build & Prep - NEW page", "Build + Prep", "Launch" — no briefs visible.

**Why it breaks:**
Marc receives work directly from marketing pods with no bridge involvement. He executes because he is a contractor who absorbs coordination overhead mid-build. The brief (if any) lives in Slack. The result is inconsistent quality and rework — the clearest illustration of why the bridge system needs to exist.

**What bridge must handle:**
Before go-live: marketing pods must be told that web subtasks must route through bridge before being assigned to Marc (or any dev). After go-live: Marc should receive tasks only via Jira (bridge-originated dev tasks with full brief). The bridge system does not solve Marc's quality issue — it solves the brief issue. If Marc has a full brief and still delivers poor quality, that is a contractor management problem.

**CU evidence:** 39 tasks across Nav 2026 (MO-31868, MO-31884, MO-31900, MO-31908), Retail (MO-31610, MO-31612), Tradeshows (MO-31450), Content (MO-33976, MO-33977), etc.

---

## Scenario 7 — Work arriving from 6 different marketing pods

**What it looks like in CU:**
Web team tasks appear in 11 folders across the Marketing space. The 6 marketing pods each create their own web requests: Retail Pod, Core Pod, Rev Recovery + Analytics Pod, Supplier Pod, Tradeshows, Corporate Marketing. Each has its own naming convention, folder structure, and priority signals. There is no standardized intake form.

Folder task counts (current): Cross-Team 97, Tradeshows 18, Retail 12, Content 12, AI/A 9, RR+A 7, Supplier 3, Corporate 2, Growth 4.

**Why it breaks:**
Bridge people do not have a single place to see new web requests. They have to monitor 11 folders across multiple CU spaces. Each pod assigns web team directly. Without a daily aggregated view, bridge people will miss new assignments or discover them late.

**What bridge must handle:**
The daily standup digest (n8n → Slack) must aggregate new assignments to web team members across all 11 folders — not just the Web folder. It must surface these assignments grouped by meaningful signals (list, creation date, naming pattern) so bridge people can decide what becomes an Epic. The digest is the intake trigger.

**CU evidence:** All 11 folders in cu-full-task-breakdown.md

---

## Scenario 8 — The multi-person project (multiple web people, multiple non-web people)

**What it looks like in CU:**
RR Rebrand (MO-27993): Joe + Radmilo. SupplierWiki (MO-34574): Katie, then Radmilo and Joe on subtasks. Nav 2026 (MO-31313–31327): Katie + Nikoleta + Marc + Radmilo + Joe all on different subtasks of the same project. Many tasks have multiple web team members assigned at different task depths.

**Why it breaks:**
When multiple web people are on different parts of the same project, who owns the web deliverable? Who writes the Jira Epic? Who is the bridge contact for the marketing side? Without a named web owner per project, tasks fall through the cracks between bridge people.

**What bridge must handle:**
Every Epic must have exactly one bridge owner. The bridge owner is responsible for the web deliverable — coordinating all web subtasks, all assets, all stakeholder review. Other web people can execute tasks under the Epic but the owner is the single point of contact. The bridge owner writes the brief, creates the dev task, and owns QA sign-off.

**CU evidence:** MO-27993, MO-34574, MO-31313–31327, MO-26904 (Social Poster: Radmilo + Predrag)

---

## Scenario 9 — The repeat/recurring work type

**What it looks like in CU:**
Some work arrives on a predictable cadence and follows the same pattern every time:
- Tradeshows: every event = Build + Prep + Launch subtasks for Joe. Happens monthly.
- SupplierWiki articles: new articles added to Content Team list on a rolling basis (6 batches visible since Jan 2026).
- Case Studies: Corporate Marketing assigns Build + Launch subtasks as new case studies are published.

**Why it breaks:**
If bridge creates a full Epic for each tradeshow landing page, each SupplierWiki article, and each case study, bridge people will drown in admin for templated work. These are not complex projects — they are repeating production tasks.

**What bridge must handle:**
Recurring work types need a different track than project work. Options: a standing Epic per work type (one "Tradeshows 2026" Epic, one "SupplierWiki Articles" Epic), a checklist/template brief, or a fast-track where the repeat pattern is pre-approved and bridge just routes. This needs a decision before go-live.

**CU evidence:** Tradeshows folder (18 tasks), Content Team / SupplierWiki Project List (12 tasks), Corporate Marketing / Case Studies (2 tasks)

---

## Scenario 10 — The escalating task (past due, still open)

**What it looks like in CU:**
Tasks that were due in the past and are still open with no visible action:
- MO-27813 (Update code live on SPS) — due 2026-04-09, stuck/blocked, Radmilo
- MO-27106 (Organization schema) — due 2026-04-17, stuck/blocked, Radmilo
- MO-31325 (Social Commerce page) — due 2026-04-16, stuck, Katie
- MO-31327 (AI Commerce page) — due 2026-04-10, dev in progress, Katie
- MO-31323 (Unify EDI page) — due 2026-04-09, needs stakeholder review, Katie
- Multiple Nav 2026 subtasks with past due dates sitting at "backlog"

**Why it breaks:**
Past-due tasks in CU generate no alerts to bridge people. They just sit. The marketing PM who created the task doesn't know it's stuck — they expect it to be done. When they follow up, they go directly to the dev (or the bridge person via Slack), not through any structured escalation.

**What bridge must handle:**
The bridge system needs a daily escalation check: any task past due date in Jira that is not at Done or Parked must appear in the standup digest with an "overdue" flag. Bridge people must address overdue tasks before new intake. The system cannot silently allow overdue tasks to accumulate.

**CU evidence:** MO-27813, MO-27106, MO-31325, MO-31327, MO-31323

---

## Open questions — not yet resolved

**Q1: What is Joe's real role in the bridge system?**
Joe has 115 tasks but the majority are stubs, QA co-assignments, and ghost tasks. His real function appears to be: SPS relationship holder, tradeshow/event owner, and QA signoff. He is not writing briefs and is not making technical decisions. Where exactly does he sit in the flow?

**Q2: How does bridge handle work that goes directly to Radmilo (not through Katie/Joe)?**
Radmilo is assigned directly to tasks in AI/A, RR Rebrand code work, SupplierWiki. The head of COE sends Radmilo problems directly. These tasks often never flow through a bridge intake — Radmilo just does them. The system must account for this without adding overhead for Radmilo.

**Q3: What is the minimum behavior change required from each marketing pod?**
The 6 pods currently assign web team directly. The bridge system requires that pods route through intake instead. This is the largest change management problem. What is the minimum ask from each pod?

**Q4: How does the repeat work track work — standing Epic or something else?**
Tradeshows, SupplierWiki articles, and Case Studies are recurring. Does each get its own Epic, or is there a standing lane? This must be decided before pilot.

**Q5: When does Predrag's work become visible in Jira?**
Predrag's AI/backend work is tracked in Radmilo's personal Jira. During the pilot, how does this get migrated or mirrored so bridge can see his load?
