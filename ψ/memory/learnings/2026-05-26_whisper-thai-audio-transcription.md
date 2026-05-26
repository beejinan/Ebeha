# Whisper Thai Audio Transcription — What Works

**Date**: 2026-05-26
**Source**: Session — Apple brief M4A transcription (109 min)
**Confidence**: High (confirmed by 2 model runs)

---

## Core Lesson

**สำหรับ Thai audio ยาวหรือ mixed-language — ใช้ `large-v3` เสมอ ไม่ใช่ `base` หรือ `turbo`**

| Model | Thai Quality | Time (109 min) | Verdict |
|---|---|---|---|
| base | ❌ hallucinate/repetitive | ~30 min (killed) | ใช้ไม่ได้ |
| turbo | ⚠️ usable แต่ noisy | ~77 min | ต้องการ human review |
| large-v3 | ✅ expected good | ~3-4 hrs | ใช้สำหรับงานสำคัญ |

---

## Standard Workflow (Thai Audio)

```bash
# 1. Convert to 16kHz mono WAV (mandatory)
ffmpeg -i input.m4a -ar 16000 -ac 1 output.wav

# 2. Sample check ก่อน full run (2 นาทีแรก)
python3 -c "
import whisper
model = whisper.load_model('large-v3')
result = model.transcribe('output.wav', language='th', fp16=False,
  start=0, duration=120)
print(result['text'])
"

# 3. Full run ถ้า sample quality OK
python3 -c "
import whisper
model = whisper.load_model('large-v3')
result = model.transcribe('output.wav', language='th', fp16=False, verbose=False)
with open('/tmp/transcript.txt', 'w') as f:
    f.write(result['text'])
"
```

---

## Why turbo Fails on Thai

- Thai audio ที่มี code-switching (Thai + English mixed) สร้าง confusion ให้ turbo
- turbo ถูก optimize สำหรับ English speech — Thai เป็น secondary
- hallucination pattern: repetitive words, garbled phrases, mixed-language nonsense
- large-v3 trained on multilingual data ที่ larger — handles Thai+English switching ดีกว่า

---

## Time Estimates (CPU, no GPU)

- 109 min audio + turbo = ~77 min processing time (0.7× real-time)
- 109 min audio + large-v3 = ~3-4 hrs (2-2.5× real-time)
- Pre-sampling 2 min = ~2-3 min → worthwhile investment before full run

---

## Applied In

- Apple brief `The ct apple บรีฟ.m4a` (109 min) — transcribed with turbo 2026-05-26
- `/tmp/brief_transcript_turbo.txt` — 124K, quality requires human review
