---
allowed-tools: Read, Edit, Bash(wc:*), Bash(cat:*), Glob, Grep
description: End-of-session handoff — updates AGENT_CONTEXT.md and outputs a compact summary.
---

## Context

- Current directory: !`pwd`
- Context file exists: !`test -f handoff/AGENT_CONTEXT.md && echo "YES" || echo "NO"`
- Line count: !`wc -l < handoff/AGENT_CONTEXT.md 2>/dev/null || echo "0"`

## Instructions

Run the end-of-session handoff. Two steps only: **update the context file**, then **print a short summary**. No external protocol files. No verbose debrief. No infra verification.

If `handoff/AGENT_CONTEXT.md` does not exist, tell the user and stop.

### Step 1 — Update `handoff/AGENT_CONTEXT.md`

Read the file in full, then make these edits in as few Edit calls as possible:

1. **Session Log:** Append one row:
   `| YYYY-MM-DD | summary ≤120 chars | DL-NNN refs or — | line count after edits |`

2. **What's Next:** Check off (`[x]`) completed items. Add new items if work was identified. Mark the top unchecked item `<- START HERE`.

3. **Recent Decisions:** If decisions were made this session, append with the next DL-NNN number. If the table exceeds 5 rows, move oldest to `handoff/DECISIONS.md` (create if needed).

4. **Current State / Tech Debt:** Update Working/In-Progress/Tech-Debt bullets if anything changed.

5. **Line budget:** After edits, run `wc -l handoff/AGENT_CONTEXT.md`. If over **200 lines**, move oldest Session Log rows to `handoff/ARCHIVE.md` (create if needed with `# Session Archive` header and same table columns). Trim enough to get under 180. Do NOT trim other sections.

### Step 2 — Print Handoff Summary

Output **only** this to the user:

```
## Handoff
**Health:** G/Y/R — one-line reason if not Green
**This session:** one-sentence summary
**Next:** the #1 action (the <- START HERE item)
**Lines:** N/200
```

Then, on a new line after the summary block, print the next action as a standalone copy-paste prompt inside a fenced code block so the UI renders a copy button:

```
Continue: <the START HERE item as a direct instruction>
```

This lets the user copy it straight into the next session.

### Rules

- Do NOT read or look for any external protocol file.
- Do NOT read CLAUDE.md or run infra verification. If infra checks matter, they should have run during the session — just record the result in Current State.
- Do NOT produce a "Session Debrief", "Project Snapshot", or "Housekeeping" section.
- Keep it fast. Aim for ≤3 tool calls total.
