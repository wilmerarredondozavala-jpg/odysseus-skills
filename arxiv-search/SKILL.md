---
name: arxiv-search
description: "Search arXiv papers by keyword, author, category, or ID."
---

# arXiv Research

## When to use
When you need to search academic papers on arXiv by keyword, author, or category.

## How

### Basic Search
```bash
curl -s "https://export.arxiv.org/api/query?search_query=all:transformer+attention&max_results=5"
```

### Clean Output
```bash
curl -s "https://export.arxiv.org/api/query?search_query=all:GRPO+reinforcement+learning&max_results=5&sortBy=submittedDate&sortOrder=descending" | python3 -c "
import sys, xml.etree.ElementTree as ET
ns = {'a': 'http://www.w3.org/2005/Atom'}
root = ET.parse(sys.stdin).getroot()
for i, entry in enumerate(root.findall('a:entry', ns)):
    title = entry.find('a:title', ns).text.strip().replace('\n', ' ')
    arxiv_id = entry.find('a:id', ns).text.strip().split('/abs/')[-1]
    published = entry.find('a:published', ns).text[:10]
    authors = ', '.join(a.find('a:name', ns).text for a in entry.findall('a:author', ns))
    summary = entry.find('a:summary', ns).text.strip()[:200]
    print(f'{i+1}. [{arxiv_id}] {title}')
    print(f'   Authors: {authors}')
    print(f'   Published: {published}')
    print(f'   Abstract: {summary}...')
    print(f'   PDF: https://arxiv.org/pdf/{arxiv_id}')
    print()
"
```

### Search Syntax
- `all:` — all fields
- `ti:` — title
- `au:` — author
- `abs:` — abstract
- `cat:` — category (cs.AI, cs.CL, cs.CV, cs.LG)
- Boolean: `AND`, `OR`, `ANDNOT`
- Exact phrase: `ti:"chain of thought"`

### Sort and Pagination
- `sortBy=relevance|lastUpdatedDate|submittedDate`
- `sortOrder=ascending|descending`
- `start=0` (offset)
- `max_results=10` (max 30000)

### Semantic Scholar API (Citations, Recommendations)
```bash
# Paper details
curl -s "https://api.semanticscholar.org/graph/v1/paper/arXiv:2402.03300?fields=title,authors,citationCount,abstract"

# Citations
curl -s "https://api.semanticscholar.org/graph/v1/paper/arXiv:2402.03300/citations?fields=title,year&limit=10"

# Recommendations
curl -s -X POST "https://api.semanticscholar.org/recommendations/v1/papers/"   -H "Content-Type: application/json"   -d '{"positivePaperIds": ["arXiv:2402.03300"]}'
```

### Rate Limits
- arXiv: ~1 req/3 seconds
- Semantic Scholar: ~1 req/second
