# File Management Commands

Complete reference for Obsidian CLI file operations.

## create

Create a new note in the vault.

**Syntax:**
```bash
obsidian create file=<name> [content=<text>] [template=<template-name>] [overwrite]
```

**Parameters:**
| Parameter | Required | Description |
|-----------|----------|-------------|
| `file` | Yes | Note name or path (without `.md` extension) |
| `content` | No | Initial content for the note |
| `template` | No | Template to use for note creation |
| `overwrite` | No | Flag — overwrite if note already exists |

**Examples:**
```bash
# Simple note
obsidian create file="quick-note"

# Note with content
obsidian create file="meetings/standup-2024-01-15" content="# Standup\n\n## Updates\n- ..."

# Note from template
obsidian create file="projects/new-project" template="project-template"

# Overwrite existing
obsidian create file="scratch" content="Fresh start" overwrite
```

**Tips:**
- Directories are created automatically (e.g., `file="new-folder/note"`)
- Without `content` or `template`, creates an empty note
- `template` refers to templates configured in Obsidian's Templates core plugin
- Use `\n` for newlines in content

## read

Read the content of an existing note.

**Syntax:**
```bash
obsidian read file=<name>
obsidian read path=<exact-path>
```

**Parameters:**
| Parameter | Required | Description |
|-----------|----------|-------------|
| `file` | Yes* | Note name (wikilink resolution) |
| `path` | Yes* | Exact path from vault root |

*Use either `file` or `path`, not both.

**Examples:**
```bash
# Read by name (wikilink resolution)
obsidian read file="project-plan"

# Read by exact path
obsidian read path="projects/2024/project-plan.md"
```

**Tips:**
- `file=` uses wikilink-style resolution (matches shortest unique path)
- `path=` requires exact path from vault root including `.md`
- Output is the raw Markdown content including frontmatter

## append

Add content to the end of an existing note.

**Syntax:**
```bash
obsidian append file=<name> content=<text>
```

**Parameters:**
| Parameter | Required | Description |
|-----------|----------|-------------|
| `file` | Yes | Target note name |
| `content` | Yes | Content to append |

**Examples:**
```bash
# Append a log entry
obsidian append file="changelog" content="\n\n## v1.2.0\n- Added new feature"

# Append a task
obsidian append file="todo" content="\n- [ ] Review PR #123"
```

## prepend

Add content to the beginning of a note (after frontmatter if present).

**Syntax:**
```bash
obsidian prepend file=<name> content=<text>
```

**Parameters:**
| Parameter | Required | Description |
|-----------|----------|-------------|
| `file` | Yes | Target note name |
| `content` | Yes | Content to prepend |

**Examples:**
```bash
# Prepend an important notice
obsidian prepend file="readme" content=">[!warning] This document is outdated\n\n"
```

**Tips:**
- Content is inserted after YAML frontmatter (if present), before existing body

## move

Rename or relocate a note within the vault.

**Syntax:**
```bash
obsidian move file=<name> to=<new-name-or-path>
```

**Parameters:**
| Parameter | Required | Description |
|-----------|----------|-------------|
| `file` | Yes | Current note name |
| `to` | Yes | New name or path |

**Examples:**
```bash
# Rename
obsidian move file="draft" to="final-report"

# Move to different folder
obsidian move file="inbox/note" to="processed/note"

# Rename and move
obsidian move file="old-name" to="archive/new-name"
```

**Tips:**
- Obsidian automatically updates all internal links pointing to the moved note
- Target directories are created automatically

## delete

Remove a note from the vault.

**Syntax:**
```bash
obsidian delete file=<name> [permanent]
```

**Parameters:**
| Parameter | Required | Description |
|-----------|----------|-------------|
| `file` | Yes | Note to delete |
| `permanent` | No | Flag — permanently delete instead of trash |

**Examples:**
```bash
# Move to trash (recoverable)
obsidian delete file="scratch-note"

# Permanently delete
obsidian delete file="sensitive-data" permanent
```

**Tips:**
- Without `permanent` flag, note moves to system trash (recoverable)
- With `permanent`, note is permanently deleted (not recoverable)

## open

Open a note in the Obsidian editor (brings Obsidian to focus).

**Syntax:**
```bash
obsidian open file=<name>
```

**Examples:**
```bash
obsidian open file="project-plan"
```

**Tips:**
- Brings Obsidian app to foreground
- Opens the note in the active editor pane

## Vault Selection

All file commands support `vault=` parameter to target a specific vault:

```bash
obsidian read file="note" vault="Work"
obsidian create file="idea" content="..." vault="Personal"
```

When `vault=` is omitted, the CLI uses the most recently active vault.
