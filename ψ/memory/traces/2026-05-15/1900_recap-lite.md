---
query: "/recap lite"
target: "Ebeha"
mode: smart
timestamp: 2026-05-15 19:00
friction_score: 0.7
coverage: [files, git]
confidence: high
---

# Trace: /recap lite

**Target**: Ebeha
**Mode**: smart | **Friction**: 0.7 | **Confidence**: high
**Time**: 2026-05-15 19:00

## Oracle Results
None (Oracle MCP not queried — escalated to files)

## Files Found
- `/Users/iqgraphicdesigniqgraphicdesign/.claude/skills/recap-lite/SKILL.md` — the skill definition
- `/Users/iqgraphicdesigniqgraphicdesign/.claude/skills/VERSION.md` — listed as installed skill
- `/Users/iqgraphicdesigniqgraphicdesign/.claude/skills/forward-lite/SKILL.md` — references recap-lite as next-session command

## Git History
Not searched (files found with high confidence, Wave 2 skipped)

## GitHub Issues/PRs
Not searched

## Cross-Repo Matches
Not searched

## Oracle Memory
Not indexed (no Oracle MCP available)

## Friction Analysis
**Score**: 0.7 — Visible (found in repo files with high confidence)
**Coverage**: files, skills directory
**Goal check**: Yes — found the skill definition. `/recap-lite` is an installed [core] skill at standard profile tier. Clear purpose and content confirmed.

## Summary
`/recap-lite` is a lite version of `/recap` — a quick session orientation skill.

**What it does**:
1. Runs `git status` + `git log -3`
2. Reads the most recent handoff from `ψ/inbox/handoff/*.md`
3. Shows: last session summary, pending items, git state
4. Ends with "What's next?"

**Profile**: Core skill (`[core]`), installed at standard profile via `arra-oracle-skills-cli v26.4.18-alpha.22`

**Upgrade path**: `/go standard` → full `/recap` with retro summaries + session mining

**Referenced in**: `forward-lite` skill — suggests running `/recap-lite` at next session start
