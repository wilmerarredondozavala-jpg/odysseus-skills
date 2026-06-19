---
name: obsidian-cli
description: "Interact with Obsidian vaults using the Obsidian CLI."
---

# Obsidian CLI

## When to use
When you need to interact with a running Obsidian instance from the command line.

## How

### Syntax
- Parameters: `key="value"` (quote values with spaces)
- Flags: boolean switches without values
- Multiline: use `\n` for newline, `\t` for tab

### File Targeting
- `file="Name"` — resolves like wikilink
- `path="folder/note.md"` — exact path from vault root

### Common Commands
```bash
obsidian read file="My Note"
obsidian create name="New Note" content="# Hello" silent
obsidian append file="My Note" content="New line"
obsidian search query="search term" limit=10
obsidian daily:read
obsidian daily:append content="- [ ] New task"
obsidian property:set name="status" value="done" file="My Note"
obsidian tasks daily todo
obsidian tags sort=count counts
obsidian backlinks file="My Note"
```

### Useful Flags
- `--copy` — copy output to clipboard
- `silent` — prevent files from opening
- `total` — get count on list commands

### Plugin Development
```bash
obsidian plugin:reload id=my-plugin
obsidian dev:errors
obsidian dev:screenshot path=screenshot.png
obsidian dev:dom selector=".workspace-leaf" text
obsidian dev:console level=error
obsidian eval code="app.vault.getFiles().length"
```
