---
name: blogwatcher
description: "Monitor blogs and RSS/Atom feeds via blogwatcher-cli tool."
---

# Blogwatcher - RSS/Blog Monitor

## When to use
When you need to monitor blogs and RSS/Atom feeds for updates.

## How

### Installation
```bash
go install github.com/JulienTant/blogwatcher-cli/cmd/blogwatcher-cli@latest
# Or download binary from GitHub releases
```

### Managing Blogs
```bash
blogwatcher-cli add "Blog Name" https://blog.com
blogwatcher-cli add "Blog Name" https://blog.com --feed-url https://blog.com/feed.xml
blogwatcher-cli blogs
blogwatcher-cli remove "Blog Name" --yes
blogwatcher-cli import subscriptions.opml
```

### Scanning and Reading
```bash
blogwatcher-cli scan           # Scan all blogs
blogwatcher-cli scan "Blog"    # Scan one blog
blogwatcher-cli articles       # List unread
blogwatcher-cli articles --all # List all
blogwatcher-cli read 1         # Mark read
blogwatcher-cli unread 1       # Mark unread
blogwatcher-cli read-all       # Mark all read
```

### Environment Variables
- `BLOGWATCHER_DB` — database path
- `BLOGWATCHER_WORKERS` — concurrent workers (default 8)
- `BLOGWATCHER_SILENT` — only output "scan done"
- `BLOGWATCHER_YES` — skip confirmations

### Notes
- Auto-discovers RSS/Atom feeds from blog homepages
- Falls back to HTML scraping with `--scrape-selector`
- Import from OPML (Feedly, Inoreader, etc.)
- Database: `~/.blogwatcher-cli/blogwatcher-cli.db`
