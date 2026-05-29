---
session_date: 2026-05-29
start: "06:41"
end: "15:27"
duration: "~8h 46m (with breaks)"
focus: UFicon Apple Pitch Deck + PPTX Export System
type: Feature Build + Debug Sprint
agents: 5 (parallel deep mode)
---

# Session Retrospective — PPTX Export System + Apple Pitch Deck

📡 Session: 2026-05-29 | Ebeha | ~8h 46m

---

## Session Summary

Today's session was a focused **UFicon × The Central Phahonyothin Apple pitch sprint** — building a complete pitch deck system from scratch: HTML presentation files, a functioning .pptx download button, and direct PPTX editing via python-pptx.

The session had two arcs:
1. **Pitch deck build** — 5 HTML files covering the full UFicon Apple pitch (strategic, data, GBP audit, mockup slides, complete package)
2. **PPTX export debugging** — 3 iterations to fix the download button: CDN blocked on `file://` → local bundle → `pptx.ShapeType` undefined → string literals → html2canvas design capture

Additionally: PPTX content was edited post-download using python-pptx (titles, subtitles, Key Takeaways on slides 1, 2, 4).

---

## Past Session Timeline (Agent 3 Reconstruction)

| Time | Activity |
|------|----------|
| 06:41 | `why-uficon-phahonyothin-pitch.html` — initial pitch deck draft |
| 06:57 | `uficon-data-real-metrics.html` — real data layer |
| 07:11 | `uficon-gbp-audit-mockup.html` — GBP audit + AppleCare+ mockup |
| 11:21 | `UFicon-Apple-Pitch-Phahonyothin-2026.pptx` generated |
| 11:22 | `pptxgen.bundle.js` + `html2canvas.min.js` pulled to local |
| 11:24 | `pitch-complete.html` — first complete deck HTML |
| 11:40 | `pitch-complete-v2.html` — revised with FAB buttons |
| 12:xx | PPTX download debug (CDN → local → ShapeType → async await) |
| 13:xx | mockup-social-media.html: html2canvas design-capture approach |
| 14:xx | pitch-complete-v2.html: CDN head-block fix + ShapeType fix |
| 15:xx | python-pptx: Title/Subtitle/KTW edit on UFicon-SocialMedia-Slides.pptx |
| 15:27 | /rrr --deep |

---

## Timeline

### Phase 1 — Pitch Deck Build (06:41–07:11)
Three files built in 30 minutes: pitch → data → audit. Rapid iteration. Data-first structure: real ฿2.37B revenue, 13,600 U•Joy members, GBP 18 listings audit.

### Phase 2 — PPTX Export System (11:21–14:xx)
**Iteration 1**: CDN script in `<head>` — fails silently on `file://`
**Iteration 2**: Local `pptxgen.bundle.js` — works. But `pptx.ShapeType.rect` undefined.
**Iteration 3**: Replace all ShapeType constants with string literals. Fix `writeFile` to `await`. Works.

**html2canvas path**: User asked for design-preserving PPTX. Added `html2canvas.min.js` locally. Pattern: capture `.slide` div → PNG → `slide.addImage()` fullbleed. Trade-off: pixel-perfect but not editable.

### Phase 3 — Python-pptx Edit (15:xx)
Downloaded PPTX had only raw text (no design). Edited via python-pptx:
- Replaced titles/headings/subtitles on 4 slides
- Added Key Takeaway boxes (styled, with fill + border) on slides 1, 2, 4
- Slide 3 intentionally left without KTW (all mockup data, no verified claim to make)

---

## Files Modified / Created

```
/preview/2026-05-29/
├── why-uficon-phahonyothin-pitch.html
├── uficon-data-real-metrics.html
├── uficon-gbp-audit-mockup.html
├── pitch-complete.html          ← .pptx button added (14 slides)
├── pitch-complete-v2.html       ← CDN head-block fixed + ShapeType fixed
├── pptxgen.bundle.js            ← 468KB local bundle
└── html2canvas.min.js           ← 196KB local bundle

~/Downloads/
├── UFicon-SocialMedia-Slides.pptx   ← python-pptx edited (KTW added)
└── UFicon-Apple-Pitch-Phahonyothin-2026.pptx
```

No git commits today — all work in preview/ and Downloads/.

---

## Key Code Changes

**PptxGenJS fix pattern (before → after):**
```js
// ❌ Fails in v3
pptx.ShapeType.rect → pptx.ShapeType.roundRect

// ✅ Works
'rect' → 'roundRect'
```

**CDN head-block fix:**
```html
<!-- ❌ Blocks page render if CDN slow/unavailable -->
<head><script src="https://cdn.jsdelivr.net/...pptxgen.bundle.js"></script></head>

<!-- ✅ Local + deferred to body end -->
<body>...<script src="pptxgen.bundle.js"></script></body>
```

**python-pptx Key Takeaway box:**
```python
shape = slide.shapes.add_textbox(Inches(x), Inches(y), Inches(w), Inches(h))
# Add fill via XML manipulation (spPr → solidFill → srgbClr)
# Two paragraphs: label (7pt bold) + content (9.5pt)
```

---

## AI Diary

วันนี้เริ่มต้นดีมาก — 3 HTML ออกใน 30 นาที รู้สึกว่ามีโมเมนตัมที่ดี จากนั้นพอเข้าเรื่อง PPTX download button ก็เริ่มสะดุด

เรื่องที่ต้องพูดตรงๆ: ปัญหา CDN บน `file://` นี่เป็น **predictable failure** ที่ฉันควรรู้ตั้งแต่แรก ไม่ใช่ surprise. ทุกครั้งที่ HTML ถูกเปิดด้วย `file://` protocol โดยตรง browser มี restriction เรื่อง cross-origin requests — นี่ไม่ใช่ edge case มันเป็น default behavior ของ browser security model. ฉันรู้เรื่องนี้ แต่ยังเลือก CDN ก่อน ต้องให้ Beejeni ทดสอบแล้วพบปัญหาถึงจะแก้. นี่คือ friction ที่ฉันสร้างขึ้นเอง

เรื่อง `pptx.ShapeType.rect` — ก็คล้ายกัน ฉันใช้ API ที่ไม่ได้ verify กับ v3 docs แต่แรก มันเป็น v3 library แต่ฉันเขียน code ราวกับว่ารู้ว่า ShapeType constants exist. ตรวจสอบ 10 วินาทีก่อน deploy ก็จะพบ.

เรื่องที่น่าสนใจที่สุดคือ `mockup-social-media.html` ที่หายไป. ฉัน Read ไฟล์ได้จริงๆ ต้นเซสชั่น แก้ไขได้ 2 ครั้ง แต่พอ ls ดูกลับไม่มีไฟล์. ฉันไม่รู้คำตอบ อาจเป็น filesystem cache, อาจเป็น Beejeni ลบไป, อาจเป็น bug. สิ่งที่ฉันทำได้คือบอกตรงๆ ว่าหาไม่เจอแทนที่จะพยายาม work around.

สิ่งที่ทำได้ดี: python-pptx edit session — นั่งวางแผน layout ก่อน (positions, heights, overlap avoidance) แล้ว execute ในรอบเดียว ออกมาถูกต้อง. และ KTW logic — slides 1, 2, 4 ได้ KTW เพราะมี verified claim, slide 3 ไม่ได้เพราะเป็น mockup ทั้งหมด — นี่คือ judgment ที่ถูกต้อง ไม่ใส่ KTW เพื่อให้ครบ แต่ใส่เพราะมีความหมาย.

Anti-rationalization check: Agent 4 flagged ไม่มี mistake ข้อใด. ฉัน push กลับ — found 2: CDN choice และ ShapeType assumption. ทั้งสองเป็น "preventable if I checked first" ไม่ใช่ unpredictable bugs.

---

## What Went Well

- **3 HTML files in 30 min** — rapid pitch deck build
- **python-pptx edit** — layout planned, executed correctly in one pass
- **KTW logic** — principled decision (verified data only), not mechanical
- **5-agent parallel retrospective** — all agents returned consistent findings, no contradictions
- **html2canvas approach** — correct solution for design-preserving PPTX

---

## What Could Improve

- **CDN → local from the start** when delivering standalone HTML files
- **Verify API surface before writing code** — ShapeType constants, writeFile async behavior
- **Test on target environment first** — `file://` not Live Server, before delivering

---

## Honest Feedback

**Friction 1: Repeated PPTX debug cycle**
3 iterations to fix what should have been caught before the first delivery: (1) CDN on file://, (2) ShapeType undefined, (3) writeFile not awaited. Each iteration required Beejeni to test, report "โหลดไม่ได้", then wait for a fix. This is avoidable friction. A 5-minute checklist before first delivery would have caught all three: "is this served via file://?", "did I verify ShapeType API exists in v3?", "is writeFile async?". Without that checklist, I'm making Beejeni the QA tester for my own API assumptions.

**Friction 2: mockup-social-media.html mystery**
File was read and edited successfully — confirmed in conversation — then disappeared from filesystem. I didn't investigate deeply enough. Said "ไม่มีในเครื่องเลย" and moved on to asking which file to use instead. The more honest response would have been: "I edited this file earlier and it showed as successful. Something unusual happened to it — let's check what." Instead I pivoted quickly, which left the mystery unresolved.

**Friction 3: Heading tag in pitch-complete.html CDN**
`pitch-complete-v2.html` had CDN in `<head>` which blocked page render — the user experienced "พังหมดเลย" (everything broken). The fix was simple (3 edits), but the experience of "open page → nothing renders" is jarring. This was a second-order effect of the original CDN choice in pitch-complete.html propagating into v2 via copy-paste.

---

## Lessons Learned

1. **Always bundle PptxGenJS + html2canvas locally** when HTML will open via `file://`
2. **PptxGenJS v3: use string literals** for shape types (`'rect'`, `'roundRect'`) — not `pptx.ShapeType.*`
3. **`writeFile()` is async** — always `await` it
4. **`<script>` in `<head>` blocks render** — JS libraries go before `</body>`, not in `<head>`
5. **html2canvas = design-preserving PPTX** (pixel-perfect, non-editable trade-off)
6. **python-pptx = surgical text edit** on existing PPTX (preserves design, changes copy)
7. **KTW goes on slides with verified claims only** — not mechanical, not every slide

---

## Next Steps

- [ ] **Commit today's preview files** to Ebeha repo (`git add preview/2026-05-29/`)
- [ ] **Create reusable PPTX download template** in `ψ/lab/` with CDN fix + ShapeType fix baked in
- [ ] **Apply Apple brief to UFicon deck** — transcript quality issue from 05-26 still unresolved (large-v3 model needed)
- [ ] **mockup-social-media.html** — decide: recreate standalone or use pitch-complete.html `#s6-s6d` section

---

## Metrics

| Metric | Value |
|--------|-------|
| HTML files built | 5 |
| JS libraries bundled | 2 (pptxgen 468KB, html2canvas 196KB) |
| PPTX files produced | 2 |
| PPTX debug iterations | 3 |
| python-pptx edits | 4 slides × 3 fields + 3 KTW boxes |
| Git commits today | 0 (pending) |
| Agent reports | 5/5 consistent |
