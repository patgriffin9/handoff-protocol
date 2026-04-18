# {{Project Name}} — Agent Context

> **TL;DR:** {{One-sentence description of this project — what it is, who it's for, what it runs on.}}

---

## Load Instructions

Quick resume: read this file's TL;DR + What's Next. Full context: read Current State and Recent Decisions.

---

## Current State

### Working
- {{Thing that currently works — include date verified if relevant}}

### Broken / Needs Attention
- {{Thing that's currently broken, with enough detail to reproduce or fix}}

### Open Tech Debt
- {{Known shortcut, workaround, or deferred cleanup — link to a DL-NNN if a decision was recorded}}
<!-- UPDATE: Add new tech debt items here -->

---

## Codebase Overview

```
{{project-root}}/
├── {{dir}}/    # {{what it is}}
├── {{dir}}/    # {{what it is}}
└── handoff/    # this context file + spillovers (DECISIONS.md, ARCHIVE.md)
```

---

## Architecture

{{2–5 bullets on the shape of the system: runtime, key services, auth model, external dependencies. Enough that a new contributor doesn't have to reverse-engineer it.}}

---

## Recent Decisions

*Full history in `DECISIONS.md` (created automatically when this table exceeds 5 rows). Load before making any architectural choice.*

| # | Decision | Choice | Why |
|---|----------|--------|-----|
| DL-001 | {{What was being decided}} | {{What was chosen}} | {{One-line reason}} |
<!-- UPDATE: Keep last 5 decisions here; older ones get moved to DECISIONS.md by the /handoff command. Increment the DL-NNN number. -->

---

## Session Log

| Date | Summary (≤120 chars) | DL refs | Line count |
|------|----------------------|---------|------------|
<!-- UPDATE: /handoff appends one row per session. Rows move to ARCHIVE.md when this file crosses 200 lines. -->

---

## What's Next

- [ ] <- START HERE: {{The single most important next action, written as a direct instruction the next session can act on}}
- [ ] {{Next action}}
- [ ] {{Next action}}
<!-- UPDATE: /handoff checks off completed items and re-marks the top unchecked one as <- START HERE. Remove checked items after 2 sessions. -->

---

*Hard limit: ≤ 200 lines. Look for `<!-- UPDATE: ... -->` markers to find the edit points.*
