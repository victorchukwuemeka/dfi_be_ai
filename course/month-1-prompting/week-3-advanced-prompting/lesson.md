# Week 3: Advanced Prompting — Few-Shot Patterns and Controlled Outputs

## Few-Shot Prompting

Give the model examples before asking it to perform. This is the most reliable way to get consistent formatting and reasoning.

### Zero-Shot (no examples)
"Classify this customer review as positive, negative, or neutral."

### Few-Shot (with examples)
```
Classify each review as positive, negative, or neutral.

Review: "This product changed my life!"
Classification: Positive

Review: "Arrived broken. Terrible support."
Classification: Negative

Review: "It works as expected."
Classification: Neutral

Review: "I've been using it for a month. It's okay for the price."
Classification:
```

### Why Few-Shot Works
- Shows the model your definition of each category
- Demonstrates edge cases
- Sets a consistent output format

## Chain-of-Thought (CoT) Prompting

Ask the model to reason step by step before answering. Dramatically improves accuracy on reasoning tasks.

Without CoT:
"A bat and a ball cost $1.10. The bat costs $1.00 more than the ball. How much is the ball?" → Often gets "10 cents" (wrong)

With CoT:
"Let's think step by step. The bat costs $1.00 more than the ball. If the ball costs X, then the bat costs X + $1.00. Total: X + (X + $1.00) = $1.10. So 2X = $0.10. X = $0.05." → $0.05 (correct)

## Controlled Outputs

### Structured Data Extraction
```
Extract the following fields from the email below as JSON:
- sender_name
- request_type (meeting_request, question, status_update, other)
- urgency (high, medium, low)
- deadline (if mentioned, else null)

Email: [email text]
```

### Format Enforcement
```
Respond ONLY with a bullet list. No paragraphs, no introductions, no conclusions.
```

### Negative Constraints
```
Do not use the words "innovative," "synergy," or "leverage."
Do not mention competitors by name.
```

## Combining Techniques

```
You are a legal analyst. (role)
Review this contract clause and identify risks. (task)
Use chain-of-thought: first list potential issues, then rate each as high/medium/low. (CoT)
Return a table with columns: Clause Section | Risk | Rating | Suggested Revision (schema)
Do not include legal advice disclaimers. (negative constraint)
```
