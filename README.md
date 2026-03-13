# cfcu-digital Claude Skills

Shared [Claude Code](https://claude.ai/claude-code) skills library for the cfcu-digital engineering team.

## Available Skills

| Skill | Description |
|-------|-------------|
| [testrail-test-cases](./skills/testrail-test-cases/) | Generate TestRail-importable CSV test cases by visually examining the live digital banking experience |

## Installation

Clone the repo to `~/.claude/cfcu-skills/`, then symlink each skill into the directory Claude Code scans:

```bash
git clone https://github.com/cfcu-digital/claude-skills ~/.claude/cfcu-skills

# Symlink all skills at once
for dir in ~/.claude/cfcu-skills/skills/*/; do
  ln -s "$dir" ~/.claude/skills/"$(basename "$dir")"
done
```

> **Why symlinks?** Claude Code loads skills from `~/.claude/skills/<skill-name>/SKILL.md`. The repo stores skills under a `skills/` subdirectory for organization, so we symlink each one into the expected location.

For a **project-scoped** install (available only in one repo):
```bash
git clone https://github.com/cfcu-digital/claude-skills .claude/cfcu-skills

for dir in .claude/cfcu-skills/skills/*/; do
  ln -s "$(pwd)/$dir" .claude/skills/"$(basename "$dir")"
done
```

### Keeping skills up to date
```bash
cd ~/.claude/cfcu-skills && git pull
```
(Symlinks don't need to be recreated — they point into the repo directory.)

## Using a Skill

Once installed, invoke any skill via slash command in Claude Code:
```
/testrail-test-cases
```

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for how to add or update skills.
