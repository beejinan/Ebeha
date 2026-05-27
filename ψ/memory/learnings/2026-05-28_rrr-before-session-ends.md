# Learning: รัน /rrr ก่อน Session จบ ไม่ใช่หลัง

**Date**: 2026-05-28
**Source**: rrr: Ebeha (fb7f7c26)

## Pattern

เมื่อ session ถูกปิด (crash, shutdown, iOS update, etc.) แล้วต้อง reopen session ใหม่เพื่อรัน /rrr — ทำให้:
- Context ถูก split เป็น 2 session
- Session ใหม่ต้องโหลด context ใหม่ทั้งหมด (cache miss)
- JSONL ของ retro session มีแค่ 1-2 ข้อความ ไม่มี substance

## Rule

> ถ้าจะหยุดทำงาน ให้รัน `/rrr` ก่อนเสมอ — ใน session เดิม ก่อนปิด

## ข้อยกเว้น

- Session crash โดยไม่ตั้งใจ → reopen + /rrr ก็โอเค แต่ต้องระบุใน retro ว่า "session split"
- งานยาวมากจน context เต็ม → `/rrr` ตรงนั้นเลย แล้วค่อย resume

## Related

[[00.47_preview-gallery-live-june-plan]] — session ที่ถูก split ออกมา
