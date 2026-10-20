# PROJECT CONTEXT — SDD Lite

**Updated:** 2026-10-17 · **Origin:** existing project (analyzed) · **Artifact language:** English (`assumption`, following the existing documentation)

## Purpose

SDD Lite is a globally installable agent skill for a lightweight, documented development workflow. It guides users through project initialization, feature and bug planning, implementation, and review across projects and agents. Evidence: `README.md`, `skills/sdd-lite/SKILL.md`.

## Stack and constraints

- **Languages/runtime:** Markdown instructions and templates; a standalone HTML/CSS/JavaScript documentation page. No application runtime, package manifest, or versioned toolchain is present.
- **Infrastructure:** `docs/` is described as a GitHub Pages site deployed from `main` / `/docs`; repository hosting configuration was not verified. The README documents consumer installation with `npx skills add paulobezerra/sdd-lite -g` (not run here).
- **Constraint:** The skill is project-agnostic; a consuming project's knowledge belongs in that project's `.specs/`, not in this skill. Evidence: `README.md`, `skills/sdd-lite/SKILL.md`, `skills/sdd-lite/guidelines/workflow.md`.

## Structure and boundaries

- `skills/sdd-lite/SKILL.md` routes invocations to one command file in `commands/`. Shared behavior lives in `guidelines/`; artifact shapes live in `templates/`; `agents/openai.yaml` is an agent adapter.
- `docs/index.html` is the standalone public documentation page; `README.md` explains installation, commands, and publishing.
- `.specs/` records this repository's own context. No application source, database, tests, CI, or deployment configuration is tracked.

## Commands

- **Consumer installation (documented, unverified):** `npx skills add paulobezerra/sdd-lite -g` on the host (`README.md`).
- **Repository run/test/focused test/lint/format/static analysis/full gate:** no project command is defined in tracked manifests, scripts, or CI. Documentation changes require a manual consistency, link, and diff review; no automated gate is established.
- **Publishing (documented, unverified):** configure GitHub Pages to deploy `main` / `/docs` in repository settings (`README.md`).

## Conventions

Implementation rules live in [implementation.md](implementation.md).

## Authorization limits

Do not commit, push, publish, deploy, send messages, or perform destructive operations without an explicit request. Do not add credentials or sensitive data to the repository. Evidence: `skills/sdd-lite/guidelines/workflow.md`.

## Current state and known risks

- The seven command procedures, four shared guidelines, and seven artifact templates are present; the README and one-page site describe the workflow.
- No automated tests or CI gate are present, so documentation and cross-file consistency are not automatically checked.
- The README's GitHub Pages publishing instructions describe a manual setup; its live configuration was not verified.

## Open questions

- Confirm English as the language for this repository's SDD artifacts.
- Decide whether to add an automated documentation/consistency gate and a repository publishing configuration.
