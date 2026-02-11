# Properties (Metadata) Commands

Complete reference for managing YAML frontmatter properties on Obsidian notes.

## Overview

Properties are YAML frontmatter fields at the top of notes. Obsidian CLI provides commands to set, read, and remove properties without manually editing the frontmatter block.

```yaml
---
title: My Note
status: in-progress
tags:
  - project
  - architecture
created: 2024-01-15
---
```

## property set

Set or update a property on a note.

**Syntax:**
```bash
obsidian property set file=<name> name=<property> value=<value> [vault=<name>]
```

**Parameters:**
| Parameter | Required | Description |
|-----------|----------|-------------|
| `file` | Yes | Target note |
| `name` | Yes | Property name |
| `value` | Yes | Property value |
| `vault` | No | Target vault |

**Examples:**
```bash
# Set a status property
obsidian property set file="feature-spec" name="status" value="approved"

# Set a date property
obsidian property set file="meeting-notes" name="date" value="2024-01-15"

# Set tags (as comma-separated or list)
obsidian property set file="note" name="tags" value="project, architecture"

# Set numeric value
obsidian property set file="sprint" name="story-points" value="5"
```

**Tips:**
- Creates frontmatter block if none exists
- Overwrites existing property value
- Values are stored as strings by default
- Obsidian interprets certain property types (dates, tags, links) based on property name

## property read

Read all properties from a note.

**Syntax:**
```bash
obsidian property read file=<name> [vault=<name>]
```

**Examples:**
```bash
# Read all properties
obsidian property read file="project-plan"

# Read from specific vault
obsidian property read file="config" vault="Work"
```

**Output:** Key-value pairs of all frontmatter properties.

**Tips:**
- Returns all properties defined in the note's frontmatter
- Returns empty/error if note has no frontmatter

## property remove

Remove a property from a note.

**Syntax:**
```bash
obsidian property remove file=<name> name=<property> [vault=<name>]
```

**Examples:**
```bash
# Remove a property
obsidian property remove file="draft" name="draft"

# Remove status
obsidian property remove file="task" name="assigned-to"
```

**Tips:**
- Removes the property entirely from frontmatter
- Does not affect other properties
- No error if property doesn't exist

## Common Workflows

### Project Tracking

```bash
# Set project status
obsidian property set file="projects/auth-service" name="status" value="in-progress"
obsidian property set file="projects/auth-service" name="priority" value="high"
obsidian property set file="projects/auth-service" name="assignee" value="yoonho"

# Mark as complete
obsidian property set file="projects/auth-service" name="status" value="complete"
obsidian property set file="projects/auth-service" name="completed" value="2024-01-20"
```

### Note Metadata Management

```bash
# Add metadata to a new note
obsidian property set file="architecture-decision" name="type" value="ADR"
obsidian property set file="architecture-decision" name="status" value="proposed"
obsidian property set file="architecture-decision" name="date" value="2024-01-15"
obsidian property set file="architecture-decision" name="tags" value="architecture, decision"

# Review metadata
obsidian property read file="architecture-decision"
```

### Workflow Automation

```bash
# Mark notes as reviewed
obsidian property set file="spec-doc" name="reviewed" value="true"
obsidian property set file="spec-doc" name="reviewed-by" value="yoonho"
obsidian property set file="spec-doc" name="reviewed-date" value="2024-01-15"

# Clean up temporary properties
obsidian property remove file="spec-doc" name="needs-review"
```
