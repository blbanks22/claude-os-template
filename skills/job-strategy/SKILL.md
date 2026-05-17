---
name: job-strategy
description: Use this skill whenever a user wants to build a personalized, advanced strategy to land an AI role (AI PM, AI Engineer, AI Product, ML, Data Science, AI Strategy roles, etc.). Triggers include: "help me get an AI job", "I want to break into AI", "create my job strategy", "how do I get an AI PM role", "help me plan my AI career", "what's my path to AI", "review my AI job plan", "I want to transition into AI", or any request to build a structured career plan for AI roles. Also trigger when someone shares their CV, LinkedIn, or background and asks for AI career guidance. This skill walks users through a deep, section-by-section strategy workshop using interactive questions: use it proactively for any AI career planning conversation.
---

# Advanced AI Job Strategy Builder

This skill guides the user through a **comprehensive, personalized job strategy** to land an AI role. It is modeled on a proven 7-section strategy framework and adds advanced layers missing from basic templates: competitive benchmarking, personal brand building, network strategy, financial planning, skill gap analysis, and appendix support.

Go **section by section**: ask questions using `ask_user_input`, draft that section, confirm with the user, then move on. Do NOT front-load all questions at once.

---

## SECTION 1: DIAGNOSIS

> *Goal: Deeply understand where the user is today, experience, domain, challenges, and market position.*

### Q1: Experience Level
```
ask_user_input:
  question: "Where would you place yourself right now in your career?"
  type: single_select
  options:
    - "Student / Fresh graduate (0–1 yr)"
    - "Early career (1–3 yrs, non-AI)"
    - "Mid-career (3–7 yrs, non-AI)"
    - "Senior (7+ yrs, non-AI)"
    - "Already in tech/AI, looking to level up or pivot"
```

### Q2: Employment Status
```
ask_user_input:
  question: "What's your current employment situation?"
  type: single_select
  options:
    - "Employed in a relevant role"
    - "Employed in an unrelated role"
    - "Career gap (6 months+)"
    - "Freelancing / Consulting"
    - "Recently laid off"
```

### Q3: Domain Expertise
```
ask_user_input:
  question: "Which domain do you bring the most credibility or depth in? (This will anchor your AI niche)"
  type: single_select
  options:
    - "Healthcare / Biotech / Pharma"
    - "Finance / Fintech / Banking"
    - "Enterprise SaaS / B2B Software"
    - "Consumer / E-commerce / Retail"
    - "Manufacturing / Supply Chain / Logistics"
    - "Education / EdTech"
    - "Legal / GovTech / Public Sector"
    - "No clear domain yet, still exploring"
```

### Q4: Location & Work Mode Constraints
```
ask_user_input:
  question: "What location or work mode constraints do you have?"
  type: multi_select
  options:
    - "Must stay in my current city"
    - "Open to relocating within my country"
    - "Open to international relocation"
    - "Remote only"
    - "Targeting a specific city (e.g. SF Bay Area, NYC, London)"
```

### Q5: Competitive Self-Assessment
```
ask_user_input:
  question: "Compared to peers applying for AI roles, how do you assess yourself?"
  type: single_select
  options:
    - "Behind, they have more AI experience and credentials"
    - "Roughly equal, similar background, need differentiation"
    - "Ahead in domain, behind in AI technical skills"
    - "Strong all-around, need to accelerate application volume"
```

**Draft Section 1 covering:**
- Current situation summary (1–2 lines)
- Key challenges: location, employment status, experience gaps, career narrative
- Key opportunities: domain, transferable skills, curiosity, engineering mindset, unique background
- Market context note: Enterprise AI > Consumer AI; domain expertise > generic passion; real company AI > personal projects

---

## SECTION 2: GUIDING POLICY

> *Goal: Set the overarching philosophy and non-negotiables that will guide ALL decisions.*

### Q6: Target AI Role
```
ask_user_input:
  question: "Which AI role are you primarily targeting?"
  type: single_select
  options:
    - "AI Product Manager (AI PM)"
    - "AI/ML Engineer or MLE"
    - "Data Scientist / AI Analyst"
    - "AI Researcher (applied or fundamental)"
    - "AI Strategy / Business Lead"
    - "Founder / Building my own AI company"
    - "Open, want guidance on best fit"
```

### Q7: Non-Negotiables
```
ask_user_input:
  question: "What are your absolute non-negotiables? (pick all that apply)"
  type: multi_select
  options:
    - "Salary must significantly increase (e.g. 2x)"
    - "Must work in AI, no compromise"
    - "People management / leadership track required"
    - "Must be in a specific location (e.g. California)"
    - "Work-life balance cannot be sacrificed"
    - "Company must have strong AI mission / culture"
```

### Q8: Approach Preference
```
ask_user_input:
  question: "Which best describes your strategic approach to breaking in?"
  type: single_select
  options:
    - "Apply broadly and build fast (volume + speed)"
    - "Build credibility first, then apply selectively"
    - "Pivot internally at current company into AI"
    - "Start a company / build in public to signal expertise"
    - "Hybrid, build AND apply simultaneously"
```

**Draft Section 2 covering:**
- Overall approach and methodology tailored to their preference
- Core principles (from non-negotiables)
- Key strategic insight: focus on DOMAIN + AI intersection, not just AI alone
- Guidance note: Building AI for real companies > side projects; Enterprise AI > Consumer AI

---

## SECTION 3: MARKET & COMPETITIVE ANALYSIS

### Q9: Competitive Benchmarking Sources
```
ask_user_input:
  question: "Have you researched what people who successfully landed AI roles look like?"
  type: single_select
  options:
    - "Yes, I've reviewed LinkedIn profiles of AI PMs / Engineers"
    - "Somewhat, I've seen a few but haven't done deep analysis"
    - "No, I haven't done this yet"
    - "Yes, I know people in my cohort/network who got AI roles"
```

### Q10: Skill Gap Awareness
```
ask_user_input:
  question: "What do you feel are your biggest skill gaps for your target AI role? (pick all that apply)"
  type: multi_select
  options:
    - "AI/ML technical knowledge (models, architectures, APIs)"
    - "Prompt engineering and LLM product knowledge"
    - "Data analysis / SQL / Python"
    - "Product management fundamentals"
    - "AI product metrics and evaluation frameworks"
    - "Storytelling and executive communication"
    - "Portfolio / proof of work (GitHub, case studies)"
```

**Draft Section 3 covering:**
- Market trends: LLM-era AI roles, enterprise adoption curve, most in-demand AI PM/Eng skills
- Competitive landscape: what successful candidates look like (domain + AI credentials + proof of work)
- Skill gap analysis table: Current level vs. Required level vs. Gap vs. Priority
- How to do ongoing competitive research: LinkedIn "new role" announcements, cohort profiling, job description pattern analysis
- Differentiation strategy: what will make the user stand out vs. generic applicants

---

## SECTION 4: STRATEGIC OBJECTIVES

### Q11: 3-Year Vision
```
ask_user_input:
  question: "Where do you want to be in 3 years?"
  type: single_select
  options:
    - "Senior AI PM or Staff AI Engineer at a top company"
    - "Director / Head of AI Product or Engineering"
    - "Founding or leading my own AI startup"
    - "AI Researcher at a leading lab or university"
    - "VP / C-suite with AI as core responsibility"
```

### Q12: Target Timeline to First AI Role
```
ask_user_input:
  question: "What's your realistic target timeline to land your first AI role?"
  type: single_select
  options:
    - "3 months (aggressive)"
    - "6 months (focused)"
    - "12 months (steady)"
    - "18+ months (building from scratch)"
```

### Q13: Success Metrics
```
ask_user_input:
  question: "Beyond getting the job, what does success look like at 6 months in role? (pick top 2)"
  type: multi_select
  options:
    - "Leading a shipped AI product or feature"
    - "Managing a team of AI engineers or PMs"
    - "Achieving a specific compensation milestone"
    - "Building industry reputation / speaking / writing"
    - "Having a clear path to promotion within 12 months"
```

**Draft Section 4 covering:**
- Long-term goal (3-year)
- SMART short-term objectives (specific, measurable, with dates based on their timeline)
- Success definition at 6 months in-role
- Interim milestones: certification complete, portfolio live, applications launched, offer received

---

## SECTION 5: ACTION PLAN

### Q14: Key Initiatives
```
ask_user_input:
  question: "Which initiatives will you commit to? (pick all that apply)"
  type: multi_select
  options:
    - "Complete an AI PM or AI Engineering certification"
    - "Build and ship an AI side project (real users or real company)"
    - "Launch an AI startup or MVP with a small team"
    - "Champion an AI initiative at my current employer"
    - "Contribute to open-source AI projects (GitHub)"
    - "Write publicly about AI (LinkedIn, blog, newsletter)"
    - "Conduct 20+ informational interviews with AI professionals"
```

### Q15: Resource Commitment
```
ask_user_input:
  question: "What resources are you willing to invest? (pick all that apply)"
  type: multi_select
  options:
    - "Time: 5–10 hrs/week on upskilling and projects"
    - "Time: 10–20 hrs/week (serious commitment)"
    - "Time: 20+ hrs/week (all-in)"
    - "Money: Invest in a course or certification (< $500)"
    - "Money: Invest significantly ($500–$5,000 for bootcamp, dev help, etc.)"
    - "Money: Major investment ($5,000+, e.g. dev team, startup runway)"
    - "Social capital: Leverage my existing network actively"
```

### Q16: Team & Support Structure
```
ask_user_input:
  question: "Who will support or hold you accountable on this journey?"
  type: multi_select
  options:
    - "A mentor or coach in the AI space"
    - "A cohort or learning community (e.g. course cohort)"
    - "Friends or colleagues building alongside me"
    - "A paid dev team or collaborators"
    - "Accountability partner (check-in weekly)"
    - "Going solo for now"
```

**Draft Section 5 covering:**
- Key initiatives list with rationale for each
- Resource allocation: time per week, financial investment, team structure
- Roles & responsibilities: User = CEO, Mentors = Board, Collaborators = Team
- Financial planning note: estimated costs, ROI framing (investment vs. salary uplift)
- Accountability structure: who checks in, how often, what gets measured

---

## SECTION 6: PERSONAL BRAND & NETWORK STRATEGY

### Q17: Current Online Presence
```
ask_user_input:
  question: "What's your current online presence like?"
  type: single_select
  options:
    - "Strong LinkedIn + GitHub / portfolio already"
    - "LinkedIn exists but not optimized for AI"
    - "Minimal, rarely post or share work"
    - "Starting from zero"
```

### Q18: Content & Visibility Willingness
```
ask_user_input:
  question: "How comfortable are you building in public / creating content?"
  type: single_select
  options:
    - "Very comfortable, I enjoy writing and sharing"
    - "Somewhat, I'll do it if it helps get the role"
    - "Uncomfortable but willing to try"
    - "Prefer to stay low-profile, focus on work quality"
```

**Draft Section 6 covering:**
- LinkedIn optimization checklist: headline, about section, featured projects, AI keywords
- GitHub / portfolio strategy: what to build and showcase
- Content strategy: 1–2 posts/week cadence, topic ideas (AI tools, domain + AI intersection, learnings)
- Network activation plan: warm outreach templates, informational interview approach, community participation
- Signal-building tactics: commenting on AI thought leaders, sharing project updates, announcing milestones

---

## SECTION 7: IMPLEMENTATION ROADMAP

Based on the user's timeline from Q12, generate specific milestone dates from today.

### Q19: Application Strategy
```
ask_user_input:
  question: "What's your job application approach?"
  type: single_select
  options:
    - "High volume: 20–30+ applications/week"
    - "Targeted: 5–15 carefully chosen applications/week"
    - "Referral-first: prioritize warm intros before cold applying"
    - "Internal first: focus on internal transfers before external search"
```

### Q20: Interview Readiness
```
ask_user_input:
  question: "How prepared do you feel for AI role interviews right now?"
  type: single_select
  options:
    - "Not ready, need significant prep"
    - "Partially ready, need to practice AI-specific questions"
    - "Mostly ready, just need mock interviews and refinement"
    - "Ready, focus is on landing calls, not prep"
```

**Draft Section 7 covering:**
- Week-by-week or month-by-month timeline with specific milestone dates
- Phase 1 (Foundation): Skills, portfolio, LinkedIn optimization
- Phase 2 (Launch): Applications, networking, content publishing
- Phase 3 (Convert): Interview prep, mock interviews, offer negotiation
- KPI Dashboard:
  - Leading indicators: jobs applied, LinkedIn posts, GitHub commits, informational interviews, mocks done
  - Lagging indicators: recruiter responses, interview calls, final rounds, offers received
  - Financial: money earned from side projects, salary at offer

---

## SECTION 8: RISK MANAGEMENT

### Q21: Top Risks
```
ask_user_input:
  question: "What are your biggest concerns about this journey? (pick all that apply)"
  type: multi_select
  options:
    - "Running out of money / financial pressure"
    - "Taking too long, losing motivation or momentum"
    - "Not having strong enough technical AI skills"
    - "Rejection fatigue from applications"
    - "Family or personal obligations limiting time"
    - "Imposter syndrome / self-doubt"
    - "Competition is too fierce, market is saturated"
    - "Unclear on which exact role or path to pursue"
```

### Q22: Mitigation Readiness
```
ask_user_input:
  question: "Do you have any of these buffers in place already?"
  type: multi_select
  options:
    - "6+ months of financial runway saved"
    - "A mentor or coach actively guiding me"
    - "A community or cohort keeping me accountable"
    - "A plan B role / income source while I build"
    - "None of the above yet"
```

**Draft Section 8 covering:**
- Risk register: each identified risk with likelihood and impact rating
- Mitigation plan per risk (specific actions, not generic advice)
- Contingency plans: what to do if timeline slips by 3 months, what to do if no callbacks after 50 apps
- Mental health & resilience note: normalize rejection, build in review points, celebrate small wins

---

## SECTION 9: APPENDIX & SUPPORTING RESOURCES

**Auto-generate this section based on their target role and domain. Include:**

- **Recommended certifications** by role (AI PM cert, DeepLearning.AI courses, Reforge AI, etc.)
- **Key communities** to join (AI PM Slack groups, relevant LinkedIn communities, local meetups)
- **Job boards & sources** for AI roles (LinkedIn, Levels.fyi, Y Combinator jobs, specific company career pages)
- **People to follow** on LinkedIn in their target domain + AI intersection
- **Books / resources**: relevant AI product / strategy books
- **Portfolio project ideas** tailored to their domain (e.g. Healthcare AI PM → build a clinical AI triage tool prototype)
- **Competitive profiles to study**: prompt user to look at profiles of people who recently got AI roles and list 3 commonalities

---

## FINAL STRATEGY DOCUMENT FORMAT

Compile all drafted sections into this clean document:

```markdown
# [Name]'s AI Job Strategy, [Date]

## Executive Summary
*3–5 bullet summary of the full strategy*

## 1. Diagnosis
### Current Situation
### Key Challenges
### Key Opportunities
### Market Context

## 2. Guiding Policy
### Overall Approach
### Core Principles & Non-Negotiables

## 3. Market & Competitive Analysis
### Market Trends
### Competitive Landscape
### My Skill Gap Analysis
### Differentiation Strategy

## 4. Strategic Objectives
### Long-Term Goal (3 Years)
### SMART Short-Term Objectives
### Success Definition

## 5. Action Plan
### Key Initiatives
### Resource Allocation
### Roles & Responsibilities
### Financial Plan

## 6. Personal Brand & Network Strategy
### LinkedIn & GitHub Optimization
### Content Strategy
### Network Activation Plan

## 7. Implementation Roadmap
### Phase 1, Foundation (Month 1–2)
### Phase 2, Launch (Month 2–4)
### Phase 3, Convert (Month 4–6+)
### KPI Dashboard

## 8. Risk Management
### Risk Register
### Mitigation Plans
### Contingency Plans

## 9. Appendix
### Recommended Resources
### Portfolio Project Ideas
### Communities & Job Boards

---
*Strategy last updated: [Date] | Next review: [Date + 4 weeks]*
```

---

## QUALITY STANDARDS

- **Specificity over generality**: use the user's exact answers, never generic filler
- **Domain-first always**: every section reinforces their domain as the anchor for their AI pivot
- **Enterprise AI > Consumer AI**: frame project and role choices accordingly
- **Real company AI > personal projects**: prioritize initiatives that happen inside companies
- **Actionable**: every section ends with 2–3 concrete next actions
- **Honest**: don't sugarcoat gaps; acknowledge them and give a path forward
- **Dated milestones**: use real calendar dates, not vague "month 1, month 2"

---

## EDGE CASES & NOTES

- **User shares CV or LinkedIn**: Extract domain, experience level, and gap automatically; pre-fill Q1–Q5 answers and confirm with user before proceeding
- **User skips a question**: Make a reasonable assumption, state it explicitly, and allow correction
- **User is already in AI**: Adjust framing to "accelerating" rather than "breaking in"; focus on leveling up, salary increase, and leadership track
- **User is a student**: Adjust Section 5 heavily toward certifications, GitHub projects, internships, and network-building over job applications
- **User has a specific company target**: Add a company-specific section after Section 3 with tailored advice on that company's AI hiring signals
- **After full doc is presented**: Always offer to (a) refine any section, (b) export to PDF or Word, (c) set a 4-week check-in reminder prompt
