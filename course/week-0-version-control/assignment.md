# Assignment: Version-Controlled Prompt Library

## Due
Before Week 1

## Task
Create a Git repository containing a small personal prompt library (at least 3 prompts) with a documented revision history showing iterative improvement.

## Requirements

### Structure
```
your-prompt-library/
├── README.md          # what this library is and how to use it
├── .gitignore
└── prompts/
    ├── summarize.md
    ├── brainstorm.md
    └── revise.md
```

### Each prompt file must have:
- Version history in comments or commit messages
- At least 2 revisions showing iterative improvement (the `git log` should show this)

### README must include:
- Purpose of the library
- How you use AI in your workflow
- One insight about version control you learned

## Submission
Provide:
1. A link to your repository (GitHub/GitLab) OR
2. Output of `git log --oneline --all --graph` pasted into a document

## Grading Criteria
- Repository is properly initialized with `.gitignore`
- README is clear and complete
- Each prompt has visible revision history (multiple commits)
- Commit messages are descriptive
- Evidence of branching (bonus)
