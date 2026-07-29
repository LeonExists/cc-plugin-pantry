# Contributing to cc-plugin-pantry

Thank you for your interest in contributing! Whether you're submitting a plugin or improving existing ones, you're helping build the Claude Code ecosystem.

## Submitting a Plugin

1. Fork the repository
2. Create your plugin directory: `plugins/your-plugin-name/`
3. Add the required structure:
   ```
   plugins/your-plugin-name/
   ├── .claude-plugin/
   │   └── plugin.json          # Plugin manifest (required)
   ├── commands/                 # Slash commands (optional)
   │   └── your-command.md
   └── skills/                   # Skills (optional)
       └── your-skill/
           └── SKILL.md
   ```
4. Fill in your `plugin.json`:
   ```json
   {
     "name": "your-plugin-name",
     "version": "1.0.0",
     "description": "What your plugin does in one sentence.",
     "author": { "name": "YourGitHubUsername" },
     "repository": "https://github.com/YourUsername/your-repo",
     "license": "MIT",
     "keywords": ["relevant", "keywords"]
   }
   ```
5. Open a Pull Request with a clear description of what your plugin does

## Plugin Guidelines

- **One purpose per plugin** — do one thing well
- **Clear descriptions** — users should know what it does from the one-liner
- **Tested** — try your plugin in a fresh Claude Code session before submitting
- **No secrets** — never include API keys, tokens, or credentials
- **MIT-compatible** — plugins must use an MIT-compatible license

## Improving Existing Plugins

Found a bug or want to improve a plugin? PRs welcome:

1. Fork the repo
2. Create a branch: `git checkout -b fix/plugin-name-issue`
3. Make your changes
4. Open a PR describing what you fixed and why

## Questions?

Open a [Discussion](https://github.com/LeonExists/cc-plugin-pantry/discussions) or file an [Issue](https://github.com/LeonExists/cc-plugin-pantry/issues).
