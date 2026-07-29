# Plugin Structure Guide

Every plugin in cc-plugin-pantry follows this structure:

```
plugins/your-plugin-name/
├── .claude-plugin/
│   └── plugin.json              # Required: plugin manifest
├── commands/                    # Optional: slash commands
│   └── your-command.md          # Each file = one command
├── skills/                      # Optional: skills
│   └── your-skill/
│       └── SKILL.md             # Skill definition
├── agents/                      # Optional: agent definitions
│   └── your-agent.md
└── hooks/                       # Optional: lifecycle hooks
    └── your-hook.md
```

## plugin.json (Required)

```json
{
  "name": "your-plugin-name",
  "version": "1.0.0",
  "description": "What your plugin does — one clear sentence.",
  "author": { "name": "YourGitHubUsername" },
  "repository": "https://github.com/You/your-plugin",
  "license": "MIT",
  "keywords": ["relevant", "search", "terms"]
}
```

## Commands

Markdown files in `commands/` become slash commands. The filename (minus `.md`) is the command name.

**Frontmatter:**
```yaml
---
name: command-name
description: What this command does
allowed-tools: ["Read", "Write", "Bash"]
---
```

## Skills

Skills are triggered automatically based on context. Each skill lives in its own directory with a `SKILL.md` file.

**Frontmatter:**
```yaml
---
name: skill-name
description: When and how this skill should be triggered
version: 1.0.0
---
```

## Submission Checklist

- [ ] `plugin.json` has all required fields
- [ ] Description is under 100 characters
- [ ] At least one command or skill is included
- [ ] Tested in a fresh Claude Code session
- [ ] No hardcoded paths or credentials
- [ ] MIT-compatible license
