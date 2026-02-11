# Search & Navigation Commands

Complete reference for Obsidian CLI search and vault navigation operations.

## search

Full-text search across vault content.

**Syntax:**
```bash
obsidian search query=<text> [vault=<name>]
```

**Parameters:**
| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search text (matches note content and titles) |
| `vault` | No | Target vault name |

**Examples:**
```bash
# Basic search
obsidian search query="authentication"

# Multi-word search
obsidian search query="database migration strategy"

# Search in specific vault
obsidian search query="API design" vault="Work"
```

**Tips:**
- Returns matching notes with context snippets
- Matches both note titles and content
- Quote queries containing spaces

## tags

List all tags in the vault with occurrence counts.

**Syntax:**
```bash
obsidian tags [vault=<name>]
```

**Examples:**
```bash
# List all tags
obsidian tags

# Tags in specific vault
obsidian tags vault="Personal"
```

**Output:** List of tags with counts, e.g.:
```
#project (45)
#meeting (32)
#todo (28)
#idea (15)
```

**Tips:**
- Includes both inline tags (`#tag`) and frontmatter tags
- Useful for understanding vault taxonomy and finding related content

## tasks

List and filter tasks (checkboxes) across the vault.

**Syntax:**
```bash
obsidian tasks [status=<complete|incomplete>] [file=<name>|daily] [vault=<name>]
```

**Parameters:**
| Parameter | Required | Description |
|-----------|----------|-------------|
| `status` | No | Filter: `complete` or `incomplete` |
| `file` | No | Filter by note name, or `daily` for today's note |
| `vault` | No | Target vault name |

**Examples:**
```bash
# All tasks
obsidian tasks

# Only incomplete tasks
obsidian tasks status=incomplete

# Tasks from specific note
obsidian tasks file="project-plan"

# Tasks from today's daily note
obsidian tasks file=daily

# Complete tasks in specific vault
obsidian tasks status=complete vault="Work"
```

**Tips:**
- Tasks are Markdown checkboxes: `- [ ]` (incomplete) and `- [x]` (complete)
- `file=daily` is a special shortcut for today's daily note
- Output includes file location and task text

## backlinks

Find all notes that link TO a target note.

**Syntax:**
```bash
obsidian backlinks file=<name> [vault=<name>]
```

**Examples:**
```bash
# Find what links to "api-design"
obsidian backlinks file="api-design"

# Backlinks for a note in specific vault
obsidian backlinks file="architecture" vault="Work"
```

**Tips:**
- Shows notes containing `[[target-note]]` wikilinks
- Useful for understanding note importance and relationships
- High backlink count indicates a hub/index note

## links

Find all outgoing links FROM a note.

**Syntax:**
```bash
obsidian links file=<name> [vault=<name>]
```

**Examples:**
```bash
# See what "project-plan" links to
obsidian links file="project-plan"
```

**Tips:**
- Shows all `[[wikilinks]]` contained in the note
- Complementary to `backlinks` — together they map the full link graph
- Useful for understanding note dependencies

## orphans

Find notes with no incoming links (not linked to by any other note).

**Syntax:**
```bash
obsidian orphans [vault=<name>]
```

**Examples:**
```bash
# Find orphan notes
obsidian orphans
```

**Tips:**
- Orphan notes may be:
  - Newly created and not yet integrated
  - Forgotten/abandoned notes
  - Entry points that don't need backlinks (e.g., MOCs, index notes)
- Review orphans periodically to maintain vault health
- Consider linking orphans into relevant notes or deleting unused ones

## deadends

Find notes with no outgoing links (don't link to any other note).

**Syntax:**
```bash
obsidian deadends [vault=<name>]
```

**Examples:**
```bash
# Find dead-end notes
obsidian deadends
```

**Tips:**
- Dead-end notes may benefit from adding links to related content
- Not necessarily a problem — some notes are self-contained (e.g., reference tables)
- Useful for identifying notes that could be better connected

## Common Workflows

### Knowledge Discovery

```bash
# Start with a search
obsidian search query="microservices"

# Explore related notes via backlinks
obsidian backlinks file="microservices-architecture"

# Check outgoing connections
obsidian links file="microservices-architecture"

# Find potentially related but unlinked notes
obsidian orphans
```

### Vault Health Check

```bash
# Check for disconnected notes
obsidian orphans
obsidian deadends

# Review tag taxonomy
obsidian tags

# Check outstanding tasks
obsidian tasks status=incomplete
```

### Project Status

```bash
# Find all project-related notes
obsidian search query="Project Alpha"

# Check project tasks
obsidian tasks file="projects/alpha/plan"

# See what references the project
obsidian backlinks file="projects/alpha/plan"
```
