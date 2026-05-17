---
name: pitch-deck-narrative
description: Use this skill whenever the user wants to articulate a portfolio project as a narrative, for interviews, pitch decks, take-home presentations, or LinkedIn write-ups. Triggers include "pitch [project]", "write the narrative for [X]", "how do I present [project] in an interview", "portfolio writeup for [X]", "explain [project] to a hiring manager", "elevator pitch for [project]", or "if I had to present this in 5 slides". Produces a structured story arc, not a feature list.
version: 1.0.0
argument-hint: <project name> [+ audience: interviewer / VC / hiring panel / blog readers]
---

# Pitch Deck Narrative

## Trigger
Activate on "pitch [project]", "narrative for [X]", "present [project]", "portfolio writeup", "elevator pitch", or "explain [project] to [audience]."

## Context

If the user builds personal projects partly as portfolio proof of applied product thinking, the bar for a portfolio piece in a senior interview isn't "did you ship something", it's "can you tell a story about why you built this, what you learned, and what the hard tradeoff was?"

This skill produces a 6-section narrative arc. Same arc whether the output is a 5-slide deck, a 90-second elevator pitch, a take-home presentation, or a LinkedIn long-form post. The arc adapts; the structure is constant.

## Behavior

### Step 1: Inputs

Required:
- Project name
- Audience (interviewer / panel / VC / blog readers, affects depth and what to emphasize)
- Format target (slides / talk / written post / verbal answer)

Optional but helpful:
- Specific role/company this is being told for (changes which beats to emphasize)
- What the user thinks the "headline" is

Check `claude-os/knowledge/` and `~/Documents/projects/[project]/` for existing context. Pull README, recent commits, key decisions.

### Step 2: Produce the 6-beat narrative

```
# Narrative: [Project Name], [Audience]

## Beat 1: The problem
[Specific. Not "people struggle with X", a concrete user/moment/pain point the user personally observed or experienced. Anchored in time and place. 30 seconds verbal / 1 slide.]

The strongest opening is a moment, not a category:
- WEAK: "Job seekers struggle with tailoring resumes."
- STRONG: "I was applying to a Senior PM role in payments. The JD wanted 8 specific things. I'd hit all 8 in my actual career. But my generic resume only spoke to 3 of them. The other 5 were buried in 12 years of bullet points. That's the problem."

## Beat 2: The insight
[What did the user see that most people miss? This is the load-bearing beat. Without a non-obvious insight, the pitch reads as "I built a thing that already exists." 30 seconds verbal / 1 slide.]

Examples of an insight:
- "Resume tailoring isn't a writing problem, it's a JD comprehension problem. The bottleneck is reading 50 JDs, not rewriting 50 resumes."
- "Nutrition apps fail because they treat groceries as the output. The output is *what to actually cook tonight*. Groceries are downstream."
- "Style apps don't fail at recommending outfits, they fail at understanding what's already in your closet."

## Beat 3: The solution
[The product, in plain English. Avoid jargon. Avoid feature dumps. What does it do, from the user's POV? 30-60 seconds / 1-2 slides.]

For each capability: who it's for, when they use it, what they get. Three capabilities max in the verbal version.

## Beat 4: The hard tradeoff
[CRITICAL beat for interview audiences. Every real product has a tradeoff that's not obvious. Senior interviewers listen for this, it's the test of whether the candidate is a builder or just a describer. 30-60 seconds / 1 slide.]

Examples:
- "I chose to ingest from 6 job board APIs instead of scraping. Tradeoff: fewer sources, but no fragile parsers. Worth it because pipeline stability beats source breadth at the n=1 user scale."
- "I built single-tenant first, refactored to household-scoped multi-tenant later. Tradeoff: rework cost. Worth it because the single-tenant version validated the core flow in 2 weeks."

If the user can't name the tradeoff, the project hasn't been built thoughtfully, push for one.

## Beat 5: What it taught me
[What's the transferable lesson? This is the beat that turns "I built a side project" into "here's why this experience makes me a better PM at YOUR company." Tailor to the audience. 30 seconds / 1 slide.]

For interview audiences specifically:
- Tie the lesson to the JD or the company's known challenges.
- Example: interviewing at a payments company → "The biggest lesson was the cost of ignoring entity resolution upstream, same lesson I'd apply to a fraud platform where signal quality starts at the merchant onboarding flow."

## Beat 6: What I'd do with 10x resources
[The closer. Shows ambition without overclaiming. Honest about the limits of what was built. 30 seconds / 1 slide.]

Two or three specific scale moves:
- "First: I'd add the 7 sources I cut. Today I cover 60% of postings; full coverage needs 12 sources."
- "Second: I'd ship a re-ranking model that learns from user accept/reject signals."
- "Third: I'd open it to 10-20 friends as a closed beta to test whether the value compounds across users."

The 10x answer signals where the strategic thinking is, not where the team would go next.
```

### Step 3: Output format

If audience is verbal/interview: produce as bullet sketch (30-60 sec per beat).

If audience is slides: produce one slide per beat with a title + 3-5 bullet points + speaker notes for the verbal version.

If audience is written (blog, LinkedIn long-form, take-home doc): produce as flowing prose, 4-7 paragraphs total.

## Rules

- **Beat 2 is load-bearing.** A narrative without a real insight fails. If the insight is generic ("AI is changing X"), push harder until you find the specific thing the user saw that others missed.
- **Beat 4 (hard tradeoff) is the senior signal.** Don't skip. If the user can't name a tradeoff, that's the conversation to have before drafting.
- **No fabricated metrics.** Defer to `metric-honest` if any number lands in the narrative. "10x faster" without methodology is a red flag.
- **The narrative is not a feature list.** If you find yourself listing capabilities in 3+ beats, restructure.
- **Match length to audience.** A 90-second pitch is not the same as a 15-slide deck, don't bloat the short form, don't truncate the long form.
- **Tie to the audience explicitly in Beat 5.** A narrative that doesn't change when the audience changes hasn't been adapted.

## Anti-patterns

- **Opening with "I built a tool that..."** Replace with the moment that made you build it.
- **Beat 2 is just a market trend.** "AI is hot" isn't an insight. The insight is what the user saw inside the problem.
- **Hard tradeoff section says "speed vs. quality."** Vague. Name the actual decision and what got cut.
- **"What I learned" is generic PM platitude.** "I learned the value of customer feedback" is useless. Tie to a specific transferable mental model.
- **10x section turns into a wishlist.** Two or three specific moves, each with a "why this next."
