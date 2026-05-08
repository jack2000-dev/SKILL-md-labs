# SKILL-md-labs

Personal lab for building and storing Claude Code skills.

## Skills

| Skill | Domain | Trigger |
|-------|--------|---------|
| [data-analysis-frameworks](skills/data/data-analysis/SKILL.md) | data | "perform data analysis", "analyze data" |
| [invest-mud](skills/finance/invest-mud/SKILL.md) | finance | personal finance, investing, debt, life/career planning |
| [super-explainer](skills/learning/super-explainer/SKILL.md) | learning | "[X] explained", "what is [X]", "explain [X]" |

## Quick Start

**New skill:**
```bash
cp -r skills/_template skills/<domain>/<name>
# edit skills/<domain>/<name>/SKILL.md
```

**Install a skill locally:**
```bash
cp -r skills/<domain>/<name> ~/.claude/skills/<name>
```

## Reference

- [Building Skills for Claude (PDF)](material/The-Complete-Guide-to-Building-Skill-for-Claude.pdf)
