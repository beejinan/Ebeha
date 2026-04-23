---
name: Preview Output Rule
description: ทุกไฟล์ที่สร้างจากการอ่านหรือทำงานต้องอยู่ที่ ~/preview/{date}/{filename} เสมอ
type: feedback
---

ทุกครั้งที่ช่วยทำไฟล์ หรือ Beejeni สั่งให้อ่านไฟล์/สร้างอะไรสักอย่าง — output ต้องเก็บไว้ที่ `~/preview/{date}/{files}` เสมอ

**Why:** Beejeni ต้องการให้ output ทุกชิ้นอยู่ในที่เดียว จัดระเบียบตามวันที่ ง่ายต่อการหาย้อนหลัง ไม่กระจายไปที่ Downloads หรือที่อื่น

**How to apply:**
- เมื่ออ่านไฟล์ PDF/doc → สร้าง HTML/MD summary ที่ `~/preview/YYYY-MM-DD/`
- เมื่อสร้างไฟล์ใดๆ (Keynote, HTML, รายงาน) → เก็บที่ `~/preview/YYYY-MM-DD/`
- date = วันที่ทำงาน (today's date)
- ทำโดยอัตโนมัติ ไม่ต้องรอให้ Beejeni บอก
