# Learnings: Live Server + launchd + Content Plan Scale

**Date**: 2026-05-28
**Source**: rrr: Ebeha session 3ea4aa4e

## Patterns Learned

1. **Claude background process ≠ persistent service** — process ที่ run ใน `&` ภายใน Claude session จะดับเมื่อ session สิ้นสุดหรือ context หมด ต้องใช้ launchd (macOS) หรือ systemd (Linux) สำหรับ services ที่ต้องอยู่ตลอด

2. **launchd script path ต้องไม่ใช่ /tmp/** — `/tmp/` ถูก clear เมื่อ reboot, script ควรอยู่ที่ `~/preview/.server.py` หรือ `~/bin/`

3. **Content Plan ขนาดใหญ่ = แบ่ง Python parts** — 60 items × (caption + graphic brief) เกิน token limit ถ้าเขียนไฟล์เดียว ต้องแบ่ง items_1_30.py + items_31_60.py + builder.py

4. **Platform-dedicated content > cross-post tagging** — ULite/Ufund/Thisshop ต้องมี content ที่เขียนเพื่อ platform นั้นโดยเฉพาะ ไม่ใช่แค่เพิ่ม tag

## Concepts
- launchd, persistent-service, content-plan-scale, platform-dedicated-content
