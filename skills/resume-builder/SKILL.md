---
name: resume-builder
description: Use this skill whenever a user wants to build, improve, review, or tailor their CV or resume for AI/ML roles including AI PM, AI Engineer, ML Engineer, Data Scientist, AI Strategist, or any AI-adjacent position. Triggers include: "help me write my resume", "review my CV", "update my resume for an AI role", "how do I add AI keywords to my CV", "write my bullet points", "tailor my resume to this job description", "help me highlight my AI experience", "what should I put on my resume", or when a user shares their existing CV or job description and asks for improvements. Also trigger after completing the AI Job Strategy skill: the resume is always the next step. Use proactively whenever resume or CV improvement for AI roles is mentioned, even casually.
---

# AI Resume Builder

This skill helps users build, upgrade, and tailor a **high-impact, AI-optimized resume** for AI/ML product and engineering roles. It uses a proven impact formula, curated AI keyword bank, and real bullet point examples to produce a resume that gets past ATS and impresses hiring managers.

> Note: The original skill ships with a `references/keywords-and-bullets.md` keyword bank and bullet examples. That file is not bundled with the base template. The skill still works (the impact formula and structure are below), but for a fully-loaded keyword bank you can add your own.

---

## HOW TO USE THIS SKILL

Work **section by section** using `ask_user_input` to gather information. Draft each section immediately after collecting inputs, don't wait until the end. Keep it conversational and encouraging.

**Two modes, detect which applies:**
- **Build from scratch**: User has no existing CV → go through all sections in order
- **Review & upgrade**: User shares existing CV → run a gap analysis first, then improve section by section

---

## STEP 0: DETECT MODE

### Q0: Starting Point
```
ask_user_input:
  question: "Where are we starting from?"
  type: single_select
  options:
    - "I have an existing CV, help me upgrade it"
    - "Starting from scratch, build me a new one"
    - "I have a job description, tailor my resume to it"
    - "Just review my bullet points and improve them"
```

**If they share an existing CV:** Run a gap analysis against best-practice checks before asking any questions. Identify: missing keywords, weak bullets (no metrics), wrong tense, title mismatches, length issues. Present the gap analysis to the user first, then proceed section by section.

---

## STEP 1: PROFILE & TARGET ROLE

### Q1: Target Role
```
ask_user_input:
  question: "Which AI role are you targeting with this resume?"
  type: single_select
  options:
    - "AI Product Manager (AI PM)"
    - "Generative AI PM / LLM Product Owner"
    - "ML Engineer / AI Engineer"
    - "Data Scientist / AI Analyst"
    - "AI Strategy / Business Lead"
    - "Multiple roles, build a flexible base resume"
```

### Q2: Years of Experience
```
ask_user_input:
  question: "How many years of total work experience do you have?"
  type: single_select
  options:
    - "0–2 years (student / early career)"
    - "3–5 years"
    - "6–10 years"
    - "10+ years (senior / leadership)"
```

### Q3: AI Experience Level
```
ask_user_input:
  question: "How much direct AI/ML experience do you have?"
  type: single_select
  options:
    - "None yet, pivoting into AI"
    - "Some, worked with AI tools or alongside AI teams"
    - "Moderate, shipped 1–2 AI features or products"
    - "Strong, led multiple AI products or ML systems"
```

**Draft the resume header and summary section:**
- Name, Title (use the TARGET title, not current), LinkedIn/GitHub/Portfolio links
- 3-line professional summary: [Who you are] + [Domain expertise] + [AI focus] + [Career goal]
- Tailor summary keywords to the target role

---

## STEP 2: WORK EXPERIENCE (Most Critical Section)

Go role by role. For each role, ask:

### Q4: Role Details (repeat per role)
```
ask_user_input:
  question: "Tell me about your most recent / most relevant role. What did you actually do day-to-day?"
  type: single_select  [use as prompt: collect free text or follow up]
  options:
    - "I'll describe it, ask me follow-up questions"
    - "I'll paste my existing bullet points to improve"
    - "Let me describe the role and you write the bullets"
```

### Q5: AI Impact Areas (per role)
```
ask_user_input:
  question: "Which AI/ML areas did this role touch? (pick all that apply)"
  type: multi_select
  options:
    - "Built or managed LLM / Generative AI features"
    - "Used Prompt Engineering or RAG"
    - "Worked with ML models or data pipelines"
    - "Ran A/B tests or experimentation frameworks"
    - "AI roadmap, strategy, or ethics decisions"
    - "Cost/latency optimization of AI systems"
    - "Cross-functional delivery of AI product"
    - "Computer Vision or NLP features"
    - "No direct AI, but adjacent work"
```

### Q6: Metrics Available
```
ask_user_input:
  question: "Do you have any numbers or metrics from this role?"
  type: multi_select
  options:
    - "% improvement in a metric (speed, accuracy, engagement)"
    - "$ revenue or cost impact"
    - "Number of users or teams impacted"
    - "Time saved (hours, weeks, months)"
    - "Delivery speed (launched X% ahead of schedule)"
    - "No hard numbers, help me estimate"
```

**For each role, produce 3–5 bullets using the impact formula:**
`Accomplished [X] as measured by [Y] by doing [Z]`

Rules:
- Past tense always
- Start each with a strong action verb
- Include at least one AI technology by name (LLM, RAG, NLP, etc.)
- Lead with the most impressive bullet
- If no metrics: help user estimate ("roughly how many users saw this?", "did it save hours per week?")

**Job Title Check:** After drafting, flag if the user's internal HR title undersells the actual AI work. Suggest the appropriate market title (e.g. "AI PM" over "Senior Associate").

---

## STEP 3: AI PROJECTS & SIDE WORK

### Q7: Projects to Include
```
ask_user_input:
  question: "Do you have any AI projects, certifications, or side work to include?"
  type: multi_select
  options:
    - "Built an AI side project (personal or startup)"
    - "Completed an AI certification (DeepLearning.AI, Reforge, etc.)"
    - "GitHub contributions / open source AI work"
    - "Published LinkedIn posts, articles, or a blog on AI"
    - "Prototype or proof-of-concept built at work"
    - "None yet, skip this section"
```

**For each project, draft:**
- Project name + one-line description
- Technologies used (name tools, models, frameworks)
- 1–2 impact bullets using the formula
- Link if available (GitHub, demo, article)

**Pro tip to add:** If they have weak or no projects, suggest 2–3 quick high-impact project ideas tailored to their domain using agentic RAG, LLMs, or AI automation.

---

## STEP 4: SKILLS SECTION

### Q8: Technical Skills Inventory
```
ask_user_input:
  question: "Which of these have you actually worked with? (pick all that apply)"
  type: multi_select
  options:
    - "Python / SQL"
    - "LangChain / LangFlow / CrewAI"
    - "OpenAI API / Anthropic API / Gemini"
    - "Hugging Face / PyTorch / TensorFlow"
    - "RAG / Vector DBs (Chroma, Pinecone, Weaviate)"
    - "AWS SageMaker / Azure ML / Google Vertex AI"
    - "MLflow / Kubeflow / LLMOps tools"
    - "Power Automate / n8n / Zapier (AI automation)"
    - "Prompt Engineering"
    - "A/B Testing / Experimentation"
    - "Figma / Product Tools (Jira, Linear, etc.)"
```

**Draft Skills Section organized into 3 tiers:**
1. **AI/ML Tools & Frameworks**: tools they've actually used
2. **AI Concepts & Methods**: relevant concepts matched to target role
3. **Domain & Product Skills**: domain expertise + PM/eng fundamentals

**Keyword optimization:** Cross-reference against the target role's likely ATS keywords. Add all relevant terms the user qualifies for.

---

## STEP 5: EDUCATION & CERTIFICATIONS

### Q9: Credentials
```
ask_user_input:
  question: "What education or certifications do you have or are completing?"
  type: multi_select
  options:
    - "University degree (any field)"
    - "AI PM certification (e.g. Reforge, Product School)"
    - "DeepLearning.AI / Coursera ML courses"
    - "AWS / Azure / GCP AI certifications"
    - "Bootcamp or intensive program"
    - "Currently enrolled, in progress"
    - "None, plan to add soon"
```

Draft education section. If certifications are in progress, include them with "(In Progress, Expected [Month Year])".

---

## STEP 6: JOB DESCRIPTION TAILORING (if applicable)

If the user has a specific job description to target:

### Q10: Tailoring Mode
```
ask_user_input:
  question: "Do you want to tailor this resume to a specific job description?"
  type: single_select
  options:
    - "Yes, I'll paste the job description now"
    - "Yes, help me create a master resume I can tailor from"
    - "No, keep it general for now"
```

**If yes, run tailoring process:**
1. Extract top 5–7 required skills/keywords from the JD
2. Map each to existing resume bullets, identify gaps
3. Rewrite the top 3 bullets of the most relevant role to front-load those keywords
4. Update the professional summary to mirror the JD language
5. Flag any JD requirements the user genuinely can't claim, suggest honest framing

**Pro Tip to share with user:**
> "Create one master resume, then for each application update just the summary and the top bullet of your most relevant role to match the top 3 skills in that JD. This keeps quality high without rewriting from scratch every time."

---

## STEP 7: FINAL REVIEW & CHECKLIST

After drafting all sections, run the full checklist and present results:

```
✅ / ❌  1 page (< 10 yrs) or 2 pages (senior+)
✅ / ❌  Every bullet follows X → Y → Z formula
✅ / ❌  Past tense throughout
✅ / ❌  Most impactful bullet listed first per role
✅ / ❌  3–5 bullets per role max
✅ / ❌  AI keywords match target role
✅ / ❌  Strategic AI thinking demonstrated
✅ / ❌  Job titles reflect actual AI work done
✅ / ❌  Skills section covers tools used
✅ / ❌  No generic filler phrases ("responsible for", "helped with")
```

Flag any ❌ items and offer to fix them immediately.

---

## FINAL OUTPUT FORMAT

Produce the complete resume in clean markdown:

```markdown
# [Full Name]
[Target Job Title] | [City, Country] | [Email] | [LinkedIn] | [GitHub/Portfolio]

---

## Professional Summary
[3 sentences: Who you are + Domain expertise + AI focus + What you're seeking]

---

## Work Experience

### [Job Title, use market title, not HR title]
**[Company Name]** | [City] | [Start Date] – [End Date or Present]
- [Most impactful bullet, metric + AI tech + outcome]
- [Second bullet]
- [Third bullet]
- [Fourth bullet, if strong]

### [Previous Role]
...

---

## AI Projects & Initiatives
### [Project Name]
*[One-line description] | Technologies: [list]*
- [Impact bullet]

---

## Skills
**AI/ML Tools & Frameworks:** [list]
**AI Concepts & Methods:** [list]
**Domain & Product:** [list]

---

## Education & Certifications
**[Degree / Cert Name]**, [Institution] | [Year]
**[Cert in progress]**, [Institution] | Expected [Month Year]
```

---

## QUALITY STANDARDS

- **Never use:** "responsible for", "helped with", "assisted in", "worked on", these are weak; always rewrite
- **Always name the AI tech:** Don't say "built a chatbot", say "built an LLM-powered chatbot using GPT-4 and LangChain"
- **Metrics first:** If a bullet has no number, push user to estimate one before finalizing
- **Domain + AI intersection:** Every resume should show the user's domain expertise PLUS AI application in that domain
- **ATS-safe format:** No tables, no graphics, no columns in the text output, clean markdown only

---

## EDGE CASES

- **No AI experience at all:** Focus on transferable skills + adjacent work; add a "Learning & Projects" section for in-progress AI work; be honest but frame positively
- **Career gap:** Address briefly in summary, "Following a career break, now focused on transitioning into AI product management"; don't hide it, contextualize it
- **Too many roles:** Help user select the 3–4 most relevant; archive older roles in a 1-line "Earlier Career" section
- **Overqualified / senior:** Ensure resume shows leadership scale, team size managed, org-level AI strategy, not just execution
- **Student / no work experience:** Lead with projects, certifications, and coursework; use internships and academic AI work as primary experience
- **After finishing:** Always offer to (a) export to Word/PDF, (b) tailor to a specific JD, (c) write a matching LinkedIn headline and About section
