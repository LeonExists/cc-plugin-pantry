# cc-plugin-pantry

A marketplace of plugins for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — grab what you need, leave what you don't.

## Add the marketplace

Pick whichever method matches your setup:

**GitHub shorthand** (uses your default git protocol):
```
/plugin marketplace add LeonExists/cc-plugin-pantry
```

**HTTPS** (works behind corporate proxies, no SSH key needed):
```
/plugin marketplace add https://github.com/LeonExists/cc-plugin-pantry.git
```

**SSH** (if you authenticate with SSH keys):
```
/plugin marketplace add git@github.com:LeonExists/cc-plugin-pantry.git
```

Then browse and install plugins directly from within Claude Code.

## Available plugins

| Plugin | Description |
|--------|-------------|
| `github-init` | Automates GitHub project creation with personalized preferences — suggests names, descriptions, licenses, and generates starter files. |
| `repofinery` | Transform any repository into a star-worthy open source project. Audits, scores, and refines repos across 20 categories — from README quality to viral potential. |

## Install a plugin

```
/plugin install github-init@cc-plugin-pantry
```

After installing, run `/reload-plugins` to activate it in your current session.

## License

[MIT](LICENSE) — use freely, contribute gladly.
