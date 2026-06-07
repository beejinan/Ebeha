---
name: pitch-data-verification-and-claim-integrity
description: Pitch claims must have verified sources before rendering — 4 unsupported claims found and removed from UFicon pitch deck
metadata:
  type: feedback
---

Every claim in a pitch deck must have a verified source before it is rendered. "Verified ✅" badge = platform export file exists. "Projection 📍" = calculated from verified data. Untagged = remove.

**Why:** Session found 4 claims labeled ✅ with no supporting data:
- 120-day channel values (฿62.4/38.4/18.3...) — hardcoded, no source
- 4× member revenue multiplier — math actually shows 0.7× from real data
- ฿41M incremental CRM revenue — math fails when run against real numbers
- B&E ฿8M+ FY26 — SALES_BD sheet empty (NaN), Smart Quotation FTP not exported

All 4 removed or re-labeled. Apple will ask. "Where does that come from?" with no answer = credibility loss.

**How to apply:**
1. Before adding any number to pitch HTML, identify the source file
2. Open the file and verify the number exists exactly as stated
3. If source is a calculation, write the formula explicitly
4. If source doesn't exist → 📍 label or remove
5. Never use "Verified ✅" without a file path you can open

Related: [[pptx-export-system-patterns]], [[pitch-framework-and-docx-patterns]]
