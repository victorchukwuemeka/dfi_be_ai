# Lab: Few-Shot and Chain-of-Thought

## Objective
Compare zero-shot vs few-shot vs chain-of-thought prompting.

## Instructions

### Part 1: Classification Task
Create a classification prompt for a task relevant to your work (e.g., classify emails, prioritize tasks, categorize feedback).

1. Write a zero-shot version
2. Write a few-shot version with 3 examples
3. Run both on the same 5 inputs
4. Compare accuracy and consistency

### Part 2: Reasoning Task
1. Give the model a logic puzzle or analysis question without CoT
2. Give the same question with "Let's think step by step" or "First, list the relevant facts, then reason through each"
3. Compare outputs

### Part 3: Schema Enforcement
Prompt: "Extract name, date, amount, and category from this receipt."

1. Run without schema specification
2. Run with: "Return JSON: {name, date, amount, category}"
3. Compare parseability

## Deliverables
- All prompts and outputs for Parts 1-3
- Which technique gave the biggest improvement for your use case?
