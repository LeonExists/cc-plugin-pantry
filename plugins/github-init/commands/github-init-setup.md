---
name: github-init-setup
description: Configure your GitHub project creation preferences
allowed-tools: ["Read", "Write", "Bash"]
---

# GitHub Init Setup

You are configuring the user's preferences for automated GitHub project creation. Walk through each setting below, one at a time, and save the results.

## Pre-flight Check

1. Verify `gh` CLI is available by running: `gh --version`
   - If not installed, inform the user they need to install it: https://cli.github.com/
   - If not authenticated, inform them to run `gh auth login`
2. Check if `.claude/github-init.local.md` already exists
   - If it does, read the current settings and offer to update them (show current values as defaults)
   - If it doesn't, start fresh

## Settings to Configure

Ask the user about each setting one at a time. For EVERY setting, always include "Ask every time" as an option — this stores the value `"ask"` and means the create-project skill will prompt for it during each project creation.

Present each setting with a clear explanation of what it controls.

### 1. Default License

Options: MIT, Apache-2.0, GPL-3.0, BSD-3-Clause, ISC, Unlicense, None, **Ask every time**

Explain briefly:
- **MIT** — Do whatever you want, just keep the copyright notice.
- **Apache-2.0** — Like MIT but also grants patent rights. Good for enterprise.
- **GPL-3.0** — Derivative works must also be GPL. Strong copyleft.
- **BSD-3-Clause** — Like MIT but can't use author's name to endorse derivatives.
- **ISC** — Functionally identical to MIT, shorter text.
- **Unlicense** — Public domain. No restrictions whatsoever.
- **None** — No license file (all rights reserved by default).

### 2. README Style

Options: minimal, standard, detailed, **Ask every time**

Explain:
- **minimal** — Project name, one-line description, basic install/usage
- **standard** — Badges, description, installation, usage, contributing, license sections
- **detailed** — Full documentation structure with table of contents, API docs, examples, FAQ

### 3. Gitignore Templates

Options: Node, Python, Go, Rust, Java, C++, Ruby, Swift, Kotlin, None, **Ask every time**

The user can pick multiple templates to combine. Store as a list.

### 4. Naming Convention

Options: kebab-case, snake_case, camelCase, PascalCase, **Ask every time**

This controls how repo names are suggested (e.g., "my-cool-project" vs "my_cool_project").

### 5. Default Visibility

Options: public, private, **Ask every time**

### 6. Default Branch Name

Options: main, master, **Ask every time**

### 7. Include CI/CD Starter

Options: true, false, **Ask every time**

If true, a basic GitHub Actions workflow will be included in the generated project.

### 8. CI Type

Only ask this if the user chose `true` or `"ask"` for Include CI/CD.

Options: lint, test, deploy, **Ask every time**

- **lint** — Runs linting on push/PR
- **test** — Runs test suite on push/PR
- **deploy** — Basic deploy workflow template

## Save Settings

After collecting all answers, write the settings to `.claude/github-init.local.md`:

```
---
default_license: "<value or ask>"
readme_style: "<value or ask>"
gitignore_templates: <["Template1", "Template2"] or "ask">
naming_convention: "<value or ask>"
default_visibility: "<value or ask>"
default_branch: "<value or ask>"
include_ci: <true, false, or "ask">
ci_type: "<value or ask>"
---

# GitHub Init Settings

These settings are used by the `create-project` skill to personalize your GitHub project creation experience. Re-run `/github-init-setup` to change them.
```

## Finish

Confirm to the user that their settings are saved. Remind them they can re-run `/github-init-setup` anytime to change preferences.
