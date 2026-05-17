# claude-os-template

A scaffold for your **personal Claude operating system**: a single directory of skills, memory conventions, and a knowledge base that you keep version-controlled in Git and load into every Claude Code session.

This template gives you the structure. You bring the content.

## What this is

If you've used Claude Code for more than a few weeks, you've probably noticed a pattern: the same prompts, the same setup explanations, the same context-rebuilding at the start of every session. A personal Claude OS solves that by externalizing all of it into version-controlled files that Claude reads automatically.

Three load-bearing pieces:

1. **Skills** are reusable prompt-as-code: PRD writing, market research, weekly reviews, interview prep, and so on. Each skill lives in `skills/<name>/SKILL.md` and is invoked by slash command (`/<name>`) or natural-language trigger.
2. **Memory** is a structured store of who you are, how you work, your current projects, and pointers to external systems. Memory files persist across sessions and inform Claude's behavior.
3. **Knowledge** is your personal long-form knowledge base: career notes, company research, reading synthesis, postmortems. Skills read from here; some skills also write here.

CLAUDE.md and GOALS.md sit at the root and load in every session.

## How to use this template

1. Click **Use this template** on GitHub to create your own repo (or clone this one and re-init git).
2. Clone your new repo to `~/Documents/projects/<your-claude-os>/` (or wherever you prefer).
3. Personalize `CLAUDE.md` and `GOALS.md` (search for `[PLACEHOLDER:` markers).
4. Symlink the relevant pieces into `~/.claude/` so Claude Code picks them up globally:

   ```
   ln -s ~/Documents/projects/<your-claude-os>/skills    ~/.claude/skills
   ln -s ~/Documents/projects/<your-claude-os>/agents    ~/.claude/agents
   ln -s ~/Documents/projects/<your-claude-os>/commands  ~/.claude/commands
   ln -s ~/Documents/projects/<your-claude-os>/CLAUDE.md ~/.claude/CLAUDE.md
   ```

   Now any edit you make here is instantly live in every Claude Code session, everywhere.
5. Delete the four `*_example.md` files in `memory/` once you've understood the format, and start writing real memories as you encounter information worth keeping.
6. Populate `knowledge/` over time as you accumulate notes that span sessions.

## Directory layout

```
CLAUDE.md           Global "about me" + how-I-work + rules. Loaded by Claude in every session.
GOALS.md            Personal quarterly goals. Reviewed weekly by you, optionally by a weekly-review skill.
.gitignore          Excludes secrets, OS junk, and editor state.

agents/             Custom subagents. Generic ones included; add more as workflows emerge.
commands/           Project-scoped slash commands. Often empty until needed.
templates/          Project starter templates (e.g., a new-project scaffold).

memory/             Structured persistent memories. Four types: user, feedback, project, reference.
  MEMORY.md         Index of all memory files with one-line descriptions.
  user_example.md   Example user-type memory (delete after you understand the format).
  feedback_example.md
  project_example.md
  reference_example.md

knowledge/          Long-form personal knowledge base.
  career/           Job-search notes, comp benchmarks, target-role research.
  company/          Company profiles for prospects, employers, or research targets.
  people/           Notes on people in your network or who you'll interview with.
  notes/            Free-form notes that don't fit elsewhere; includes postmortems/ subdir.
  reading/          Synthesized notes from articles, talks, papers. The synthesize-articles skill writes here.

skills/             Reusable prompts-as-code. Each in its own subdirectory with a SKILL.md.
```

## The 18 skills included

Each is invoked via `/<name>` or a natural-language trigger (see each `SKILL.md` for triggers).

| Skill | One-line purpose |
|---|---|
| `prd` | Draft a PRD at one of six stages (kickoff, planning, XFN, solution, launch, impact). |
| `prd-review` | Run a structured PRD quality audit against a 30-item checklist. |
| `market-research` | Strategic market landscape analysis: competitors, sizing, trends, pricing. |
| `competitive-teardown` | Focused 1-page strategic teardown of a single competitor. |
| `user-research` | Synthesize raw interview notes into ranked findings with confidence levels. |
| `metric-honest` | Audit any quantitative claim before it lands in a finished artifact. |
| `weekly-review` | PM-style weekly retro on your own work, scanned from git activity and goals. |
| `project-eval` | Score and review a product idea against a weighted 17-check rubric. |
| `interview-prep` | Produce a focused interview prep packet for a specific company and role. |
| `pitch-deck-narrative` | Articulate a portfolio project as a 6-beat narrative arc. |
| `product-postmortem` | Capture an honest, structured postmortem on a shipped or pivoted project. |
| `substack-writer` | End-to-end research, style learning, and drafting of a long-form article. |
| `resume-builder` | Build or tailor a resume for AI/ML roles using an impact-formula framework. |
| `job-strategy` | Build a personalized advanced strategy to land an AI role. |
| `directors-brief` | Structure a non-trivial task as Role/Goal/Task/Context/Constraints before delegating. |
| `synthesize-articles` | Process a batch of article URLs into a three-bucket knowledge base format. |
| `session-handoff` | Generate a paste-able handoff doc so a new session resumes with zero ramp. |
| `video-insights` | Extract a transcript from a video URL (YouTube etc.) and produce a structured insight summary. |

## The four memory types

| Type | Purpose | Example |
|---|---|---|
| `user` | Who the user is, their role, knowledge, preferences. | "User is a backend engineer, 8 years in Python, currently learning Rust." |
| `feedback` | Guidance about how the user wants you to work. | "User prefers terse responses; do not summarize at end." |
| `project` | What's happening now: who, what, why, when. | "Project Atlas kicks off 2026-06-15; goal is to migrate the payments queue." |
| `reference` | Pointers to external systems where authoritative info lives. | "Bug tracking lives in Linear project ATL; on-call dashboard at grafana.internal/atl." |

The full conventions are documented in `memory/MEMORY.md`.

## A note on `references/` subfolders

A handful of skills reference auxiliary files inside their own folder (e.g., `skills/market-research/references/query-handling.md`, `skills/resume-builder/references/keywords-and-bullets.md`). Those files are not included in this template. The skills work without them, but you can add your own as you build out the skill over time, or strip the reference lines from the SKILL.md.

## License

MIT. See [LICENSE](LICENSE).

## Attribution

Adapted from the personal claude-os of Bryan Banks. The original is private; this template is the sanitized scaffolding.
