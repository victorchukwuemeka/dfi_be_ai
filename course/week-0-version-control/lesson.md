# Week 0: Version Control with Git

## Why Version Control Matters for AI-Assisted Work

When working with AI tools, you generate many iterations of prompts, outputs, and refinements. Without version control, you end up with files named `final_v2_really_final_approved.md` and no way to remember what changed between them. Version control solves this.

It helps you:
- **Track** what changed between iterations — see exactly what you modified
- **Revert** when an AI output makes things worse — undo with one command
- **Document** your thought process — commit messages explain why you made each change
- **Experiment** safely — branches let you try wild ideas without breaking working code
- **Collaborate** with others on prompt libraries and workflows — merge changes from teammates
- **Keep a history** of what worked and what didn't — look back at successful approaches

### Example: The AI Iteration Problem

Without Git:
```
prompts/
├── summary-final.md
├── summary-final-2.md
├── summary-v3-USE-THIS.md
├── summary-v4-tone-fix.md
├── summary-working.txt
└── summary-actually-this-one.md
```

With Git:
```
$ git log --oneline
a1b2c3d Fix: make summary more concise for executives
d4e5f6a Add tone constraint (formal, not casual)
f7g8h9a Initial summary prompt
```

You can see the exact change in each commit and revert to any previous state instantly.

---

## Core Concepts

### The Three States of Git

Every file in your repository is always in one of three states:

1. **Modified** — you changed the file but haven't saved it to your repository yet
2. **Staged** — you marked the modified file to be included in your next commit
3. **Committed** — the change is safely stored in your Git history

The workflow is: **Modify → Stage → Commit**. Repeat.

### The Git Data Flow

```
Working Directory    Staging Area    .git Directory (Repository)
    (your files)      (index)         (commit history)
         |                |                  |
    edit file  ──→  git add  ──→  git commit
         |                |                  |
    git checkout ◄── git restore ◄── git restore --staged
```

---

## Git Basics — Every Command You Need Daily

### 1. `git init` — Start Tracking

```bash
git init
```

Creates a hidden `.git` folder in your project. This is where Git stores all its history. Run this once per project, at the beginning.

```bash
# After git init, your project structure looks like:
my-project/
├── .git/          # Git's database (don't touch this manually)
├── README.md      # your files
└── prompts/
```

### 2. `git status` — See What's Happening

```bash
git status
```

The most frequently used command. It shows:
- Which files are **untracked** (Git doesn't know about them yet)
- Which files are **modified** (changed but not staged)
- Which files are **staged** (ready to be committed)
- Which branch you're on

Example output:
```
On branch main
Untracked files:
  prompts/summary.md

Changes not staged for commit:
  modified: README.md

Changes to be committed:
  new file: .gitignore
```

### 3. `git add` — Stage Changes

```bash
git add prompts/summary.md      # stage a specific file
git add .                       # stage all changes in current directory
git add *.md                    # stage all .md files
```

Staging is like packing a suitcase: you decide which changes go into the next commit.

### 4. `git commit` — Save a Snapshot

```bash
git commit -m "Add summary prompt with tone control"
```

Creates a permanent snapshot of your staged changes. Think of commits as checkpoints in a video game — you can always go back.

**Commit message conventions:**
- Present tense: "Add feature" not "Added feature"
- Short first line (under 50 chars)
- More detail after a blank line if needed

Good examples:
```
Add prompt template for executive summaries
Fix: constrain output to exactly 3 bullet points
Refine tone from casual to formal in email prompt
Remove deprecated brainstorming prompt
```

Bad examples:
```
Update file
changes
stuff
```

### 5. `git log` — Browse History

```bash
git log                    # full history
git log --oneline          # one line per commit (compact)
git log --oneline --graph  # show branch structure
git log --oneline -5       # last 5 commits
git log --author="name"    # filter by author
```

Example output:
```
$ git log --oneline --graph
* a1b2c3d Fix: make summary more concise for executives
* d4e5f6a Add tone constraint (formal, not casual)
* f7g8h9a Initial summary prompt
```

### 6. `git diff` — See Exact Changes

```bash
git diff                     # unstaged changes (working directory vs staged)
git diff --staged            # staged changes (staged vs last commit)
git diff a1b2c3d d4e5f6a     # compare two commits
git diff HEAD~1              # compare with one commit ago
```

This shows line-by-line what changed. Added lines are green with `+`, removed lines are red with `-`.

### 7. `git show` — See a Specific Commit

```bash
git show a1b2c3d         # show commit details and diff
git show HEAD            # show the most recent commit
git show HEAD~1          # show the commit before HEAD
```

---

## Undoing Things

### Unstage a File (keep changes)

```bash
git restore --staged prompts/summary.md
```

If you accidentally staged a file, this unstages it without losing your edits.

### Discard Unstaged Changes

```bash
git restore prompts/summary.md
```

Reverts the file back to the last committed version. **Warning: this deletes your edits permanently.**

### Amend the Last Commit

```bash
git commit --amend -m "Better commit message"
```

If you forgot to include a file or want to fix the commit message. Only use this for commits you haven't shared yet.

### Revert a Commit (safe undo)

```bash
git revert a1b2c3d
```

Creates a NEW commit that undoes the changes from commit `a1b2c3d`. This is the safe way to undo because it preserves history.

### Reset (dangerous undo)

```bash
git reset --soft HEAD~1    # undo commit, keep changes staged
git reset --mixed HEAD~1   # undo commit, keep changes unstaged (default)
git reset --hard HEAD~1    # undo commit AND discard changes (DANGER)
```

**Never use `--hard` if you're not sure.** Once discarded, changes are gone.

---

## `.gitignore` — What NOT to Track

Some files should never be committed: secrets, temporary files, system files, large binaries, AI outputs containing sensitive data.

Create a `.gitignore` file in your project root:

```
# System files
.DS_Store
Thumbs.db

# Logs and temp
*.log
*.tmp
temp/

# Sensitive
.env
config/keys.json
*.pem

# AI generated outputs (if you don't want to track them)
outputs/
*.generated.*

# Large files
*.mp4
*.zip
node_modules/
```

Use wildcards:
- `*.log` — all files ending in `.log`
- `temp/` — entire temp directory
- `!important.log` — EXCEPT this file (override)

---

## Branching — Safe Experimentation

Branches let you work on multiple versions simultaneously. Your main branch (`main` or `master`) stays clean while you experiment.

### Creating and Switching Branches

```bash
# Create a new branch
git branch experimental-tone

# Switch to it
git switch experimental-tone

# Create AND switch in one command
git switch -c experimental-tone
```

Older style (still works):
```bash
git checkout -b experimental-tone
```

### Working on Branches

```
main:        A---B---C
                 \
experimental:     D---E (new ideas)
```

Changes on `experimental` don't affect `main`. You can switch back anytime:

```bash
git switch main   # files revert to main's state
git switch experimental-tone   # files change to experimental state
```

### Merging

When your experiment is ready, bring it back to main:

```bash
git switch main
git merge experimental-tone
```

If there are no conflicts, Git automatically integrates the changes.

### Deleting Branches

```bash
git branch -d experimental-tone           # delete if merged
git branch -D experimental-tone           # force delete (unmerged)
```

### Branch Naming Conventions

```
main                    # stable, working version
feature/tone-control    # a new feature
fix/wrong-temperature   # a bug fix
experiment/cot-prompt   # an experimental approach
draft/memo-v2           # a specific draft
```

### Branch Strategies for AI Work

```
main                  # final, approved prompts and workflows
drafts/               # work-in-progress prompts
experiments/          # alternative approaches to test
archive/              # approaches you tried but didn't use
```

---

## Working with Remote Repositories (GitHub, GitLab, Bitbucket)

### Cloning an Existing Repository

```bash
git clone https://github.com/username/repo.git
cd repo
```

Downloads the entire project and its history to your machine.

### Connecting Your Local Repo to a Remote

```bash
git remote add origin https://github.com/username/repo.git
git remote -v   # list remotes
```

### Pushing (Uploading)

```bash
git push origin main              # push main branch
git push -u origin main           # set upstream and push (first time)
git push origin experimental      # push a branch
git push --all origin             # push all branches
```

The `-u` flag sets the upstream tracking, so future pushes can be just `git push`.

### Pulling (Downloading)

```bash
git pull origin main              # fetch AND merge remote changes
git pull                          # if upstream is set
```

`git pull` is actually two commands: `git fetch` (download) + `git merge` (integrate).

### Fetching (Download Without Merging)

```bash
git fetch origin                  # download but don't merge
git diff main origin/main         # compare local main with remote main
git merge origin/main             # merge manually when ready
```

`fetch` is safer when you want to review changes before integrating them.

### Common Remote Workflows

**Backup your work:**
```bash
git push origin main
```

**Get a collaborator's changes:**
```bash
git pull origin main
```

**Share a branch for review:**
```bash
git push origin experimental-tone
# collaborator can now: git fetch && git switch experimental-tone
```

---

## Resolving Merge Conflicts

When two branches modify the same part of a file, Git can't automatically merge. This is a **merge conflict**.

### How Conflicts Happen

```
main:                    ... "tone: formal" ...
experiment branch:       ... "tone: casual" ...
```

Git doesn't know which to keep.

### Resolving a Conflict

When you run `git merge` and there's a conflict, Git tells you. Open the conflicting file and look for:

```
<<<<<<< HEAD
tone: formal
=======
tone: casual
>>>>>>> experimental-tone
```

- `<<<<<<< HEAD` — your current branch's version
- `=======` — divider
- `>>>>>>> experimental-tone` — the incoming branch's version

Edit the file to keep what you want (or combine both), remove the conflict markers, then:

```bash
git add resolved-file.md
git commit -m "Resolve tone conflict: keep formal but soften language"
```

### Tips to Avoid Conflicts

- Pull frequently: `git pull` before starting work
- Communicate with collaborators about who's editing what
- Make small, focused commits

---

## Stashing — Save Work in Progress

If you need to switch branches but have uncommitted changes:

```bash
git stash                      # save changes temporarily
git stash push -m "WIP: fixing prompt"  # with a message
git stash list                 # view stashes
git stash pop                  # apply and remove the most recent stash
git stash apply stash@{2}      # apply a specific stash
git stash drop stash@{2}       # delete a stash
git stash clear                # delete all stashes
```

---

## Tagging — Mark Important Versions

Tags are named references to specific commits, useful for marking milestones.

```bash
git tag v1.0                         # lightweight tag
git tag -a v1.0 -m "Stable prompt library"  # annotated tag
git tag                              # list tags
git show v1.0                        # see tag details
git push origin v1.0                 # share tag with remote
```

---

## Git + AI: The Iteration Workflow

This is the core workflow for AI-assisted work with version control.

### The Prompt Iteration Loop

```
1. Write a prompt              →  prompts/summary-prompt.md
2. Commit initial version      →  git commit -m "Initial summary prompt"
3. Run prompt with AI          →  get output.md
4. Review output               →  identify what needs to improve
5. Refine prompt               →  edit prompts/summary-prompt.md
6. Check what changed          →  git diff
7. Commit improvement          →  git commit -m "Add tone constraint" "Fix: limit to 3 bullets" "Add example for clarity"
8. If refinement made worse    →  git revert HEAD (undo last change)
9. Try a different approach    →  git switch -c experiment/alt-approach
10. If experiment works        →  git switch main && git merge experiment/alt-approach
11. If experiment fails        →  git branch -D experiment/alt-approach
```

### Comparing AI Outputs with Git

```bash
# Save each AI run
git commit -m "AI output v1"
# Run again, save changes
git commit -m "AI output v2"
# Compare
git diff
```

### Using AI to Write Commit Messages

```bash
git diff | your-ai-tool "Write a concise git commit message for these changes"
```

### Full Example: Building a Prompt Over Time

```
$ git log --oneline --graph
* 7e8f9a0 Refine: make summary even shorter for IM
* 4b5c6d7 Add example of good/bad summary
* 1a2b3c4 Fix: output was too verbose, added length constraint
* 9d8e7f6 Initial prompt: summarize executive briefs

$ git show 1a2b3c4
> - "Write a summary"
> + "Write a summary of exactly 3 bullet points. Each bullet max 15 words."
```

---

## Git Workflows for Teams

### Solo Workflow (simplest)
```
main → branches for experiments → merge back to main
```

### Pair Workflow
```
main → each person works on their own branch → review → merge to main
```

### Review Workflow
```
main → feature branch → pull request → review → merge to main
```

---

## Visualizing Git

### `git log --graph`

```bash
$ git log --oneline --graph --all
* 7e8f9a0 (main) Final refined prompt
* 4b5c6d7 Add examples
| * 2a3b4c5 (experiment) Try chain-of-thought approach
| * 1b2c3d4 Experimental: add step-by-step reasoning
|/
* 9d8e7f6 Initial commit
```

### GUI Tools (when you prefer visuals)
- `gitk` — built-in Git browser
- VS Code — built-in Git GUI
- GitHub Desktop — free, cross-platform
- GitKraken, Sourcetree — third-party options

---

## Quick Reference Card

| Goal | Command |
|------|---------|
| Start tracking | `git init` |
| Check status | `git status` |
| Stage file | `git add file.md` |
| Commit | `git commit -m "message"` |
| See history | `git log --oneline --graph` |
| See changes | `git diff` |
| Create branch | `git switch -c branch-name` |
| Switch branch | `git switch branch-name` |
| Merge branch | `git merge branch-name` |
| Pull remote | `git pull` |
| Push remote | `git push` |
| Undo last commit (safe) | `git revert HEAD` |
| Undo last commit (keep changes) | `git reset HEAD~1` |
| Save work-in-progress | `git stash` |
| Restore WIP | `git stash pop` |
| Ignore files | Edit `.gitignore` |

---

## Common Mistakes and How to Fix Them

| Mistake | Fix |
|---------|-----|
| Committed on wrong branch | `git reset HEAD~1 && git switch correct-branch && git add . && git commit` |
| Forgot to add a file to commit | `git add forgotten-file.md && git commit --amend --no-edit` |
| Committed sensitive data | `git filter-repo` or change the secret (it's in history) |
| Merge conflict | Edit file, remove conflict markers, `git add`, `git commit` |
| `git push` rejected | `git pull` first, resolve any conflicts, then push |
| Accidentally deleted a file | `git restore deleted-file.md` (if committed) |

---

## Next Steps

After this lesson, complete the lab to practice each command hands-on. Then do the assignment to build your own version-controlled prompt library.

The remaining weeks will assume you're comfortable with: `init`, `add`, `commit`, `status`, `log`, `diff`, `branch`, `switch`, `merge`, `push`, `pull`, and `revert`.
