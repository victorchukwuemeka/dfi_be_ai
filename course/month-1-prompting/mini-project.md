# Mini-Project: Prompt Library + Quality Checklist

## Due
End of Month 1

## Objective
Build a reusable prompt library for your real work, with a quality checklist and version history tracked in Git.

## Requirements

### Prompt Library (at least 8 prompts)
Cover at least 3 different task types:
- Writing/rewriting
- Analysis/synthesis
- Brainstorming/ideation
- Summarization
- Planning

Each prompt must include:
- Role, task, constraints
- Output schema
- At least one example (few-shot) in 3 of the 8 prompts

### Version History
- Each prompt must have at least 2 versions (committed in Git)
- Commit messages must describe the refinement (e.g., "Add tone constraint to memo prompt")
- Show `git log` for at least 3 prompts

### Quality Checklist
Create a `CHECKLIST.md` with:
- The 5-dimension rubric (accuracy, clarity, tone, usefulness, completeness)
- A pre-flight checklist before running any prompt:
  - [ ] Role defined?
  - [ ] Task specific?
  - [ ] Constraints set?
  - [ ] Output format specified?
  - [ ] Examples included (if needed)?
- A post-flight checklist:
  - [ ] Output scored against rubric?
  - [ ] Gap identified?
  - [ ] Refinement made?
  - [ ] New version committed?

### Repository Structure
```
prompt-library/
├── README.md           # overview, usage instructions
├── CHECKLIST.md        # quality checklist
├── .gitignore
└── prompts/
    ├── write/
    │   ├── memo-prompt.md
    │   └── email-prompt.md
    ├── analyze/
    │   ├── data-review.md
    │   └── sentiment-classify.md
    └── brainstorm/
        ├── ideation-prompt.md
        └── campaign-ideas.md
```

## Submission
1. Link to Git repository (GitHub/GitLab) OR zipped repo with `.git` folder
2. Output of `git log --oneline --graph --all`

## Grading Criteria
- 8+ prompts with clear structure (40%)
- Version history showing refinement for 3+ prompts (20%)
- Quality checklist is thorough and usable (20%)
- Repository is well-organized with README and .gitignore (10%)
- Prompts cover 3+ task types (10%)
