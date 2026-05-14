# SKILL-md-labs

This repo is a personal laboratory for authoring, testing, and storing Codex skills (SKILL.md files).

## Purpose

- Draft and iterate on skills
- Store evals alongside each skill
- Version-control skill development

## Structure

```
skills/
  <domain>/
    <skill-name>/
      SKILL.md        # The skill itself
      evals/
        cases.md      # Trigger tests + behavior tests
  _template/
    SKILL.md          # Skeleton for new skills
material/             # Reference PDFs and guides
```

## Domains

| Folder | What goes here |
|--------|---------------|
| `data/` | Data analysis, SQL, statistics |
| `dev/` | Coding, debugging, code review |
| `writing/` | Docs, prompts, communication |

Add new domains as needed.

## REQUIRED: Use `/skill-creator` for All Skill Work

**Always invoke the `/skill-creator` skill** when creating, editing, or improving any skill in this repo. Never write or modify a `SKILL.md` file directly without going through `/skill-creator`.

This applies to:
- Creating a new skill
- Updating an existing skill's content, triggers, or description
- Running evals or benchmarking a skill
- Optimizing a skill's trigger description

Reason: `/skill-creator` enforces consistent structure, eval coverage, and trigger accuracy across all skills.

## Workflow

1. Run `/skill-creator` — it will guide skill creation end-to-end
2. Place output at `skills/<domain>/<name>/SKILL.md`
3. Place evals at `skills/<domain>/<name>/evals/cases.md`
4. Install locally: copy SKILL.md to `~/.Codex/skills/<name>/SKILL.md`
5. Commit

## Notes

- Skills in this repo are drafts. Installed skills live in `~/.Codex/`.
- Evals are manual test cases, not automated. Run by pasting prompts into Codex.
