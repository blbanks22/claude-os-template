---
name: reference-example
description: Example reference-type memory illustrating the format. Delete after reading.
metadata:
  type: reference
---

[EXAMPLE MEMORY — delete this file once you understand the format.]

The team tracks backend bugs in Linear project `BACK`. Triage happens every Monday at 10am Pacific. PRs that close a bug should reference the Linear ticket ID in the title (format: `BACK-1234`).

The on-call dashboard for backend services lives at `grafana.internal/d/backend-overview`. Check it when investigating any latency or error-rate regression in backend code.

Architecture decision records are kept in the `docs/adrs/` directory of the main monorepo. New ADRs are numbered sequentially and require review by two senior engineers before merge.
