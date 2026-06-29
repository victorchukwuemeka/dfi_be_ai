# Lab: Your First Git-Controlled AI Project

## Objective
Set up a Git repository for an AI prompt library and practice the core workflow.

## Instructions

### Part 1: Setup
1. Open your terminal
2. Create a new directory: `mkdir ai-prompt-library && cd ai-prompt-library`
3. Init a Git repo: `git init`
4. Create a file `README.md` with a short description of your prompt library
5. Create a file `.gitignore` with these contents:
   ```
   .DS_Store
   *.log
   temp/
   ```

### Part 2: First Commit
1. Run `git status` and observe which files are tracked
2. Run `git add .` to stage everything
3. Run `git commit -m "Initial setup: README and .gitignore"`
4. Run `git log --oneline` to see your first commit

### Part 3: Iterate Like an AI Workflow
1. Create a file `prompts/summary-prompt.md`:

   ```markdown
   # Summary Prompt v1
   You are an executive assistant. Summarize the following text in 3 bullet points.
   ```

2. Stage and commit: `git add . && git commit -m "Add summary prompt v1"`
3. Edit the file to v2 — add a tone instruction and output format
4. Run `git diff` to see changes
5. Stage and commit: `git commit -m "Add tone control and bullet format"`
6. Edit the file to v3 — add a length constraint
7. Run `git log --oneline` and `git diff HEAD~1` to review history

### Part 4: Branching Experiment
1. Create a branch for an experimental approach: `git branch experimental`
2. Switch to it: `git switch experimental`
3. In `prompts/summary-prompt.md`, radically change the approach
4. Commit: `git commit -m "Experimental: chain-of-thought before summary"`
5. Switch back to main: `git switch main`
6. The file reverts to v3 — experiment is isolated

### Part 5: Merge (Optional)
1. If the experiment worked: `git merge experimental`
2. If not: delete the branch with `git branch -D experimental`

## Deliverables
- Screenshot or paste of `git log --oneline --graph` showing your commit history
- A brief reflection (2-3 sentences) on how this workflow applies to AI-assisted work
