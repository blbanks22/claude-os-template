---
name: project-example
description: Example project-type memory illustrating the format. Delete after reading.
metadata:
  type: project
---

[EXAMPLE MEMORY — delete this file once you understand the format.]

The team is in a merge freeze from 2026-06-15 through 2026-06-22 for the iOS release branch cut.

**Why:** The mobile team is producing a release branch for the Q3 launch and any backend changes that ship during the freeze risk being missed in mobile QA.

**How to apply:** Flag any backend PR scheduled during the freeze window. Suggest deferring non-critical merges to 2026-06-23 or later. Critical-path fixes are allowed but require explicit sign-off from the release manager (see [[reference-release-process]] if it exists).
