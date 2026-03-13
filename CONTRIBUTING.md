# Contributing to cfcu-digital Claude Skills

## Adding a New Skill

1. Create a new directory under `skills/` named after your skill:
   ```
   skills/your-skill-name/
   └── SKILL.md
   ```

2. Add a `SKILL.md` with the required frontmatter:
   ```markdown
   ---
   name: your-skill-name
   description: What it does and when Claude should invoke it automatically
   allowed-tools: Read, Grep, Bash(git *)
   disable-model-invocation: true   # add for side-effect skills (deploy, etc.)
   ---

   # Skill content here
   ```

3. Optionally add an `examples/` subdirectory with usage examples.

4. Update the skill index table in [README.md](./README.md).

5. Open a PR — CI will validate your `SKILL.md` frontmatter.

## Frontmatter Reference

| Field | Required | Notes |
|-------|----------|-------|
| `name` | Yes | Becomes the `/slash-command` name — use kebab-case |
| `description` | Yes | Drives auto-invocation; be specific about when to trigger |
| `allowed-tools` | Yes | Always restrict to minimum needed tools |
| `disable-model-invocation` | No | Set `true` for skills with side effects (deploys, writes) |

## Updating an Existing Skill

1. Edit the relevant `SKILL.md`
2. Open a PR with a clear description of what changed and why
3. Once merged, teammates using manual clone should `git pull`

## Skill Quality Guidelines

- `description` should answer: "When should Claude automatically use this?"
- `allowed-tools` should be as narrow as possible
- Include concrete examples in the skill body
- Test your skill locally before opening a PR:
  ```bash
  cp -r skills/your-skill ~/.claude/skills/your-skill
  # then test in Claude Code
  ```
