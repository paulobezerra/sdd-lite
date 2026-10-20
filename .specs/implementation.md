# IMPLEMENTATION CONVENTIONS — SDD Lite

**Updated:** 2026-10-17 · **Origin:** observed in repository instructions and templates

Starting point for Spec, Code, Bug and Review. `observed` rules are supported by the cited files; `assumption` items are not enforced in Review. Stack, commands, and structure live in [project-context.md](project-context.md).

## Boundaries and composition

- Keep invocation routing in `SKILL.md`, command procedures in the corresponding command file, common rules in `guidelines/`, and output structure in `templates/`. Update a shared rule in the guideline and relevant command rather than duplicating it in an adapter. — `observed`; `skills/sdd-lite/SKILL.md`, `skills/sdd-lite/guidelines/workflow.md`.
- Keep the workflow usable through repository files alone; agent-specific adapters may aid discovery but cannot be its only enforcement mechanism. — `observed`; `skills/sdd-lite/guidelines/workflow.md`, `README.md`.

## Contracts and security

- Execute one requested command per invocation and preserve earlier validated artifacts across later stages; record divergences in the current artifact with explicit user approval. — `observed`; `skills/sdd-lite/SKILL.md`, `skills/sdd-lite/guidelines/workflow.md`, `skills/sdd-lite/templates/{feature,spec,plan,review}.md`.
- Record validation in the artifact being validated, with the user's supplied name and an OS date. Never infer validation from silence or a checkbox. — `observed`; `skills/sdd-lite/guidelines/workflow.md`, `skills/sdd-lite/templates/{feature,spec,plan,bug}.md`.
- Do not store credentials, real environment files, tokens, sensitive logs, or dumps in artifacts. — `observed`; `skills/sdd-lite/guidelines/workflow.md`, `skills/sdd-lite/commands/init.md`.

## Data and persistence

- Project-specific knowledge is stored in the consuming project's `.specs/project-context.md` and `.specs/implementation.md`; feature and bug records remain in their own folders. No database or migration convention applies to this repository. — `observed`; `skills/sdd-lite/SKILL.md`, `skills/sdd-lite/guidelines/workflow.md`, `README.md`.

## Client and interface

- The documentation page currently uses one HTML file with inline CSS and JavaScript; its controls select a theme and copy the install command. Keeping that structure for future changes is an `assumption`; evidence for the current structure: `docs/index.html`.
- Keep the README, documentation page, command procedures, and templates aligned on command names, flows, and artifact paths. — `observed`; `skills/sdd-lite/guidelines/quality.md`, `README.md`, `docs/index.html`.

## Testing and quality gates

- For documentation or guideline changes, check links, examples, consistency with current commands, and the diff; record checks actually run and limits. — `observed`; `skills/sdd-lite/guidelines/quality.md`, `skills/sdd-lite/guidelines/review.md`.
- No repository test runner, CI workflow, formatter, or static-analysis command is defined. — `observed`; tracked repository files and `README.md`.
