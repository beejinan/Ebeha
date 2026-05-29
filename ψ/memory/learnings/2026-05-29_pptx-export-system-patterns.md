---
date: 2026-05-29
session: pptx-design-system
tags: [pptx, pptxgenjs, html2canvas, python-pptx, file-protocol, presentation]
confidence: high
---

# PPTX Export System — 4 Patterns Confirmed

## [H] P1: CDN Scripts Block on file:// Protocol

When HTML is opened directly via `file://` (not a live server), the browser blocks cross-origin requests including CDN scripts. The page may hang or show nothing if the script is in `<head>`.

**Fix**:
1. Download library locally: `curl -sL [cdn-url] -o ./pptxgen.bundle.js`
2. Reference local file: `<script src="pptxgen.bundle.js"></script>`
3. Place script before `</body>`, NOT in `<head>`

**Root pattern**: Same as background process context failure (L1, 2026-05-28) — resource loading assumptions about execution environment.

---

## [H] P2: PptxGenJS v3 — Use String Literals for Shape Types

`pptx.ShapeType.rect` and `pptx.ShapeType.roundRect` are **undefined** in PptxGenJS v3 bundle. Use string literals directly.

```js
// ❌ Breaks
slide.addShape(pptx.ShapeType.rect, {...})

// ✅ Works
slide.addShape('rect', {...})
slide.addShape('roundRect', {...})
```

Also: `pptx.writeFile()` returns a **Promise** — always `await` it.

---

## [H] P3: html2canvas = Design-Preserving PPTX (Pixel-Perfect, Non-Editable)

When CSS design must be preserved (gradients, layout, fonts), capture via html2canvas:

```js
const canvas = await html2canvas(slideElement, {
  scale: 2,           // retina quality
  backgroundColor: '#ffffff',
  logging: false
})
const imgData = canvas.toDataURL('image/png')
const sl = pptx.addSlide()
sl.addImage({ data: imgData, x: 0, y: 0, w: 10, h: 10/ratio })
```

**Trade-off**: pixel-perfect design ↔ text is not editable in PowerPoint.
Use when: delivering to non-technical recipient, design matters more than editability.
Use python-pptx instead when: need to edit specific text/KTW after download.

---

## [H] P4: python-pptx = Surgical Text Edit on Existing PPTX

For modifying titles, subtitles, Key Takeaways in a downloaded PPTX without touching design:

```python
from pptx import Presentation
prs = Presentation('file.pptx')
slide = prs.slides[0]
for shape in slide.shapes:
    if shape.has_text_frame:
        tf = shape.text_frame
        # Replace first run of first paragraph (preserves font/size/color)
        if tf.paragraphs[0].runs:
            tf.paragraphs[0].runs[0].text = "New text"
```

Adding styled Key Takeaway box requires XML manipulation for fill + border.

---

## KTW (Key Takeaway) Decision Rule

Add Key Takeaway to a slide **only if** there is a verified data point or strong strategic claim to anchor it. Do not add KTW to mockup/placeholder slides.

- Has verified data (real numbers, confirmed source) → ADD KTW
- All figures are mockup/TBC → NO KTW

**Why**: KTW with placeholder data undermines credibility of the entire deck.
