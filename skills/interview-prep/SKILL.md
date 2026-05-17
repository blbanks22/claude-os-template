---
name: interview-prep
description: Use this skill whenever the user is preparing for a job interview, PM, AI PM, AI Engineer, ML, Data Science, or AI Strategy roles. Triggers include "prep me for [company] interview", "interview prep for [role]", "I have an interview at [X]", "help me prep for [interviewer name]", "what should I expect at [company]", "STAR stories for this JD", "tailor my prep to this job description", or any request that mentions an upcoming interview. Pulls from claude-os/knowledge/company/, knowledge/people/, and knowledge/career/job-search/ when relevant context exists.
version: 1.0.0
argument-hint: <company name> [+ role title] [+ JD url or pasted JD] [+ interviewer names]
---

# Interview Prep

## Trigger
Activate on "prep me for [company]", "interview prep", "I have an interview at [X]", "help me prep for [interviewer]", "what should I expect at [company]", "STAR stories for this JD", or pasting a JD with "tailor my prep."

## Context

This skill produces a focused prep packet for a specific interview, not generic "interview tips."

The prep packet integrates three sources:
1. **Public research**: company strategy, recent moves, product, competitive position.
2. **`claude-os/knowledge/`**: existing notes on the company, people, or career thinking that the user has already captured.
3. **JD analysis**: surface the specific signals the hiring team is looking for.

Output is interview-ready: questions the user is likely to face, stories they can tell, questions they should ask back, and 1-2 sharp insights that make them sound like they're already half-inside the company.

## Behavior

### Step 1: Gather inputs

Ask only for what's missing:
- Company name (required)
- Role title (required)
- JD link or pasted text (strongly preferred, adapt prep if missing)
- Interviewer name(s) and titles (optional)
- Interview round/format (phone screen, hiring manager, panel, exec, take-home)
- Date of interview (informs depth, same-day prep is different from a week out)

Check `claude-os/knowledge/company/[company-name]*` and `knowledge/people/[interviewer-name]*` for existing notes. Reference them if found.

### Step 2: Produce the prep packet

```
# Interview Prep: [Company], [Role]

**Round:** [Phone / HM / panel / exec]
**Interviewer(s):** [Name, title], [LinkedIn if known]
**Date:** [If known]
**JD link:** [URL]

## What they're actually hiring for
[2-3 sentences. The real read on the JD, not the bullet list. What's the unstated need? What pain are they trying to fix? Cite specific JD phrasing.]

## Company in 5 bullets
- **Stage + scale:** [funding, revenue, headcount if known]
- **Strategic moment:** [what they're trying to do *right now*, earnings call, recent launch, layoff, pivot]
- **Product:** [one-line, in your words]
- **How they compete:** [the wedge, what do they do that competitors don't?]
- **Hot topic in their space:** [the thing that would be in the news for their industry today]

## The 5-7 questions you're most likely to face
For each: the question, what they're really testing, and a sketch of how the user should answer.

1. **[Question]**
   - Testing: [the underlying competency]
   - Approach: [outline of a strong answer, not the full answer, just the structure]
   - Pull from: [which STAR story or example to use]

[... repeat for 5-7 questions ...]

## STAR stories mapped to this JD
Match the user's existing experience to specific JD requirements. For each:

**Story: [short name]**
- JD bullet this maps to: [exact phrase]
- Situation: [1 sentence]
- Task: [1 sentence]
- Action: [2-3 sentences]
- Result: [1 sentence with a *real* metric the user can verify, never fabricate]

[3-5 stories minimum, mapped to the JD's top signals]

## Questions you should ask THEM
5-7 questions, organized by who you'd ask each:
- **For the hiring manager:** [questions about role, scope, success metrics in 6/12 months]
- **For the team:** [questions about how decisions get made, what success looks like, what's hard]
- **For the exec / final round:** [questions about strategy, where the bet is, what would make this role fail]

Skip generic "what's the culture like" filler. Every question should reveal something or set up a follow-up.

## Sharp insights you can drop (1-2)
[Things the user should know about this company that 80% of candidates won't. A specific recent move + strategic read. A specific competitive vulnerability. A non-obvious observation about their product that signals they've been paying attention.]

## Red flags to listen for
- [Things they might say that should make the user reconsider, e.g., "we're rebuilding the team", "the previous person left after 6 months"]

## Logistics + format
- [What to expect for this round]
- [Time, format, what to bring]
- [Anything specific to this company's interview process, Glassdoor signal if relevant]

## Sources
[List with dates]
```

### Step 3: Save the prep packet

Write the output to `claude-os/knowledge/career/job-search/prep/[company]-[YYYY-MM-DD].md`. This builds institutional memory across the user's job search, by the third interview they've done with a company family (e.g., several fintechs), the prep gets sharper because past prep is available.

## Rules

- **Never fabricate metrics in STAR stories.** Top rule: "Never fabricate metrics, stats, or citations. Say 'I don't know' instead." If a story needs a number the user hasn't given, write `[NEED: user to fill in result metric]` instead of guessing.
- **Never invent the interviewer's background.** If you don't have data on them, say "Couldn't find a public profile" rather than making up their experience.
- **Calibrate depth to time.** A same-day prep is 1 page focused on stories + questions. A week-out prep can go deeper on company strategy.
- **STAR stories pull from prior conversation context first.** If the user has mentioned specific projects in this session or memory, draw from those before asking for new ones.
- **For technical/AI PM roles**, add a "Technical depth questions" section with 3-5 questions that probe ML/AI fluency (model selection, eval design, productionizing LLMs, etc.).
- **The packet earns its place if the user walks in knowing 2 things 80% of candidates won't.** If the "Sharp insights" section is generic, redo it.

## Anti-patterns

- **Listicle of generic PM interview questions.** Every question must be tied to *this* role at *this* company. "Tell me about a time you led a cross-functional initiative" is fine if mapped to a specific JD bullet that demands it.
- **STAR stories without metrics.** Empty action without measurable result. Push for the number.
- **Questions to ask them that feel like fishing.** "What's the team's biggest challenge?" is filler unless the user has an angle on it. Replace with "I read that [X] is being deprioritized this quarter, how does that affect this role's first 90 days?"
- **No company-specific signal.** If the prep could be reused for any role at any company, it failed.
