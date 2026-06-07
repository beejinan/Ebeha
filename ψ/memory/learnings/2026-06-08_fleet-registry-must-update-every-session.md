---
name: fleet-registry-must-update-every-session
description: Fleet registry ต้องอัปเดตทุก session — Ebeha ทิ้งไว้ 49 วัน คือ failure to perform core responsibility
metadata:
  type: feedback
---

Fleet registry (`ψ/memory/fleet/registry.md`) ต้องถูก touch ทุก session หรืออย่างน้อย verify ว่ายัง current

**Why:** CLAUDE.md ระบุ "เก็บ fleet registry ให้ up-to-date เสมอ" แต่ตั้งแต่ Bejinan เกิด (2026-04-20) จนถึง 2026-06-08 — 49 วัน, 10 sessions — ไม่มีครั้งไหนที่ registry ถูก update นี่คือ accountability gap ใน core responsibility ของ Ebeha

**How to apply:** ก่อนทำ /rrr ทุกครั้ง check fleet registry — ถ้า last_session ไม่ใช่วันนี้ ให้ update minimal: last_session date + brief activity summary ก็พอ

Links: [[session-discipline-short-sessions]], [[feedback-proactive-session-open]]
