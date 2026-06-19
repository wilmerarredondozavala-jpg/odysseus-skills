---
name: polymarket
description: "Query Polymarket: markets, prices, orderbooks, history."
---

# Polymarket - Prediction Market Data

## When to use
When you need to query prediction market data from Polymarket (probabilities, volume, history).

## How

### Three Public APIs (No Auth Required)
1. **Gamma API** — `gamma-api.polymarket.com` (discovery, search)
2. **CLOB API** — `clob.polymarket.com` (real-time prices, orderbooks)
3. **Data API** — `data-api.polymarket.com` (trades, open interest)

### Key Concepts
- **Events** contain one or more **Markets** (1:many)
- **Markets** are binary outcomes with Yes/No prices (0.00-1.00)
- Prices ARE probabilities: 0.65 = 65%
- `outcomePrices`: JSON array like `["0.80", "0.20"]`
- Volume in USDC

### Typical Workflow
1. Search with Gamma API
2. Parse response — extract events and nested markets
3. Present: question, prices as %, volume
4. Deep dive: orderbook, price history

### Example Queries
```bash
# Search events
curl -s "https://gamma-api.polymarket.com/events?active=true&closed=false&limit=20"

# Get market details
curl -s "https://gamma-api.polymarket.com/markets?limit=10&active=true"

# Price history
curl -s "https://data-api.polymarket.com/prices?market={tokenId}"
```

### Rate Limits
- Gamma: 4,000 req/10s
- CLOB: 9,000 req/10s
- Data: 1,000 req/10s

### Limitations
- Read-only (no trading)
- Trading requires wallet-based crypto auth
