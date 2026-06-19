---
name: github-repo-management
description: "Clone/create/fork repos; manage remotes, releases."
---

# GitHub Repository Management

## When to use
When you need to clone, create, fork, or manage GitHub repositories and releases.

## How

### Cloning
```bash
git clone https://github.com/owner/repo.git
git clone --depth 1 https://github.com/owner/repo.git  # Shallow
```

### Creating Repos
```bash
# With gh
gh repo create my-project --public --clone

# With curl
curl -s -X POST   -H "Authorization: token $GITHUB_TOKEN"   https://api.github.com/user/repos   -d '{"name":"my-project","private":false,"auto_init":true}'
```

### Forking
```bash
# With gh
gh repo fork owner/repo --clone

# With curl
curl -s -X POST   -H "Authorization: token $GITHUB_TOKEN"   https://api.github.com/repos/owner/repo/forks
# Then clone and add upstream remote
git remote add upstream https://github.com/owner/repo.git
```

### Sync Fork
```bash
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

### Releases
```bash
# With gh
gh release create v1.0.0 --title "v1.0.0" --generate-notes

# With curl
curl -s -X POST   -H "Authorization: token $GITHUB_TOKEN"   https://api.github.com/repos/$OWNER/$REPO/releases   -d '{"tag_name":"v1.0.0","name":"v1.0.0","generate_release_notes":true}'
```

### Secrets (GitHub Actions)
```bash
gh secret set API_KEY --body "value"
gh secret list
gh secret delete API_KEY
```

### Branch Protection
```bash
curl -s -X PUT   -H "Authorization: token $GITHUB_TOKEN"   https://api.github.com/repos/$OWNER/$REPO/branches/main/protection   -d '{"required_status_checks":{"strict":true,"contexts":["ci/test"]},"required_pull_request_reviews":{"required_approving_review_count":1}}'
```
