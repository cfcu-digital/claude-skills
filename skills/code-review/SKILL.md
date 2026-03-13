---
name: code-review
description: Review code changes against cfcu-digital engineering standards. Use when the user asks to review code, check a PR, audit changes, or evaluate a diff.
allowed-tools: Read, Grep, Glob, Bash(git diff *), Bash(git log *), Bash(gh pr *)
---

# Code Review Skill

Review code changes consistently against cfcu-digital team standards.

## Review Process

### 1. Understand the Change
```bash
# Get PR details if reviewing a PR
gh pr view <number>

# Or review local diff
git diff main...HEAD
```

### 2. Checklist

Work through each category and note any issues found.

#### Correctness
- [ ] Logic is correct and handles edge cases
- [ ] No obvious bugs or off-by-one errors
- [ ] Error handling is appropriate
- [ ] No silent failures

#### Security
- [ ] No secrets, credentials, or PII hardcoded
- [ ] Input is validated at system boundaries
- [ ] No SQL injection, XSS, or command injection vectors
- [ ] Dependencies added are from trusted sources

#### Code Quality
- [ ] Functions/methods have single responsibility
- [ ] No unnecessary complexity or premature abstraction
- [ ] Naming is clear and consistent with the codebase
- [ ] No dead code or commented-out blocks

#### Tests
- [ ] New behavior has test coverage
- [ ] Tests cover happy path and failure cases
- [ ] No tests rely on hardcoded external state

#### Documentation
- [ ] Public interfaces have sufficient documentation
- [ ] Complex logic has inline comments explaining *why*, not *what*
- [ ] README or runbook updated if behavior changed

### 3. Output Format

Summarize findings as:

```
## Summary
One-sentence description of what the change does.

## Approval Status
[ ] Approved  [ ] Approved with nits  [ ] Changes requested

## Issues
### Blocking
- (list blocking issues, if any)

### Non-blocking
- (list suggestions/nits)
```

## Standards Reference

- Follow existing patterns in the file being changed
- Prefer simple, readable code over clever code
- Security issues are always blocking — no exceptions
