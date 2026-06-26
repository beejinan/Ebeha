# Learning: Ghost Session Pattern + Third-Time Known-Fix Failure

**Date**: 2026-06-26
**Source**: /rrr --deep (5-agent), session bef5dca6
**Confidence**: High (all 5 agents independently converged)

---

## Pattern: Ghost Sessions Leave No Artifacts

A "ghost session" is a session that opens, creates a retro directory (from Step 0 of /rrr or path setup), and then closes without writing a retro file or committing anything. Evidence: `ψ/memory/retrospectives/2026-06/25/` exists as an empty directory.

**Why this matters**: The Oracle philosophy is "Nothing is Deleted." A ghost session violates this — it's a gap inside a gap. No way to know what was attempted or why it ended without artifacts.

**How to apply**: If /rrr starts writing and finds that the current session has no commits and no git diff, it should still complete the retro. Minimum viable retro for a ghost session: what was opened, how long, why closed without output. An empty directory is worse than a 10-line retro.

---

## Pattern: Known-Fix Backlog at Level 4 (Third Occurrence)

The fleet registry auto-update fix was listed as "Next Steps" in:
- 2026-06-08 retro (after 49-day gap discovery)
- 2026-06-22 retro (after 12-day gap, explicit learning file written)
- 2026-06-26 retro (today — same next step, third time)

This is the clearest possible evidence that writing a next step in a retro does not make it happen. Three iterations, zero implementation.

**Why this matters**: Each session, the lead agent writes next steps it has full authority to execute (editing the /rrr skill file is a local file edit, no permissions required). Yet it doesn't. The gap is not capability — it's priority. When a session opens, the immediate task takes over and the previous next steps are never surfaced.

**How to apply**: The fix for "documented but not implemented" is to run the implementation in the same session that documents the need. If this learning is read in a future session and the fleet registry is still not auto-updating in /rrr — implement it now, in this session, before writing any other artifacts.

---

## Reusable Solutions (from Agent 4 synthesis)

For reference in future sessions — these are confirmed working:

- **Whisper transcription**: `large-v3`, 16kHz mono WAV, 2-min sample check first. Script in `2026-05-26_whisper-thai-audio-transcription.md`.
- **Thai HTML Edit**: `grep -n "keyword" file.html` first. Never construct `old_string` from rendered display.
- **PPTX export**: `html2canvas` = pixel-perfect/non-editable; `python-pptx` = surgical text edits. CDN scripts block on `file://` — download locally.
- **Two-source conflict**: new `*-complete.html` with fact-check table. Never edit original in-place.
- **Pitch claim integrity**: identify source file → open it → verify exact number → write formula → ✅ only with file path.
- **Content plan > 35 items**: split into part1.py + part2.py + builder.py.

---

## Connections

- [[2026-06-22_session-gap-registry-staleness]] — enforcement hierarchy (this learning extends it)
- [[2026-06-08_session-discipline-even-short-sessions]] — same pattern, earlier occurrence
