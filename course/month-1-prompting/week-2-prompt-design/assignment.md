# Assignment: Prompt Design Portfolio

## Task

Create 5 structured prompts for real tasks you face in your work (or realistic simulated tasks). Each prompt should use the 5-component framework. Run each prompt, evaluate the output, and document one refinement you'd make.

## Requirements

### For Each Prompt, You Must:

1. **Label all 5 components** (Role, Task, Constraints, Examples, Schema) — or explicitly note which you chose to omit and why
2. **Use a different task type** for each prompt (e.g., don't write 5 email-drafting prompts)
3. **Run the prompt** and capture the actual output
4. **Evaluate the output** using the criteria below
5. **Write one refinement** — what specific change would you make to improve the output, and why?

### Component Minimums

Each prompt must include at least 3 of the 5 components. At least 2 of your 5 prompts must use all 5 components.

| Prompt | Components Used | Task Type |
|--------|----------------|-----------|
| Prompt 1 | | |
| Prompt 2 | | |
| Prompt 3 | | |
| Prompt 4 | | |
| Prompt 5 | | |

## Deliverable

A document (Markdown, Google Doc, or Word) containing:

### For Each Prompt:

**1. The Prompt (copy-paste ready)**
```
[Your complete prompt with components labeled]
```

**2. Task Description**
- What real work task does this prompt solve?
- Who would use this prompt?

**3. Output**
[Paste the actual output from running the prompt]

**4. Evaluation**

| Criterion | Score (1-5) | Notes |
|-----------|:-----------:|-------|
| Accuracy | | Is the information correct? |
| Usefulness | | Would you actually use this? |
| Format match | | Does it match your schema? |
| Tone | | Is it appropriate for the audience? |
| Completeness | | Does it address all requirements? |

**5. Refinement**
- What would you change in the prompt?
- Why? (which rubric dimension does it target?)
- What do you expect to improve?

---

## Example Topics by Task Type

Choose from these or use your own. Aim for variety:

### Writing Tasks
- Draft a project status update for your manager
- Write a client-facing email declining a scope change
- Create a 1-page brief from a longer document
- Draft a meeting agenda for a cross-functional sync

### Analysis Tasks
- Analyze survey responses and identify top themes
- Compare two vendor proposals across key criteria
- Summarize a long email thread into action items
- Review a document and flag risks or gaps

### Extraction Tasks
- Pull key dates, names, and commitments from meeting notes
- Extract structured data from a messy report
- Convert a narrative paragraph into a table

### Creative Tasks
- Generate 10 blog post titles on a specific topic
- Brainstorm 5 campaign taglines with different angles
- Rewrite a technical paragraph for a non-technical audience

### Communication Tasks
- Draft talking points for a presentation
- Write a feedback email (positive or constructive)
- Create an FAQ document from a product description

---

## Example of a Completed Prompt Entry

### Prompt: Analyze Customer Feedback

**The Prompt:**
```
Role: You are a customer insights analyst at a SaaS company.
Task: Analyze the following customer feedback responses and identify
the top 3 themes, with frequency counts.
Constraints: Use plain language. Max 250 words. Only identify themes
that appear in 3+ responses.
Example:
Input: ["Love the product but the onboarding is confusing",
        "Great features, onboarding was hard though",
        "Onboarding needs work, otherwise amazing"]
Output:
1. Onboarding difficulty (3 mentions) — customers find the initial
   setup process confusing or hard to navigate
2. Product quality (2 mentions) — positive sentiment about core features

Input:
[paste your feedback data here]
Schema:
| Theme | Frequency | Representative Quotes | Sentiment |
```

**Task Description:**
I work with customer feedback data monthly. This prompt helps me quickly identify themes without manually reading through hundreds of responses.

**Output:**
[Paste actual output here]

**Evaluation:**

| Criterion | Score | Notes |
|-----------|:-----:|-------|
| Accuracy | 4 | Themes were correct, frequency counts accurate |
| Usefulness | 5 | Ready to share with the product team |
| Format match | 3 | Got a table but it included an extra "Priority" column I didn't ask for |
| Tone | 4 | Professional and clear |
| Completeness | 4 | Covered the top themes, missed one minor one |

**Refinement:**
- Change: Add "Do not add columns or fields beyond the schema provided" as a constraint
- Targets: Format match (scored 3)
- Expected improvement: The table should match my schema exactly, without extra columns

---

## Grading Criteria

| Criterion | Points | Description |
|-----------|:------:|-------------|
| 5 prompts submitted | 20 | One point per prompt |
| Components labeled | 20 | Each prompt has components clearly identified |
| Task variety | 10 | Different task types across the 5 prompts |
| Output included | 15 | Actual output captured for each prompt |
| Evaluation quality | 15 | Specific, honest scoring with notes (not generic) |
| Refinement quality | 15 | Specific, actionable changes targeting a rubric dimension |
| Template usage | 5 | At least 2 prompts use all 5 components |

**Total: 100 points**

---

## Submission Checklist

Before submitting, verify:

- [ ] 5 prompts submitted with components labeled
- [ ] Each prompt targets a different task type
- [ ] Actual output included for each prompt
- [ ] Evaluation table filled in with scores and notes
- [ ] Refinement note for each prompt specifies what to change and why
- [ ] At least 2 prompts use all 5 components
- [ ] All prompts are copy-paste ready (not abbreviated or truncated)
