# Dev Brief — Press Center: Custom Post Type
**Task:** [MO-27819](https://app.clickup.com/t/9003000798/MO-27819)
**Status:** Revisions requested
**Assignees:** Radmilo Petrovic, Marc Bloomquist

---

## What needs to be built

A custom post type (CPT) for Press Releases, similar to the existing `[sps_system_integrations]` shortcode pattern.

---

## URL structure
Confirmed by SEO (Hallie Froehlich) and Joe Cady.

- Hub page: `/press/`
- Individual releases: `/press/{slug}/`
- Press kit: `/press/press-kit/`

**Rules:**
- No dates or "sps-commerce" in slugs
- Keep slugs concise (40–50 chars max)
- Include the key press concept in the slug

---

## CPT requirements

- `/press/` is a standard WordPress **page** — not a CPT archive
- CPT posts sit under `/press/` as the URL parent: `/press/{slug}/`
- CPT archive should be disabled — the `/press/` page handles the listing via shortcode
- Date field on each release — used for chronological sorting on the hub
- Currently 12 press releases to populate

---

## Shortcode for hub page listing

Similar to `[sps_system_integrations]`. Each listing renders:

```html
<h4> Publish Date
<h3> Release title
<p>  Excerpt / body copy
<a>  Continue Reading → individual release URL
```

---

## References

- Hub stubbed at: https://www.spscommerce.com/press/
- Press kit stubbed at: https://www.spscommerce.com/press/press-kit/
- Figma linked in task
- Excel sheet of press releases linked in task comments
