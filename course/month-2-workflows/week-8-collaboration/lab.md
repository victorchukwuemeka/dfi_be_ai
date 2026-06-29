# Lab: Collaborative Review and Versioning

## Objective
Practice the human-AI review loop and use Git to track versions.

## Instructions

### Part 1: Generate and Review
1. Generate a document with AI (500+ words on any topic)
2. Use a review prompt to get AI feedback on its own output
3. Make 3 human edits to the document

### Part 2: Git Workflow
1. `git init` in a new folder
2. Save the AI draft: `git add . && git commit -m "AI draft v1"`
3. Save the AI feedback: `git add . && git commit -m "AI self-review"`
4. Apply your edits: `git add . && git commit -m "Human edits applied"`
5. Run `git log --oneline`

### Part 3: Branch Experiment
1. Create a branch: `git checkout -b alternate-approach`
2. Generate a completely different version of the document
3. Commit: `git commit -m "Alternate: narrative style instead of bullet format"`
4. Switch between branches and compare

## Deliverables
- All 3 versions (AI draft, AI review, human edit)
- `git log --oneline --graph` output
- Which version was stronger — the original or the alternate?
