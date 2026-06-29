# Week 8: Collaboration — Review Loops, Versioning, and Human Edits

## The Human-AI Collaboration Loop

AI is not a replacement — it's a collaborator. The best results come from iterative human-AI interaction.

### The Loop
1. **Draft** — AI produces first version from your prompt
2. **Review** — you evaluate against rubric
3. **Edit** — you make direct changes OR refine the prompt
4. **Repeat** — until quality threshold is met

## Versioning with Git for Collaborative Writing

### Branch Strategy for Writing
```
main          — final, approved versions only
drafts/       — work-in-progress
experiments/  — alternate approaches
reviews/      — versions shared for feedback
```

### Workflow
1. Create a branch for your draft: `git checkout -b drafts/memo-v1`
2. Write prompt and generate output → save to file
3. Commit: `git add memo.md && git commit -m "AI draft: Q3 planning memo"`
4. Edit manually or regenerate with refined prompt
5. Commit again: `git commit -m "Human edit: shortened intro, added data"`
6. When approved: `git checkout main && git merge drafts/memo-v1`

## Prompt Patterns for Collaboration

### Requesting Feedback from AI
```
Review this document. Identify:
1. Three things that work well
2. Three things that could be clearer
3. One structural change that would improve flow
```

### Comparing Versions
```
Compare these two versions of the same document.
Version A: [text]
Version B: [text]
Which is stronger? Why? Suggest a hybrid.
```

### Incorporating Edits
```
Here are my edits to your draft: [edits]
Generalize from these edits — what patterns should you follow next time?
Update your writing guidelines accordingly.
```

## Review Checklist for Human Edits
- [ ] Does the intro state the purpose clearly?
- [ ] Is each paragraph about one idea?
- [ ] Are claims supported?
- [ ] Is the tone appropriate for the audience?
- [ ] Is the call to action clear?
- [ ] Can any sentence be shortened?
