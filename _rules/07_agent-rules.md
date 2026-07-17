---
topic: agent-rules
type: how-to
---

# Agent Execution Rules

## Purpose
Defines the behavioral contract for AI agents, prompts, skills, and hooks operating on backlog files. These rules are enforceable and violations should be flagged.

---

## Mandatory Behaviors

| Rule | Description |
|---|---|
| Preserve IDs | Never modify an existing ticket ID |
| No ID reuse | Never assign an ID that already exists in the tree |
| Update `updated` | Set the `updated` frontmatter field on every meaningful edit |
| Update status/progress | Set `status` and `progress` before starting and after completing any action on a ticket |
| Bidirectional links | When adding a child ticket, add its link in the parent's `## Child Tickets` table |
| Valid YAML | All frontmatter must parse as valid YAML after every edit |
| Minimal blast radius | Only edit files directly related to the current task; do not touch unrelated tickets |

---

## Status/Progress Gate

Agents must not mark work complete without updating both fields. Hooks and prompts should reject or warn when:

- `status` is `done` but `progress` < 100.
- `status` is `backlog` but `progress` > 0.
- `status` is `in-progress` but `updated` date is unchanged from `created`.

---

## Score Recalculation Trigger

Whenever a feature or story `status` changes to `done`, the agent must:

1. Recompute the epic's `A` score using the formula in [[./04_status-and-progress|Status and Progress]].
2. Update the `Score (A/B)` cell in `Index.md` for that epic.
3. Validate that no per-feature score falls in the invalid 1–2 exclusive band.

---

## File Creation Rules

When creating a new ticket container:

1. Generate the ID using the hierarchical hex format `EEFFSSTT` (for example, `01010000`).
2. Create the folder with the correct `<HierarchicalHexId>_<Slug>` name.
3. Create `Overview.md` using the appropriate template from `_knowledge/_templates/`.
4. Add the child link row in the parent `Overview.md`'s `## Child Tickets` table.
5. Do not create `Directive.md` unless explicitly requested.
