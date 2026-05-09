---
title: "Skeleton Diff Engine & UI Integration"
parent: ".scratch/issues/001-prd-diff-visualization.md"
labels: ["ready-for-agent"]
status: "closed"
---

## What to build

Add the `diff` (jsdiff) dependency to the frontend and create a skeleton `diff-engine.ts` module. Refactor `ui.ts` to use this engine for rendering file modifications in the timeline.

## Acceptance criteria

- [ ] `diff` library added to `package.json`
- [ ] `diff-engine.ts` created with a basic `generateDiff(oldStr, newStr)` function
- [ ] `ui.ts` calls `diff-engine` to render diffs instead of the manual line-by-line loop
- [ ] Diffs are still visible in the timeline after refactoring

## Blocked by

None - can start immediately
