---
name: product-postmortem
description: Use this skill whenever the user wants to capture a postmortem on a project, feature, restart, deprecation, failed launch, or pivot. Triggers include "do a postmortem", "postmortem on X", "what went wrong with [project]", "retro on [thing]", "I'm pivoting [project], capture why", "we restarted [project] from scratch", "deprecating X, what did we learn", or any reflection on a finished or pivoted initiative. Saves to claude-os/knowledge/notes/postmortems/.
version: 1.0.0
argument-hint: <project/feature name> [+ context: what happened, what changed]
---

# Product Postmortem

## Trigger
Activate on "postmortem on X", "what went wrong with [project]", "retro on [thing]", "we restarted/pivoted/deprecated [X]", or any reflection on a finished or pivoted initiative.

## Context

Projects generate postmortem-worthy moments regularly: features that shipped but missed expectations, architecture decisions that paid off or didn't, experiments that worked or didn't, restarts where V0 got rebuilt as V1.

A postmortem is not a blame document or a feel-good summary. It's an honest, structured capture so that the user (and their future Claude sessions, via memory) can learn from it. The goal: same mistake doesn't happen twice; same insight doesn't get lost.

## Behavior

### Step 1: Establish what's being post-mortem'd

Confirm the scope. A postmortem covers one of:
- **A project that shipped but missed expectations** (built it, used it, learned it wasn't right)
- **A project that was restarted/rebuilt**
- **A project that was deprecated** (stopped working on it)
- **A specific feature or technical decision** within a project
- **An experiment** (outreach approach, marketing test, etc.)

Don't run a postmortem on something still in flight. If it's still active, route to `weekly-review` instead.

### Step 2: Pull facts before opinions

Before asking the user to reflect, gather the factual record:
- `git log` for the project in question, what was actually built?
- `claude-os/memory/project_[name].md` if it exists, what's the captured history?
- Conversation history if available, what was the user trying to do?

Use these to *anchor* the postmortem in reality, not memory. Memory edits the past; commits don't.

### Step 3: Run the postmortem template

```
# Postmortem: [Project / Feature / Decision Name]

**Date:** [YYYY-MM-DD]
**Status:** [Shipped & deprecated / Restarted / Abandoned / Pivoted]
**Duration:** [Start → end dates]
**Outcome:** [1 sentence, what actually happened]

## What we were trying to do
[The original goal. What problem? For whom? What did "good" look like? Pull from notes/memory if possible. Be specific.]

## What we built
[Concrete artifacts. Architecture, key features, tech stack. Not what was planned, what actually existed.]

## What happened
[Timeline of meaningful events. Decisions made, points where direction changed, when problems surfaced. Stick to facts.]

## What worked
- [Specific thing that turned out well, be honest, not generous]
- [Pattern / approach / decision that paid off]
- [Skill / capability that was built that's reusable]

## What didn't work
- [Specific thing that didn't pan out, what was the underlying mismatch?]
- [Pattern / decision that backfired]
- [Assumption that turned out to be wrong]

## The single most important lesson
[ONE thing. The thing that, if you'd known it at the start, would have changed the trajectory. Force ranking matters here, most postmortems have one real lesson and a bunch of secondary observations.]

## What I'd do differently if starting over
[Specific. Not "be more careful", actual structural changes. Different tech choice, different scope, different timeline, different validation step, etc.]

## What I'd keep doing
[Just as important. What worked that should carry to the next project? Patterns to repeat, not just mistakes to avoid.]

## Was this avoidable?
[Honest answer. Sometimes the lesson is "this had to fail for me to learn X", that's a real category. Sometimes it's "I should have caught this in week 2." Distinguish.]

## Where this project's artifacts live
[Repo, branch, key files. So the user can find the actual code even after pivoting.]

## Open question
[1 thing this postmortem doesn't yet answer that's worth coming back to.]
```

### Step 4: Save to canonical location

Write to `claude-os/knowledge/notes/postmortems/[YYYY-MM-DD]-[project-slug].md`.

If a project memory file exists at `claude-os/memory/project_[name].md`, add a one-line link back to the postmortem so future sessions discover it.

### Step 5: Surface the lesson to memory if it generalizes

If the "most important lesson" is project-specific (e.g., "this Supabase quirk bit me"), leave it in the postmortem.

If the lesson generalizes across projects (e.g., "low-code/no-code architectures hit a wall when state management gets complex, start in code if state is non-trivial"), offer to save it as a feedback memory in `claude-os/memory/feedback_[name].md` so future Claude sessions apply it.

## Rules

- **Facts before reflection.** Anchor in git log and notes. Memory rewrites the past, don't let it.
- **One real lesson, not seven.** Force ranking. The skill of a postmortem is identifying *the* lesson.
- **Distinguish "what didn't work" from "what was bad."** Things can be honest failures even if every decision along the way was reasonable given what was known at the time.
- **No moralizing.** "Should have known better" is useless. "The assumption that [X] was true broke when [Y] happened" is useful.
- **Capture even short / cheap pivots.** Small projects often pivot quickly, those are still postmortem-worthy because the pivot itself contains the insight.
- **For restarts specifically**, document the bridge: what carried forward from V0 to V1? What got thrown away? Sometimes the V0 was the necessary prototype, sometimes it was wasted effort. Be honest.

## Anti-patterns

- **"It was a learning experience."** Filler. Cut.
- **"We didn't have enough resources."** Almost always partially true and never the actionable answer. Push: what should have been deprioritized to make resources?
- **Bullet lists of every micro-decision.** Cluster into the 3-5 real shifts.
- **No artifact links.** A postmortem that can't be traced back to the actual code/PRs is gossip.
- **"Next time I'll be more careful."** Specify the structural change, not the resolution to try harder.
