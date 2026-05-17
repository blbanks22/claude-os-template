# knowledge/reading/

Synthesized notes from articles, talks, podcasts, papers, and other long-form content.

The `synthesize-articles` skill writes here. It produces per-article notes in a three-bucket format: `[ACT]` (actions to adopt now), `[AWARE]` (signals to track), `[KB]` (domain knowledge). It also produces cross-batch rollups and a per-source `INDEX.md`.

## Suggested subdirectories

Created on demand by the synthesize-articles skill:

- `substack/` — Substack newsletter articles.
- `medium/` — Medium articles.
- `blogs/` — personal blogs and company engineering blogs.
- `papers/` — academic papers.
- `talks/` — conference talks (synthesized from transcripts).

You can also add subdirectories manually for any reading source where you accumulate notes.

## Conventions

Per-article notes use this format:

```markdown
---
url: <full url>
author: <author or publication>
publication: <publication name>
date_published: <YYYY-MM-DD or "unknown">
read_date: <YYYY-MM-DD>
topics: [tag, tag, tag]
---

# <Article Title>

## TL;DR
<one sentence>

## [ACT] Actions / behaviors to adopt now
- ...

## [AWARE] Watch for / future behavior shifts
- ...

## [KB] Domain knowledge
- ...

## Quotes worth keeping
> "..."
```

Cross-batch rollups follow the pattern `_rollup-<YYYY-MM-DD>.md`.
