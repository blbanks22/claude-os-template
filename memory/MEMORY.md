# Memory Index

This is the index of all memory files in this directory. Claude loads this file at session start, then loads individual memory files on demand when relevant.

## Conventions

- Each memory lives in its own file: `<type>_<short-kebab-slug>.md`.
- Files use YAML frontmatter with `name`, `description`, and `metadata.type`.
- The four types are: `user`, `feedback`, `project`, `reference`. (Details below.)
- Each line in this index is: `- [Title](filename.md) — one-line hook (under 150 chars total)`.
- Keep this index under 200 lines; lines past that may be truncated when loaded.

## Active memories

- [User example (delete after reading)](user_example.md) — illustrates the user-type memory format.
- [Feedback example (delete after reading)](feedback_example.md) — illustrates the feedback-type memory format.
- [Project example (delete after reading)](project_example.md) — illustrates the project-type memory format.
- [Reference example (delete after reading)](reference_example.md) — illustrates the reference-type memory format.

## The four memory types

### `user`
Information about the user's role, goals, responsibilities, and knowledge. Used to tailor work to who the user is. Save when you learn anything new about the user's role, preferences, or background. Example: "User is a data scientist, 5 years in Python, currently transitioning into ML engineering."

### `feedback`
Guidance the user has given about how to approach work, both what to avoid and what to keep doing. Record from corrections AND from explicit approvals of unusual approaches. Always include a `Why:` line so future-you can judge edge cases. Example: "User prefers integration tests over mocks. Why: prior incident where mocked tests passed but a real migration failed."

### `project`
Information about ongoing work, goals, initiatives, bugs, or incidents that is not derivable from the code or git history. Project memories decay quickly; keep them up to date. Convert relative dates to absolute dates when saving. Example: "Migration freeze begins 2026-06-15 for the mobile release cut."

### `reference`
Pointers to where authoritative information lives in external systems (Linear, Slack, Jira, Grafana, etc.). Used when the user references an external system or you need to find current state of something. Example: "Pipeline bugs are tracked in Linear project INGEST."

## Writing a new memory

1. Decide which of the four types fits best.
2. Create a new file `<type>_<short-kebab-slug>.md` in this directory.
3. Use this frontmatter:

   ```markdown
   ---
   name: <short-kebab-slug>
   description: <one-line summary used to decide relevance in future sessions>
   metadata:
     type: <user | feedback | project | reference>
   ---

   <memory body. For feedback and project memories, include **Why:** and **How to apply:** lines.>
   ```

4. Add a one-line entry to this index pointing at the new file.

## When not to save memory

- Anything derivable from reading the current project state (architecture, conventions, file paths).
- Git history, recent changes, or who-changed-what.
- Debugging recipes (the fix is in the code; context belongs in the commit message).
- Ephemeral task or session state.
- Anything already documented in CLAUDE.md.

## Cross-linking

Use `[[other-memory-slug]]` in the body to link to related memories. The target doesn't have to exist yet; a dangling link marks something worth writing later.
