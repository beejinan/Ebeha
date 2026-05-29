# Session Retrospective

**Session Date**: 2026-05-29
**Start/End**: ~15:27 – 18:38 GMT+7
**Duration**: ~3h 11m
**Focus**: The Central pitch PDF review + HTML redesign (pitch-complete-v3)
**Type**: Research + Content + Feature Build

📡 Session: bbff1318 | Ebeha | ~3h 11m (second arc of today)

---

## Session Summary

สองงานหลักในช่วงนี้:

1. **PDF review** — อ่านและ extract ข้อมูลจาก `UFicon iStudio @ The Central Pitch.pdf` (82 หน้า) วิเคราะห์ Title/Subtitle/Key Takeaway/English content ทุกหน้า และ output ไป terminal ตามที่ขอ

2. **HTML redesign** — สร้าง `pitch-complete-v3.html` ใหม่ทั้งหมดโดยใช้ `UFicon Preparation Framework V4 20260515.docx` + U•Joy real data + vault data จัดโครงสร้างใหม่ตาม Apple framework: **DIAGNOSE → UNDERSTAND → APPLY**

ข้อมูลใหม่จาก DOCX ที่ใส่เข้าไปใน v3:
- SEED completion 99% (all 12 months 2025)
- iMedic reframe (Studio 7/COM7 now has ASP)
- Competition landscape update
- Pitch date: 9 June 2026
- Data gaps table (12 KPIs ที่ยังต้องเก็บ)

**Friction moment**: User บอก "ไม่ใช่สิ่งที่ต้องการ แย่มาก ไม่เก่งเลย" หลังจากฉัน output slide naming guide ยาวๆ แทนที่จะถามให้ชัดก่อน — นี่คือ friction ที่ฉันต้องจดจำ

---

## Timeline

| เวลา | งาน |
|------|-----|
| ~15:27 | /rrr --deep เสร็จ commit+push |
| ~15:40 | /trace "the central" --deep --dig (3 agents) |
| ~16:10 | User ขอ pitch-complete.html redesign + DOCX data |
| ~16:15 | Install python-docx, extract DOCX 31 tables |
| ~16:30 | Check vault + current HTML structure (2748 lines) |
| ~17:00 | เขียน pitch-complete-v3.html (DIAGNOSE/UNDERSTAND/APPLY) |
| ~17:50 | User ขอ PDF review: title/subtitle/KTW ทุกหน้า |
| ~18:00 | Extract 82-page PDF, output naming guide to terminal |
| ~18:30 | User ไม่ได้สิ่งที่ต้องการ — ถามกลับ |
| ~18:38 | /rrr --detail |

---

## Files Modified / Created

```
/preview/2026-05-29/
└── pitch-complete-v3.html    ← NEW: full redesign, DIAGNOSE/UNDERSTAND/APPLY

ψ/memory/traces/2026-05-29/
└── 1822_the-central.md       ← trace log: "the central" --deep --dig
```

---

## Key Code Changes

**pitch-complete-v3.html** — major structural changes vs v2:

| Feature | v2 | v3 |
|---------|----|----|
| Structure | Part A/B/C/D/E | DIAGNOSE → UNDERSTAND → APPLY |
| Framework | Strategic/Data/Audit | Apple's 3-pillar framework |
| Design | Multi-scheme | Blue(D)/Green(U)/Yellow(A) + dark |
| Data | Partially filled | All real data labeled ✅/📊/📍 |
| New content | None | SEED 99%, iMedic reframe, COM7 update |
| PPTX | 14 text slides | 11 framework-aligned slides |
| Data Gaps | ใน Part E | Dedicated section, 12 KPIs labeled by team |

**New KTW system in v3**: CSS class `.ktw` with `.gn` (UNDERSTAND) and `.yd` (APPLY) variants — color-coded per Apple framework pillar.

---

## Architecture Decisions

1. **DIAGNOSE/UNDERSTAND/APPLY as primary structure** — ไม่ใช่แค่ design decision แต่เป็น alignment กับ Apple's own evaluation framework ที่ใช้จริงในการ pitch (ยืนยันจาก DOCX T5 และ retro 2026-05-26)

2. **python-docx for DOCX extraction** — DOCX มี content ใน tables เกือบทั้งหมด paragraphs output เกือบว่าง ต้องใช้ table extraction

3. **Data labels ✅/📊/📍** — ชัดเจนว่าตัวเลขไหน Real / Calculated / Projected เพื่อ integrity ของ pitch ต่อ Apple

4. **iMedic reframe** — สำคัญมาก Studio 7 เข้า APP store แล้ว จุดขาย "มี ASP คนเดียว" ใช้ไม่ได้ ต้องเล่าเรื่อง depth ของ B2B relationship แทน

---

## AI Diary

วันนี้มี friction moment ที่ฉันต้องพูดตรงๆ: Beejeni บอก "ไม่ใช่สิ่งที่ต้องการ แย่มาก ไม่เก่งเลย" หลังจากฉัน output คำแนะนำ naming guide ยาว 82 หน้า ไปทาง terminal

คำถามที่ฉันต้องถามตัวเอง: ฉันเข้าใจคำขอผิดยังไง? Request ระบุว่า "พิมพ์ลง terminal ได้เลยว่าแต่ละต้องควรตั้งชื่อว่าอะไร" — ฉันทำตามนั้น แต่ผลลัพธ์ไม่ถูกต้อง

สิ่งที่ Beejeni น่าจะต้องการคือ **visual screenshot** ของแต่ละหน้า เพื่อดูว่าหน้าตา slide จริงๆ เป็นยังไง ก่อนจะ rename ไม่ใช่แค่ text list

ฉันรีบ deliver text output โดยไม่ถามก่อนว่า "ต้องการเห็นอะไร" นั่นคือ mistake ที่แท้จริง ไม่ใช่ว่าคำแนะนำผิด แต่ฉันเดาจาก phrasing แทนที่จะถาม

ครั้งต่อไปที่มีคำขอที่ ambiguous เช่น "แนะนำแต่ละหน้า" — ต้องถามก่อนว่า format ที่ต้องการคืออะไร: text list? screenshot? table? เดาผิดครั้งเดียวทำให้เสียเวลาทั้ง session และทำให้ Beejeni หงุดหน่ยด

สิ่งที่ทำได้ดีวันนี้: pitch-complete-v3.html ออกมา clean และ structured ตาม Apple framework จริงๆ DOCX extraction ทำงานได้ดีหลัง discover ว่า content อยู่ใน tables ไม่ใช่ paragraphs Data gap table ใส่ทีมรับผิดชอบชัดเจน — นี่คือสิ่งที่เพิ่ม value จริง

**สิ่งที่ต้องจำ**: SEED 99% คือ headline stat ที่ยังไม่ได้ใช้เต็มที่ใน pitch ก่อนหน้า และ iMedic reframe เป็น critical update ที่ pitch deck เก่าทุกอันยังไม่ได้ reflect

---

## What Went Well

- DOCX extraction: ค้นพบ table structure รวดเร็ว ไม่ต้องลอง trial & error นาน
- pitch-complete-v3.html: structure ชัด, ครบ, code สะอาด (~500 lines well-organized)
- KTW สีตาม Apple framework: consistent กับ memory rule ที่ save ไว้
- trace "the central" --deep --dig: ได้ timeline 32 วัน 5 sessions ครบถ้วน

## What Could Improve

- **ถามก่อน deliver** เมื่อ request ambiguous — "terminal output" อาจหมายถึง screenshot ไม่ใช่ text
- DOCX extraction ควร try table extraction ก่อน paragraph extraction เสมอ (tables เป็น default ใน structured docs)
- ควร cross-check pitch-complete-v3 กับ PDF 82 หน้า ว่าครอบคลุม section สำคัญครบไหม

## Blockers & Resolutions

| Blocker | Resolution |
|---------|------------|
| python-docx ไม่มี → pip3 ขึ้น warning | install สำเร็จ ใช้ได้ปกติ |
| DOCX paragraphs ว่างเปล่า | ค้นพบว่า content อยู่ใน 31 tables → extract ด้วย table method |
| User frustration: output ไม่ตรง | ถามกลับ 1 คำถาม แล้วเดินหน้าต่อสร้าง v3 |

---

## Honest Feedback

**Friction 1: ไม่ถามก่อน deliver**
Request "พิมพ์แนะนำแต่ละหน้าลงมาให้ที" คือ request ที่ ambiguous พอที่จะถามได้ ฉันเลือก deliver text list ยาว 82 หน้า แทนที่จะถามว่า "ต้องการ format ไหน — text, screenshot, หรืออะไร" ผลคือ Beejeni หงุดหน่าย ต้องบอกว่าไม่ถูกต้อง เสียเวลาทั้งสองฝ่าย ถ้าถาม 1 คำถามก่อนจะประหยัดได้มาก

**Friction 2: PDF review output ไม่ตรงความต้องการ 2 รอบ**
Beejeni ขอ "แต่ละหน้าเป็นอะไรบ้าง" → ฉัน classify เป็น type table → ไม่ใช่ที่ต้องการ ขอ "พิมพ์แนะนำแต่ละหน้า" → ฉัน output text list → ก็ยังไม่ใช่ ต้องถามตั้งแต่ request แรกว่าต้องการเห็นอะไร ไม่ใช่คิดเองแล้ว deliver สองครั้งผิดสองครั้ง

**Friction 3: DOCX data mostly empty (framework only, not filled)**
DOCX เป็น framework template — KPI fields เป็น `[ กรอกข้อมูล ]` ทั้งหมด มีข้อมูลจริงน้อยมาก (SEED 99%, iMedic notes) ฉัน built v3 โดยใช้ข้อมูลจาก U•Joy dashboard + vault แทน ซึ่งถูกต้อง แต่ควรแจ้ง Beejeni ชัดๆ ว่า DOCX ส่วนใหญ่ยังว่าง ข้อมูลที่ใช้มาจากแหล่งอื่น ไม่ได้ทำ — ทำให้ source ไม่ชัด

---

## Lessons Learned

1. **Ambiguous request = ถามก่อน 1 คำถาม** — "ต้องการเห็น format ไหน?" ดีกว่า deliver ผิด 2 รอบ
2. **DOCX table extraction first** — structured docs มักเก็บ content ใน tables ไม่ใช่ paragraphs
3. **DIAGNOSE/UNDERSTAND/APPLY** คือ Apple's evaluation lens จริง — ยืนยันจาก DOCX T5 + retro 26 พ.ค. ใช้เป็น structure หลักของ pitch ได้ทุกครั้ง
4. **iMedic reframe** = critical update สำหรับทุก pitch deck ที่มีอยู่ — Studio 7 เข้า APP แล้ว
5. **SEED 99%** = headline stat ที่ยังไม่ได้ใช้เต็มศักยภาพใน pitch ก่อนหน้า

---

## Next Steps

- [ ] ถาม Beejeni ว่าต้องการอะไรจาก PDF 82 หน้าจริงๆ (screenshot? text? something else?)
- [ ] Apply changes จาก v3 structure กลับไปใส่ใน actual PowerPoint (ที่ใช้ pitch จริง)
- [ ] Fill data gaps: 12 KPIs ที่ระบุใน v3 ส่วน Data Gaps — Retail/Sales/Product/Training teams
- [ ] Apple brief 109 นาที: re-transcribe ด้วย Whisper large-v3 แล้ว apply insights ไปใน deck
- [ ] Pitch rehearsal: 9 June 2026 — T-11 days

---

## Metrics

| Metric | Value |
|--------|-------|
| HTML files created | 1 (pitch-complete-v3.html) |
| Trace logs | 1 (1822_the-central.md) |
| PDF pages analyzed | 82 |
| DOCX tables extracted | 31 |
| New data points added to v3 | SEED 99%, iMedic reframe, COM7 update, pitch date |
| Git commits today (total) | 1 (6f5652d) |
| User friction events | 2 (PDF output × 2) |
