---
name: deploy
description: Deploy applications and services. Use when the user asks to deploy, release, ship, or promote code to any environment (dev, staging, production).
allowed-tools: Bash(git *), Bash(gh *), Read, Grep
disable-model-invocation: true
---

# Deploy Skill

This skill guides deployments following cfcu-digital runbooks.

## Pre-Deploy Checklist

Before deploying, confirm:

1. **Branch status** — verify you're on the correct branch and it's up to date
   ```bash
   git status && git log --oneline -5
   ```

2. **Tests passing** — confirm CI is green on the target branch
   ```bash
   gh run list --branch $(git branch --show-current) --limit 3
   ```

3. **Environment** — confirm target environment (dev / staging / prod)

4. **Approvals** — production deploys require a merged PR with at least one approval

## Deploy Steps

### Dev / Staging
```bash
# Example — replace with your actual deploy command
gh workflow run deploy.yml --field environment=staging
```

### Production
```bash
# Example — replace with your actual deploy command
gh workflow run deploy.yml --field environment=production
```

## Post-Deploy Verification

After deploying:
1. Check the workflow run completed successfully
2. Verify the deployment in the target environment
3. Monitor logs for any errors in the first 5 minutes

## Rollback

If something goes wrong:
```bash
# Example — replace with your actual rollback command
gh workflow run rollback.yml --field environment=<env> --field version=<previous-version>
```

## Notes

- Never deploy directly to production without a merged PR
- Tag releases after successful production deploys: `git tag -a vX.Y.Z -m "Release vX.Y.Z"`
- Update this skill with your actual deploy commands and runbook links
