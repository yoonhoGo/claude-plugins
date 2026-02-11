# obsidian-cli

Obsidian CLI integration plugin for Claude Code.

A Claude Code plugin that lets you control your Obsidian vault from the terminal.

[한국어](README_KO.md)

## Features

- **Note Management** — Create, read, edit, move, and delete notes
- **Daily Notes** — Read and write to today's daily note
- **Knowledge Search** — Full-text search, tags, backlinks, and orphan note discovery
- **Properties** — YAML frontmatter metadata management
- **Task Management** — List and filter tasks across your vault
- **Advanced Features** — Manage plugins, themes, workspaces, Publish, and Sync
- **Developer Tools** — JS eval, console, screenshots, and CSS inspection

## Prerequisites

- Obsidian 1.12+ (version with CLI support)
- Obsidian app running (CLI communicates with the running app)
- `obsidian` binary available in PATH
- Catalyst license (early access)

## Installation

```bash
# Register marketplace (one-time setup)
/plugin marketplace add ~/workspace/claude-plugins

# Install from marketplace
/plugin install obsidian-cli@yoonho-plugins

# Or add locally (without marketplace)
/plugin add ~/workspace/claude-plugins/obsidian-cli
```

## Usage

### Skill (Auto-activating)

The skill activates automatically when you make Obsidian-related requests:

```
"Search for meeting notes in Obsidian"
"Add a work log to today's daily note"
"Check backlinks"
"Create a new note"
```

### Command

Use the `/obsidian` command to execute natural language instructions:

```
/obsidian read today's daily note
/obsidian search for notes about "auth module"
/obsidian append progress update to project-plan note
/obsidian show me the tag list
```

## Plugin Structure

```
obsidian-cli/
├── .claude-plugin/
│   └── plugin.json              # Plugin manifest
├── commands/
│   └── obsidian.md              # /obsidian command
├── skills/
│   └── obsidian-cli/
│       ├── SKILL.md             # Core skill (auto-activating)
│       └── references/
│           ├── file-management.md
│           ├── daily-notes.md
│           ├── search-navigation.md
│           ├── properties.md
│           ├── advanced.md
│           └── developer-tools.md
└── README.md
```

## Components

### Skill: obsidian-cli

Provides comprehensive knowledge of all Obsidian CLI commands. Automatically activates when you make Obsidian-related requests and executes the appropriate CLI commands.

**Trigger examples:** "create a note", "search vault", "add to daily note", "check backlinks", etc.

### Command: /obsidian

Takes natural language input and translates it into the appropriate `obsidian` CLI command(s) for execution.

## License

MIT
