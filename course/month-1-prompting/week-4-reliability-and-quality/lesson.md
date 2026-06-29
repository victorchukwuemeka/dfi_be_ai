# Week 4: Reliability Tactics and Quality Rubric

## Reliability Tactics

### 1. Clarifying Questions
Before the model answers, ask it to identify what information is missing.

"Before answering, list any assumptions you're making about [topic]."

### 2. Validation Steps
Ask the model to verify its own output.

"After writing the analysis, add a 'Confidence' rating for each claim (high/medium/low) and note any claims you're unsure about."

### 3. Self-Checks
Have the model review its work.

"Review the above response. Identify any errors, omissions, or unsupported claims. List them."

### 4. Round-Trip Verification
Ask the same question in a different way and compare.

"Explain this concept in simple terms." then "Now explain it to an expert." — inconsistencies reveal misunderstanding.

### 5. Cite Sources
Require the model to reference where it got information.

"For each claim, cite the source document and paragraph number."

## Quality Rubric

Use this rubric to evaluate any AI output:

| Dimension | Excellent (3) | Adequate (2) | Poor (1) |
|-----------|--------------|--------------|----------|
| Accuracy | Facts are correct with no errors | Minor errors that don't affect meaning | Significant factual errors |
| Clarity | Easy to follow, well-structured | Understandable but messy | Confusing or contradictory |
| Tone | Appropriate for audience and context | Mostly appropriate | Wrong tone for context |
| Usefulness | Actionable, ready to use | Needs moderate editing | Requires complete rewrite |
| Completeness | Addresses all requirements | Addresses most requirements | Misses key requirements |

## Workflow: Prompt, Evaluate, Refine

1. **Draft prompt** — write it using the framework
2. **Run and evaluate** — score output using the rubric
3. **Identify gap** — which dimension scored lowest?
4. **Refine prompt** — add constraint or example targeting that gap
5. **Re-run** — compare scores
6. **Commit** — save winning prompt to version control

This is your core iteration loop. Every prompt improves through this cycle.
