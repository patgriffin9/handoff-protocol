# Handoff Protocol

End-of-session state capture for Claude Code projects. One slash command updates a single per-project context file so the next session (or a different developer) can pick up without re-explaining the project.

## What's in here

- **`handoff.md`** — the `/handoff` slash command definition. Reads and edits your project's `handoff/AGENT_CONTEXT.md`, then prints a compact summary.
- **`AGENT_CONTEXT.template.md`** — starter template for the living context file. Drop a copy into each project you want the protocol to cover.

## Install

```bash
# 1. Clone this repo
git clone <this-repo-url> handoff-protocol
cd handoff-protocol

# 2. Install the slash command globally (available in every project)
cp handoff.md ~/.claude/commands/handoff.md

# 3. For each project you want to use it in:
mkdir -p <your-project>/handoff
cp AGENT_CONTEXT.template.md <your-project>/handoff/AGENT_CONTEXT.md
# Then open AGENT_CONTEXT.md and fill in the {{placeholders}} — at minimum the TL;DR.
```

## Use

At the end of a Claude Code session, run:

```
/handoff
```

The command:

1. Appends one row to the **Session Log** table (date, ≤120-char summary, any DL-NNN decision refs, current line count).
2. Ticks off completed items in **What's Next** and re-marks the top unchecked item as `<- START HERE`.
3. Appends any new decisions to the **Recent Decisions** table with the next DL-NNN number (spills oldest rows to `handoff/DECISIONS.md` once the table exceeds 5 rows).
4. Updates **Current State / Tech Debt** if anything changed.
5. Enforces a 200-line budget — when exceeded, oldest Session Log rows move to `handoff/ARCHIVE.md` until the file is back under 180 lines.

It then prints a short block you can read at a glance:

```
## Handoff
**Health:** G/Y/R — one-line reason if not Green
**This session:** one-sentence summary
**Next:** the #1 action (the <- START HERE item)
**Lines:** N/200
```

…followed by a copy-paste-ready `Continue: <next action>` prompt so you can drop it straight into the next session.

## Files the command maintains

| File | Purpose | Created by |
|------|---------|------------|
| `handoff/AGENT_CONTEXT.md` | Main living context (≤200 lines) | You, from the template |
| `handoff/DECISIONS.md` | Decision log overflow (DL-NNN history) | `/handoff` when Recent Decisions exceeds 5 rows |
| `handoff/ARCHIVE.md` | Session log overflow | `/handoff` when AGENT_CONTEXT.md crosses 200 lines |

## Updates

Pull protocol changes with:

```bash
cd handoff-protocol
git pull
cp handoff.md ~/.claude/commands/handoff.md
```

Existing `AGENT_CONTEXT.md` files in your projects are yours — they don't get overwritten by pulling updates to the template.
