# Developer Tools Commands

Reference for Obsidian CLI developer and debugging commands.

## Overview

Developer tools provide programmatic access to Obsidian's internal state, useful for plugin development, debugging, and automation.

## dev:screenshot

Capture a screenshot of the Obsidian application window.

**Syntax:**
```bash
obsidian dev:screenshot [path=<output-path>]
```

**Examples:**
```bash
# Capture screenshot
obsidian dev:screenshot

# Save to specific path
obsidian dev:screenshot path="~/screenshots/obsidian-state.png"
```

**Tips:**
- Captures the current state of the Obsidian window
- Useful for documentation, bug reports, or UI testing
- Default save location depends on OS configuration

## dev:eval

Execute JavaScript code in Obsidian's application console.

**Syntax:**
```bash
obsidian dev:eval code=<javascript>
```

**Examples:**
```bash
# Get active file name
obsidian dev:eval code="app.workspace.getActiveFile()?.basename"

# Count open tabs
obsidian dev:eval code="app.workspace.getLeavesOfType('markdown').length"

# Get vault name
obsidian dev:eval code="app.vault.getName()"

# List all loaded plugins
obsidian dev:eval code="Object.keys(app.plugins.plugins).join('\n')"

# Get current theme
obsidian dev:eval code="app.vault.config?.cssTheme || 'Default'"
```

**Tips:**
- Full access to Obsidian's `app` object and API
- Returns the evaluated result as string
- Useful for querying app state not exposed through other CLI commands
- Exercise caution — `dev:eval` can modify application state
- Refer to Obsidian API documentation for available methods

## dev:console

View captured console messages from Obsidian.

**Syntax:**
```bash
obsidian dev:console
```

**Tips:**
- Shows `console.log`, `console.warn`, `console.error` output
- Useful for debugging plugins or observing app behavior
- Messages are captured from the Obsidian renderer process

## dev:css

Inspect CSS rules and their source locations.

**Syntax:**
```bash
obsidian dev:css [selector=<css-selector>]
```

**Examples:**
```bash
# Inspect CSS for a selector
obsidian dev:css selector=".workspace-leaf"

# Check theme CSS
obsidian dev:css selector=".markdown-preview-view"
```

**Tips:**
- Shows computed CSS rules with source file information
- Useful for theme development and CSS snippet creation
- Identifies which file/plugin contributes a specific style

## plugin:reload

Reload a specific plugin during development.

**Syntax:**
```bash
obsidian plugin:reload id=<plugin-id>
```

**Examples:**
```bash
# Reload a plugin being developed
obsidian plugin:reload id="my-plugin"
```

**Tips:**
- Essential for Obsidian plugin development workflow
- Reloads without restarting Obsidian
- Plugin must already be installed and enabled
- Picks up code changes immediately

## Common Developer Workflows

### Plugin Development Cycle

```bash
# Build plugin (in plugin project directory)
npm run build

# Reload in Obsidian
obsidian plugin:reload id="my-plugin"

# Check for errors
obsidian dev:console

# Verify UI state
obsidian dev:screenshot path="./screenshots/after-change.png"
```

### Debugging

```bash
# Check console for errors
obsidian dev:console

# Inspect app state
obsidian dev:eval code="app.workspace.getActiveFile()?.path"
obsidian dev:eval code="app.vault.getFiles().length"

# Check CSS conflicts
obsidian dev:css selector=".my-plugin-element"
```

### Vault Inspection

```bash
# Count total files
obsidian dev:eval code="app.vault.getFiles().length"

# Count markdown files
obsidian dev:eval code="app.vault.getMarkdownFiles().length"

# Get vault config
obsidian dev:eval code="JSON.stringify(app.vault.config, null, 2)"
```
