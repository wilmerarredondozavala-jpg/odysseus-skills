---
name: github-pr-workflow
description: "GitHub PR lifecycle: branch, commit, open, CI, merge."
---

# GitHub Pull Request Workflow

## When to use
When you need to create, review, monitor CI, and merge pull requests.

## How

### 1. Branch Creation
```bash
git fetch origin
git checkout main && git pull origin main
git checkout -b feat/add-feature
```
Naming: `feat/`, `fix/`, `refactor/`, `docs/`, `ci/`

### 2. Making Commits
```bash
git add src/file.py tests/test_file.py
git commit -m "feat: add new feature

- Add endpoint
- Add tests
- Update docs"
```
Types: `feat`, `fix`, `refactor`, `docs`, `test`, `ci`, `chore`, `perf`

### 3. Push and Create PR
```bash
git push -u origin HEAD

# With gh
gh pr create --title "feat: add feature" --body "Summary

Closes #42"

# With curl
BRANCH=$(git branch --show-current)
curl -s -X POST   -H "Authorization: token $GITHUB_TOKEN"   https://api.github.com/repos/$OWNER/$REPO/pulls   -d '{"title":"feat: add feature","body":"Summary","head":"'$BRANCH'","base":"main"}'
```

### 4. Monitor CI
```bash
# With gh
gh pr checks --watch

# With curl
SHA=$(git rev-parse HEAD)
curl -s -H "Authorization: token $GITHUB_TOKEN"   https://api.github.com/repos/$OWNER/$REPO/commits/$SHA/status
```

### 5. Auto-Fix CI Failures
1. Get failure details → read logs
2. Fix code → commit → push
3. Re-check CI
4. Repeat (max 3 attempts)

### 6. Merge
```bash
# With gh
gh pr merge --squash --delete-branch

# With curl
curl -s -X PUT   -H "Authorization: token $GITHUB_TOKEN"   https://api.github.com/repos/$OWNER/$REPO/pulls/$PR_NUMBER/merge   -d '{"merge_method":"squash"}'
```
Merge methods: `merge`, `squash`, `rebase`
