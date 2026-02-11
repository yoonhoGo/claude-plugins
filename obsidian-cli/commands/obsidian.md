---
name: obsidian
description: Execute Obsidian CLI operations using natural language
argument-hint: <natural language instruction>
allowed-tools: Bash(obsidian:*), Read
---

Interpret the user's natural language request and execute the appropriate Obsidian CLI command(s).

**User request:** $ARGUMENTS

## Execution Rules

1. **Translate** the user's natural language request into one or more `obsidian` CLI commands
2. **Execute** commands using Bash tool with the `obsidian` binary
3. **Report** results clearly — summarize output, don't just dump raw text
4. **Chain** multiple commands when the request requires it (e.g., "create a note and add to daily" → `create` then `daily:append`)

## Command Quick Reference

| Category | Commands |
|----------|----------|
| File ops | `create`, `read`, `append`, `prepend`, `move`, `delete`, `open` |
| Daily | `daily`, `daily:read`, `daily:append`, `daily:prepend` |
| Search | `search query=`, `tags`, `tasks`, `backlinks file=`, `links file=`, `orphans`, `deadends` |
| Properties | `property set file= name= value=`, `property read file=`, `property remove file= name=` |
| System | `help`, `version`, `reload`, `restart` |
| Plugins | `plugins`, `plugin install id=`, `plugin enable id=`, `plugin disable id=`, `plugin:reload id=` |
| Dev | `dev:screenshot`, `dev:eval code=`, `dev:console`, `dev:css` |

## Syntax Rules

- Parameters: `name=value` (quote values with spaces: `name="my value"`)
- File targeting: `file=<name>` (wikilink resolution) or `path=<exact-path>`
- Vault selection: `vault=<name>` (omit for default vault)
- Newlines in content: Use `\n`
- Flags: Just the flag name, no value (e.g., `permanent`, `overwrite`)

## Behavior Guidelines

- If the request is ambiguous, ask for clarification before executing
- If a `read` or `search` returns useful content, present it in a formatted, readable way
- If creating/modifying notes, confirm the action taken and show relevant details
- If an error occurs (e.g., Obsidian not running), explain the issue and suggest a fix
- If the `obsidian` command is not found or cannot be executed, inform the user:
  - Obsidian CLI requires **version 1.12+** — check in `Settings → General → Current version`
  - CLI is an early access feature requiring a **Catalyst license** and **"Receive early access versions"** enabled in `Settings → General → App`
  - After updating, restart Obsidian and ensure the `obsidian` binary is in PATH
- For destructive operations (`delete`, `move`), confirm before executing unless the user's intent is explicit
