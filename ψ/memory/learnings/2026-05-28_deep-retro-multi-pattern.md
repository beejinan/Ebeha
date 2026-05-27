# Learning (Deep Mode): Session 2026-05-28 — Multi-Pattern Extract

**Date**: 2026-05-28
**Source**: rrr --deep: Ebeha (3ea4aa4e + fb7f7c26)
**Confidence levels**: H=High, M=Medium

---

## Patterns

### [H] L1: Claude Background Process ≠ Persistent Service
ทุก process ที่รันด้วย `&` หรือ background shell ใน Claude จะตายเมื่อ context compress, session timeout, หรือ user ปิด Claude  
**Fix**: ใช้ launchd (macOS) / systemd (Linux) สำหรับ service ที่ต้องอยู่ข้าม session

### [H] L2: launchd Script ห้ามอยู่ใน /tmp/
`/tmp/` ถูก clear เมื่อ reboot ทำให้ launchd register ได้แต่ fail หลัง restart  
**Fix**: permanent path = `~/preview/.server.py`, `~/bin/`, หรือ `~/.local/bin/`

### [H] L3: launchctl load ต้องรัน Manual โดย User ไม่ใช่ Claude Background Task
`launchctl load` ใน Claude background shell → exit 143 (timeout/kill) → ไม่มีผล  
**Fix**: ให้ Beejeni รัน `launchctl load ~/Library/LaunchAgents/com.uficon.plist` เอง แล้ว verify ด้วย `launchctl list | grep uficon`

### [H] L4: Content Plan >35 items ต้องแบ่ง Python script
60 items × (caption + graphic brief) เกิน token limit ใน single generation  
**Pattern**: `items_part1.py` + `items_part2.py` + `builder.py` (import ทั้งสอง)  
→ สามารถ template สำหรับ content plan ขนาดใหญ่ทุกครั้ง

### [M] L5: Platform-Dedicated Content Series > Cross-Post Tag
ULite/Ufund/Thisshop ต้องมี content series เฉพาะ — ไม่ใช่แค่ tag ชื่อ platform  
ตัวอย่าง: ULite Weekly Exclusive, Ufund FAQ, Thisshop Monday Deal

### [H] L6: /rrr ต้องรันก่อน Session ปิด ไม่ใช่หลัง Reopen
session split ทำให้ JSONL ว่างเปล่า retro ขาด substance  
**Rule**: รัน /rrr ก่อนปิด — ถ้า session crash แล้ว reopen ให้ระบุ "session split" ใน retro

### [M] L7: Fleet Coordination — Content Oracle งาน → Route ไป Bejinan
Content Plan / Campaign งาน เป็น Bejinan's domain  
ถ้า Ebeha execute งาน content → log handoff ใน fleet registry เสมอ

---

## Connections

[[2026-05-28_live-server-launchd-content-plan]] — เวอร์ชันสั้น (รายการเดิม)
[[2026-05-28_rrr-before-session-ends]] — L6 ขยายจากไฟล์นี้
[[2026-04-23_preview-output-rule]] — output ไปยัง ~/preview/{date}/ (applied correctly today)
