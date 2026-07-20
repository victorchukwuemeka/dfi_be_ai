# Lab: Build a Structured Prompt

## Objective

Practice writing prompts using the Role-Task-Constraints-Examples-Output Schema framework. Build the skill of identifying what each component adds to a prompt.

## Instructions

### Part 1: Component Identification

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
Status: "Sprint velocity down 15%. Two engineers out sick.
Client demo moved to Friday. Design team delivered wireframes."

Status: "Design review complete. Three feedback items from
leadership. Budget approved for Q3 hiring. API migration
delayed 2 weeks due to vendor dependency."
```

**For each prompt above, label:**
- Role: (what text?)
- Task: (what text?)
- Constraints: (what text?)
- Example: (what text?)
- Schema: (what text?)

**Then run both prompts and compare the outputs.** Did the example influence the output format?

---

### Part 2: Rewrite a Weak Prompt

Take this weak prompt and rewrite it using all 5 components:

**Weak prompt:** "Tell me about marketing."

**Your rewrite should include:**
- A specific role (who is the AI acting as?)
- A specific task (what exactly should it produce?)
- At least 2 constraints (length, tone, format, or scope)
- 1 example showing the desired output style
- An output schema (how should the response be structured?)

**Write your rewrite here:**

---

**Run both prompts and compare:**

| Criterion | Weak Prompt | Your Rewrite |
|-----------|------------|--------------|
| Usefulness (1-5) | | |
| Specificity (1-5) | | |
| Actionability (1-5) | | |
| Format match (1-5) | | |

---

### Part 3: Prompt A/B Test

Pick a task relevant to your work (summarizing a document, drafting an email, analyzing data, brainstorming ideas, etc.).

**Version A — Minimal prompt (Role + Task only):**
```
[Your role]
[Your task]
```

**Version B — Full prompt (all 5 components):**
```
Role: [specific role]
Task: [specific task]
Constraints: [at least 2 constraints]
Example: [1 example showing desired output]
Schema: [output structure]
```

**Run both on the same input, 3 times each.** Record all outputs.

**Compare outputs:**

| Criterion | Version A (avg of 3) | Version B (avg of 3) |
|-----------|---------------------|---------------------|
| Accuracy (1-5) | | |
| Usefulness (1-5) | | |
| Consistency across runs (1-5) | | |
| Format match (1-5) | | |
| Time to get usable result | | |

**Which version won? Why?**

---

### Part 4: Constraint Experimentation

Take one prompt and run it with different constraint combinations to see how each constraint shapes the output.

**Base prompt:** "You are a business analyst. Analyze this sales data and identify trends."

**Test 4 variations:**

| Version | Added Constraint | How Did Output Change? |
|---------|-----------------|----------------------|
| V1 | + "Under 150 words" | |
| V2 | V1 + "Use a table format" | |
| V3 | V2 + "Focus only on revenue and margin trends" | |
| V4 | V3 + "Do not mention absolute numbers, only percentages" | |

**Observation:** Which constraint had the biggest impact on usability? Why?

---

### Part 5: Build a Reusable Template

Choose a task you do regularly at work. Build a reusable prompt template with all 5 components, using `[placeholder]` for variable content.

**Template structure:**

```
Role: You are a [specialization] with expertise in [domain].

Task: [action] the following [content type]:
[content]

Constraints:
- [length constraint]
- [tone constraint]
- [format constraint]

Example:
Input: [sample input]
Output: [sample output matching your desired format]

Schema:
[output structure]
```

**Fill in your template for a task you'll actually use:**

---

**Test your template with 3 different inputs.** Does it produce consistent, usable output each time?

---

## Deliverables

1. **Part 1:** Component labels for the sample prompt + output comparison
2. **Part 2:** Your rewritten prompt + comparison table
3. **Part 3:** Both prompt versions + all 6 outputs + comparison table + your conclusion
4. **Part 4:** The 4 variation outputs + your observation about which constraint mattered most
5. **Part 5:** Your completed template + results from 3 test runs

## Self-Check

Before submitting, verify:
- [ ] Each prompt in Parts 1-3 uses at least 3 of the 5 components
- [ ] Part 3 includes outputs from both versions (not just the prompts)
- [ ] Part 5 template uses `[placeholder]` syntax for variable content
- [ ] Part 5 template was tested with 3 different inputs
- [ ] All comparison tables are filled in with specific observations
