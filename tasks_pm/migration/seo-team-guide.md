# SPS Commerce — SEO Migration and Redirection Status

**Audit date:** 2026-05-01  
**Prepared by:** Web Team

---

## What was audited

All English WordPress blog posts (253) and non-case-study resources (47 FAQ Pages, Infographics, White Papers, Research & Evaluation) — **300 posts total** — were checked against:

- The WordPress Redirection plugin (are redirects in place?)
- The /community CMS (does the article exist?)
- Live HTTP responses (do the redirect destinations actually load?)

Two deliverable files were produced:

| File | Purpose |
|---|---|
| `sps-community-migration-status.xlsx` | EN blog + resource audit — full status per post with actions needed |
| `language-redirects.xlsx` | DE/NL/FR redirect pairs — 298 ready to import, 2 FR pending /community page creation |

---

## Key findings — English content

| Status | Count | What it means |
|---|---|---|
| ✅ Confirmed working | 154 | WP redirect in place, /community page live — nothing to do |
| ⚠️ Issues — need action | 5 | Resources in your SEO plan with a problem |
| ❓ No redirect — decision needed | 97 | Live WP posts with no redirect at all |
| 🔍 Redirected elsewhere — review needed | 47 | Posts redirected to non-/community destinations |
| 🔧 Ready to add to WP | 92 | Posts already in /community — just need the WP redirect added |
| **Total reviewed** | **303** | |

---

## File 1: sps-community-migration-status.xlsx

### ✅ Working (154)

154 redirects confirmed working end-to-end. No action needed. Included for reference only.

---

### ⚠️ Issues (5)

5 resources from your SEO plan that have a problem. Each row has an **Action needed** column.

| Resource | Problem | Action |
|---|---|---|
| `benefits-of-edi-for-peter-grimm` | /community page is 404 | /community team fixes broken page first, then WP team adds redirect |
| `podcast-sps-commerce-connects-global-supply-chain` | /community page is 404 | /community team fixes broken page first, then WP team adds redirect |
| `fulfilling-consumer-demand` | No WP redirect | WP team adds redirect |
| `inventory-turnover-ratio` | No WP redirect | WP team adds redirect |
| `sps-commerce-white-paper-point-sale-data-sharing` | No WP redirect | WP team adds redirect |

**Owner:** /community team for the 2 broken pages; WP team for all 5 redirects once pages are confirmed live.

---

### ❓ No Redirect (97)

97 posts currently live on WordPress with no redirect — visitors land on the WP page with no forwarding. Each row includes a **Recommended action** column and an **In /community?** column.

| In /community? | Count | Breakdown | Recommended action |
|---|---|---|---|
| yes | 89 | 89 blog posts | WP redirect needed — article already exists in /community. These 89 are listed in the **🔧 Add Redirect** tab. |
| no | 8 | 3 FAQ Pages, 3 White Papers, 1 Infographic, 1 R&E | Content not yet in /community — decide: migrate, retire, or redirect elsewhere |

**Owner:** SEO team decides per row for the 8 not yet in /community. The 89 that are in /community are already handled in the **🔧 Add Redirect** tab.

---

### 🔍 Redirected Elsewhere (47)

47 posts that do have a WP redirect, but it points somewhere other than /community.

| Destination pattern | Count | Notes |
|---|---|---|
| → /blog/ listing page | 22 | Likely retired content — confirm these are intentionally dead-ended |
| → another specific page | 24 | Intentional-looking redirects — confirm destination is still correct |
| → /community/ (broken hub) | 1 | Points to a generic /community/articles/ page — needs a specific destination |

**Owner:** SEO team reviews each row and confirms the redirect is correct, or flags for a /community redirect instead.

---

### 🔧 Add Redirect (92)

The most actionable tab. These 92 posts are **already live in /community** — the only thing missing is the WordPress redirect. Each row has the exact source and destination ready to enter in the Redirection plugin.

| Column | Description |
|---|---|
| WP source path | Enter this as the **Source URL** in the Redirection plugin |
| /community destination | Enter this as the **Target URL** |
| HG headline (verify) | The article title in /community — confirm it matches the WP post before adding |

92 rows: 89 blog posts + 3 resources.

**Owner:** WP team adds all 92 redirects in the Redirection plugin.

---

## File 2: language-redirects.xlsx

### Current state

Zero redirects currently exist for any non-English blog post. All DE, NL, and FR posts are live on WordPress with no forwarding.

### What's in the file — ready to import (298 of 300)

These posts are covered by the SEO plan — source and destination already defined. Each row has three columns:

- **WP source path** — e.g. `/de/blog/some-slug/`
- **/community destination** — e.g. `/community/articles/some-slug/`
- **In /community?** — `yes` or `no` — whether the destination page actually exists

| Sheet | Language | Total rows | Ready (yes) | Pending (no) |
|---|---|---|---|---|
| DE | German | 106 | 106 | 0 |
| NL | Dutch | 100 | 100 | 0 |
| FR | French | 94 | 92 | 2 |
| **Total** | | **300** | **298** | **2** |

**Owner:** WP team imports rows where **In /community? = yes**. The 2 FR rows marked `no` need the /community page created first before the redirect can be added.

### What's not in the file — decisions needed (98 posts)

These posts exist in WordPress but are not covered by the SEO plan. They have no redirect and no defined destination.

| Language | Posts not in SEO plan | Action needed |
|---|---|---|
| DE | 30 | SEO team: decide per post — migrate to /community, retire, or redirect elsewhere |
| NL | 35 | SEO team: decide per post — migrate to /community, retire, or redirect elsewhere |
| FR | 33 | SEO team: decide per post — migrate to /community, retire, or redirect elsewhere |
| **Total** | **98** | |

### EUR and AU — not included

EUR (22 posts) and AU (66 posts) are not in this file — **no EUR or AU content exists in /community at all.** The /community CMS (Hygraph) only has English, Dutch, French, and German articles. These 88 posts have no /community equivalent to redirect to.

They are covered in a separate tab in `sps-community-migration-status.xlsx` — see **Sheet 6 — EUR/AU** below.

---

---

## Sheet 6 — EUR/AU (sps-community-migration-status.xlsx)

### Current state

88 WordPress posts exist in EUR (22) and AU (66) locales. **No EUR or AU content exists in /community.** The /community CMS only has English, Dutch, French, and German articles.

### What's in the tab

Each row is a EUR or AU post currently live on WordPress with no redirect and no /community equivalent.

| Column | Description |
|---|---|
| Language | `eur` or `au` |
| WP source URL | The WordPress URL that needs a redirect |
| Slug | The post slug |
| EN /community URL | Populated if an English /community article with the same slug exists — a possible redirect target |
| Redirect destination | **Blank — SEO team fills this in** |
| Notes | `EN article available in /community` (22 rows) or `No /community equivalent found` (66 rows) |

| Group | Count | Notes |
|---|---|---|
| EN article exists in /community | 22 | Can redirect to the EN `/community/articles/{slug}/` URL |
| No /community equivalent | 66 | AU-specific or older content — decide: retire or redirect elsewhere |

### What the SEO team needs to decide per row

- Redirect to the EN /community equivalent (where one exists)
- Redirect elsewhere (e.g. a related page)
- Retire (e.g. → `/blog/` listing)

Fill in the **Redirect destination** column, then hand to WP team to add the redirects.

---

## Summary of actions by team

### /community team
- Fix 2 broken EN resource pages: `benefits-of-edi-for-peter-grimm` and `podcast-sps-commerce-connects-global-supply-chain`
- Create 2 missing FR pages flagged in `language-redirects.xlsx` (FR sheet, **In /community? = no**)

### WP team
- Add 92 EN redirects from the **🔧 Add Redirect** tab in `sps-community-migration-status.xlsx`
- Add 5 EN resource redirects from the **⚠️ Issues** tab (after /community pages are fixed)
- Import 298 DE/NL/FR redirects from `language-redirects.xlsx` (rows where **In /community? = yes**)
- **Total: ~395 redirects to add now, +7 once broken pages are fixed**

### SEO team
- Review the **❓ No Redirect** tab — 8 EN posts not yet in /community: decide migrate, retire, or redirect elsewhere
- Review the **🔍 Redirected Elsewhere** tab — 47 EN posts: confirm existing redirects are correct or flag for /community
- Decide on 98 DE/NL/FR posts not covered by the SEO plan (30 DE, 35 NL, 33 FR)
- Fill in **Redirect destination** in the **🌏 EUR/AU** tab — 88 posts with no /community equivalent (22 have an EN article to redirect to; 66 need a decision)
