---
name: two-source-conflict-new-file-not-edit
description: เมื่อมีสองแหล่งข้อมูลขัดแย้งกัน ให้สร้างไฟล์ใหม่พร้อม fact-check แทนการแก้ของเก่า
metadata:
  type: feedback
---

เมื่อมี 2 sources ที่ขัดแย้งกัน (เช่น PDF กับ HTML ที่สร้างจาก screen recording) ให้สร้างไฟล์ใหม่ที่ merge ทั้งสองเข้าด้วยกัน พร้อม fact-check table ระบุว่าอะไรถูก/ผิด/เพิ่มเติม

**Why:** การแก้ไข in-place ทำให้ไม่รู้ว่าอะไรเปลี่ยนไปจากอะไร และอาจทำลาย context ที่มีคุณค่า โดยเฉพาะ document ที่ผ่านมาหลาย session

**How to apply:** สร้างไฟล์ชื่อ `*-complete.html` / `*-complete.docx` แทนการแก้ไขไฟล์เดิม และระบุใน footer ว่าอ้างอิงจากแหล่งใดบ้าง

ตัวอย่าง session นี้: wwdc2026-summary.html (iOS 20/macOS 16 — ผิด) + PDF (iOS 27/macOS 27 — ถูก) → สร้าง wwdc2026-complete.html ใหม่

[[no-unverified-benchmarks]]
