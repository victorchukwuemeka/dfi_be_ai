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

---

## Common Pitfalls

### Pitfall 1: The "More Words = Better" Trap
**What happens:** Students write long, rambling prompts hoping more context helps.
**Reality:** Extra words dilute your signal. The model has to sift through noise.
**Fix:** Write your prompt, then cut it in half. Remove every word that doesn't change the output.

### Pitfall 2: Assuming the Model "Knows" You
**What happens:** "Fix this code" (no code provided, no language specified, no error described).
**Reality:** The model has zero context about your situation unless you provide it.
**Fix:** Always include: what you have, what you want, what's going wrong.

### Pitfall 3: Ignoring Output Format
**What happens:** Students ask for "analysis" and get a wall of text.
**Reality:** If you don't specify format, the model picks one (usually a paragraph).
**Fix:** Explicitly request: "Return as JSON", "Use bullet points", "Format as a table".

### Pitfall 4: Temperature Confusion
**What happens:** Students set temperature to 1.5 for factual queries, then complain about hallucinations.
**Reality:** High temperature = more randomness = more hallucination risk.
**Fix:** Match temperature to task. Factual = 0-0.3. Creative = 0.7-1.0.

### Pitfall 5: Forgetting Token Limits in Responses
**What happens:** "Summarize this 10-page document" → response cuts off at page 3.
**Reality:** The model ran out of output tokens.
**Fix:** Specify length: "Summarize in 200 words" or "Give me 5 bullet points".

---

## Interactive Exercises

### Exercise 1: Token Budget Challenge
**Goal:** Understand how prompts consume context window.

1. Open an AI tool with token counting (ChatGPT, Claude, etc.)
2. Start with this prompt: "Explain photosynthesis."
3. Note the token count.
4. Rewrite it as: "You are a biology teacher explaining to a 10-year-old. Explain photosynthesis in 3 sentences using a food analogy."
5. Compare token counts. Did the more specific prompt use more or fewer tokens?
6. Which output was more useful?

### Exercise 2: Temperature Ladder
**Goal:** See how temperature changes output.

Use this prompt at temperatures 0, 0.5, 1.0, 1.5:
"Write a product tagline for noise-canceling headphones."

Record:
- Which version is most professional?
- Which is most creative?
- Which would you actually use in marketing?

### Exercise 3: Prompt Autopsy
**Goal:** Learn from bad prompts.

Here's a vague prompt that failed:
"Write something about dogs."

Analyze it:
1. What's missing? (audience, format, tone, length, specific topic)
2. Rewrite it 3 different ways for 3 different audiences (kids, vets, pet store owners)
3. Test all 3. Compare the outputs.

### Exercise 4: Context Window Stress Test
**Goal:** Experience token limits firsthand.

1. Paste a long article (1,000+ words) into your AI tool
2. Ask: "Summarize this." → Note where it stops
3. Ask: "Summarize this in exactly 3 bullet points, each under 10 words." → Compare
4. Discuss: Why did the second version give you more control?

---

## Real-World Scenarios

### Scenario 1: Customer Support Bot
**Challenge:** Auto-reply to customer complaints.
**Bad prompt:** "Respond to this customer."
**Good prompt:** "You are a friendly customer support agent for a SaaS company. The customer is frustrated because their export feature stopped working. Acknowledge their frustration, apologize, and provide 2 troubleshooting steps. Keep response under 100 words. Tone: empathetic but professional."

### Scenario 2: Code Review
**Challenge:** Review Python code for issues.
**Bad prompt:** "Review this code."
**Good prompt:** "You are a senior Python developer. Review the following code for: bugs, performance issues, style violations. Return findings as a numbered list with severity (critical/warning/info). Code:\n```python\n[PASTE CODE]\n```"

### Scenario 3: Content Creation
**Challenge:** Write social media posts.
**Bad prompt:** "Write a tweet about our product."
**Good prompt:** "Write 3 tweet options for launching a new project management tool. Each tweet should: be under 280 characters, include one benefit (save time, reduce meetings, or improve accountability), use a casual tone, and end with a call-to-action. Vary the styles: one question, one stat, one story."

### Scenario 4: Data Extraction
**Challenge:** Pull structured data from unstructured text.
**Bad prompt:** "Extract info from this email."
**Good prompt:** "Extract the following fields from this email and return as JSON: sender_name, company, meeting_date, meeting_time, agenda_items (array). If a field is missing, set it to null. Email:\n[PASTE EMAIL]"

---

## Quick Reference Cheat Sheet

### Prompt Building Blocks

| Component | Purpose | Example |
|-----------|---------|---------|
| **Role** | Sets expertise/perspective | "You are a financial analyst" |
| **Task** | Defines what to do | "Analyze this quarterly report" |
| **Format** | Controls output structure | "Return as a markdown table" |
| **Constraints** | Sets boundaries | "Under 200 words" |
| **Examples** | Shows desired pattern | "Like this: [example]" |
| **Tone** | Sets communication style | "Formal and professional" |
| **Audience** | Who it's for | "Explain to a non-technical manager" |

### Temperature Quick Guide

| Task Type | Temperature | Why |
|-----------|-------------|-----|
| Factual Q&A | 0-0.2 | Accuracy matters most |
| Code generation | 0-0.3 | Correctness over creativity |
| Summarization | 0.3-0.5 | Fidelity to source |
| Business writing | 0.5-0.7 | Balance of formality and flow |
| Creative writing | 0.7-1.0 | Exploration and variety |
| Brainstorming | 0.8-1.2 | Maximum idea diversity |

### Token Estimation Formula

```
English words × 1.3 = approximate tokens
Characters ÷ 4 = approximate tokens
```

**Examples:**
- 100 words ≈ 130 tokens
- 500 words ≈ 650 tokens
- 1,000 words ≈ 1,300 tokens

---

## Discussion Questions

1. **If a model predicts the next word, how can it write code it's never seen before?**
   → It's not "writing" — it's predicting patterns it learned from billions of code examples during training.

2. **Why might two identical prompts give different results?**
   → Temperature, different model versions, server load, or randomness in sampling. Even at temperature 0, some systems add micro-variation.

3. **When would you use a system message vs. just putting everything in the user message?**
   → System messages persist across conversation turns. Use them for rules/persona that should always apply. User messages are one-time requests.

4. **What happens when you hit the context window limit mid-conversation?**
   → The model "forgets" the earliest messages. Solutions: summarize history, start new conversation, or use models with larger context windows.

5. **Can a model know when it's wrong?**
   → Generally no. It predicts likely tokens, not "true" tokens. It may express uncertainty ("I'm not sure, but...") if trained to, but it doesn't actually know.

---

## Hands-On Lab Ideas

### Lab 1: Build a Prompt Library
Create 5 reusable prompt templates for common tasks:
1. Email writer
2. Code reviewer
3. Meeting summarizer
4. Data extractor
5. Creative brainstormer

For each, include: role, task, format, constraints, and one example.

### Lab 2: A/B Test Your Prompts
Pick a task. Write two versions of the prompt (vague vs. structured). Test both 3 times. Score each output on:
- Accuracy (0-5)
- Usefulness (0-5)
- Conciseness (0-5)

Calculate average scores. Which prompt won?

### Lab 3: Token Optimization Challenge
Take this bloated prompt and reduce its token count by 50% while keeping the output quality:

> "I would like you to please help me by writing a professional and well-crafted email that is directed toward a potential business partner who might be interested in collaborating with our company on a joint marketing initiative that we believe could be mutually beneficial for both parties involved. The email should be friendly but professional in tone and should clearly explain what we are proposing and why it would be advantageous for them to work with us on this particular project."

### Lab 4: Error Recovery
Use a deliberately bad prompt and iteratively improve it:
1. Start with: "Make a thing."
2. Note the useless output.
3. Add one constraint. Re-test.
4. Keep adding constraints until the output is what you wanted.
5. Document what each constraint changed.

---

## Glossary

| Term | Definition |
|------|------------|
| **Token** | The smallest unit a model processes; roughly 0.75 words or 4 characters |
| **Context Window** | Total tokens the model can see (prompt + response combined) |
| **Temperature** | Controls randomness; 0 = deterministic, 2 = maximum randomness |
| **Top-p** | Filters tokens by cumulative probability threshold |
| **System Message** | High-priority instructions that set model behavior/persona |
| **Hallucination** | When the model generates confident but factually incorrect information |
| **Prompt** | The text input you send to the model to guide its output |
| **Inference** | The act of the model generating a response from a prompt |
| **Fine-tuning** | Additional training on specific data to customize model behavior |
| **Few-shot** | Including examples in your prompt to guide the model's output format |
| **Zero-shot** | Prompting without examples; relying on the model's pre-trained knowledge |
| **API** | Application Programming Interface; how you programmatically talk to models |

---

## Further Reading

- OpenAI Tokenizer: https://platform.openai.com/tokenizer
- Anthropic Prompt Engineering Guide: https://docs.anthropic.com/claude/docs/prompt-engineering
- Google AI Prompt Design: https://ai.google.dev/docs/prompt_best_practices
- "Prompt Engineering Guide" (DAIR.AI): https://www.promptingguide.ai

---

*End of Week 1 Lesson — Continue to the Lab and Assignment for hands-on practice.*
