---
name: session-handoff
description: Generate a structured session handoff, captures current plan, progress, decisions, and next steps so a new Claude session can pick up exactly where this one left off. Use before compaction or when ending a work session.
disable-model-invocation: true
allowed-tools: Bash(git *) Read Glob TodoWrite
---

# Session Handoff

Generate a complete, copy-pasteable handoff document for the current session. The goal is that the user can open a new Claude Code session, paste this, and resume with zero ramp-up.

## Steps

1. **Gather dynamic context** using the shell injections below: do NOT skip or summarize these away.
2. **Review the conversation** from the beginning of this session to extract: what was asked, what was done, what decisions were made, and what is still pending.
3. **Write the handoff document** in the format below.
4. Output the final document in a fenced markdown block so the user can copy it cleanly.

---

## Dynamic Context (auto-injected)

**Git status:**
!`git -C "$(pwd)" status --short 2>/dev/null || echo "(not a git repo or no changes)"`

**Recent commits (last 5):**
!`git -C "$(pwd)" log --oneline -5 2>/dev/null || echo "(no commits)"`

**Current branch:**
!`git -C "$(pwd)" branch --show-current 2>/dev/null || echo "(unknown)"`

**Working directory:**
!`pwd`

---

## Handoff Document Format

Produce the handoff document using this exact structure:

```
# Session Handoff, [date]

## Project / Context
[1-2 sentences: which project, what area of the codebase or problem space]

## Goal This Session
[What the user was trying to accomplish, the original ask]

## What Was Completed
- [Bullet list of concrete things done: files changed, decisions made, outputs produced]

## Current State
[Where things stand RIGHT NOW, what's working, what's broken, what's in-flight]

## Decisions Made
- [Any non-obvious choices made this session, with the reasoning; these are the things most likely to confuse a fresh session]

## What's Next
- [ ] [Immediate next action]
- [ ] [Following action]
- [ ] [Anything blocked or waiting]

## Files Touched / Key Paths
- [file or directory paths relevant to resuming work]

## Paste This to Resume
> [One paragraph the user can paste as the opening message of a new session to re-establish full context, written in first person as if the user is speaking]
```

## Notes

- Be specific. Vague bullets like "worked on auth" are useless: name the file, the function, the decision.
- The "Paste This to Resume" section is the most important: make it self-contained and actionable.
- If there's an active plan or todo list in this session, include its current state verbatim under "What's Next."
- Do not editorialize. Report what happened and what's pending; the user will decide what to do next.
