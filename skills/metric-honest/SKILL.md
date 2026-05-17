---
name: metric-honest
description: Use this skill BEFORE any quantitative claim lands in a user-authored artifact, resume bullet, PRD, interview answer, pitch deck, application essay, postmortem, weekly review, or LinkedIn post. Triggers include "is this number okay", "fact-check this claim", "metric check", "did I really hit that number", "can I say [X]% improvement", "verify this stat", "is this defensible", or surfacing automatically when Claude is about to write a quantitative claim in a finished artifact. Aligns with the rule, never fabricate metrics, stats, or citations.
version: 1.0.0
argument-hint: <the quantitative claim or stat you're about to use>
---

# Metric Honest

## Trigger
Activate before any number lands in a user-authored artifact. Also activate on "is this number okay", "fact-check this", "verify this stat", "can I claim [X]", or when Claude is drafting content that includes a metric.

Use proactively. If Claude is generating a resume bullet or PRD section that includes a percentage, dollar figure, count, or comparative claim, run this check before writing the final version.

## Context

The top rule: **never fabricate metrics, stats, or citations.** This isn't paranoia, it's the same discipline that keeps a platform PM out of trouble, and the same discipline that prevents a resume claim from getting torn apart in an interview reference check.

The risk surface for fabrication:
- **Resume bullets** that claim impact without verifiable source ("reduced fraud 30%")
- **PRD problem sections** with made-up customer counts or survey percentages
- **Interview answers** that retrofit clean numbers onto messy real outcomes
- **Pitch deck slides** that round up or round down inconvenient figures
- **LinkedIn posts** that quote a stat from "a recent study" without naming or linking it
- **Postmortems** that misattribute cause-and-effect to flatter outcomes

The fix is a 4-question audit before any number ships.

## Behavior

### Step 1: Capture the claim

User input is a quantitative claim. Restate it exactly as proposed:

> Claim: "[Exact wording]"

### Step 2: Run the 4-question audit

Ask each, get answers from the user, write down the answer:

1. **What's the source?**
   - Not "I remember it was about 30%", the actual artifact: dashboard URL, report file, query result, customer survey export, an email confirming the figure.
   - If the source is a memory or estimate, mark the claim as `[ESTIMATE]` or replace with a range.

2. **What's the methodology?**
   - How was the number measured? Over what time window? What's the population?
   - "30% reduction" → 30% of what, vs what baseline, over what period?
   - A claim is only as good as the methodology behind it.

3. **What's the attribution?**
   - Did *this work* cause the outcome, or did it correlate with it?
   - Were there other changes happening at the same time (seasonality, other launches, team changes)?
   - "Led to" vs "contributed to" vs "coincided with", match the language to the actual evidence.

4. **What's the caveat?**
   - Every number has one. Sample size? Time window short? Specific segment only? Pre-launch baseline noisy?
   - The caveat doesn't have to appear in the final claim, but the user should be able to answer "what's the limitation of that number?" if asked in an interview.

### Step 3: Verdict and revised claim

Output one of three verdicts:

**A) Defensible as stated.** The user can use the claim as is. Note the source so it's recoverable.

**B) Defensible with revision.** Suggest a tighter, more honest version.
- Example: "30% reduction in fraud" → "30% reduction in card-not-present false declines for the merchant cohort onboarded Q2 2024, measured 90 days post-launch (n=12 merchants)."
- Or: "30% improvement" → "Contributed to a 30% improvement; specific attribution to my work was the dashboard redesign that surfaced the underlying signal."

**C) Don't use.** If source is "I think I remember," methodology is unclear, attribution is shaky, and there's no recoverable artifact, recommend either:
  - Replace with a directional claim ("Materially reduced false declines", no number)
  - Drop the line entirely
  - Or do the work to get the real number from the system of record

```
# Metric Audit

**Original claim:** "[Exact wording]"

**Source:** [What the user provided]
**Methodology:** [How it was measured]
**Attribution:** [Causal link evidence]
**Caveat:** [What's true but uncomfortable]

**Verdict:** [A / B / C]

**Revised claim (if needed):** "[Tighter version]"

**Note for future use:** [Where this number can be re-verified, what the underlying artifact is, who would know if challenged in an interview.]
```

### Step 4: For batch checks (e.g. whole resume)

If the user is auditing multiple claims (a full resume, a PRD section with many stats), produce a table:

| Claim | Verdict | Revised | Source / Issue |
|---|---|---|---|
| ... | A/B/C | ... | ... |

Flag the C-verdict items prominently, those are the ones that get tested in an interview.

## Rules

- **No "probably." No "roughly." No "about."** If the number is approximate, say so explicitly (`~30%` or `[ESTIMATE]`), don't hide the uncertainty under a confident-sounding round number.
- **Distinguish "led to" from "correlated with."** Causal language requires evidence. Without evidence, use weaker language.
- **A range is more honest than a precise number you can't defend.** "20-35%" beats "30%" if the latter is a midpoint guess.
- **If the user can't name the source of a number, that's a C-verdict by default.** No exceptions.
- **The bar is "could you defend this on a 30-min reference call with someone who saw the data?"** If no, revise or drop.
- **Don't moralize.** This isn't a lecture about honesty, it's a practical tool to prevent embarrassing reference-check failures and to make the user's claims more credible by being tighter.

## Anti-patterns

- **"30% improvement" with no time window.** Always specify the period.
- **"Reduced fraud", fraud what? Volume, dollar amount, false positive rate, true positive rate?** Specificity changes the claim.
- **"Increased adoption" without a baseline.** A metric without baseline is a wish.
- **Citing "industry research shows X" without naming the source.** Either name the report or drop the claim.
- **Letting a clean round number (10x, 50%, 3 months) slide unchecked.** Round numbers are the most often fabricated. Push hardest on these.

## When to use this skill silently vs explicitly

- **Silently:** Whenever drafting a resume bullet, PRD claim, interview STAR story result, or LinkedIn post, run the audit internally first. If verdict is A, use as-is and move on. If B or C, raise it.
- **Explicitly:** When the user invokes the skill by name or pastes a specific claim to verify.
