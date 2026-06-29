# Week 7: Structured Outputs — Tables, Comparisons, Scoring, and Action Plans

## Why Structured Outputs Matter
Structured outputs are parseable, scannable, and actionable. They reduce editing time and make AI outputs directly usable in documents, spreadsheets, and presentations.

## Table Generation

Prompt for a comparison table:
```
Create a comparison table with these columns:
| Feature | Tool A | Tool B | Tool C |
|---|---|---|---|
| Price | | | |
| Ease of use | | | |
| Key strength | | | |

Fill in based on this research: [research notes]
```

## Scoring and Ranking

```
Score each option on a scale of 1-5 for these criteria:
- Cost efficiency
- Implementation time
- Team capacity
- Risk level

Return a ranked list with total scores.

Options:
1. [option A]
2. [option B]
...
```

## Decision Frameworks

### Pros/Cons
```
List pros and cons for [decision]. Format:
| Pro | Con |
|---|---|
| [pro] | [counter-argument or con] |
```

### Action Plan with Owners
```
Create an action plan for [goal]:
| Action | Owner | Deadline | Dependencies | Status |
|---|---|---|---|---|
| [task] | [person] | [date] | [dependency] | [not started/in progress/done] |
```

### Risk Matrix
```
For [project], identify risks:
| Risk | Likelihood (1-5) | Impact (1-5) | Score | Mitigation |
|---|---|---|---|---|
| [risk] | [score] | [score] | [product] | [strategy] |
```

## Iterating on Structure
If the first table is too dense: "Simplify to 3 columns only."
If rankings are unclear: "Add a rationale column explaining each score."
If action items are vague: "Make each action start with a verb."

## Pro Tip
Design your output schema before writing the prompt. The schema is your specification — the prompt is how you communicate it.
