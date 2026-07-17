---
topic: principles-and-hierarchy
type: explanation
---

# Principles and Canonical Hierarchy

## Purpose
Defines the philosophical intent of this system and the canonical folder structure every initiative must follow.

## Design Principles

1. Every container is a ticket.
2. Parent tickets only summarize and link; they should not duplicate child detail.
3. Every ticket has structured YAML frontmatter for machine readability.
4. Every ticket has skimmable markdown sections for human readability.
5. Cross references are first-class (markdown links and wiki links are both allowed).
6. IDs are hierarchical and sortable so flattened views preserve containment order.

## Canonical Hierarchy

```text
backlog/
  Index.md
  README.md
  Tracking.md                     ← compatibility shim only
  _rules/                         ← governance topic files (this folder)
  _knowledge/                     ← reference knowledge graph (books, papers, wiki packs)
    _templates/                   ← starter files for both backlog and knowledge systems
  <epic-hex-id>_<epic-slug>/
    Overview.md
    Directive.md                  ← optional: strategic intent and constraints
    <feature-hex-id>_<feature-slug>/
      Overview.md
      <story-hex-id>_<story-slug>/
        Overview.md
        <task-hex-id>_<task-slug>.md      ← leaf node, no children
```

## Containment Rule

Each level only links its direct children. Traversal to deeper descendants is inferred through parent containers. Never flatten the hierarchy into a single file or index.
