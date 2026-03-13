# cfcu-digital Claude Skills

Shared [Claude Code](https://claude.ai/claude-code) skills library for the cfcu-digital engineering team.

## Available Skills

| Skill | Description |
|-------|-------------|
| [testrail-test-cases](./skills/testrail-test-cases/) | Generate TestRail-importable CSV test cases by visually examining the live digital banking experience |

## Installation

### Option A: Team/Enterprise (recommended)
If your org is on a Claude Team or Enterprise plan, an admin can upload each skill zip at:
**Organization settings → Skills → + Add**

### Option B: Manual clone
Clone into your personal skills directory (available across all your projects):
```bash
git clone https://github.com/cfcu-digital/claude-skills ~/.claude/skills/cfcu-skills
```

Or clone into a specific project (scoped to that project only):
```bash
git clone https://github.com/cfcu-digital/claude-skills .claude/skills/cfcu-skills
```

### Keeping skills up to date
```bash
cd ~/.claude/skills/cfcu-skills && git pull
```

## Using a Skill

Once installed, invoke any skill via slash command in Claude Code:
```
/deploy
/code-review
/pr-summary
```

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for how to add or update skills.
