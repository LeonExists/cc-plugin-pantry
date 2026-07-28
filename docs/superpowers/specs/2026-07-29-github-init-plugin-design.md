# github-init Plugin Design

## Overview

A Claude Code plugin that fully automates GitHub project creation through a personalized, conversational experience. It combines a **command** for one-time preference configuration with a **skill** for creative, conversational project creation.

## Plugin Structure

```
plugins/github-init/
├── plugin.json
├── commands/
│   └── setup.md
└── skills/
    └── create-project.md
```

## Architecture: Command + Skill Hybrid

- **Command (`/github-init-setup`)** — Mechanical configuration. Walks the user through setting preferences for how their repos should be created. Stored via Claude Code plugin settings.
- **Skill (`create-project`)** — Creative conversational flow. Suggests names, descriptions, licenses, generates README, and executes `gh repo create`. Uses saved preferences as defaults, prompts for any setting marked as `"ask"`.

## Setup Command

### Purpose

One-time (re-runnable) preference configuration. Asks the user a series of questions and stores answers in plugin settings.

### Settings

Every setting supports either a concrete value or the string `"ask"` (prompts the user during each project creation).

| Setting | Type | Options | Default |
|---------|------|---------|---------|
| `default_license` | string \| "ask" | MIT, Apache-2.0, GPL-3.0, BSD-3-Clause, ISC, Unlicense, None | "ask" |
| `readme_style` | string \| "ask" | minimal, standard, detailed | "ask" |
| `gitignore_templates` | string[] \| "ask" | Node, Python, Go, Rust, Java, etc. | "ask" |
| `naming_convention` | string \| "ask" | kebab-case, snake_case, camelCase, PascalCase | "ask" |
| `default_visibility` | string \| "ask" | public, private | "ask" |
| `default_branch` | string \| "ask" | main, master | "main" |
| `include_ci` | boolean \| "ask" | true, false | "ask" |
| `ci_type` | string \| "ask" | lint, test, deploy | "test" |

### UX Flow

The setup command presents each setting with all valid options plus "Ask every time" as the final choice. Example:

> **Default license:** MIT / Apache-2.0 / GPL-3.0 / BSD-3-Clause / ISC / Unlicense / None / **Ask every time**

The command can be re-run at any time to change preferences.

## Create Project Skill

### Trigger

Activated when the user describes wanting to start a new GitHub project, create a repo, or initialize a new project.

### UX: Smart Hybrid

- **Conversational by default** — asks what the user is building, suggests names with reasoning, discusses licenses in plain English.
- **Fast-track available** — if the user says "just do it" or indicates they want speed, the skill uses all stored defaults without prompting and moves through creation quickly.

### Flow

1. **Understand intent** — ask what the user is building (or read context if already described)
2. **Suggest names** — offer 3-5 repo name options following naming convention preference, with brief reasoning for each
3. **Craft description** — propose a concise GitHub description (the one-liner on the repo page)
4. **License guidance** — suggest a license based on project type, explain what it means in plain English (what you can/can't do), respect the default but offer alternatives
5. **Generate README** — create a starter README matching the template style preference
6. **Confirm and create** — summarize all choices, then execute:
   - `gh repo create <name> --<visibility> --description "<desc>"`
   - Initialize with chosen branch name
   - Commit README, LICENSE, .gitignore, and optional CI config
   - Push to remote

### License Explanations

The skill explains licenses conversationally:

- **MIT** — "Do whatever you want, just keep the copyright notice. No warranty."
- **Apache-2.0** — "Like MIT but also grants patent rights. Good for enterprise."
- **GPL-3.0** — "Anyone can use it, but derivative works must also be GPL. Copyleft."
- **BSD-3-Clause** — "Like MIT but can't use the author's name to endorse derivatives."
- **ISC** — "Functionally identical to MIT, just shorter text."
- **Unlicense** — "Public domain. No restrictions whatsoever."

### Handling "ask" Settings

For each setting marked `"ask"`, the skill weaves the question naturally into the conversation at the appropriate point in the flow. It doesn't dump all questions at once — it asks them as they become relevant (e.g., license question comes up during the license discussion step).

## Dependencies

- `gh` CLI must be installed and authenticated
- The skill should check for `gh` availability early and inform the user if it's missing

## Future Extensibility

The plugin is designed to be extended later with:
- .gitignore suggestions by project type
- GitHub Actions starter workflows
- Issue/PR templates
- CONTRIBUTING.md, CODE_OF_CONDUCT.md
- Topics/labels suggestions
- Security policy

These can be added as additional settings in the setup command and additional steps in the skill without restructuring.
