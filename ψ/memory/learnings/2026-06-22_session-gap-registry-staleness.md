# Learning: Documented Rules Without Enforcement Are Noise

**Date**: 2026-06-22
**Source**: /rrr --deep: Ebeha
**Confidence**: High (multi-agent corroboration)

---

## Core Pattern

A rule written in a learning file does not change behavior unless the system enforces it. The fleet registry staleness demonstrates this concretely: the rule `fleet-registry-must-update-every-session` was written 2026-06-08 after a 49-day gap was discovered. Fourteen days later (2026-06-22), the registry is stale again. The same outcome, half the time.

This is not unique to the registry. 7 of 8 recurring frictions in this session's pattern analysis have existing learning files. The Thai Edit byte mismatch has been documented 3 times. The unverified-numbers-get-✅-badges cycle has been documented twice. Writing the learning is not the fix.

---

## Enforcement Hierarchy (strongest → weakest)

1. **System-enforced** — The skill does the action automatically (e.g., /rrr itself updates the registry)
2. **Checklist at decision point** — A mandatory check before committing or closing
3. **CLAUDE.md rule** — Visible at session open, reviewed each time
4. **Learning file** — Only consulted when explicitly searched; easy to miss

Current state for fleet registry: level 4 (weakest). Should be level 1.

---

## What to Do Differently

- When writing a learning that says "always do X", ask: is X embedded in a skill, checklist, or CLAUDE.md rule? If not, the learning may not change behavior.
- For high-recurrence frictions: promote the rule up the enforcement hierarchy, not just write it down again.
- Specific proposed change: add fleet registry update to the /rrr skill flow (Step 0 or Step 4) as an automatic bash command, not a remembered guideline.

---

## Related

- [[fleet-registry-must-update-every-session]] — the predecessor learning this one extends
- [[pitch-deck-content-patterns]] — same pattern: rule documented, then violated same session
