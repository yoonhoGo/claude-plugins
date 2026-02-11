# Daily Notes Commands

Complete reference for Obsidian CLI daily note operations.

## Overview

Daily notes commands provide shorthand access to today's daily note. These commands use the Daily Notes core plugin configuration (date format, folder location, template).

**Prerequisites:** Daily Notes core plugin must be enabled in Obsidian settings.

## daily

Open or create today's daily note.

**Syntax:**
```bash
obsidian daily [vault=<name>]
```

**Behavior:**
- If today's daily note exists → opens it in Obsidian
- If today's daily note doesn't exist → creates it (using configured template) and opens it

**Examples:**
```bash
# Open/create today's daily note
obsidian daily

# In specific vault
obsidian daily vault="Work"
```

## daily:read

Read the content of today's daily note.

**Syntax:**
```bash
obsidian daily:read [vault=<name>]
```

**Examples:**
```bash
# Read today's daily note
obsidian daily:read

# Read from specific vault
obsidian daily:read vault="Personal"
```

**Tips:**
- Returns raw Markdown content including frontmatter
- Fails if today's daily note doesn't exist yet — use `daily` first to create it

## daily:append

Append content to the end of today's daily note.

**Syntax:**
```bash
obsidian daily:append content=<text> [vault=<name>]
```

**Examples:**
```bash
# Add a log entry
obsidian daily:append content="\n- 10:00 Started working on auth module"

# Add a section
obsidian daily:append content="\n\n## Afternoon\n- Code review session\n- Deploy to staging"

# Add a task
obsidian daily:append content="\n- [ ] Follow up on PR feedback"
```

**Tips:**
- Creates the daily note if it doesn't exist
- Content is added at the very end of the note
- Always start with `\n` for clean formatting

## daily:prepend

Insert content at the beginning of today's daily note (after frontmatter).

**Syntax:**
```bash
obsidian daily:prepend content=<text> [vault=<name>]
```

**Examples:**
```bash
# Add priority notice at top
obsidian daily:prepend content=">[!important] Deadline today for Project X\n\n"

# Add morning plan
obsidian daily:prepend content="## Morning Plan\n- [ ] Review PRs\n- [ ] Standup at 10\n\n"
```

**Tips:**
- Content is inserted after YAML frontmatter, before existing body
- Creates the daily note if it doesn't exist

## Common Workflows

### Development Day Log

```bash
# Morning: Check what's on today
obsidian daily:read

# Throughout the day: Log activities
obsidian daily:append content="\n- 09:30 PR #456 reviewed and approved"
obsidian daily:append content="\n- 11:00 Fixed auth token refresh bug"
obsidian daily:append content="\n- 14:00 Paired with @alice on API design"
obsidian daily:append content="\n- 16:30 Deployed v2.1.0 to staging"
```

### Standup Notes

```bash
# Add standup section
obsidian daily:append content="\n\n## Standup\n### Yesterday\n- Completed auth module\n\n### Today\n- Start API integration\n- Code review for team\n\n### Blockers\n- Waiting on DB access credentials"
```

### Quick Capture

```bash
# Capture an idea quickly
obsidian daily:append content="\n\n## Ideas\n- Consider using Redis for session store instead of JWT"

# Capture a meeting note
obsidian daily:append content="\n\n## Meeting: Architecture Review\n- Decision: Move to event-driven architecture\n- Action: @yoonho to draft ADR by Friday"
```
