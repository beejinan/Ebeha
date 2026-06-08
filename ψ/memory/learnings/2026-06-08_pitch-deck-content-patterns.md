# Pitch Deck Content Patterns — UFicon Central Sprint

**Date**: 2026-06-08
**Source**: /rrr --deep: Ebeha (Session 49394434)
**Confidence**: High (cross-verified by 5 agents)

## Patterns

### 1. Read-with-offset before Edit on Thai HTML after context break
When a context window compaction has occurred, Thai multibyte UTF-8 characters in the Edit tool's `old_string` may fail to match even though they look identical. Always Read the file at the specific offset first to confirm the exact byte sequence before editing.

**How to apply**: Any session that continues from a summary AND touches Thai-heavy HTML → Read-with-offset before every Edit call.

### 2. Unverified numbers need visual markers, not ✅ badges
A slide that renders unverified figures as confirmed damages pitch credibility if questioned. Use "฿8M+ Target (TBC)" or a ⚠️ label until the source system (SALES_BD, etc.) confirms the number.

**How to apply**: Before marking any metric ✅, ask: "Can I open the source file and show this number right now?" If no → ⚠️ or omit.

### 3. List deliverables need files, not just chat output
KOL names, campaign structures, and any reference list delivered as chat text is effectively ephemeral. Always Write to `preview/{date}/uficon-{topic}.html` or `.md`.

**How to apply**: Any time the output is a list of names, recommendations, or structured reference data → create a file.

### 4. Two segmentation models in same deck = story contradiction
3-passion-group model (Family/Career/Creative %) and 4-segment profile model (G1A/G1B/G2A/G1C) coexist in UFicon pitch directory. Before Grand Opening, one must be designated as the "lead" model.

**How to apply**: Ask Beejeni which model leads. Update all slides to reference the same model.

### 5. DUA CSS design system is extract-ready
All 9 UFicon HTML pitch files use identical `:root` CSS variables. Extracting to `uficon-pitch.css` removes ~200 lines of duplication per file and makes global color changes instant.

**How to apply**: On next major pitch update, propose extracting shared CSS (low-risk refactor).
