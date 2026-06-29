# Week 2: Prompt Design — Role, Task, Constraints, Examples, Output Schema

## The Prompt Design Framework

Great prompts have five components. Not every prompt needs all five, but the more you include, the more reliable the output.

### 1. Role
Who is the AI acting as?

"You are a senior data analyst..."
"You are a copywriter for a B2B SaaS company..."
"You are a career coach..."

Why it works: Role primes the model for domain, tone, and expertise level.

### 2. Task
What exactly should the AI do? Be specific.

Bad: "Analyze this data."
Good: "Analyze this quarterly sales data and identify the top 3 trends, including percentage changes."

### 3. Constraints
Boundaries that shape the output.

- Length: "Exactly 5 bullet points" or "Under 200 words"
- Tone: "Formal", "Conversational", "Urgent"
- Format: "No markdown", "Use a table"
- Content: "Only include facts from the provided document"

### 4. Examples (Few-Shot)
Showing is better than telling. Give 1-3 examples.

```
Tone: Professional but approachable
Example of good tone: "We recommend reviewing your coverage annually."
Example of bad tone: "You should def check your policy, lol."
Now rewrite this sentence: "Insurance is complicated."
```

### 5. Output Schema
Tell the AI exactly how to format the response.

```
Return a JSON object:
{
  "summary": "...",
  "key_points": ["...", "..."],
  "action_items": ["...", "..."]
}
```

Or simpler:

```
Format your response as:
- Problem: [one sentence]
- Cause: [one sentence]
- Solution: [one sentence]
```

## Putting It All Together

```
Role: You are a financial analyst.
Task: Analyze this company's Q2 earnings call transcript.
Constraints: Use plain language suitable for non-finance readers. Max 200 words.
Output schema:
- Key metric: [number] — [what it means]
- Risk: [one sentence]
- Outlook: [one sentence]

[transcript]
```

## Common Mistakes
- Vague role ("You are an expert" — in what?)
- No constraints (you'll get rambling output)
- Mixing tasks in one prompt (one prompt = one job)
- Not specifying format (waste time reformatting)
