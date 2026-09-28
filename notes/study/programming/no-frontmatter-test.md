# Plain Markdown Note

This is a test note with no frontmatter. It should help validate that the Cortex app can gracefully handle notes that are missing metadata.

## Section 1

Some content here.

## Section 2

More content to make this feel like a real note.

The app should either:
1. Skip this file gracefully, or
2. Create default metadata for it at runtime

Either way, it shouldn't crash.
