---
name: create-project
description: Use when the user wants to create a new GitHub repository, start a new project, or initialize a new repo. Handles name suggestions, descriptions, license selection, README generation, and full repo creation via gh CLI.
version: 1.0.0
---

# Create GitHub Project

You are helping the user create a new GitHub repository. You handle everything from naming to pushing the first commit.

## Pre-flight Checks

1. Verify `gh` CLI is installed: `gh --version`
   - If missing, tell the user to install it from https://cli.github.com/
2. Verify `gh` is authenticated: `gh auth status`
   - If not authenticated, tell them to run `gh auth login`
3. Read settings from `.claude/github-init.local.md`
   - If the file doesn't exist, inform the user they can run `/github-init-setup` to configure defaults, but proceed anyway by asking for each preference as needed

## UX Mode: Smart Hybrid

- **Conversational by default**: Ask what the user is building, suggest names with reasoning, discuss licenses naturally.
- **Fast-track**: If the user says "just do it", "use defaults", "quick setup", or similar — use all stored defaults without prompting and move through creation rapidly. Only stop to ask for settings marked `"ask"` and for the project description (since that's always unique).

## Creation Flow

### Step 1: Understand the Project

Ask the user what they're building. If they've already described it in the conversation, use that context instead of re-asking. Gather:
- What the project does (purpose)
- Target audience or use case
- Primary language/framework

### Step 2: Suggest Repository Names

Based on what they described and their `naming_convention` preference:
- Offer 3-5 name suggestions with brief reasoning for each
- Follow the naming convention (kebab-case, snake_case, etc.)
- If naming_convention is `"ask"`, first ask which convention they prefer

Example:
> Based on your CLI tool for managing Docker containers, here are some name ideas:
> 1. **dock-pilot** — nautical theme, implies steering/control
> 2. **container-cli** — straightforward, instantly clear
> 3. **dockhand** — a person who handles dock operations
> 4. **cbox** — short, memorable, "container box"

Let the user pick or provide their own.

### Step 3: Craft Description

Propose a concise GitHub description (the one-liner shown on the repo page). Keep it under 100 characters. Offer 2-3 options:

Example:
> 1. "A CLI tool for managing Docker containers with ease"
> 2. "Streamlined Docker container management from the terminal"
> 3. "Docker container orchestration made simple"

### Step 4: License Selection

Check the `default_license` setting:
- If it's a concrete value (not `"ask"`), use it as the default but mention what was chosen and offer to change
- If it's `"ask"`, present license options with plain-English explanations:

| License | What it means |
|---------|--------------|
| **MIT** | Do whatever you want, just keep the copyright notice. No warranty. |
| **Apache-2.0** | Like MIT but also grants patent rights. Good for enterprise use. |
| **GPL-3.0** | Anyone can use it, but derivative works must also be GPL. Copyleft. |
| **BSD-3-Clause** | Like MIT but can't use the author's name to endorse derivatives. |
| **ISC** | Functionally identical to MIT, just shorter text. |
| **Unlicense** | Public domain dedication. No restrictions whatsoever. |
| **None** | No license file. All rights reserved by default. |

Help the user choose based on their project type:
- Open source library → MIT or Apache-2.0
- Want to ensure derivatives stay open → GPL-3.0
- Maximum freedom → Unlicense
- Corporate/enterprise → Apache-2.0

### Step 5: Generate README

Based on the `readme_style` setting (or ask if `"ask"`), generate an appropriate README:

**minimal:**
```markdown
# {project-name}

{description}

## Installation

```bash
# Installation instructions
```

## Usage

```bash
# Usage example
```

## License

{license}
```

**standard:**
```markdown
# {project-name}

{badges}

{description}

## Features

- Feature 1
- Feature 2

## Installation

```bash
# Installation instructions
```

## Usage

```bash
# Usage example
```

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

## License

{license}
```

**detailed:**
```markdown
# {project-name}

{badges}

{description}

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [API Reference](#api-reference)
- [Examples](#examples)
- [Contributing](#contributing)
- [FAQ](#faq)
- [License](#license)

## Features

- Feature 1
- Feature 2

## Installation

### Prerequisites

- Prerequisite 1

### Steps

```bash
# Installation instructions
```

## Usage

### Basic Usage

```bash
# Basic example
```

### Advanced Usage

```bash
# Advanced example
```

## API Reference

Document the public API here.

## Examples

Additional examples and use cases.

## Contributing

Contributions are welcome! Please read the contributing guidelines first.

## FAQ

**Q: Common question?**
A: Answer here.

## License

{license}
```

Fill in the project name, description, and license. For features, installation, and usage — fill in reasonable placeholders based on the project description that the user can easily customize later.

### Step 6: Confirm and Create

Present a summary of all choices:

> **Summary:**
> - **Name:** {name}
> - **Description:** {description}
> - **Visibility:** {public/private}
> - **License:** {license}
> - **Branch:** {main/master}
> - **Gitignore:** {templates}
> - **CI/CD:** {yes/no, type}
> - **README style:** {style}

Ask for confirmation. On "yes", execute the creation:

```bash
# 1. Create a temporary directory and initialize
mkdir {name} && cd {name}
git init -b {branch}

# 2. Create the files
# - Write README.md
# - Write LICENSE (fetch from GitHub's license API or use gh)
# - Write .gitignore (combine selected templates)
# - If CI enabled, write .github/workflows/ci.yml

# 3. Create the GitHub repo
gh repo create {name} --{visibility} --description "{description}" --source . --push
```

### CI/CD Templates

If `include_ci` is true, generate based on `ci_type`:

**lint (ci.yml):**
```yaml
name: Lint
on: [push, pull_request]
jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run linter
        run: echo "Add your lint command here"
```

**test (ci.yml):**
```yaml
name: Test
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run tests
        run: echo "Add your test command here"
```

**deploy (ci.yml):**
```yaml
name: Deploy
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy
        run: echo "Add your deploy command here"
```

### Step 7: Post-Creation

After successful creation:
1. Confirm the repo was created with a link: `https://github.com/{user}/{name}`
2. Tell the user their project is ready
3. Mention they can `cd {name}` to start working
4. If they're already in a directory where they want the project, offer to clone it there instead

## Error Handling

- If `gh repo create` fails due to name conflict, suggest alternative names
- If authentication fails mid-flow, guide the user to re-authenticate
- If any file write fails, report the error and suggest manual steps

## Settings Reference

All settings from `.claude/github-init.local.md`:

| Setting | Values | Behavior when "ask" |
|---------|--------|-------------------|
| default_license | MIT, Apache-2.0, GPL-3.0, BSD-3-Clause, ISC, Unlicense, None | Present license table |
| readme_style | minimal, standard, detailed | Ask which style |
| gitignore_templates | ["Node", "Python", ...] | Ask which templates |
| naming_convention | kebab-case, snake_case, camelCase, PascalCase | Ask before suggesting names |
| default_visibility | public, private | Ask public or private |
| default_branch | main, master | Ask which branch name |
| include_ci | true, false | Ask if they want CI |
| ci_type | lint, test, deploy | Ask which CI type |
