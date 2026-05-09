---
title: "Contextual Line Management"
parent: ".scratch/issues/001-prd-diff-visualization.md"
labels: ["ready-for-agent"]
status: "closed"
---

## What to build

Enhance `diff-engine.ts` to only show a few lines of context around each change, rather than the entire file. This makes diffs more compact and readable.

## Acceptance criteria

- [ ] `generateDiff` supports a `context` option (defaulting to 3 lines)
- [ ] Unchanged lines far from any change are omitted and replaced with a '...' indicator
- [ ] Unit tests verify context management for various edge cases

## Blocked by

- .scratch/issues/002-skeleton-diff-engine.md
