# Cortex Notes Repository

This repository is the data store for the **Cortex** personal note-taking app. Files are read and written by the app through the GitHub API.

## File Structure & Conventions

All notes live under the `/notes` directory as Markdown files following these conventions:

- **Notebooks:** Organized as folders under `/notes/<notebook>/<slug>.md`. Nesting is supported (e.g., `/notes/study/programming/python-basics.md`).
- **Uncategorized notes:** Notes placed directly under `/notes` (no folder) are treated as uncategorized.
- **Filenames:** Must be lowercase kebab-case slugs (e.g., `atomic-habits.md`, `quick-thoughts.md`).

## Frontmatter Format

Every note **must** start with YAML frontmatter containing exactly these keys:

```yaml
---
title: string
date: YYYY-MM-DD
tags: [tag1, tag2, ...]
pinned: true or false
---
```

The frontmatter is followed by the note body in standard Markdown.

## Editing

While the Cortex app is the primary interface for managing notes, manual edits are supported provided that:
- The frontmatter format remains valid (all four keys must be present)
- Dates follow the `YYYY-MM-DD` format
- Tags are properly formatted as an inline YAML list

⚠️ Invalid or missing frontmatter may cause the app to fail to parse or display the note correctly.
