---
name: sdd-lite
description: "Lightweight spec-driven development workflow for any project. Commands: init (create/update the project context), feature, spec, plan, code, bug (short flow for a pinpoint bug), review. Use when the user invokes $sdd-lite or /sdd-lite <command>, or asks to start a feature, write a spec or plan, implement a plan task, fix a bug through the SDD flow, or audit delivered work."
license: MIT
metadata:
  version: "1.0"
---

# SDD Lite

Invocation: `$sdd-lite <command> [ID or free text]` (Codex) · `/sdd-lite <command> [ID or free text]` (Claude Code and others). If the agent has no native syntax, the user may say "run sdd-lite <command>".

## Dispatch

Take the first word after `sdd-lite` as the command, read **only** that command file (paths relative to this skill's directory), and execute it. The remainder is the user's ID or context.

| Command | File | Purpose | Artifact (in the user's project) |
|---|---|---|---|
| `init` | [commands/init.md](commands/init.md) | Create or refresh the project context and implementation conventions (empty or existing project) | `.specs/project-context.md`, `.specs/implementation.md` |
| `feature` | [commands/feature.md](commands/feature.md) | Define the product need | `.specs/features/NNN-name/feature.md` |
| `spec` | [commands/spec.md](commands/spec.md) | Choose and write the technical contract | `.../spec.md` |
| `plan` | [commands/plan.md](commands/plan.md) | Split the spec into tasks | `.../plan.md` |
| `bug` | [commands/bug.md](commands/bug.md) | One-step flow for a pinpoint bug (replaces feature → spec → plan) | `.specs/bugs/NNN-name/bug.md` |
| `code` | [commands/code.md](commands/code.md) | Implement one task (feature **or** bug) | updates the checklist only |
| `review` | [commands/review.md](commands/review.md) | Audit the delivered work (feature **or** bug) | `review.md` in the feature/bug folder |

No command, an unknown command, or `help`: list this table and ask which one to run. Do not guess.

## Flows

- **Feature:** `feature → spec → plan → code → review` (artifacts: feature, spec, plan, review).
- **Bug:** `bug → code → review` (artifacts: bug, review). The bug command triages first; if the problem is not a pinpoint bug it redirects to the feature flow.
- `code` and `review` serve both flows: the ID tells them which (`T…` = feature task, `B…` = bug task) and they work inside that item's folder.

## Shared rules (read when needed, not on every call)

- [guidelines/workflow.md](guidelines/workflow.md) — validation gates, immutability between steps, isolation, exceptions, branches, change policy. **Every command applies it.**
- [guidelines/specification.md](guidelines/specification.md) — used by `spec`.
- [guidelines/quality.md](guidelines/quality.md) — used by `code`, `bug`, `review`.
- [guidelines/review.md](guidelines/review.md) — used by `review`.
- [templates/](templates/) — one per artifact.

## Project-specific knowledge

This skill is project-agnostic. Everything about a given project lives in two files created by `init`: `.specs/project-context.md` (stack, structure, commands, limits) and `.specs/implementation.md` (boundaries, contracts, security, data and testing conventions). Every command reads the first; `spec`, `code`, `bug` and `review` also read the second; if it is missing, tell the user to run `$sdd-lite init` (or proceed with a warning if they insist).
