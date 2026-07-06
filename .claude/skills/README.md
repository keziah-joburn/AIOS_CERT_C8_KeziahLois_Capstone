# Skills

Reusable workflows for this workspace live here. Claude Code **auto-discovers**
any skill placed in `.claude/skills/`.

## How to add a skill
Create a subfolder with a `SKILL.md` file:

```
.claude/skills/
└── my-skill/
    └── SKILL.md
```

`SKILL.md` starts with YAML frontmatter, then instructions:

```markdown
---
name: my-skill
description: One line describing when Claude should use this skill.
---

# My Skill
Step-by-step instructions for the workflow...
```

- Claude applies a skill automatically when its `description` matches the task,
  or you can invoke it directly with `/my-skill`.
- Add `disable-model-invocation: true` to the frontmatter for skills with side
  effects you only want to trigger manually.

## Available skills
- **`AIOS_CERT_C8_KeziahLois_WeeklyReport`** (`/weekly-report`) — asks about the week, drafts the weekly report, uploads it to Drive, and sends the Slack summary.
