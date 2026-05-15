---
date: 2026-05-15
session: a0971f1c
tags: [thai-html, crm, workflow, content-production]
---

# Lock Segments Before Building Slides

When building CRM, influencer, or campaign slides — define the audience segmentation axis (by product? by persona? by channel?) before creating any structure. Rebuilding mid-session is expensive and introduces version confusion.

**Pattern**: Ask "by product or by customer type?" as the first question, not after slides exist.

---

# Thai Character Edit Trap

When using Edit tool on Thai-language HTML/JS files, always `grep -n` the exact target line first before constructing `old_string`. Thai characters can diverge subtly between rendered display and raw file content, causing silent mismatches.

**Fix pattern**: `grep -n "keyword" file.html` → use surrounding ASCII context to anchor the match.

---

# Thai Accordion Pattern (Reusable Shell)

CSS + JS pattern for Thai explainer dropdowns in HTML briefs:
- `.explain-btn` — pill button with arrow
- `.explain-box` — hidden panel with `.etag` chips
- `toggleExplain(btn)` — single toggle function

Confirmed working in bts-gtm-briefing-uficon.html. Reuse for any future campaign or pitch HTML file without redesign.

---

# Medical/Education Professional = Standing Segment

Beejeni's B2B/B2C expansion increasingly targets two non-student professional segments:
- บุคลากรทางการแพทย์ (~8K contacts) — iPad clinical workflow angle
- บุคลากรทางการศึกษา (~12K contacts) — Mac for teaching/research angle

These appear in BTS 2026 and the KKC strategy. Treat as a persistent segment in future CRM and KOL briefs.
