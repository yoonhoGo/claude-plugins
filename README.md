# claude-plugins

A collection of [Claude Code](https://claude.com/claude-code) plugins that extend Claude's capabilities with external tool integrations and productivity workflows.

## What is this?

This repository serves as a **Claude Code plugin marketplace** — a curated set of plugins that give Claude Code the ability to interact with external applications and services directly from your terminal. Each plugin provides skills (auto-activating knowledge), commands (slash commands), or both, enabling natural language control over tools you already use.

## Plugins

| Plugin | Category | Description | Version |
|--------|----------|-------------|---------|
| [obsidian-cli](./obsidian-cli) | Productivity | Obsidian CLI integration — manage notes, search knowledge, and control Obsidian from the terminal via natural language | 0.1.0 |

### obsidian-cli

Bridges Claude Code with the official [Obsidian CLI](https://help.obsidian.md/cli) to give you full control over your Obsidian vault without leaving the terminal.

**What you can do:**
- Create, read, edit, move, and delete notes
- Read and append to daily notes
- Full-text search across your vault, explore tags, backlinks, and orphan notes
- Manage YAML frontmatter properties
- List and filter tasks
- Control plugins, themes, workspaces, Publish, and Sync

**How it works:**
- **Skill (auto-activating):** Just mention anything Obsidian-related in conversation — Claude automatically understands and executes the right CLI commands
- **Command (`/obsidian`):** Use the slash command for direct natural language instructions

> Requires Obsidian 1.12+ with a [Catalyst license](https://obsidian.md/pricing) (early access). See the [obsidian-cli README](./obsidian-cli/README.md) for full details.

## Installation

### From Marketplace

```bash
# Register this repository as a marketplace source (one-time setup)
/plugin marketplace add https://github.com/yoonhoGo/claude-plugins

# Install a plugin
/plugin install obsidian-cli@yoonho-plugins
```

### Direct from GitHub

```bash
# Install a specific plugin without marketplace registration
/plugin add https://github.com/yoonhoGo/claude-plugins/tree/main/obsidian-cli
```

### Local Installation

```bash
# Clone the repository
git clone https://github.com/yoonhoGo/claude-plugins.git

# Add a plugin directly
/plugin add ./claude-plugins/obsidian-cli
```

## Repository Structure

```
claude-plugins/
├── .claude-plugin/
│   └── marketplace.json    # Marketplace manifest (plugin registry)
├── obsidian-cli/            # Obsidian CLI integration plugin
│   ├── .claude-plugin/
│   │   └── plugin.json
│   ├── commands/
│   ├── skills/
│   ├── README.md
│   └── README_KO.md
└── README.md
```

## Contributing

To add a new plugin, create a directory at the repository root with its own `.claude-plugin/plugin.json` manifest, then register it in `.claude-plugin/marketplace.json`.

## License

MIT
