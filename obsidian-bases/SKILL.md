---
name: obsidian-bases
description: "Create and edit Obsidian Bases (.base files) with views, filters, formulas, and summaries."
---

# Obsidian Bases

## When to use
When creating database-like views of notes in Obsidian with filters, formulas, and multiple view types.

## How

### File Structure (.base files)
```yaml
filters:
  and:
    - 'status == "done"'
    - 'priority > 3'

formulas:
  days_until_due: 'if(due, (date(due) - today()).days, "")'
  is_overdue: 'if(due, date(due) < today() && status != "done", false)'

properties:
  status:
    displayName: Status
  formula.days_until_due:
    displayName: "Days Until Due"

views:
  - type: table
    name: "Active Tasks"
    filters:
      and:
        - 'status != "done"'
    order:
      - file.name
      - status
      - due
      - formula.days_until_due
    summaries:
      formula.days_until_due: Average
```

### Filter Operators
`==`, `!=`, `>`, `<`, `>=`, `<=`, `&&`, `||`, `!`

### Filter Structure
```yaml
filters:
  and:
    - 'status == "done"'
  or:
    - 'file.hasTag("book")'
  not:
    - 'file.hasTag("archived")'
```

### Key Functions
- `date(string)` — parse string to date
- `now()` — current datetime
- `today()` — current date
- `if(condition, trueResult, falseResult?)` — conditional
- `duration(string)` — parse duration

### Duration Type
When subtracting dates, result is Duration (not number). Access `.days`, `.hours`, etc.
```yaml
"(now() - file.ctime).days"  # Days since created
"(date(due) - today()).days"  # Days until due
```

### View Types
- **table** — tabular view with columns
- **cards** — gallery/card view
- **list** — simple list
- **map** — geographic (requires lat/lng + Maps plugin)

### File Properties
`file.name`, `file.path`, `file.folder`, `file.ext`, `file.size`, `file.ctime`, `file.mtime`, `file.tags`, `file.links`, `file.backlinks`

### Default Summaries
Average, Min, Max, Sum, Range, Median, Stddev, Earliest, Latest, Checked, Unchecked, Empty, Filled, Unique

### YAML Quoting Rules
- Use single quotes for formulas with double quotes: `'if(done, "Yes", "No")'`
- Use double quotes for simple strings: `"My View"`
