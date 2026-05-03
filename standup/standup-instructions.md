# Standup Generation Instructions

Full how-to for generating and syncing the daily standup doc. Read this file whenever running either standup command.

---

## Two commands — run on working days (Mon–Fri) only

---

### 1. Morning — generate standup

**Steps in order:**

1. Check today is Mon–Fri — stop if not a working day.
2. Find the most recent page in Bridge Standup doc (`8c9xryy-118171`) — this is the previous standup date.
3. Carry forward any unchecked `- [ ]` questions per person (Joe, Katie, Radmilo) from that page.
4. Query **New Intake** (`901113657903`) for tasks created after the previous standup date → build New Intake section.
5. Query **Site Bug & Updates** (`901113645407`) for tasks created after the previous standup date → build Site Bug & Updates section.
6. Query **Defining** (`901113657911`), **Ready for Dev** (`901113657913`), and **Dev in Progress** (`901113657914`) for tasks overdue or due within 3 days → build Active Work section.
7. Save to `standup/YYYY-MM-DD.md` — Radmilo reviews.
8. On approval: create new CU page in doc `8c9xryy-118171` with today's date as title.

---

### 2. After call — sync

- Read the CU page for today's date from doc `8c9xryy-118171`.
- Overwrite `standup/YYYY-MM-DD.md` with the final version (includes decisions filled during the call).

---

## How to query bridge lists via API

Bridge lists use **secondary list membership** — tasks originate in "All Marketing Requests" (primary list) and are added to bridge lists as secondary members. `get_tasks` by list ID returns 0. Always use `clickup_search` with `filters.location.subcategories`:

```
filters: {
  asset_types: ["task"],
  location: { subcategories: ["<list_id>"] },
  created_date_from: "YYYY-MM-DD"   ← optional, for "new since" queries
}
```

This applies to all bridge lists and Site Bug & Updates. The `@taazkareem` `get_tasks` tool and `clickup_filter_tasks` both fail for these lists.

**Bridge list IDs:**
| List | ID |
|---|---|
| New Intake | `901113657903` |
| Defining | `901113657911` |
| Ready for Dev | `901113657913` |
| Dev in Progress | `901113657914` |
| Parked | `901113657916` |
| Site Bug & Updates | `901113645407` |

---

## Section rules

### New Intake — what to show

- Only tasks created **after the previous standup date** with **no assignee** (bridge hasn't started them).
- Exclude tasks that also appear in the Defining list (already pushed).
- Exclude tasks with statuses: `live / launched`, `complete`, `closed`, `done`, `approved`.
- Sort by due date ascending (closest first); no due date goes at the end — flat list, no status grouping.
- If nothing qualifies: `_No new tasks since [date]._`

**Dependency check:** for each New Intake task, fetch full details via `mcp__claude_ai_ClickUp__clickup_get_task` (detail_level: detailed) and inspect the `dependencies` array. If upstream dependencies exist (type 1 = waiting on), look up each blocking task to get its name, assignee, due date, and CU status. Surface this on the Status line.

**Per-task block:**
```
#### [MO-XXXXX](url) — Task Name
- **Due:** [date] · [X days overdue / in X days]   ← omit if no due date
- **Status:** [CU status] OR blocked — waiting on [MO-XXXXX](url) Name · Assignee · due date · CU status
- **Owner:** [name or —]
- **Requestor:** [creator name]

> One-sentence plain-language description of what the task is asking for.
```

Overview is a blockquote (`>`), not a bullet. Description should be plain language — what actually needs to happen, not the CU task title repeated.

---

### Site Bug & Updates — what to show

- Tasks created after the previous standup date.
- If none: `_No new bugs or updates since [date]._`
- Same per-task block format as New Intake (H4, blockquote description).

---

### Active Work — Overdue & Due Within 3 Days

Query Defining, Ready for Dev, and Dev in Progress for tasks that are overdue or due within 3 days. Group by list under H3 subheadings. Each group is a markdown table:

```
### Defining

| Task | Name | Assignee | Status | Due |
|---|---|---|---|---|
| [MO-XXXXX](url) | Task Name | Assignee name(s) | status | Apr 30 · 2 days overdue |
```

- Omit H3 groups with no qualifying tasks.
- If nothing qualifies across all three lists: `_Nothing due within 3 days._`

---

## Doc structure (standup/YYYY-MM-DD.md)

```markdown
# [Month Day, Year] — [Day of week]

---

## Questions for the Call

### Joe
- [ ] Question

### Katie
- [ ] Question

### Radmilo
- [ ] Question

**Rule:** only add `- [ ] Question` placeholder if the person has no carried questions. If they already have carried items, omit the placeholder.

---

## New Intake — New Since [prev date] (N tasks)

[per-task blocks]

---

## Site Bug & Updates — New Since [prev date] (N tasks)

[per-task blocks]

---

## Active Work — Overdue & Due Within 3 Days (N tasks)

### Defining

| Task | Name | Assignee | Status | Due |
|---|---|---|---|---|

### Ready for Dev

| Task | Name | Assignee | Status | Due |
|---|---|---|---|---|

### Dev in Progress

| Task | Name | Assignee | Status | Due |
|---|---|---|---|---|

---

## Decisions & Actions

| Decision / Action | Owner | Due |
|---|---|---|
|  |  |  |

---

_Notetaker transcript → subpage of this doc_
```

---

## Notes

- **Local standup files accumulate over time** — use them to spot patterns: tasks sitting in New Intake across multiple days, recurring question types, questions carried forward repeatedly.
- **n8n will automate morning generation** once the Claude Code CLI flow is validated. The local copy remains even after n8n takes over.
