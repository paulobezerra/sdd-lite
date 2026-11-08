# BUG — Readable Plan task fields

**ID:** 004-plan-task-readability · **Status:** approved · **Date:** 2026-11-08

**Branch:** `fix/004-plan-task-readability`, created from freshly fetched `origin/main`.

## Problem

Plan tasks put the task title and all eight fields in one long paragraph. Readers must scan dense text to locate scope, acceptance, tests, gates, or dependencies. Expected: each field is a separate visible item beneath its task, in both Markdown source and rendered output. Severity: low; affects people reading or executing generated Plans.

## Reproduction

1. Open `skills/sdd-lite/templates/plan.md`, Tasks section.
2. Observe that line 11 combines the title, Requirements, Precondition, Scope, Acceptance, TDD/characterization, Gate, and Dependencies.
3. Following that template reproduces the dense paragraph. The source pattern was verified; generation in a separate agent and rendered preview were not run.

## Root cause

Verified: `skills/sdd-lite/templates/plan.md:11` models every task as one Markdown paragraph. Ordinary wrapping does not give fields separate rendered items. The repeat instruction at line 13 propagates that shape. This is a local presentation defect; task semantics need no change.

The same compact pattern exists in `skills/sdd-lite/templates/bug.md:25`. Changing Bug task presentation is outside this request, which specifically targets Plan tasks; no shared rendering helper is involved. Focused searches of existing Review artifacts found no matching open finding.

## Fix

Change the Plan template to retain the task ID/title as the parent item and place each of its eight fields in a separate nested Markdown bullet. Make the corresponding Plan procedure explicitly require this presentation so source line breaks cannot collapse into one rendered paragraph. Preserve field names, order, content, task IDs, dependencies, approval rules, and execution ownership. Do not reformat existing approved Plans or change other artifact templates.

## Tasks

- **B004-01 — Separate every Plan task field into a readable item.**
  - **Acceptance:** given a Plan task containing all eight fields, when the template and Plan procedure are followed, then each field appears once on its own source line and as its own rendered list item under the task title, preserving the existing contract and task grouping.
  - **Test:** inspect the current template as the failing baseline: all fields share one paragraph. After the change, review a representative two-task Markdown example with all fields, including a dependency on the first task; verify source separation, rendered list structure, and unchanged field coverage. Manual rendering is appropriate because this repository has no agent-generation or Markdown rendering test harness; no new test infrastructure is required.
  - **Gate:** manual consistency review of `skills/sdd-lite/templates/plan.md` and `skills/sdd-lite/commands/plan.md`, local link checks, example review, and `git diff --check`, as required by project-context for documentation changes.

## Notes

The user explicitly selected `origin/main` and requested persisting it in `.specs/project-context.md` for future feature and bug branches. That context-only update is authorized in addition to this Bug artifact. This stage records the diagnosis only; implementation, regression validation, commits, and publication remain outside this invocation.
