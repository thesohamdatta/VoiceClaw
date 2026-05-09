---
title: "PRD: High-Fidelity Contextual Diff Visualization"
labels: ["ready-for-agent"]
status: "open"
---

## Problem Statement

The current diff visualization in VoiceClaw presents code changes as a simple list of removed lines followed by added lines. For large files or subtle changes, this results in a 'wall of text' that is difficult to verify by voice. Users are forced to switch to their IDE to understand what actually changed, breaking the voice-first experience.

## Solution

Implement High-Fidelity Contextual Diff Visualization that provides clear, line-level diffs with context lines and intra-line highlighting. This will allow users to instantly verify changes within the VoiceClaw timeline.

## User Stories

1. As a developer, I want to see context lines around a code change, so I can understand where in the file the change occurred.
2. As a developer, I want changed characters within a line to be highlighted, so I can quickly spot subtle fixes like a single character change.
3. As a developer, I want the diff to be compact, showing only the relevant parts of the file, so I don't have to scroll through irrelevant code.
4. As a developer, I want the diff view to be toggleable, so I can see a summary first and expand for detail.
5. As a developer, I want the diff to be visually distinct from other timeline events, so I can easily identify file modifications.

## Implementation Decisions

- **New Module: `diff-engine.ts`**: A deep module to handle diff computation using the `diff` (jsdiff) library. It will provide a clean interface for generating contextual diffs.
- **Frontend Dependency**: Add `diff` (jsdiff) to `package.json`.
- **UI Update**: Refactor `ui.ts` to use the `diff-engine` for rendering file changes.
- **CSS Enhancements**: Update `style.css` to support intra-line highlighting (dimming unchanged parts, bolding/coloring changes).
- **Toggle State**: Persist the expanded/collapsed state of diffs within the session.

## Testing Decisions

- **Unit Tests**: Create `diff-engine.test.ts` to verify diff generation across various scenarios (new file, modified lines, multiple chunks, intra-line changes).
- **Test Strategy**: Focus on external behavior (correctly formatted diff structures) rather than implementation details of the underlying library.

## Out of Scope

- Full side-by-side diff viewer (retaining the current unified diff flow for now).
- Syntax highlighting within the diff view (focusing on diff highlighting first).
