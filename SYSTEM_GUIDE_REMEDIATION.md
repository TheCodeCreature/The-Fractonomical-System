# System Guide Remediation Log

Date: 2026-07-16
Scope: Canonical naming, template boundaries, tag namespace alignment, and broken index links

## Completed Fixes

1. Repaired index integrity in `Index.md`.
2. Removed stale active epic reference and broken `Details.md` link in `Index.md`.
3. Added canonical root backlog templates under `_templates/`.
4. Removed obsolete backlog templates from `_knowledge/_templates/`.
5. Corrected tag catalog path in `_rules/09_tag-library.md`.
6. Added `kind:` namespace to `_rules/09_tag-library.md` and `_meta/Tags.md`.
7. Clarified template separation and dual-ID policy in `_rules/10_knowledge-system.md`.
8. Added template-location clarity links in `README.md` and `_knowledge/README.md`.
9. Marked `SYSTEM_GUIDE_REVIEW.md` as historical snapshot context.

## Current Canonical Locations

- Backlog templates: `_templates/`
- Knowledge templates: `_knowledge/_templates/`
- Backlog governance rules: `_rules/`
- Tag catalog: `_meta/Tags.md`

## Follow-up Recommendation

Add a simple validation script (or checklist) to catch:
- Broken markdown links
- `Details.md` references in new backlog nodes
- Unknown tag namespaces
- Missing `updated` on meaningful changes
