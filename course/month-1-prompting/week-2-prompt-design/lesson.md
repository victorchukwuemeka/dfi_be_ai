# Week 2: Prompt Design — Role, Task, Constraints, Examples, Output Schema

## Why Prompt Design Matters

Last week you learned how the model works: tokens, context windows, temperature. This week you learn how to control it. Prompt design is the difference between getting a generic wall of text and getting something you can actually use.

**The core idea:** Great prompts are not longer prompts. They are *structured* prompts. Structure comes from five components working together:

```
┌──────────────────────────────────────────────────────────────────┐
│                      THE 5-COMPONENT FRAMEWORK                  │
│                                                                  │
│   1. ROLE        → Who is the AI acting as?                     │
│   2. TASK        → What exactly should it do?                   │
│   3. CONSTRAINTS → Boundaries that shape the output             │
│   4. EXAMPLES    → Show, don't tell                             │
│   5. SCHEMA      → How to format the response                  │
│                                                                  │
│   Not every prompt needs all five. But the more you include,    │
│   the more reliable the output.                                 │
└──────────────────────────────────────────────────────────────────┘
```

---

## Component 1: Role

**What:** Tell the AI who it is — what expertise, perspective, or persona to adopt.

**Why it works:** Role primes the model for domain vocabulary, tone, reasoning style, and depth. A "senior data analyst" produces different output than a "marketing intern."

### Role Examples

| Role | Effect on Output |
|------|-----------------|
| "You are a senior data analyst at a Fortune 500 company" | Technical, precise, uses industry jargon, references metrics |
| "You are a copywriter for a B2B SaaS company" | Persuasive, benefit-focused, uses marketing language |
| "You are a career coach for mid-career professionals" | Empathetic, action-oriented, uses coaching frameworks |
| "You are a 5th-grade science teacher" | Simple language, analogies, step-by-step explanations |
| "You are a skeptical auditor reviewing financial statements" | Questioning, detail-oriented, flags inconsistencies |

### Good vs Bad Roles

**Weak role:** "You are an expert."
→ Expert in what? This tells the model nothing useful. It will default to a generic, safe tone.

**Strong role:** "You are a senior financial analyst with 15 years of experience in healthcare sector valuations."
→ Now the model knows: domain (finance), sub-domain (healthcare), seniority level (experienced), and context (valuations).

### When to Use a Role

- When the task requires domain knowledge (finance, legal, medical, technical)
- When tone and voice matter (executive communication, customer support)
- When you want a specific reasoning style (skeptical reviewer vs. optimistic brainstormer)
- When audience matters (explain to a child vs. explain to an expert)

### When to Skip a Role

- Simple formatting tasks ("Convert this to a table")
- Quick factual lookups ("What's the boiling point of water?")
- When the task itself implies the expertise ("Summarize this article")

---

## Component 2: Task

**What:** The specific action the AI should take. Be explicit, measurable, and singular.

**Why it works:** The model predicts the most likely continuation. If you don't tell it exactly what to do, it guesses. A precise task narrows the prediction space dramatically.

### Good vs Bad Tasks

| Vague Task | Specific Task |
|-----------|---------------|
| "Analyze this data" | "Analyze this quarterly sales data and identify the top 3 trends, including percentage changes from last quarter" |
| "Write about productivity" | "Write a 3-paragraph memo to a team about improving meeting productivity, with one technique per paragraph" |
| "Help me with this email" | "Rewrite this email to be more concise, reduce it from 200 words to under 80, and make the call-to-action clearer" |
| "Explain this concept" | "Explain this concept in 3 sentences using an analogy a non-technical person would understand" |
| "Summarize this document" | "Summarize this document in exactly 5 bullet points, each under 15 words, focusing on financial implications only" |

### The One-Prompt-One-Job Rule

**Bad:** "Analyze this sales data, write a summary for the CEO, and draft an email to the team about the findings."
→ Three different jobs in one prompt. The model has to guess which to prioritize, and the output will be unfocused.

**Good:** Three separate prompts:
1. "Analyze this sales data and identify the top 3 trends."
2. "Write a 100-word executive summary of the following analysis for a CEO."
3. "Draft a short email to the marketing team about these findings. Tone: factual, under 150 words."

### Task Verbs to Use

| Verb | What It Signals |
|------|----------------|
| "Analyze" | Break down, find patterns, draw conclusions |
| "Summarize" | Condense, extract key points |
| "Draft" | Create a first version (implies iteration) |
| "Rewrite" | Improve existing content (provide the original) |
| "Extract" | Pull specific data points from text |
| "Compare" | Identify similarities and differences |
| "Evaluate" | Assess against criteria, assign ratings |
| "Brainstorm" | Generate multiple ideas (set quantity) |
| "Translate" | Convert from one format/audience to another |

---

## Component 3: Constraints

**What:** Boundaries that shape the output — length, tone, format, content rules, and exclusions.

**Why it works:** Constraints prevent the model from wandering. Without them, it defaults to a generic 5-paragraph format at medium tone. Constraints force it into the shape you need.

### Constraint Categories

#### Length Constraints

| Constraint | Effect |
|-----------|--------|
| "Exactly 5 bullet points" | Forces conciseness, prevents rambling |
| "Under 200 words" | Keeps output short and focused |
| "3 paragraphs of 2-3 sentences each" | Controls structure and density |
| "One sentence only" | Forces maximum compression |

#### Tone Constraints

| Tone | When to Use |
|------|------------|
| "Formal and professional" | Executive communication, legal, official docs |
| "Casual and friendly" | Internal team messages, social media |
| "Direct and actionable" | Memo, instructions, to-do lists |
| "Empathetic but firm" | Difficult feedback, customer complaints |
| "Neutral and factual" | Reports, summaries, analysis |
| "Urgent and concise" | Alerts, time-sensitive communications |

#### Format Constraints

| Format | Effect |
|--------|--------|
| "Use a markdown table" | Structured comparison data |
| "Return as JSON" | Machine-readable structured output |
| "No markdown, plain text only" | Clean copy-paste into other tools |
| "Use numbered list" | Ordered steps or ranked items |
| "Headers and bullet points" | Scannable document structure |

#### Content Constraints

| Constraint | Effect |
|-----------|--------|
| "Only include facts from the provided document" | Prevents hallucination |
| "Do not mention competitors by name" | Legal/brand safety |
| "Only use data from Q3 2024" | Time-bound accuracy |
| "Focus on financial implications only" | Narrows scope |
| "Do not use the words 'innovative', 'synergy', or 'leverage'" | Eliminates buzzwords |

### Constraints in Action

**No constraints:** "Write about our product launch."
→ You'll get a generic 300-word essay about product launches in general.

**With constraints:** "Write a 150-word product launch announcement for our new project management tool. Tone: enthusiastic but professional. Audience: existing customers. Include one specific feature benefit. End with a CTA linking to the signup page."
→ Focused, usable, audience-aware, actionable.

---

## Component 4: Examples (Few-Shot)

**What:** Show the model exactly what you want by providing 1-3 input-output examples before the actual request.

**Why it works:** Examples demonstrate your definition of "good." They are more precise than any written instruction. The model learns the pattern from your examples and applies it to new input.

### Zero-Shot vs Few-Shot

**Zero-shot (no examples):**
```
Classify this customer review as positive, negative, or neutral.
Review: "The product works but shipping was slow."
```
→ The model guesses the format. It might say "Neutral" or "Mixed" or write a paragraph explaining its reasoning.

**Few-shot (with examples):**
```
Classify each review as positive, negative, or neutral.

Review: "This product changed my life!"
Classification: Positive

Review: "Arrived broken. Terrible support."
Classification: Negative

Review: "It works as expected."
Classification: Neutral

Review: "The product works but shipping was slow."
Classification:
```
→ The model follows the pattern: single word classification, matching the format you demonstrated.

### Example Design Principles

1. **Match your output format.** If you want "Positive" as output, show "Positive" — not "I would rate this as positive."
2. **Cover edge cases.** Show examples that cover different categories, especially ambiguous ones.
3. **Keep examples concise.** Long examples waste tokens and can confuse the pattern.
4. **Use 2-3 examples.** One is often enough for formatting. Two to three cover the range. More than five rarely helps and costs tokens.

### Examples for Different Tasks

**Tone example:**
```
Tone: Professional but approachable

Good: "We recommend reviewing your coverage annually to ensure it still meets your needs."
Bad: "You should def check your policy, lol."

Now rewrite: "Insurance is complicated."
```

**Format example:**
```
Format your response exactly like this:

- Problem: [one sentence]
- Impact: [one sentence]
- Solution: [one sentence]

Now analyze: [your input]
```

**Reasoning example:**
```
I'll work through this step by step.

Input: "Revenue grew 12% but costs grew 18%"
Analysis: Revenue is growing, but costs are growing faster. This means margins are shrinking. The business is scaling but becoming less efficient per dollar of revenue. Key risk: if cost growth outpaces revenue growth for 2 more quarters, profitability will decline.

Now analyze: "Customer count grew 25% but average order value dropped 10%"
```

---

## Component 5: Output Schema

**What:** Tell the AI exactly how to structure the response — headers, fields, format, or data structure.

**Why it works:** Schema eliminates format guessing. The model won't give you a table when you need JSON, or a paragraph when you need bullet points. It also makes output machine-parsable if needed.

### Schema Examples

**JSON schema:**
```
Return a JSON object with the following fields:
{
  "summary": "2-3 sentence overview",
  "key_points": ["point 1", "point 2", "point 3"],
  "action_items": ["action 1", "action 2"],
  "risk_level": "high | medium | low"
}
```

**Table schema:**
```
Format as a markdown table with columns:
| Category | Finding | Severity | Recommendation |
```

**Section schema:**
```
Structure your response as:
## Executive Summary
[2-3 sentences]

## Key Findings
- [finding 1]
- [finding 2]

## Recommended Actions
1. [action 1]
2. [action 2]

## Timeline
[When to do each action]
```

**Minimal schema:**
```
Format your response as:
- Problem: [one sentence]
- Cause: [one sentence]
- Solution: [one sentence]
```

### When to Use a Schema

| Situation | Schema Needed? |
|-----------|---------------|
| Output will be copy-pasted into another tool | Yes — JSON or CSV |
| Output needs to be shared with a team | Yes — consistent format |
| Output will appear in a report or presentation | Yes — headers and structure |
| Quick personal use | Optional — simple format often enough |
| Data extraction | Yes — structured fields prevent data loss |

---

## Putting It All Together

Here's how a complete prompt uses all five components:

```
ROLE: You are a financial analyst specializing in SaaS company valuations.

TASK: Analyze this company's Q2 earnings call transcript and extract
the most important financial signals.

CONSTRAINTS: Use plain language suitable for non-finance readers.
Max 200 words. Focus only on revenue, costs, and growth metrics.
Do not speculate beyond what was stated.

EXAMPLES:
Input: "Revenue hit $45M, up 22% YoY. Churn dropped to 3%. We hired 40 people."
Output:
- Revenue: $45M (+22% YoY) — strong growth trajectory
- Churn: 3% — healthy retention, below industry average of 5-7%
- Headcount: +40 — aggressive hiring signals confidence in pipeline

SCHEMA:
- Revenue: [number] — [what it means]
- Cost Trend: [direction] — [what it means]
- Growth Signal: [positive/negative/mixed] — [one sentence]

[transcript here]
```

### What Happens Without Each Component

| Missing Component | What Goes Wrong |
|------------------|----------------|
| No role | Output is generic, may not match the expertise level needed |
| No task | Model guesses what you want, produces unfocused output |
| No constraints | Output is too long, wrong tone, wrong format, rambling |
| No examples | Model follows a different pattern than you intended |
| No schema | Output is a wall of text, hard to parse or share |

---

## The Framework Diagram

```
                    ┌─────────────┐
                    │    ROLE     │  "Who is the AI?"
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │    TASK     │  "What should it do?"
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
       ┌──────▼──────┐ ┌──▼────────┐ ┌─▼────────────┐
       │ CONSTRAINTS │ │ EXAMPLES  │ │    SCHEMA    │
       └──────┬──────┘ └──┬────────┘ └─┬────────────┘
              │            │            │
              └────────────┼────────────┘
                           │
                    ┌──────▼──────┐
                    │   OUTPUT    │  Reliable, usable result
                    └─────────────┘
```

Role and Task are the foundation. Constraints, Examples, and Schema are the refinement layer. The more of these you include, the more predictable the output.

---

## Practical Demonstrations

### Example 1: Email Rewriting

**Task:** Rewrite a rambling email to be more concise.

**Prompt with all 5 components:**
```
Role: You are an executive communications coach.
Task: Rewrite the following email to be concise and actionable.
Constraints: Under 80 words. Remove all filler phrases. Keep the original intent.
Example:
  Original: "Hi, I just wanted to reach out to see if maybe we could possibly
  schedule a time to chat about the project because I think there might be some
  things we should discuss."
  Rewrite: "Hi — can we schedule 30 minutes this week to discuss the project?
  I have a few items to align on."

Rewrite this email:
[original email]
```

**Why this works:** The role sets the expertise. The task is specific (rewrite, make concise). Constraints control length and intent preservation. The example shows exactly what "concise" means to you. The schema is implicit (just the rewritten email).

### Example 2: Data Extraction from Text

**Task:** Pull structured data from messy text.

```
Role: You are a data extraction specialist.
Task: Extract structured information from the following meeting notes.
Constraints: Only extract information that is explicitly stated.
If a field is not mentioned, set it to "Not mentioned."
Do not infer or guess.

Schema:
- meeting_date: [date]
- attendees: [list of names]
- decisions: [list of decisions made]
- action_items: [list, each with owner and deadline]
- next_meeting: [date or "Not scheduled"]

Meeting notes:
[paste notes here]
```

### Example 3: Comparing Options

```
Role: You are a business analyst evaluating vendor proposals.
Task: Compare these two software vendor proposals.
Constraints: Neutral tone. Only state facts from the proposals.
No recommendations — just present the comparison.
Max 300 words.

Schema:
| Criteria | Vendor A | Vendor B |
|----------|----------|----------|
| Price | | |
| Features | | |
| Support | | |
| Contract Terms | | |

Vendor A proposal:
[text]

Vendor B proposal:
[text]
```

---

## Common Mistakes

### Mistake 1: Vague Role
**Bad:** "You are an expert."
**Why it fails:** Expert in what? The model defaults to a generic voice.
**Fix:** Specify domain, seniority, and context. "You are a senior cybersecurity analyst specializing in small business infrastructure."

### Mistake 2: No Constraints
**Bad:** "Analyze this data."
**Why it fails:** The model decides length, tone, format, and depth. You get whatever it wants to give.
**Fix:** Add at least: length, tone, and format constraints.

### Mistake 3: Mixing Tasks
**Bad:** "Analyze this report, write a summary, and draft an email about it."
**Why it fails:** Three jobs in one prompt. The model splits its attention and does all three poorly.
**Fix:** One prompt = one job. Chain them: analyze first, then summarize the analysis, then draft the email.

### Mistake 4: No Examples for Formatting
**Bad:** "Classify these reviews."
**Why it fails:** The model might say "Positive" or "I would rate this as positive" or "This review is mostly positive with some negative elements."
**Fix:** Show one example of the exact output format you want.

### Mistake 5: Not Specifying Output Format
**Bad:** "Give me insights from this data."
**Why it fails:** You get a paragraph. Now you have to reformat it yourself.
**Fix:** "Return as a table with columns: Metric | Value | Trend | Significance."

### Mistake 6: Over-Specifying
**Bad:** A 500-word prompt for a simple task like "Convert these dates from US to UK format."
**Why it fails:** Unnecessary overhead. The model spends tokens processing instructions it doesn't need.
**Fix:** Match prompt complexity to task complexity. Simple tasks need simple prompts.

### Mistake 7: Confusing "Help Me" with "Do This"
**Bad:** "Help me write a business plan."
**Why it fails:** "Help me" is open-ended. The model doesn't know where to start or what you need.
**Fix:** "Write a one-page business plan template for a mobile coffee shop. Include: problem statement, solution, target market, revenue model, and first-year costs."

---

## Interactive Exercises

### Exercise 1: Component Identification

Look at this prompt and identify each of the 5 components:

```
You are a project manager writing to a cross-functional team.
Summarize the following status update.
Keep it under 5 bullet points.
Use a neutral, factual tone.
End with one question for the team.

Example:
Status: "Backend API deployed to staging. Frontend team blocked on
design assets. QA found 3 critical bugs in payment flow."
Summary:
- Backend API deployed to staging — on track
- Frontend blocked on design assets — risk to sprint goal
- 3 critical bugs found in payment flow — requires immediate attention
- QA testing halted until bugs are fixed
- Question: Can design team deliver assets by Wednesday?

Now summarize:
[actual status update]
```

**Try identifying:** Which text is the role? The task? The constraints? The example? The schema?

---

### Exercise 2: Weak Prompt Autopsy

Here's a prompt that failed:
"Write something about dogs."

**Analyze it:**
1. What's missing? (role, audience, format, tone, length, specific topic)
2. Rewrite it 3 different ways for 3 different audiences:
   - A veterinarian writing a blog post
   - A parent looking for family-friendly breed recommendations
   - A city council member debating dog park funding
3. Test all 3. Compare the outputs.

---

### Exercise 3: Progressive Constraint Building

Start with this vague prompt and add constraints one at a time:
"Write a project status update."

**Round 1:** Add role.
→ "You are a project manager writing to your VP."
**Round 2:** Add constraints.
→ "Keep it under 150 words. Use a neutral, factual tone."
**Round 3:** Add schema.
→ "Structure as: Accomplishments | Blockers | Next Steps"
**Round 4:** Add example.
→ Show a sample status update that matches the format.

**After each round, run the prompt and compare outputs.** Document what changed.

---

### Exercise 4: A/B Testing Prompts

Pick a task relevant to your work (summarize a document, draft an email, analyze data).

1. Write a **minimal prompt:** Role + Task only
2. Write a **full prompt:** Role + Task + Constraints + Examples + Schema
3. Run both on the same input, 3 times each
4. Score each output:

| Criterion | Minimal (1-5) | Full (1-5) |
|-----------|--------------|------------|
| Accuracy | | |
| Usefulness | | |
| Conciseness | | |
| Format match | | |

Which prompt consistently produces better output?

---

### Exercise 5: Cross-Domain Role Play

Take the same task and give it to prompts with different roles:
"Analyze this customer complaint and suggest a response."

- Role A: "You are a customer support manager"
- Role B: "You are a legal compliance officer"
- Role C: "You are a brand marketing director"

Compare: How does the role change the analysis, tone, and suggested response?

---

## Real-World Scenarios

### Scenario 1: Executive Brief

**Challenge:** Turn a 20-page report into a one-page executive brief.

```
Role: You are a management consultant preparing a client brief.
Task: Condense the following report into a one-page executive summary.
Constraints: Max 400 words. Formal tone. No jargon without explanation.
Focus on: key findings, financial impact, and recommended actions.

Schema:
## Executive Summary
[2-3 sentences]

## Key Findings
- [finding with supporting data]

## Financial Impact
[revenue/cost implications in plain numbers]

## Recommended Actions
1. [action — owner — timeline]
2. [action — owner — timeline]

Report:
[paste report]
```

### Scenario 2: Interview Prep

**Challenge:** Prepare for a job interview at a specific company.

```
Role: You are a career coach who has helped 500+ professionals
prepare for interviews at tech companies.
Task: Generate 10 likely interview questions for a Product Manager
role at a Series B startup, plus suggested answer frameworks.
Constraints: Mix of behavioral (STAR method) and strategic questions.
No generic questions — tailor to startup context.
Keep each answer framework to 3-4 bullet points.

Schema:
Question 1: [question]
Type: Behavioral | Strategic
Answer framework:
- Situation:
- Task:
- Action:
- Result:

[repeat for all 10]
```

### Scenario 3: Contract Review

```
Role: You are a paralegal reviewing a vendor contract for a
non-legal stakeholder.
Task: Identify the top 5 risks in this contract clause.
Constraints: Plain language, no legal jargon.
Each risk should be explainable to a non-lawyer.
Do not provide legal advice — only flag potential concerns.

Schema:
Risk 1: [one-line summary]
- Clause: [exact text from contract]
- Concern: [plain language explanation]
- Severity: High | Medium | Low
- Suggested question for legal team: [one question]
```

### Scenario 4: Content Repurposing

```
Role: You are a content strategist.
Task: Repurpose this blog post into 5 social media posts.
Constraints: Each post under 280 characters. Vary the angles:
one stat-focused, one question, one story, one tip, one quote.
Platform: LinkedIn (professional tone, industry hashtags).

Schema:
Post 1 (Stat): [text] | Hashtags: [hashtags]
Post 2 (Question): [text] | Hashtags: [hashtags]
Post 3 (Story): [text] | Hashtags: [hashtags]
Post 4 (Tip): [text] | Hashtags: [hashtags]
Post 5 (Quote): [text] | Hashtags: [hashtags]

Blog post:
[paste blog]
```

---

## When to Use Each Component

| Situation | Role | Task | Constraints | Examples | Schema |
|-----------|:----:|:----:|:-----------:|:--------:|:------:|
| Quick factual question | — | ✓ | — | — | — |
| Writing for an audience | ✓ | ✓ | ✓ | — | ✓ |
| Data extraction | ✓ | ✓ | ✓ | ✓ | ✓ |
| Classification/sorting | — | ✓ | ✓ | ✓ | — |
| Creative brainstorming | ✓ | ✓ | ✓ | — | — |
| Legal/financial analysis | ✓ | ✓ | ✓ | ✓ | ✓ |
| Repurposing content | ✓ | ✓ | ✓ | — | ✓ |
| Building a reusable template | ✓ | ✓ | ✓ | ✓ | ✓ |

**Rule of thumb:** For any task you'll do more than once, use all 5 components to build a reusable template.

---

## Cheat Sheet

### Quick Prompt Builder

```
Role: You are a [specific expertise] with [experience level]
      specializing in [domain].

Task: [Action verb] + [specific object] + [measurable outcome]

Constraints:
- Length: [word count or item count]
- Tone: [formal/casual/direct/empathetic]
- Format: [table/bullets/JSON/prose]
- Scope: [what to include]
- Exclusions: [what to leave out]

Example:
Input: [sample input]
Output: [sample output matching your desired format]

Schema:
[exact structure of the response]
```

### Role Quick Reference

| Task Type | Good Role |
|-----------|-----------|
| Business writing | "Senior [function] professional" |
| Technical explanation | "[Field] specialist explaining to non-technical audience" |
| Data analysis | "Data analyst specializing in [domain]" |
| Customer communication | "Customer success manager at a [company type]" |
| Legal review | "Paralegal reviewing for non-legal stakeholders" |
| Content creation | "Content strategist for [industry]" |

### Constraint Quick Reference

| Need | Constraint to Add |
|------|------------------|
| Shorter output | "Under [X] words" or "Exactly [N] bullet points" |
| Professional tone | "Formal, professional tone. No contractions." |
| Casual tone | "Conversational, friendly tone. Use 'you' and 'we'." |
| Specific format | "Return as a markdown table" or "JSON object with fields..." |
| Accuracy | "Only use information from the provided text. Do not infer." |
| No buzzwords | "Do not use: innovative, synergy, leverage, disrupt" |

---

## Discussion Questions

1. **When is a role unnecessary?**
   → Simple tasks that don't need domain expertise: format conversion, basic math, simple lookups.

2. **Why does one-prompt-one-job produce better results?**
   → Each additional task dilutes the model's attention. The model has to predict tokens for multiple goals simultaneously, which increases variance and reduces quality for each individual task.

3. **Can too many constraints hurt?**
   → Yes. Over-constraining can conflict (e.g., "be concise" + "include all details") or waste tokens on instructions the model doesn't need. Match constraint density to task complexity.

4. **When should you use examples vs. just describing what you want?**
   → When the desired output format is complex, ambiguous, or hard to describe precisely. A single example can replace a paragraph of instructions.

5. **How do you decide between JSON schema and natural language schema?**
   → JSON: when the output will be parsed by code or another tool. Natural language: when a human will read it. JSON is more precise but less readable.

6. **What's the difference between a role and a constraint?**
   → Role sets the model's perspective and expertise (who it IS). Constraints set boundaries on what it produces (what it DOES). A role shapes the voice; constraints shape the output.

---

## Glossary

| Term | Definition |
|------|------------|
| **Zero-shot** | Prompting without examples; relying on the model's pre-trained knowledge |
| **Few-shot** | Including 1-5 examples in your prompt to guide the model's output format |
| **Output schema** | A defined structure for the response (JSON, table, sections, etc.) |
| **Prompt template** | A reusable prompt with placeholders for variable content |
| **Token** | The smallest unit a model processes; roughly 0.75 words or 4 characters |
| **Context window** | Total tokens the model can see (prompt + response combined) |
| **System message** | High-priority instructions that set model behavior/persona |
| **Temperature** | Controls randomness; 0 = deterministic, 2 = maximum randomness |
| **Chain-of-thought** | Asking the model to show its reasoning step by step |
| **Hallucination** | When the model generates confident but factually incorrect information |
| **One-prompt-one-job** | Rule: each prompt should handle a single, focused task |
| **Structured output** | Response formatted according to a defined schema (table, JSON, etc.) |

---

## Further Reading

- Anthropic Prompt Engineering Guide: https://docs.anthropic.com/claude/docs/prompt-engineering
- OpenAI Prompt Engineering: https://platform.openai.com/docs/guides/prompt-engineering
- "Prompt Engineering Guide" (DAIR.AI): https://www.promptingguide.ai
- Google AI Prompt Design: https://ai.google.dev/docs/prompt_best_practices

---

## Key Takeaway

Prompt design is not about writing longer instructions. It's about writing *structured* instructions. Each of the five components — Role, Task, Constraints, Examples, Schema — adds a layer of control. The more structure you provide, the less the model has to guess, and the more reliable the output becomes.

**Remember:**
- Role sets the voice, Task sets the direction
- Constraints prevent wandering, Examples show the pattern
- Schema guarantees format — one prompt = one job
- Simple tasks need 2-3 components; complex tasks benefit from all 5
- A reusable prompt template saves more time than any single prompt

---

*End of Week 2 Lesson — Continue to the Lab and Assignment for hands-on practice.*
