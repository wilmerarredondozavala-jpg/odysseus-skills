---
name: github-auth
description: "GitHub authentication setup: HTTPS tokens, SSH keys, gh CLI login."
---

# GitHub Authentication Setup

## When to use
When you need to set up authentication to work with GitHub repositories, PRs, issues, and CI.

## How

### Detection Flow
1. Check `gh auth status` — if authenticated, use gh for everything
2. If gh installed but not authenticated → use gh auth method
3. If gh not installed → use git-only method

### Method 1: HTTPS with Personal Access Token (Recommended)
1. Create token at https://github.com/settings/tokens
   - Scopes: `repo`, `workflow`, `read:org`
2. Configure git:
```bash
git config --global credential.helper store
```
3. Test: `git ls-remote https://github.com/user/repo.git`
4. Set identity:
```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

### Method 2: SSH Key
```bash
ssh-keygen -t ed25519 -C "your@email.com" -f ~/.ssh/id_ed25519 -N ""
cat ~/.ssh/id_ed25519.pub  # Add to GitHub settings
ssh -T git@github.com  # Test
git config --global url."git@github.com:".insteadOf "https://github.com/"
```

### Method 3: gh CLI
```bash
gh auth login  # Interactive
echo "token" | gh auth login --with-token  # Headless
gh auth setup-git
```

### API without gh
```bash
export GITHUB_TOKEN="your_token"
curl -s -H "Authorization: token $GITHUB_TOKEN" https://api.github.com/user
```
