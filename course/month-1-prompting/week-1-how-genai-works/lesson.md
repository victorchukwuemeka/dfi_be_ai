# Week 1: How GenAI Works in Plain Terms

## Core Concepts

### What is a Language Model?
A language model predicts the next word (token) in a sequence. It's trained on vast amounts of text and learns patterns — grammar, facts, reasoning styles, tone.

### Key Terms

**Tokens** — The smallest unit the model processes. A token is roughly 0.75 words. "Hello world" is ~2 tokens. Models have a maximum token limit (context window).

**Context Window** — The total tokens the model can "see" at once. Includes your prompt + the model's response. Larger windows (32K, 100K, 1M tokens) let you feed in entire documents.

**Sampling** — How the model chooses the next token. It assigns probabilities to all possible next tokens, then picks one. Key settings:
- **Temperature** (0-2): Low = predictable/safe, High = creative/random
- **Top-p** (nucleus sampling): Only consider tokens whose cumulative probability reaches p

### How Prompting Works
The model doesn't "understand" — it pattern-matches. Your prompt sets the context and the model continues the pattern. A well-structured prompt constrains the pattern to produce useful output.

## Practical Demonstration

Try this: give the same AI tool these two prompts and compare outputs:

**Vague prompt:**
"Write about productivity."

**Structured prompt:**
"You are a time management coach. Write a 3-paragraph memo to a team about improving meeting productivity. Use a direct, actionable tone. Include one specific technique per paragraph."

The second prompt controls: role, audience, format, length, tone, and structure.

## Key Takeaway
The model is a prediction engine. Your job is to constrain the prediction space with clear signals (role, task, format, examples) to get useful output every time.
