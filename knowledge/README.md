# knowledge/

Your personal long-form knowledge base. Skills read from here. Some skills also write here.

Use this directory for notes that should persist across sessions but do not fit the structured memory format. Think of memory as "facts about the world Claude needs to apply"; knowledge is "longer-form notes that Claude (or you) can read as reference."

## Layout

- `career/` — job-search notes, target-role research, compensation benchmarks.
- `company/` — research notes on specific companies (employers, prospects, interviewees' employers).
- `people/` — notes on people in your network or who you will meet.
- `notes/` — free-form notes that do not fit elsewhere, including `notes/postmortems/` written by the `product-postmortem` skill.
- `reading/` — synthesized notes from articles, talks, podcasts, papers. Written by the `synthesize-articles` skill.

## Conventions

- Use markdown for everything.
- Use YAML frontmatter for any file that benefits from machine-readable metadata (date, tags, source URL).
- Use kebab-case filenames.
- Build an `INDEX.md` per subdirectory when the file count makes browsing painful (typically past ~15 files).
- Skills that write here will create their own subdirectories (e.g., `reading/substack/`, `notes/postmortems/`, `notes/weekly-reviews/`).

## Privacy reminder

This directory is in version control. If you push to a public repo, audit the contents first. Do not commit:

- Private contact information for people in `people/`.
- Compensation data, recruiter names, or interview content tied to specific companies you are still in process with.
- Anything covered by an NDA from your employer.
