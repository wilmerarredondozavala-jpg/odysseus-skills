---
name: obsidian-vault
description: "Read, search, create, and edit notes in the Obsidian vault using the Karpathy method."
---

# Obsidian Vault Management

## When to use
When you need to read, create, search, or edit notes in an Obsidian vault. Also for structuring knowledge bases using the Karpathy method.

## How

### Core Operations
- **Read notes:** Use file read tools with the vault's absolute path
- **Create notes:** Use file write tools with full markdown content
- **Search:** Use file search tools for both filenames and content
- **Edit:** Use patch/replace for targeted edits

### Karpathy Method (Vault Structuring)
1. **Atomic notes** — one concept per note, self-contained
2. **MOCs (Maps of Content)** — index notes that link to related atomic notes
3. **Bidirectional links** — use `[[Note Name]]` wikilinks for internal connections
4. **Hierarchical tags** — use nested paths like `sector/luxury`, `project/active`
5. **YAML frontmatter** — every structured note should have:
```yaml
---
title: Note Title
description: What this note covers
tags:
  - tag1
  - nested/tag
aliases:
  - Alternative Name
---
```

### Wikilink Syntax
- `[[Note Name]]` — link to note
- `[[Note Name|Display Text]]` — custom display text
- `[[Note Name#Heading]]` — link to heading
- `[[#Same Note Heading]]` — same-note heading link

### LaTeX Formulas
- Inline: `$e^{i\pi} + 1 = 0$`
- Block: `$$\frac{a}{b} = c$$`

### Block IDs
Add `^block-id` at the end of a paragraph to create a linkable block reference.
