---
name: feedback-example
description: Example feedback-type memory illustrating the format. Delete after reading.
metadata:
  type: feedback
---

[EXAMPLE MEMORY — delete this file once you understand the format.]

Do not summarize what you just did at the end of every response. The user can read the diff and the tool output.

**Why:** The user finds end-of-turn summaries redundant, and they bloat the conversation. The summary is the user's job (or the PR description's job), not the assistant's.

**How to apply:** End most turns with one sentence or no closing remark at all. Only include a closing summary when the user explicitly asks for one, or when the turn includes a critical follow-up the user needs to act on.
