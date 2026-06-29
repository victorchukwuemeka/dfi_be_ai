# Week 9: Research Workflow — Scoping, Question Refinement, and Verification

## The AI-Assisted Research Workflow

### Step 1: Scope
Before gathering information, define what you need.

Prompt:
```
I need to research [topic]. Help me scope this by:
1. Breaking the topic into 3-5 sub-questions
2. Ranking them by importance
3. Identifying what type of information each needs (fact, opinion, trend, data)
```

### Step 2: Question Refinement
Bad questions get bad answers. Iterate on your research questions.

Prompt:
```
Here is my research question: [question]
Critique it:
1. Is it specific enough?
2. Is it answerable?
3. Is it neutral (not leading)?
4. Suggest 2 alternative phrasings.
```

### Step 3: Gather and Synthesize
Use AI to process multiple sources (as covered in Week 6).

### Step 4: Verify
This is the most important step. AI can hallucinate confidently.

Verification prompt:
```
For each claim in the above research, identify:
1. Is this common knowledge? (likely reliable)
2. Does it cite a specific source? (verifiable)
3. Could it be a plausible-sounding fabrication? (high risk)
4. What would you fact-check first?
```

### Step 5: Document
Save your research with confidence ratings.

## Verification Techniques

### Cross-Check Prompt
```
I'm going to ask you the same question 3 different ways. Answer each, then compare for consistency.
Question 1: [phrasing A]
Question 2: [phrasing B]
Question 3: [phrasing C]
```

### Source Awareness Prompt
```
Only answer using information from the sources I provide. If the answer isn't in the sources, say "I don't have information on that."
```

### Uncertainty Prompt
```
For each statement in your answer, rate your confidence (high/medium/low) based on:
- How common/settled is this knowledge?
- Would experts disagree?
- Is this an area of active development?
```

## Research Documentation Template
```
Research Topic:
Date:
Key Questions:
Sources Used:
Findings (with confidence ratings):
Gaps/Uncertainties:
Next Steps:
```
