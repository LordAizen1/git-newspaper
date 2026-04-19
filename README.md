# git-newspaper

Generate a Victorian broadsheet newspaper from any git repository's commit history.

```bash
npx git-newspaper
```

![preview](https://raw.githubusercontent.com/LordAizen1/git-newspaper/master/preview.png)

Opens `newspaper.html` in your browser, a fully typeset front page built from your actual commits, authors, deleted files, and code churn. No API keys. No LLM. Works offline.

---

## Install

```bash
npm install -g git-newspaper
```

Or run without installing:

```bash
npx git-newspaper
```

## Usage

```bash
# Run inside any git repo
git-newspaper

# Point at a specific repo
git-newspaper --repo /path/to/repo

# Scope to recent activity
git-newspaper --since "2 weeks ago"
git-newspaper --since "2024-01-01"

# Export as PNG instead of HTML
git-newspaper --format png

# Save to a specific file
git-newspaper --output my-paper.html

# Limit commits analysed (default: 500)
git-newspaper --limit 200

# Don't open the browser automatically
git-newspaper --no-open
```

## What's in the newspaper

Every section is generated from your actual git data, nothing is made up.

| Section | Source |
|---|---|
| **Front page headline** | Your largest commit by lines changed |
| **Lead article** | Commit authors, file counts, date range |
| **Meteorological Report** | Commit sentiment and activity pattern |
| **Obituaries** | Files deleted in the period |
| **Opinion column** | Your most-modified file, writing about itself |
| **Vital Statistics** | Commit counts, top authors, churn rankings |
| **Commit Activity** | Timeline chart of activity over the period |
| **Classifieds** | Archetype-specific notices based on your repo's patterns |

## Archetypes

The tool detects what kind of repository it's looking at and adjusts the layout, tone, and content accordingly:

| Archetype | Trigger | Edition |
|---|---|---|
| Revert Crisis | >12% of commits are reverts | Crisis Edition |
| Solo Marathon | One author dominates >70% of commits | Profile Edition |
| Ghost Town | Fewer than 8 commits | Quiet Edition |
| Dependency Churn | >35% of commits touch lock files | Administrative Notice |
| Refactor Sweep | >25% of commits are refactors | Infrastructure Report |
| Bugfix Crisis | >35% of commits are fixes | Emergency Edition |
| Feature Sprint | >35% of commits are features | Launch Edition |
| Collaborative | 5+ authors with 40+ commits | Collaborative Edition |
| Balanced | Everything else | Morning Edition |

## PNG export

Requires Playwright (not installed by default):

```bash
npm install -D playwright
npx playwright install chromium
git-newspaper --format png
```

## How it works

- Parses `git log --stat` locally via [simple-git](https://github.com/steveukx/git-js), no GitHub API, no network requests
- Detects a repository archetype from commit patterns
- Selects content from archetype-specific template libraries using a seeded RNG (same repo always produces the same paper)
- Renders a self-contained HTML file with all fonts and styles inline

## Requirements

- Node.js 18 or later
- A git repository with at least one commit

## License

MIT
