---
name: weekly-review
description: Use this skill whenever the user wants a structured weekly review of their work, what shipped, what stalled, what's blocked, what to focus on next week. Triggers include "weekly review", "what did I get done this week", "weekly retro", "review my week", "what's blocked", "what should I focus on next week", or running on a Friday/Sunday near end of week. Scans recent git activity across the user's repos, GOALS.md, and conversation context to produce a PM-style retro on the user's own work.
version: 1.0.0
argument-hint: [optional: "this week" / "last week" / specific date range]
---

# Weekly Review

## Trigger
Activate on "weekly review", "review my week", "weekly retro", "what did I ship", "what's blocked", or "what should I focus on next week." Particularly useful on Friday/Sunday.

## Context

If the user runs multiple personal projects in parallel, plus active job search or other initiatives, they can lose signal on what's actually progressing vs what's stalling without structured weekly review. This skill produces a PM-style retro applied to the user's own work.

Output is a 1-page review that answers four questions:
1. **What shipped?** (concrete output, with links)
2. **What stalled?** (intent vs reality)
3. **What's blocked?** (and on what specifically)
4. **What's next?** (1-3 focused priorities, not a wishlist)

## Behavior

### Step 1: Pull the data

Scan in parallel:
- `git log --since="1 week ago" --all` across each repo in the user's personal-projects directory (commonly `~/Documents/projects/`). Use `gh api` to also check PRs opened/merged/closed in the last 7 days.
- `claude-os/GOALS.md`, what was the stated plan for the quarter? Where are we against it?
- `claude-os/knowledge/notes/` and `knowledge/career/job-search/`, any new entries this week?
- Conversation context from this session and recent sessions (if available via memory).

If a project has zero commits this week, don't gloss over it, that's signal.

### Step 2: Produce the review

```
# Weekly Review: [Week of YYYY-MM-DD]

## Headline
[1 sentence, the most important thing that happened or didn't happen this week.]

## What shipped
For each project with movement:
- **[Project]**: [What was actually done, commit count is fine, but call out specific features/decisions. Link to PRs.]

If something is functionally complete but not deployed/used, say so: "Code is shipped but not in production yet."

## What stalled
What did the user *plan* to work on (per GOALS.md or recent stated intent) that didn't get done? Be specific:
- **[Project/initiative]**: [What was planned, what actually happened, suspected reason, context switching, ambiguity, motivation, blocker]

Don't moralize. Just describe.

## What's blocked
For each blocker:
- **[Item]**: blocked on [specific thing]. Unblocking action: [what would move it].

If something is "blocked on the user thinking through X," call it out, that's solvable.

## Job search signal (if applicable)
- Applications submitted: [count]
- Interviews completed: [list with company]
- Outreach sent: [count, brief categorization]
- Pipeline state: [who's at what stage]
- [Anything notable that needs follow-up next week]

Only include this section if the user has a job-search context active (e.g., a `knowledge/career/job-search/applications.md` file exists).

## Theme of the week
[1-2 sentences. Pattern across the week, was it heads-down build mode? Lots of context switching? Recovering from a stall? Naming the theme makes the next week more deliberate.]

## Next week: 1 to 3 priorities (not a wishlist)
Pick at most 3. Force ranking matters more than completeness.

1. **[Priority]**, why this, why now, what done looks like.
2. **[Priority]**, why this, why now, what done looks like.
3. **[Priority]**, why this, why now, what done looks like.

## What to drop or defer
What's on the implicit todo list that should explicitly NOT happen next week? Calling these out frees attention.

## Open question for the user
1-2 things the user should think through before next week. Format as direct questions, not advice.
```

### Step 3: Save the review

Write to `claude-os/knowledge/notes/weekly-reviews/YYYY-MM-DD.md` so reviews accrue. Over time, this becomes a high-signal history of the user's work patterns, which projects sustain momentum, which keep stalling, what kinds of blockers recur.

## Rules

- **Honest > flattering.** A review that says "great week, lots of progress!" when the data shows 4 commits across 5 projects is useless. Name the stall.
- **Force ranking on next week.** No "and also..." dump. Three priorities max.
- **Specific links and metrics.** "Made progress on Project X" is filler. "Merged PRs #12, #14, #15, adds Greenhouse source + tests" is signal.
- **Pull from `GOALS.md` to assess intent vs reality.** This is where the retro gets sharp.
- **Don't fabricate counts.** If git log shows 0 commits, say 0. If you can't access a repo, say so.
- **Job search section only if the user has opted into tracking it.** Check for `knowledge/career/job-search/applications.md` or similar, if not present, omit the section.
- **Each review should be ~1 page.** If longer, cut.

## Anti-patterns

- **Listing every commit.** Cluster by feature/intent. Not a `git log` dump.
- **"Reasons" that are excuses.** "Was busy with other things" isn't a reason, *which* other things, and were those the right priorities?
- **Wishlist disguised as priorities.** If next week's section has 7 items, force-rank to 3.
- **Skipping "what stalled."** This is the most valuable section. Don't omit it because it's uncomfortable.
- **Generic theme.** "A productive week" isn't a theme. "Shipped project A backlog while deferring all project B work, second consecutive week of deprioritizing B" is a theme.
