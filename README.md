# SDD Lite

Lightweight **spec-driven development** as a single, globally installable agent skill. Install once, run `$sdd-lite <command>` in any project.

📖 **Docs:** https://paulobezerra.github.io/sdd-lite/

## Install

```bash
npx skills add paulobezerra/sdd-lite -g
```

## Quick start

1. `$sdd-lite init`: creates `.specs/project-context.md` and `.specs/implementation.md`. Interviews you on an empty project; analyzes the code on an existing one.
2. New capability: `$sdd-lite feature` → `spec` → `plan` → `code` → `review`.
3. Pinpoint defect: `$sdd-lite bug` → `code` → `review`.

Syntax: `$sdd-lite <command> [ID or free text]` in Codex, `/sdd-lite <command> ...` in Claude Code and similar agents. Run each command with a clean context (`/clear`).

## Commands

| Command | What it does | Writes |
|---|---|---|
| `init` | Creates/refreshes the project context and implementation conventions (interview, analysis or refresh mode) | `.specs/project-context.md`, `.specs/implementation.md` |
| `feature` | Defines the product need; creates `feature/NNN-name` | `.specs/features/NNN-name/feature.md` |
| `spec` | Grounds recommendations in Feature constraints; presents complete cards and a viability matrix for multiple viable options, or evidence for the single viable option | `…/spec.md` |
| `plan` | Splits the spec into vertical tasks (`TNNN-XX`) | `…/plan.md` |
| `bug` | Triage, root cause and a regression-test task (`BNNN-XX`); creates `fix/NNN-name`; does not fix | `.specs/bugs/NNN-name/bug.md` |
| `code` | Implements **one** task, continues in-scope work, and records `PENDING` or `SUCCESS`, evidence, and handoff | appends to `execution.md` in the feature/bug folder |
| `review` | Independently audits the delivery against approved criteria, code, diff, and checks; re-audits corrections in the same file | `review.md` in the feature/bug folder |

## Flows

```
Feature:  feature → spec → plan → code → review     (feature, spec, plan, execution, review)
Bug:      bug → code → review                       (bug, execution, review)
```

`bug` only accepts pinpoint defects (clear expected behavior, local cause, no contract change, migration or design choice) and redirects everything else to the feature flow. `code` and `review` serve both flows; the ID prefix (`T…` / `B…`) selects the folder.

## Rules in short

- **Explicit validation** of Feature, Spec and Plan (or Bug) before Code, recorded in the artifact with your name and the OS date.
- **Immutable inputs:** Each stage preserves approved upstream contracts. Code records status only in `execution.md`; Review checks those claims independently and records findings in `review.md`.
- **Clean context** per execution; a warning, never a block.
- **Evidence over claims:** only checks actually run count.
- **Never blocks you:** rule exceptions are explained and recorded when you insist.
- **Safe by default:** no commit, push, deploy or destructive operation without your request.

## What lands in your project

```
.specs/
├─ project-context.md      what the project is (stack, structure, commands, limits)
├─ implementation.md       how code is written here (observed / decided / assumption)
├─ features/NNN-name/      feature.md, spec.md, plan.md, execution.md, review.md
└─ bugs/NNN-name/          bug.md, execution.md, review.md
```

## Repository layout

```
skills/sdd-lite/
  SKILL.md        router: dispatches on the command
  commands/       one file per command
  guidelines/     workflow, specification, quality, review
  templates/      one per artifact
docs/index.html   project home (GitHub Pages)
```

Nothing project-specific lives in the skill; it all goes in your project's `.specs/`.

## Publishing the docs

GitHub Pages: **Settings → Pages → Deploy from a branch → `main` / `/docs`**.
