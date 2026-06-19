---
name: github-issues
description: "Create, triage, label, assign GitHub issues via gh or REST."
---

# GitHub Issues Management

## When to use
When you need to create, search, triage, or manage GitHub issues.

## How

### Viewing Issues
```bash
# With gh
gh issue list --state open --label "bug"
gh issue list --assignee @me
gh issue view 42

# With curl
curl -s -H "Authorization: token $GITHUB_TOKEN"   "https://api.github.com/repos/$OWNER/$REPO/issues?state=open"
```

### Creating Issues
```bash
# With gh
gh issue create --title "Bug description" --body "Details..." --label "bug" --assignee "user"

# With curl
curl -s -X POST   -H "Authorization: token $GITHUB_TOKEN"   https://api.github.com/repos/$OWNER/$REPO/issues   -d '{"title":"Bug","body":"Details","labels":["bug"]}'
```

### Managing Issues
```bash
# Labels
gh issue edit 42 --add-label "priority:high"
gh issue edit 42 --remove-label "needs-triage"

# Assignment
gh issue edit 42 --add-assignee username

# Comment
gh issue comment 42 --body "Investigated — working on fix."

# Close/Reopen
gh issue close 42
gh issue reopen 42
```

### Bug Report Template
```
## Bug Description
What's happening

## Steps to Reproduce
1. Step 1
2. Step 2

## Expected Behavior
What should happen

## Actual Behavior
What actually happens

## Environment
- OS: ...
- Version: ...
```

### Triage Workflow
1. List untriaged issues
2. Read and categorize each
3. Apply labels and priority
4. Assign if clear owner
5. Comment with triage notes
