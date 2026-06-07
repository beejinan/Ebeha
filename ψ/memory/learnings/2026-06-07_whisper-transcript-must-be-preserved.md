---
name: whisper-transcript-must-be-preserved
description: Audio transcripts from Whisper are primary source documents — save immediately to ψ/memory/traces/ not /tmp/
metadata:
  type: feedback
---

After Whisper transcription completes, copy output immediately to a permanent location. Never leave transcripts only in `/tmp/`.

**Why:** Session transcribed 193 minutes of Thai meeting audio (3 files). All outputs in `/tmp/whisper_6/`, `/tmp/whisper_7/`, `/tmp/whisper_screen/` — gone on next reboot. These contain primary source material: Apple pitch requirements, budget breakdown, Grand Opening timing decisions, AI tool development plans. If Beejeni asks to reference the meeting again, must re-transcribe from scratch.

**How to apply:**
- After `model.transcribe()` completes → immediately copy to `ψ/memory/traces/YYYY-MM-DD/`
- Naming: `HHMMM_[event-slug].txt`
- For meeting audio: also write a 1-paragraph summary alongside the raw transcript
- For Thai audio: still use `large-v3`, not `medium` or `turbo` (confirmed again this session — medium hallucinates on silence)

Related: [[whisper-thai-audio-transcription]]
