<!-- AI IMAGE PROMPT (for generating banner/social preview):
"A sleek, modern digital pantry shelf made of dark glass and neon light accents,
with glowing plugin cards floating off the shelves like holographic items.
The word 'PANTRY' subtly etched into the glass. Minimal, futuristic, dark theme.
Colors: deep navy (#0d1117), electric cyan (#58a6ff), soft purple (#bc8cff).
Style: 3D render, isometric, clean, GitHub-dark aesthetic. 1280x640 for social preview."
-->

<div align="center">

```
  ┌─────────────────────────────────────────────────────────────┐
  │                                                             │
  │   ╔═╗ ╔═╗   ╔═╗ ╦  ╦ ╦ ╔═╗ ╦ ╔╗╔   ╔═╗ ╔═╗ ╔╗╔ ╦╦═╗╦ ╦ │
  │   ║   ║     ╠═╝ ║  ║ ║ ║ ╦ ║ ║║║   ╠═╝ ╠═╣ ║║║  ║ ╠╦╝╚╦╝ │
  │   ╚═╝ ╚═╝   ╩   ╩═╝╚═╝ ╚═╝ ╩ ╝╚╝   ╩   ╩ ╩ ╝╚╝  ╩ ╩╚═ ╩  │
  │                                                             │
  │          The plugin marketplace for Claude Code             │
  │                                                             │
  └─────────────────────────────────────────────────────────────┘
```

**Claude Code plugins. One command. Instant superpowers.**

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Plugins](https://img.shields.io/badge/plugins-2-purple.svg)](#available-plugins)
[![Claude Code](https://img.shields.io/badge/built%20for-Claude%20Code-orange.svg)](https://docs.anthropic.com/en/docs/claude-code)

[Install](#install-the-marketplace) · [Browse Plugins](#available-plugins) · [Contribute](#contributing)

</div>

---

## The Problem

You're using Claude Code. It's powerful. But every session you're re-explaining the same workflows, re-configuring the same behaviors, re-writing the same prompts.

**What if Claude Code had an app store?**

## The Solution

**cc-plugin-pantry** is the first community-driven marketplace for Claude Code plugins. Browse, install, and activate plugins in seconds — no configuration files to edit, no repos to clone manually.

```
/plugin marketplace add LeonExists/cc-plugin-pantry
```

That's it. You now have access to every plugin in the pantry.

---

## Install the Marketplace

Pick whichever method matches your setup:

| Method | Command |
|--------|---------|
| **GitHub shorthand** (recommended) | `/plugin marketplace add LeonExists/cc-plugin-pantry` |
| **HTTPS** (corporate proxies) | `/plugin marketplace add https://github.com/LeonExists/cc-plugin-pantry.git` |
| **SSH** (SSH key auth) | `/plugin marketplace add git@github.com:LeonExists/cc-plugin-pantry.git` |

---

## Available Plugins

| Plugin | What it does | Install |
|--------|-------------|---------|
| 🏗️ **github-init** | Creates GitHub repos with your personal preferences — names, licenses, READMEs, CI — all from conversation | `/plugin install github-init@cc-plugin-pantry` |
| 🔧 **repofinery** | Audits and transforms any repo into a star-worthy project. Scores 20 categories, then fixes them interactively | `/plugin install repofinery@cc-plugin-pantry` |

> More plugins coming soon. [Want to contribute one?](#contributing)

After installing, run `/reload-plugins` to activate.

---

## How It Works

```mermaid
graph LR
    A[You] -->|"/plugin marketplace add"| B[cc-plugin-pantry]
    B -->|browse| C[Plugin Registry]
    C -->|"/plugin install X"| D[Your Claude Code]
    D -->|instant access| E[New Skills & Commands]

    style A fill:#58a6ff,stroke:#58a6ff,color:#0d1117
    style B fill:#bc8cff,stroke:#bc8cff,color:#0d1117
    style C fill:#3fb950,stroke:#3fb950,color:#0d1117
    style D fill:#f0883e,stroke:#f0883e,color:#0d1117
    style E fill:#58a6ff,stroke:#58a6ff,color:#0d1117
```

---

## Why This Exists

Claude Code is the most powerful AI coding tool available — but its plugin ecosystem is still in its infancy. There's no central place to discover, share, or install plugins.

**cc-plugin-pantry** changes that:

- **For users** — Stop reinventing the wheel. Install battle-tested plugins in one command.
- **For creators** — Ship your plugins where people can actually find them.
- **For the ecosystem** — A rising tide lifts all boats. More plugins = more reasons to use Claude Code.

---

## Contributing

We want your plugins! If you've built something useful for Claude Code, submit it to the pantry.

1. Fork this repo
2. Add your plugin to `plugins/your-plugin-name/`
3. Include a `.claude-plugin/plugin.json` manifest
4. Open a PR

See the [plugin structure guide](docs/PLUGIN_STRUCTURE.md) for details.

---

## Roadmap

- [ ] Plugin categories and tags
- [ ] Quality ratings and reviews
- [ ] Automated plugin validation
- [ ] Plugin templates / scaffolding
- [ ] Community voting

---

## License

[MIT](LICENSE) — use freely, contribute gladly.

---

<div align="center">

**If this saved you time, [star the repo](https://github.com/LeonExists/cc-plugin-pantry) — it helps others find it.**

</div>
