# Enterprise Search — Solution Recommendation

**Background**

The current site search only searches WordPress. It cannot return results from content managed in Hygraph. Users searching for supplier-related content get nothing or get the wrong thing. This is a structural limitation of WordPress's native search engine, not a configuration issue.

---

## Constraints

Any solution must work within these non-negotiable platform constraints:

- **Two content sources** — WordPress (Pantheon) and Hygraph (headless CMS via Next.js subfolder). Solution must connect to both.
- **10 active languages via WPML** — search results must be filtered to the visitor's active language, including 5 languages not shown in the public selector.
- **Pantheon multi-environment** — Dev, Test, and Live environments must have fully isolated search indices.
- **Editor exclusion controls** — content teams must be able to exclude pages from search without a dev request.

---

## Solutions Evaluated

| Solution | Annual Cost | Verdict |
|---|---|---|
| Algolia | ~$10,150/year | Recommended |
| Yext AI Search | $10,000–$500,000+/year | Strong technically — ruled out on pricing |
| Expertrec | ~$600–$1,900/year | Gap in Hygraph integration |
| ElasticPress | Not published (Beta) | Not suitable |

---

## Recommendation: Algolia

Algolia is the only platform that satisfies every requirement without custom engineering or meaningful gaps.

- Connects to Hygraph directly via official documented integration
- Supports all 10 languages including hidden market variants
- Editors can exclude content without dev involvement (WordPress editor + Hygraph editor + Algolia dashboard)
- Pantheon multi-environment handled — separate index per environment
- AI search (re-ranking) included in recommended plan
- Covers Next.js subfolder with official React components

---

## Why Not the Others

**ElasticPress** — No path to Hygraph without 10–20 days custom engineering. Pantheon version in Beta with no enterprise SLA.

**Expertrec** — Indexes Hygraph by crawling the frontend, not via direct API. Content has a time delay before appearing in search. Not reliable enough.

**Yext AI Search** — Technically strong but requires direct sales engagement, starts at $10,000–$500,000+/year. Ruled out on cost.

---

## Cost and Timeline

| Item | Cost |
|---|---|
| WP Search with Algolia Pro plugin | ~$149/year |
| Algolia Premium plan | ~$10,000/year |
| Hygraph sync function (Vercel free tier) | $0 |
| **Total annual recurring** | **~$10,150/year** |
| One-time development | 4–6 developer days |

---

## Proposed Next Steps

1. Approve solution and budget — confirm Algolia, approve ~$10,150/year
2. Procure licences — Algolia Premium + WP Search with Algolia Pro plugin
3. Development — 4–6 dev days
4. Phase 2 — evaluate Algolia Elevate for NeuralSearch after launch
