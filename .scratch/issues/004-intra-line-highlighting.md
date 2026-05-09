---
title: "Intra-line Highlighting & Styling"
parent: ".scratch/issues/001-prd-diff-visualization.md"
labels: ["ready-for-agent"]
status: "closed"
---

## What to build

Implement character-level diffing for changed lines to provide intra-line highlighting. Update the frontend CSS to visually distinguish additions and removals within a single line.

## Acceptance criteria

- [ ] `diff-engine` identifies and flags changed characters within modified lines
- [ ] `ui.ts` renders intra-line changes using specific HTML classes (e.g. `<span class="diff-char-added">`)
- [ ] CSS provides clear, high-contrast highlighting for these changes

## Blocked by

- .scratch/issues/003-contextual-lines.md
