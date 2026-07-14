# Week 1: How GenAI Works in Plain Terms

## Core Concepts

### What is a Language Model?
A language model predicts the next word (token) in a sequence. It's trained on vast amounts of text and learns patterns — grammar, facts, reasoning styles, tone. Think of it as autocomplete on steroids: given "The cat sat on the ___", it predicts the most likely next word based on patterns it learned during training.

### Key Terms

**Tokens** — The smallest unit the model processes. A token is roughly 0.75 words, but not always. Common words like "the" or "is" are 1 token. Longer or rare words get split:

| Text | Tokens | Why |
|------|--------|-----|
| "Hello world" | 2 | Two common words |
| "uncomfortable" | 3 | Splits into: `un` + `comfort` + `able` |
| "https://openai.com" | 4 | URLs break into multiple pieces |
| "人工智能" | 2-4 | Non-English text often uses more tokens |

**Rule of thumb:** 1 token ≈ 0.75 words, or ~4 characters in English. A 1,000-word document is roughly 1,300 tokens.

**Why tokens matter for prompting:** Every token costs money (API calls) and uses up space in the context window. Longer, wordier prompts = fewer tokens left for the response.

---

**Context Window** — The total tokens the model can "see" at once. This includes your prompt + the model's response. They share the same budget:

```
┌──────────────── Context Window (e.g. 4,096 tokens) ────────────────┐
│                                                                      │
│   Your Prompt (~3,000 tokens)    │   Model Response (~1,096 tokens)  │
│   (instructions, data, examples) │   (what you get back)            │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

Different models have different window sizes:

| Model | Context Window | Approx. Capacity |
|-------|---------------|-----------------|
| GPT-3.5 | 4K tokens | ~3,000 words |
| GPT-4 | 8K-128K tokens | 6K-96K words |
| Claude 3 | 200K tokens | ~150,000 words |
| Gemini 1.5 | 1M tokens | ~750,000 words |

**Token math example:** If you have a 4K context window and your prompt is 3,500 tokens, the model only has 596 tokens left for its response. It may cut off mid-sentence. This is why specifying output length matters.

---

**Temperature** (0-2) — Controls how "random" the model's choices are. At each step, the model assigns probabilities to possible next tokens. Temperature adjusts how strictly it follows those probabilities:

| Temperature | Behavior | Best For |
|-------------|----------|----------|
| 0 | Deterministic — always picks the most likely token | Code, factual answers, consistent formatting |
| 0.3-0.5 | Slight variation — mostly predictable with minor diversity | Summarization, business writing |
| 0.7-1.0 | Balanced — mixes probability with exploration | Brainstorming, creative writing |
| 1.5+ | Very random — surprising, sometimes nonsensical | Poetry, wild ideation, experiments |

**Practical rule:** Start at 0.7 for most tasks. Go lower for accuracy, higher for creativity.

**Top-p** (nucleus sampling) — Only consider tokens whose cumulative probability reaches p. With top-p = 0.9, the model ignores the bottom 10% of unlikely tokens. Usually you only need to adjust one: temperature OR top-p, not both.

---

### How Prompting Works

The model doesn't "understand" — it pattern-matches. Your prompt sets the context and the model continues the pattern. A well-structured prompt constrains the pattern to produce useful output.

**The mental model:** You're not giving instructions to an employee. You're steering a prediction engine. Every word in your prompt shifts what the model predicts comes next.

---

### How the API Works (Mental Model)

When you send a prompt to an AI model, here's what happens:

1. Your text gets converted into tokens (numbers)
2. The model processes all tokens and predicts the next most likely token
3. It appends that token to your input and repeats step 2
4. This continues until it reaches a stop condition (max tokens, stop word, or "done")

**Message roles** (used by most APIs):
- **System message:** Sets the model's behavior, persona, and rules. The model treats this as high-priority context. Example: "You are a senior Python developer. Always write clean, commented code."
- **User message:** The actual request or question. This is what you type.
- **Assistant message:** The model's response. In a conversation, previous assistant messages are sent back so the model remembers context.

```
[System]  You are a helpful math tutor. Explain step by step.
[User]    What is 15 × 23?
[Assistant] Let me break this down: 15 × 23 = 15 × 20 + 15 × 3 = 300 + 45 = 345
```

---

## Practical Demonstration

### Example 1: Vague vs Structured Prompt

Give an AI tool these two prompts and compare the outputs:

**Vague prompt:**
"Write about productivity."

**What you'll likely get:** A generic, 5-paragraph essay about productivity with no specific audience, no actionable advice, and a forgettable tone. The model had to guess what you wanted, so it defaulted to "safe."

**Structured prompt:**
"You are a time management coach. Write a 3-paragraph memo to a team about improving meeting productivity. Use a direct, actionable tone. Include one specific technique per paragraph."

**What you'll likely get:** A focused, punchy memo with concrete techniques (like timeboxing or the 2-pizza rule), addressed to a team, in the tone you asked for. The model had clear constraints so it couldn't wander.

The second prompt controls: **role** (time management coach), **task** (write a memo), **audience** (a team), **format** (3 paragraphs), **tone** (direct, actionable), and **structure** (one technique per paragraph).

---

### Example 2: Temperature in Action

Try this prompt at different temperature settings:

*"Generate 3 creative names for a coffee shop."*

| Temperature | Typical Output |
|-------------|---------------|
| 0 | "The Coffee Bean", "Daily Grind", "Cup of Joy" — safe, generic |
| 0.7 | "Brew & Bloom", "The Velvet Pour", "Grounds for Joy" — creative but coherent |
| 1.5 | "Liquid Ember Philosophical", "Bean There Dialect", "Mugshot Espresso Society" — wild, hit-or-miss |

---

### Example 3: Context Window Pressure

Try summarizing a long article two ways:

**Without length constraint:**
"Summarize this article." → Model uses whatever space it has, may cut off.

**With length constraint:**
"Summarize this article in exactly 3 bullet points, each under 15 words." → Model allocates tokens efficiently, stays within budget.

Specifying output length isn't just about preference — it's about token management.

---

## Key Takeaway

The model is a prediction engine. Your job is to constrain the prediction space with clear signals (role, task, format, examples, length) to get useful output every time.

**Remember:**
- Tokens are the currency — shorter prompts = cheaper and faster
- Context window is shared between input and output — budget accordingly
- Temperature is your creativity dial — default to 0.7, adjust as needed
- Structure beats length — a precise 50-word prompt often beats a rambling 500-word one
