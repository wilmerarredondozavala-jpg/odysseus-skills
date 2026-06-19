---
name: spike
description: "Throwaway experiments to validate an idea before build."
---

# Spike — Throwaway Experiments

## When to use
When you need to validate an idea before committing to a real build — feasibility, approach comparison, unknown discovery.

## How

### Core Method
```
decompose → research → build → verdict
   ↑________________________________↓
```

### 1. Decompose
Break into 2-5 independent feasibility questions. Present as table:

| # | Spike | Validates (Given/When/Then) | Risk |
|---|-------|----------------------------|------|
| 001 | websocket-streaming | Given WS connection, when LLM streams, then client receives <100ms | High |
| 002a | pdf-parse-pdfjs | Given multi-page PDF, when parsed with pdfjs, then structured text | Medium |
| 002b | pdf-parse-camelot | Given multi-page PDF, when parsed with camelot, then structured text | Medium |

Order by risk. Most likely to kill the idea runs first.

### 2. Research (per spike)
1. Brief: 2-3 sentences on what and why
2. Surface competing approaches
3. Pick one, state why

### 3. Build
- One directory per spike: `spikes/NNN-descriptive-name/`
- Bias toward interactive output (CLI > HTML > server > test)
- Depth over speed — test edge cases
- Hardcode everything, no complex setup

### 4. Verdict
```markdown
## Verdict: VALIDATED | PARTIAL | INVALIDATED

### What worked
- ...

### What didn't
- ...

### Surprises
- ...

### Recommendation for the real build
- ...
```

### Comparison Spikes
Build back-to-back, then head-to-head comparison table.

### Output
- `spikes/` directory in repo root
- One dir per spike with README.md
- Keep code throwaway — if it takes 2 days to clean up, it was a bad spike
