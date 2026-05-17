---
name: competitive-teardown
description: Use this skill whenever the user wants a focused deep-dive on a single competitor (or 2-3 head-to-head). Different from market-research (broad landscape), this is a targeted strategic teardown for a specific company. Triggers include "tear down [company]", "competitive teardown of X", "deep dive on [competitor]", "how does [competitor] really work", "what's [competitor]'s actual strategy", "audit [competitor]'s product", "compare us to [competitor]", or pasting a competitor URL with "analyze this". Use proactively when the user names a single competitor and wants more than just landscape-level info.
version: 1.0.0
argument-hint: <competitor name or URL> [+ optional context: our product, target user, what we want to learn]
---

# Competitive Teardown

## Trigger
Activate on "tear down [X]", "teardown of [X]", "deep dive on [competitor]", "what's [X] actually doing", "audit [competitor]", or any request for a focused look at one specific company (not a market sweep).

## Context

`market-research` answers "what's the landscape?" This skill answers "what is *this specific company* actually doing, why, and where are they weak?" It's the kind of analysis you do before:
- An interview with that company
- A board meeting where the question "what's their move?" will come up
- A build-vs-buy decision where they're the "buy" candidate
- A positioning sprint where you need to know their narrative cold

Output is a 1-page strategic brief: dense, evidence-backed, and immediately useful. Not a wall of text.

## Behavior

### Step 1: Confirm scope, then proceed without follow-ups

Ask one clarifying question only if the user gave just a name with zero context:
- "What's the angle: competitive positioning, hiring intel, product audit, or interview prep?"

Otherwise, infer angle from context and proceed. Default angle: competitive positioning + product audit.

### Step 2: Research with multiple search angles

Run at least 5 targeted web searches across:
1. **Official surfaces**: homepage, pricing page, product docs, changelog, blog. Read the actual product copy.
2. **Reviews**: G2, Capterra, TrustRadius, Product Hunt, Reddit. Get the unfiltered voice.
3. **News + funding**: Crunchbase, TechCrunch, SEC filings if public, recent press.
4. **Hiring signals**: job postings reveal tech stack and strategic priorities (e.g., "hiring 5 ML platform engineers" tells you they're investing there).
5. **Community signals**: HN threads, LinkedIn posts from their PMs/engineers, Twitter from the founder.

If sources conflict, cite both and call out the conflict.

### Step 3: Synthesize into the 1-page brief

```
# Teardown: [Company Name]

**Stage:** [seed / Series A-D / public / private mature]
**Funding:** $X total, last round [date, $amount, lead]
**Reported revenue:** $X ARR (year) [or "undisclosed"]
**HQ + headcount:** [city, ~size]
**One-liner:** [their own positioning, in their words, with link]

## The thesis they're betting on
[1-2 sentences. What do they believe about the market that drives every product decision? Not their tagline, their actual operating thesis.]

## Product (what it actually does)
- [Concrete capability 1 with a specific detail]
- [Concrete capability 2]
- [Concrete capability 3]
- [What's missing that you'd expect]

## Pricing + business model
| Tier | Price | What you get | Who buys |
|---|---|---|---|
| ... | ... | ... | ... |

[One sentence on pricing strategy: premium, freemium-led, usage-based, etc.]

## What they do well
1. **[Specific strength]** with evidence (review quote, feature, partnership)
2. **[Specific strength]** with evidence
3. **[Specific strength]** with evidence

## Where they're weak
1. **[Specific weakness]** with evidence (G2 complaint, missing feature, churn signal)
2. **[Specific weakness]** with evidence
3. **[Specific weakness]** with evidence

## Recent moves (last 6 months)
- [Date]: [What happened] → [Strategic read on why]
- [Date]: [What happened] → [Strategic read on why]
- [Date]: [What happened] → [Strategic read on why]

## What this means for [user's product/situation]
[3-4 bullets. Actionable, specific. Not "consider doing X", instead "X is table stakes, Y is where you win, Z is a trap to avoid."]

## Open questions / what I couldn't verify
- [Thing the user should dig into manually]
- [Thing that needs an insider conversation]

## Sources
[List with dates. Distinguish primary (official) from secondary (analyst/review).]
```

### Step 4: Honesty checks before delivering

- **No fabricated numbers.** If you can't verify ARR, headcount, or pricing, say "undisclosed" or "couldn't verify." Never make up a number to fill the table.
- **Cite specific evidence.** "Strong UX" is filler. "G2 reviewers cite the dashboard as the standout (4.7/5 across 340 reviews)" is evidence.
- **Be honest about weaknesses.** A teardown that finds zero weaknesses is a sales sheet, not analysis. There's always something, surface it.

## Rules

- One page. If you're past 600 words in the brief itself (excluding sources), cut.
- Every strength and weakness needs a specific citation, quote, or observable artifact. No generic claims.
- If the user asks for 2-3 competitors head-to-head, produce one brief per company, then a 3-row comparison matrix at the end (positioning / pricing / biggest weakness).
- For interview prep angle: add a final section "Likely interview questions about this company and how to answer them."
- For build-vs-buy angle: add a final section "Build vs buy verdict" with a clear recommendation.
- Default to neutral honest tone. Don't talk up the competitor; don't trash them. Just describe what's actually there.

## Anti-patterns

- **"They're an interesting player in the space."** Filler. Cut.
- **Pricing table with "Contact sales" in every row.** Try harder: check older snapshots on archive.org, third-party pricing analyses, or G2.
- **No dates on recent moves.** A "recent" move from 18 months ago isn't recent.
- **Strengths and weaknesses that mirror each other.** "Strong enterprise focus" / "Weak on SMB" is one observation, not two.
