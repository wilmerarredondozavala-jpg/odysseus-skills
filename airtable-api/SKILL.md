---
name: airtable-api
description: "Airtable REST API: records CRUD, filters, upserts."
---

# Airtable REST API

## When to use
When you need to manage records, filters, and views in Airtable via REST API.

## How

### API Base
`https://api.airtable.com/v0/{baseId}/{tableName}`

### Headers
```
Authorization: Bearer {api_token}
```

### CRUD Operations
```bash
# List records
curl -s "https://api.airtable.com/v0/{baseId}/{tableName}"   -H "Authorization: Bearer $AIRTABLE_TOKEN"

# Create record
curl -s -X POST "https://api.airtable.com/v0/{baseId}/{tableName}"   -H "Authorization: Bearer $AIRTABLE_TOKEN"   -d '{"fields": {"Name": "Item", "Status": "Active"}}'

# Update record
curl -s -X PATCH "https://api.airtable.com/v0/{baseId}/{tableName}"   -H "Authorization: Bearer $AIRTABLE_TOKEN"   -d '{"fields": {"Status": "Done"}}'

# Delete record
curl -s -X DELETE "https://api.airtable.com/v0/{baseId}/{tableName}/recXXXX"   -H "Authorization: Bearer $AIRTABLE_TOKEN"
```

### Filters
```bash
# filterByFormula
curl -s "https://api.airtable.com/v0/{baseId}/{tableName}?filterByFormula=AND({Status}='Active',{Priority}>3)"   -H "Authorization: Bearer $AIRTABLE_TOKEN"

# Sort
curl -s "https://api.airtable.com/v0/{baseId}/{tableName}?sort[0][field]=Name&sort[0][direction]=asc"   -H "Authorization: Bearer $AIRTABLE_TOKEN"
```

### Pagination
Use `offset` from response for next page.

### Upsert Pattern
1. Search for existing record by unique field
2. If found → PATCH (update)
3. If not found → POST (create)

### Rate Limit
5 requests/second.
