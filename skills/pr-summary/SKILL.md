---
name: pr-summary
description: Generate a structured PR description. Use when the user asks to write a PR description, summarize changes for a pull request, or create a PR.
allowed-tools: Bash(git log *), Bash(git diff *), Bash(gh pr *)
---

# PR Summary Skill

Generate clear, structured PR descriptions from the current branch's changes.

## Process

### 1. Gather context
```bash
# Commits since branching from main
git log main...HEAD --oneline

# Full diff
git diff main...HEAD
```

### 2. Generate PR Description

Use this template:

```markdown
## What
<!-- 1-3 sentences: what does this change do? -->

## Why
<!-- The motivation or ticket context. Link the issue/ticket if applicable. -->

## How
<!-- Optional: explain non-obvious implementation decisions -->

## Testing
- [ ] Unit tests added/updated
- [ ] Tested locally
- [ ] Tested in staging (if applicable)

## Checklist
- [ ] No hardcoded secrets or PII
- [ ] Error handling added for new failure modes
- [ ] Documentation updated (if needed)
```

### 3. Create the PR
```bash
gh pr create --title "<concise title under 70 chars>" --body "<generated description>"
```

## Tips

- PR title should complete the sentence: "When merged, this PR will..."
- Link related issues with `Closes #<number>` or `Refs #<number>` in the Why section
- Keep the title under 70 characters
