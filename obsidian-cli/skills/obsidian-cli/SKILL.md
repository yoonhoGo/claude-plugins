---
name: obsidian-cli
description: >-
  This skill should be used when the user asks to "create a note in Obsidian",
  "search my vault", "add to daily note", "read obsidian note", "find notes with tag",
  "manage Obsidian properties", "check backlinks", "find orphan notes",
  "append to note", "open note in Obsidian", "list tasks in vault",
  "manage Obsidian plugins", "sync Obsidian vault",
  or any interaction with Obsidian vault through the CLI.
  Provides comprehensive Obsidian CLI command reference and usage patterns.
version: 0.1.0
---

# Obsidian CLI Integration

## Overview

Obsidian CLI enables terminal-based control of Obsidian for note management, knowledge search, and vault automation. The `obsidian` command communicates with a running Obsidian instance to execute operations on vaults.

**Prerequisites:**
- Obsidian 1.12+ running (CLI communicates with the app)
- `obsidian` binary in PATH (auto-configured on install)
- Catalyst license for early access

## Core Concepts

### Command Syntax

Execute commands in single-shot mode:

```bash
obsidian <command> [parameters] [flags]
```

- **Parameters:** `name=value` format (quote values with spaces)
- **Flags:** Boolean switches (no value needed)
- **File targeting:** `file=<name>` (wikilink resolution) or `path=<exact-path>`
- **Vault selection:** `vault=<name>` to target specific vault
- **Newlines:** Use `\n` for line breaks, `\t` for tabs in content

### Output Handling

CLI output is plain text. Parse results directly from stdout. Errors go to stderr. Exit code 0 indicates success.

## Command Categories

### File Management

Core CRUD operations on vault notes:

| Command | Purpose | Key Parameters |
|---------|---------|----------------|
| `create` | Create new note | `file=`, `content=`, `template=` |
| `read` | Read note content | `file=` or `path=` |
| `append` | Add content to end | `file=`, `content=` |
| `prepend` | Add content to start | `file=`, `content=` |
| `move` | Rename/relocate note | `file=`, `to=` |
| `delete` | Remove note | `file=`, `permanent` (flag) |
| `open` | Open in Obsidian editor | `file=` |

```bash
# Create a note
obsidian create file="meeting-notes/2024-01-15" content="# Meeting Notes\n\nAttendees: ..."

# Read a note
obsidian read file="project-plan"

# Append to existing note
obsidian append file="log" content="\n## Update\nNew progress..."
```

### Daily Notes

Shorthand commands for daily note operations:

| Command | Purpose |
|---------|---------|
| `daily` | Open/create today's daily note |
| `daily:read` | Read today's daily note content |
| `daily:append` | Append to today's daily note |
| `daily:prepend` | Prepend to today's daily note |

```bash
# Add a log entry to today's daily note
obsidian daily:append content="\n- 14:30 Completed feature implementation"

# Read today's daily note
obsidian daily:read
```

### Search & Navigation

Query vault content and analyze note relationships:

| Command | Purpose | Key Parameters |
|---------|---------|----------------|
| `search` | Text search across vault | `query=` |
| `tags` | List all tags with counts | - |
| `tasks` | List/filter tasks | `status=`, `file=` |
| `backlinks` | Find notes linking to target | `file=` |
| `links` | Find outgoing links from note | `file=` |
| `orphans` | Find unlinked notes | - |
| `deadends` | Find notes with no outgoing links | - |

```bash
# Search for content
obsidian search query="authentication flow"

# Find all tasks
obsidian tasks

# Check what links to a note
obsidian backlinks file="api-design"
```

### Properties (Metadata)

Manage YAML frontmatter properties:

```bash
# Set a property
obsidian property set file="note" name="status" value="in-progress"

# Read properties
obsidian property read file="note"

# Remove a property
obsidian property remove file="note" name="draft"
```

### Advanced Features

For publish, sync, plugins, themes, and workspaces — see reference files below.

## Common Workflows

### Development Note-Taking

```bash
# Start of day: check daily note
obsidian daily:read

# Log progress during work
obsidian daily:append content="\n- Implemented user auth module"

# Create a decision record
obsidian create file="decisions/ADR-005-auth-strategy" \
  content="# ADR-005: Authentication Strategy\n\n## Status\nProposed\n\n## Context\n..."
```

### Knowledge Search

```bash
# Find relevant notes
obsidian search query="database migration"

# Check related notes via backlinks
obsidian backlinks file="database-schema"

# Find isolated knowledge
obsidian orphans
```

### Task Management

```bash
# List incomplete tasks
obsidian tasks status=incomplete

# List tasks from daily note
obsidian tasks file=daily

# List all tasks in a specific note
obsidian tasks file="project-plan"
```

## Best Practices

1. **Quote values with spaces:** `file="my note"` not `file=my note`
2. **Use wikilink-style file targeting:** `file=note-name` resolves like `[[note-name]]`
3. **Use path= for exact matches:** When multiple notes share a name
4. **Escape newlines:** Use `\n` in content parameters for multi-line content
5. **Check vault selection:** Use `vault=name` when working with multiple vaults
6. **Prefer append/prepend over create:** To avoid overwriting existing notes

## Error Handling

- If Obsidian is not running, CLI commands will fail — prompt user to start Obsidian
- If the `obsidian` command is not found or cannot be executed, guide the user to check:
  1. **Obsidian version:** CLI requires Obsidian **1.12 or later**. Run Obsidian and check `Settings → General → Current version`
  2. **Early Access:** Obsidian CLI is available through the **Catalyst** early access program. The user needs a Catalyst license and must enable **"Receive early access versions"** in `Settings → General → App`
  3. After updating, restart Obsidian and verify the `obsidian` binary is available in PATH
- If a file is not found, suggest using `search` to locate the correct note
- If vault is ambiguous, use `vault=` parameter to specify

## Additional Resources

### Reference Files

For detailed command documentation, consult:
- **`references/file-management.md`** — Complete file CRUD operations with all parameters and examples
- **`references/daily-notes.md`** — Daily note workflows and automation patterns
- **`references/search-navigation.md`** — Search, tags, tasks, backlinks, links, orphans, deadends
- **`references/properties.md`** — YAML frontmatter property management
- **`references/advanced.md`** — Publish, Sync, Plugins, Themes, Workspaces commands
- **`references/developer-tools.md`** — dev:screenshot, dev:eval, dev:console, plugin:reload
