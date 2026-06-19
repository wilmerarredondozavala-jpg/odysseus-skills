---
name: github-code-review
description: "Review PRs: diffs, inline comments via gh or REST."
---

# GitHub Code Review

## When to use
When you need to review code locally or review PRs on GitHub with inline comments and approvals.

## How

### Local Review (Pre-Push)
```bash
git diff main...HEAD --stat      # Scope of changes
git diff main...HEAD             # Full diff
git diff main...HEAD --name-only # File names only

# Check for issues
git diff main...HEAD | grep -n "print(\|console.log\|TODO\|FIXME"
git diff main...HEAD | grep -in "password\|secret\|api_key\|token.*="
```

### Review Checklist
- **Correctness** — Does it do what it claims? Edge cases?
- **Security** — No hardcoded secrets, input validation, SQL injection?
- **Code Quality** — Clear naming, DRY, single responsibility?
- **Testing** — New code paths tested? Happy path + errors?
- **Performance** — No N+1 queries, unnecessary loops?
- **Documentation** — Public APIs documented, "why" comments?

### Review Output Format
```
## Code Review Summary

### Critical
- **file.py:45** — SQL injection vulnerability

### Warnings
- **file.py:23** — Password stored in plaintext

### Suggestions
- **file.py:8** — Duplicated logic, consider consolidating

### Looks Good
- Clean separation of concerns
- Good test coverage
```

### PR Review on GitHub
```bash
# Checkout PR locally
git fetch origin pull/123/head:pr-123
git checkout pr-123

# Leave comment
gh pr comment 123 --body "Looks good overall."

# Approve
gh pr review 123 --approve --body "LGTM!"

# Request changes
gh pr review 123 --request-changes --body "See inline comments."
```

### Inline Comments (curl)
```bash
HEAD_SHA=$(curl -s -H "Authorization: token $GITHUB_TOKEN"   https://api.github.com/repos/$OWNER/$REPO/pulls/123   | python3 -c "import sys,json; print(json.load(sys.stdin)['head']['sha'])")

curl -s -X POST   -H "Authorization: token $GITHUB_TOKEN"   https://api.github.com/repos/$OWNER/$REPO/pulls/123/comments   -d '{"body":"Use parameterized queries.","path":"src/auth.py","commit_id":"'$HEAD_SHA'","line":45}'
```

### Formal Review with Multiple Comments
```bash
curl -s -X POST   -H "Authorization: token $GITHUB_TOKEN"   https://api.github.com/repos/$OWNER/$REPO/pulls/123/reviews   -d '{
    "commit_id":"'$HEAD_SHA'",
    "event":"REQUEST_CHANGES",
    "body":"Found issues — see inline comments.",
    "comments":[
      {"path":"src/auth.py","line":45,"body":"SQL injection risk."},
      {"path":"src/models.py","line":23,"body":"Hash passwords."}
    ]
  }'
```
Events: `APPROVE`, `REQUEST_CHANGES`, `COMMENT`
