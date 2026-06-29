# Week 11: Automation Basics — Reusable Prompt Chains and SOPs

## What is Prompt Automation?
Turning a one-time prompt into a repeatable, reliable process. The goal: consistent results with minimal re-prompting.

## Prompt Chains
A prompt chain is a sequence of prompts where the output of one feeds into the next.

### Chain Example: Content Creation
```
Step 1: "Generate 5 topic ideas based on [source material]"
Step 2: "Expand idea #3 into an outline with 4 sections"
Step 3: "Write section 1 of the outline in 200 words"
Step 4: "Write a 3-sentence summary of the full piece"
```

### Why Chains Work
- Each step has a focused, simple task
- Quality issues are isolated to one step
- You can intervene between steps

## Standard Operating Procedures (SOPs)

Document your AI workflows so they're repeatable by others (or by your future self).

### SOP Template
```
## [Process Name]

### When to Use
[One-line description of when this SOP applies]

### Input Needed
- [Required input 1]
- [Required input 2]

### Step 1: [Name]
Prompt:
```
[exact prompt with [placeholders]]
```
Expected output: [description]
Quality check: [what to verify]

### Step 2: [Name]
...
```

### Example SOP: Email Triage
```
## Email Triage

### When to Use
Inbox has 20+ unread emails and you need to prioritize.

### Input
Paste the full email thread.

### Step 1: Classify
Prompt:
Classify this email as: urgent action, scheduled action, FYI, delegate, or archive.
Confidence: high/medium/low.

### Step 2: Draft Response (if urgent)
Prompt:
Draft a response to this email. Tone: professional. Length: 3 sentences max.
End with a clear next step.

### Step 3: Archive or Assign
Based on classification, file or forward.
```

## Building Your Prompt Chain Library

Save reusable chains as:
- Markdown files in a `chains/` folder
- With clear input/output specs
- Version-controlled in Git

## Automation Ethics
- Never automate decisions that require human judgment
- Always review AI outputs before sending
- Document what the AI did and what you did
- Understand the limitations (hallucination, bias, stale knowledge)
