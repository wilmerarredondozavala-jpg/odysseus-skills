---
name: notion-api
description: "Notion API: pages, databases, blocks management."
---

# Notion API

## When to use
When you need to create, edit, or manage pages, databases, and content in Notion.

## How

### API Base
`https://api.notion.com/v1/`

### Headers
```
Authorization: Bearer {integration_token}
Notion-Version: 2022-06-28
```

### Pages
```bash
# Create page
curl -s -X POST https://api.notion.com/v1/pages   -H "Authorization: Bearer $NOTION_TOKEN"   -H "Notion-Version: 2022-06-28"   -d '{
    "parent": {"database_id": "..."},
    "properties": {
      "Name": {"title": [{"text": {"content": "New Page"}}]},
      "Status": {"select": {"name": "In Progress"}}
    }
  }'

# Update page
curl -s -X PATCH https://api.notion.com/v1/pages/PAGE_ID   -H "Authorization: Bearer $NOTION_TOKEN"   -d '{"properties": {"Status": {"select": {"name": "Done"}}}}'
```

### Databases
```bash
# Query database
curl -s -X POST https://api.notion.com/v1/databases/DB_ID/query   -H "Authorization: Bearer $NOTION_TOKEN"   -d '{
    "filter": {
      "and": [
        {"property": "Status", "select": {"equals": "Active"}},
        {"property": "Priority", "number": {"greater_than": 3}}
      ]
    },
    "sorts": [{"property": "Created", "direction": "descending"}]
  }'
```

### Blocks
```bash
# Append blocks to page
curl -s -X PATCH https://api.notion.com/v1/blocks/PAGE_ID/children   -H "Authorization: Bearer $NOTION_TOKEN"   -d '{
    "children": [
      {"object": "block", "type": "heading_2", "heading_2": {"rich_text": [{"text": {"content": "Section"}}]}},
      {"object": "block", "type": "paragraph", "paragraph": {"rich_text": [{"text": {"content": "Content"}}]}}
    ]
  }'
```

### ntn CLI
Use `ntn` CLI for terminal operations on Notion.
