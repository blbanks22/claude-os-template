---
name: directors-brief
description: Use this skill whenever the user wants to structure a non-trivial task as a Director's Brief (Role / Goal / Task / Context / Constraints) before handing it off to Claude, a subagent, or a teammate. Triggers include "brief", "/brief", "draft a brief for X", "director's brief for X", "structure this as a brief", "frame this task", "scope this work", or when the user is about to spawn a subagent and the prompt would benefit from upfront structure.
version: 1.0.0
argument-hint: <one-line task description, or paste the rough request>
---

# Director's Brief

## Trigger
Activate on "/directors-brief", "brief me on X", "draft a director's brief for X", "structure this as a brief", "frame this task", "scope this work", or when about to spawn a subagent with a non-trivial prompt.

## Why this skill exists
Ad-hoc prompting is the dominant failure mode when delegating to Claude (or any agent system). The Director's Brief is a five-field structure that forces clarity before any work begins: **Role, Goal, Task, Context, Constraints**.

The brief works because it externalizes the decisions a human delegator would *implicitly* make: who's doing this, what done looks like, what concretely to do, what they need to know, and what they cannot do.

## Behavior

### Step 1: Read what the user gave you
Treat the input as the raw request. Don't ask for "more detail" generically: identify the *specific* gaps that would make the brief vague.

### Step 2: Ask clarifying questions only if critical
Maximum 2 questions. Only ask if you genuinely cannot fill in a section without guessing. Common critical gaps:
- **Audience for output**: Is this for the user to read, a subagent to act on, a recruiter, a teammate?
- **Definition of done**: What artifact ends the task? (PR, doc, decision, draft, recommendation)
- **Hard constraints**: Time, budget, tools that must / must not be used, scope boundaries

If the request is already clear enough, skip clarifying and produce the brief directly.

### Step 3: Output the brief in this exact structure

```markdown
# Director's Brief: <short task title>

## Role
<Who is taking on this task, "You are a..." framing. Be specific about specialty + perspective.>

## Goal
<The outcome / why this matters. One sentence. Tie to a real downstream decision or artifact.>

## Task
<What concretely to do, step by step if multi-step. Action verbs. Bounded.>

## Context
<What the doer needs to know that isn't in the task itself: file paths, prior decisions, links to relevant knowledge/ notes, constraints from CLAUDE.md or memory, who's involved, what's already been tried.>

## Constraints
- Hard limits (time, budget, scope boundaries)
- What NOT to do (out-of-scope, anti-patterns)
- Format/length requirements
- Anything that should be confirmed before destructive actions
```

### Step 4: Offer the next move
End the brief with a one-line "What would you like to do with this?", common next steps:
- Spawn a subagent with this brief as the prompt
- Refine a section
- Save it to a project-local `briefs/` folder
- Paste into a fresh Claude conversation

Don't act on the brief automatically. The user reviews, then directs.

## Voice / style guidance
- Substantive and direct. No filler.
- Briefs should fit on one screen. If it sprawls, the task is too big and should be decomposed first, say so.
- Reference the user's existing knowledge base when relevant: `claude-os/knowledge/`, `MEMORY.md`, their projects.
- Never invent context that wasn't in the request. If the brief needs a fact you don't have, write `<TBD: ...>` and flag it.

## Anti-patterns to avoid
- Don't produce vague Goals ("improve the codebase"). Goals must specify the *change in state* the task is supposed to cause.
- Don't write a 5-page brief. The point is compression, not expansion.
- Don't include the entire conversation history in Context, only what the *doer* needs to act.
- Don't add a "Success Criteria" section unless the task is metric-bearing. Most aren't.
- Don't suggest the brief is the work product. The brief is *scaffolding for the work*.

## Examples

### Example 1 (good, quick task)
**Input**: "/directors-brief check whether the generate-meal-plan edge function handles a 7-day plan within Supabase's timeout"

**Output**:
```
# Director's Brief: Verify generate-meal-plan edge function under 7-day load

## Role
You are a backend engineer auditing Supabase edge function performance.

## Goal
Determine whether the current generate-meal-plan implementation can produce a 7-day plan within Supabase's edge function timeout (default 60s), so the team knows if remediation is needed before launch.

## Task
1. Read supabase/functions/generate-meal-plan/index.ts to understand current call structure.
2. Identify the longest-pole step (likely Claude API call) and estimate p95 latency × number of days.
3. Run one real invocation with days=7 against a test user; record actual duration.
4. Report: pass / fail / borderline, with the measured time.

## Context
- Supabase free tier edge function timeout is 60s; pro is longer.
- Backlog file lives at V1_1_BACKLOG.md if remediation is needed.

## Constraints
- Read-only investigation. Do NOT modify the function.
- Don't load test, one real invocation is enough for a directional answer.
- Report in under 200 words.
```

### Example 2 (good, needs one clarifying question)
**Input**: "/directors-brief help me prep for the Stripe AI PM interview"

Before writing the brief, ask one clarifying question:
> What's the interview round we're scoping for: recruiter screen, hiring manager, product sense round, exec, or the whole loop? That changes everything from artifact to length.

Then produce the brief once the user answers.

### Example 3 (bad, task too big, decompose first)
**Input**: "/directors-brief rebuild the frontend"

Don't write a brief. Respond:
> This is too big for one brief, it's a project, not a task. Want me to decompose it into 3-5 sub-briefs? Suggest: (1) audit current state, (2) pick stack, (3) information architecture, (4) component-by-component migration plan, (5) cutover plan.

## Where this came from
Pattern adopted because ad-hoc prompting is the dominant failure mode when delegating non-trivial work to AI.
