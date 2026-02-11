# Advanced Commands

Reference for Obsidian CLI publish, sync, plugin, theme, and workspace management.

## Publish Commands

Manage Obsidian Publish site content. Requires Obsidian Publish subscription.

### publish

Publish or unpublish notes to Obsidian Publish site.

```bash
# Publish a note
obsidian publish file=<name>

# Unpublish a note
obsidian unpublish file=<name>
```

**Tips:**
- Requires Obsidian Publish plugin enabled and configured
- Published notes are publicly accessible on the Publish site
- Links between published notes are preserved

## Sync Commands

Monitor and control Obsidian Sync status. Requires Obsidian Sync subscription.

### sync

Check sync status and manage version history.

```bash
# Check sync status
obsidian sync status

# View version history for a file
obsidian sync history file=<name>

# Restore a previous version
obsidian sync restore file=<name> version=<id>
```

**Tips:**
- Requires Obsidian Sync plugin enabled
- Sync operates automatically in background
- Version history allows recovery of previous file states

## Plugin Commands

Manage Obsidian community plugins from the CLI.

### plugins

List, install, enable, disable, and reload plugins.

```bash
# List installed plugins
obsidian plugins

# Install a community plugin
obsidian plugin install id=<plugin-id>

# Enable a plugin
obsidian plugin enable id=<plugin-id>

# Disable a plugin
obsidian plugin disable id=<plugin-id>

# Reload a specific plugin (useful for development)
obsidian plugin:reload id=<plugin-id>
```

**Examples:**
```bash
# List all plugins
obsidian plugins

# Install dataview plugin
obsidian plugin install id="dataview"

# Reload during plugin development
obsidian plugin:reload id="my-custom-plugin"
```

**Tips:**
- `plugin-id` is the community plugin identifier (from Obsidian plugin directory)
- `plugin:reload` is especially useful during Obsidian plugin development
- Enabling/disabling takes effect immediately

## Theme Commands

Manage Obsidian visual themes.

```bash
# List installed themes
obsidian themes

# Install a theme
obsidian theme install name=<theme-name>

# Activate a theme
obsidian theme use name=<theme-name>
```

**Examples:**
```bash
# List available themes
obsidian themes

# Switch to Minimal theme
obsidian theme use name="Minimal"
```

## Workspace Commands

Save, load, and manage workspace layouts (pane arrangements, open files).

```bash
# List saved workspaces
obsidian workspaces

# Save current workspace
obsidian workspace save name=<workspace-name>

# Load a workspace
obsidian workspace load name=<workspace-name>

# Delete a workspace
obsidian workspace delete name=<workspace-name>
```

**Examples:**
```bash
# Save current layout as "coding"
obsidian workspace save name="coding"

# Switch to writing layout
obsidian workspace load name="writing"

# Clean up old workspace
obsidian workspace delete name="old-layout"
```

**Tips:**
- Workspaces preserve pane layout, open files, and sidebar state
- Useful for switching between different work contexts
- Load a workspace to quickly restore a familiar editing environment

## General Commands

### help

Display available commands and usage information.

```bash
obsidian help
obsidian help <command>
```

### version

Show Obsidian version information.

```bash
obsidian version
```

### reload

Refresh the Obsidian app window.

```bash
obsidian reload
```

### restart

Restart the Obsidian application.

```bash
obsidian restart
```
