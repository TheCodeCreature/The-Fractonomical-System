# In-Depth System Review

Historical note: This document captures a pre-remediation audit snapshot from 2026-07-16 and is retained for architectural traceability.

Date: 2026-07-16
Reviewer lens: Systems architecture + Zettelkasten/knowledge-graph design
Scope: Governance hub, rule set, knowledge system contracts, templates, and current repository conformance

## Executive Assessment

Your system is strong conceptually and unusually well articulated for both humans and agents. The core architecture combines:

1. Deterministic structural grammar (hierarchical IDs and locality-based navigation)
2. Operational telemetry (status/progress discipline with rollup scoring)
3. Knowledge graph controls (anti-singularity and dependency declaration)

At the same time, the current repository implementation is in a transitional state where key runtime artifacts (active epic path, template locations, tag namespace consistency) are out of sync with the governance contract.

Bottom line:

- System design quality: High
- Current implementation conformance: Medium-Low
- Agent/tooling reliability under current drift: Medium risk

## Findings (Ordered by Severity)

### Critical

1. Index points to a non-existent active epic path and legacy file name.
Evidence:
- [Index.md](Index.md#L9) links to an epic container path ending in Details.md.
- [Index.md](Index.md#L3) marks the same epic as active.
- No matching container exists in the workspace for that ID/prefix.
Why this matters:
- Breaks top-level navigation contract.
- Invalidates active-work discovery for both humans and agents.
- Creates immediate false positives in automation that trusts the index as source of truth.

2. Backlog templates are stored under knowledge templates and use knowledge navigation roots.
Evidence:
- Canonical backlog hierarchy expects root-level templates per [01_principles-and-hierarchy.md](./_rules/01_principles-and-hierarchy.md#L29).
- Epic/feature/story/task backlog templates currently live under knowledge templates and route to Knowledge Catalog in examples such as [_knowledge/_templates/01000000_Epic-Title/Overview.md](./_knowledge/_templates/01000000_Epic-Title/Overview.md#L22), [_knowledge/_templates/01000000_Epic-Title/01010000_Feature-Title/Overview.md](./_knowledge/_templates/01000000_Epic-Title/01010000_Feature-Title/Overview.md#L24), and [_knowledge/_templates/01000000_Epic-Title/01010000_Feature-Title/01010100_Story-Title/Overview.md](./_knowledge/_templates/01000000_Epic-Title/01010000_Feature-Title/01010100_Story-Title/Overview.md#L26).
Why this matters:
- Crosses two bounded systems (delivery backlog and reference knowledge), violating separation intent.
- Makes generated tickets structurally incorrect by default.
- Introduces propagation of wrong links from template-based creation.

### High

3. Legacy naming migration remains unresolved at the live index boundary.
Evidence:
- Rule declares Overview as the canonical replacement in [02_naming-and-ids.md](./_rules/02_naming-and-ids.md#L22).
- Index still points to Details in [Index.md](Index.md#L9).
Why this matters:
- Humans and tools cannot rely on one canonical container filename.
- Causes brittle traversal logic and migration ambiguity.

4. Tag registry and tag rules are internally inconsistent with knowledge-system examples.
Evidence:
- Knowledge-system frontmatter examples include kind tags in [10_knowledge-system.md](./_rules/10_knowledge-system.md#L81) and [10_knowledge-system.md](./_rules/10_knowledge-system.md#L102).
- Tag-library namespace table does not declare a kind namespace in [09_tag-library.md](./_rules/09_tag-library.md#L35).
- Tag catalog contains only domain/layer/type/signal/team headings in [_meta/Tags.md](./_meta/Tags.md#L14), [_meta/Tags.md](./_meta/Tags.md#L32), [_meta/Tags.md](./_meta/Tags.md#L47), [_meta/Tags.md](./_meta/Tags.md#L64), [_meta/Tags.md](./_meta/Tags.md#L80).
Why this matters:
- Namespace drift erodes query reliability.
- Agents enforcing catalog-before-use cannot validate knowledge tags cleanly.

5. Tag-library contains an incorrect catalog path in the add-tag procedure.
Evidence:
- Step points to [09_tag-library.md](./_rules/09_tag-library.md#L59) with ../Tags.md, while the catalog is under _meta.
Why this matters:
- Small but high-frequency friction point for editors and agents.
- Encourages accidental creation of duplicate tag files.

### Medium

6. Backlog template metadata semantics are misaligned at story/task levels.
Evidence:
- Story and task templates carry type:feature tagging and task includes an extra feature key in [_knowledge/_templates/01000000_Epic-Title/01010000_Feature-Title/01010100_Story-Title/Overview.md](./_knowledge/_templates/01000000_Epic-Title/01010000_Feature-Title/01010100_Story-Title/Overview.md#L15), [_knowledge/_templates/01000000_Epic-Title/01010000_Feature-Title/01010100_Story-Title/01010101_Task-Title.md](./_knowledge/_templates/01000000_Epic-Title/01010000_Feature-Title/01010100_Story-Title/01010101_Task-Title.md#L7), and [_knowledge/_templates/01000000_Epic-Title/01010000_Feature-Title/01010100_Story-Title/01010101_Task-Title.md](./_knowledge/_templates/01000000_Epic-Title/01010000_Feature-Title/01010100_Story-Title/01010101_Task-Title.md#L16).
Why this matters:
- Pollutes filter dimensions.
- Weakens consistent role semantics for tags vs type field.

7. Knowledge source ID strategy is ambiguous between catalog and knowledge-system template examples.
Evidence:
- Catalog uses FS-style IDs in [_knowledge/Catalog.md](./_knowledge/Catalog.md#L7).
- Source document uses source_id with explanation type in [_knowledge/_sources/Fractonomical System/Fractonomical System Definition.md](./_knowledge/_sources/Fractonomical%20System/Fractonomical%20System%20Definition.md#L3) and [_knowledge/_sources/Fractonomical System/Fractonomical System Definition.md](./_knowledge/_sources/Fractonomical%20System/Fractonomical%20System%20Definition.md#L4).
- Knowledge-system template example shows 02000000 + knowledge-source in [10_knowledge-system.md](./_rules/10_knowledge-system.md#L71).
Why this matters:
- It is unclear whether knowledge IDs are global-hex, source-scoped, or dual-scheme.

### Low

8. Rule language is very complete but occasionally over-coupled to process enforcement wording.
Why this matters:
- Strong enforcement language improves rigor.
- Overly rigid phrasing can reduce adaptability when the repository has mixed maturity stages.

## What Is Working Exceptionally Well

1. The anti-singularity rule is excellent and rare in small-team knowledge systems.
2. Diataxis labeling across governance docs improves retrieval and authoring mode clarity.
3. Lifecycle + scoring model gives both local and aggregate progress signals.
4. Separation of governance (_rules) vs knowledge (_knowledge) is conceptually clean.
5. The Fractonomical definition document gives a durable conceptual anchor.

## Zettelkasten and Knowledge-System Appraisal

Your knowledge design is closer to a structured evergreen system than a pure timestamp-slip Zettelkasten, and that is a strength for engineering organizations.

Strengths from a ZK perspective:

1. Atomicity by topic node (Overview, Snippets, Links)
2. Strong link intentionality (reasoned links rather than indiscriminate backlink inflation)
3. Explicit chronology channel via Sessions
4. Separation between source capture and operational delivery

Areas to sharpen for long-term graph quality:

1. Introduce an explicit link-typing vocabulary in Links files (supports, contrasts, extends, prerequisite-for).
2. Add anti-orphan checks for topic nodes with zero inbound links except parent.
3. Define source ingestion stages (raw capture, distilled, integrated) to avoid half-normalized notes.

## Architectural Risk Profile

1. Navigation Integrity Risk: High until Index and template roots are corrected.
2. Metadata Integrity Risk: Medium due to namespace and template drift.
3. Automation Reliability Risk: Medium-High because agents will follow contracts that current artifacts violate.
4. Scalability Risk: Low conceptually, Medium operationally if drift is not corrected early.

## Recommended Remediation Roadmap

### Phase 1 (Immediate: 1-2 sessions)

1. Fix Index links and align to existing canonical file names.
2. Decide whether the active epic exists yet:
	- If yes, create it at canonical path and add Overview.
	- If no, remove active epic pointer and keep index honest.
3. Correct tag-library path to tag catalog.

### Phase 2 (Short-term: 1 week)

1. Split backlog templates out of _knowledge into a root _templates tree.
2. Rewrite backlog template navigation to point to Index, not Catalog.
3. Normalize story/task template tags and frontmatter conventions.

### Phase 3 (Stabilization: 1-2 weeks)

1. Resolve ID policy for knowledge sources (FS-series vs hex) and document the decision in one place.
2. Add a lightweight lint checklist or script for:
	- broken links
	- forbidden Details references for new nodes
	- unknown tag namespaces
	- status/progress consistency
3. Add a conformance dashboard note in Index and Knowledge Catalog headers.

## Suggested Governance Clarifications

1. Add a formal status for repository maturity (bootstrap, migrating, converged).
2. Add rule precedence text when contracts conflict (templates vs rules vs existing artifacts).
3. Define strict vs lenient agent mode for migration periods.

## Review Conclusion

You have built a high-quality governance architecture with strong system thinking and graph-aware discipline. The primary challenge is not conceptual design; it is contract conformance in the current repo snapshot. Once template placement, index integrity, and namespace consistency are corrected, this will be a robust and automation-friendly knowledge-and-delivery system.
