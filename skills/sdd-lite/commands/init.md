# SDD Lite · Init

Create or refresh two project artifacts: `.specs/project-context.md` (what the project is: purpose, stack, structure, commands, limits; [template](../templates/project-context.md)) and `.specs/implementation.md` (how code is written here: boundaries, contracts, security, data, testing conventions; [template](../templates/implementation.md)). Read [workflow](../guidelines/workflow.md) first. These two artifacts are the single source of project-specific knowledge: every other command reads `project-context.md` before acting, and `spec`, `code`, `bug` and `review` also read `implementation.md`, so they replace the repository-rules file (`AGENTS.md`-style) that other workflows keep per project. This step documents the project; it does not change source code, start a feature, or invent facts. By default, end after Init; continue into other explicitly requested commands only.


## 1. Detect the mode

1. Inspect the project root: manifests, source directories, tests, CI/deploy files, README and docs, git history, and any existing agent-rules file (`AGENTS.md`, `CLAUDE.md`, etc.). Check whether `.specs/project-context.md` and `.specs/implementation.md` already exist.
2. Choose the mode:
   - **New/empty project** (no meaningful source or manifests): **interview mode**.
   - **Existing project**: **analysis mode**.
   - **Artifacts already exist**: **refresh mode**. Read them and verify each statement against the repository; update only what changed or is wrong, keep decisions the user wrote, and list what you changed.
3. If the mode is ambiguous (for example a bare scaffold with a few files), ask the user which applies. A project may combine both: analyze what exists and interview for what is still to be decided.

## 2a. Interview mode (new project)

Ask **one question at a time**, with options when possible, and only what is needed to write a useful context. Cover, in this order and skipping what the user already said:

1. Purpose: what the project is, for whom, and the problem it solves.
2. Stack and versions, or help choosing. If the user says "decide for me", propose a stack with a one-line reason per piece and record it as decided only after they confirm.
3. Deployment and hosting model, external services, and hard constraints (no build step, compliance, budget, compatibility).
4. Intended structure: layering, where each kind of code lives, dependency direction.
5. Quality expectations: test levels and style, lint/format/static analysis, definition of a passing gate.
6. Security and data rules, and operations agents must not run without authorization.
7. Implementation conventions: layering and dependency rules, error and validation handling, authentication and data rules, migration policy, testing expectations, and patterns to avoid. Offer defaults suited to the chosen stack and record each as `decided` only after the user confirms it.
8. Language for SDD artifacts.

Do not ask what can be inferred, and do not turn the interview into a Spec. Anything unanswered goes to **Open questions**; do not fill it with invented defaults. Commands that do not exist yet are recorded as "to be defined" rather than guessed.

## 2b. Analysis mode (existing project)

Be economical: use search tools and manifests rather than reading the repository. Gather, with file evidence:

1. **Purpose and stack:** README/docs; manifests for language, framework and versions (read lockfile headers only, never in full); runtime and infrastructure from Docker, CI, and deploy configuration.
2. **Structure and boundaries:** top-level layout, layering and dependency direction **as actually observed** (check imports across layers), where each kind of code lives, and any rule the code already enforces (architecture tests, lint rules).
3. **Commands:** install, run, test (and focused test), lint/format/static analysis, migrate, and full quality gate, taken from manifest scripts, Makefile, CI and README. Verify them with safe read-only invocations (`--version`, `--help`, listing tests) when possible. Do not start services, install dependencies, or run anything destructive or slow; mark unverified commands as such and say how they must be run (host or container, services required).
4. **Implementation conventions** (go to `implementation.md`): naming, error handling, validation, test layout and style, API and contract practices, migration policy, security mechanisms (authentication, authorization, CSRF, sessions, rate limiting) as implemented, dependency policy. Derive each rule from repeated evidence (a pattern across several files, an architecture test, a lint rule, a review comment in history) and cite it; a single occurrence is not a convention. Mark it `observed`.
5. **Current state and risks:** the main existing features/areas in one line each, tech debt, fragile or untested areas, and gaps between docs and code.
6. **Authorization limits:** destructive operations specific to this project (database reset, volume cleanup, deploys, production access).

If the project already has an agent-rules file, reference it instead of copying its content and flag contradictions with what the code does. Never record secrets, `.env` values, tokens, or personal data. Separate **observed** facts from **assumptions**; a rule you inferred but the user has not confirmed is marked `assumption` or goes to open questions, and Review must not enforce it. Where the code contradicts the docs or itself, record the conflict in Open questions instead of choosing a side.

## 3. Write, confirm, deliver

1. Create `.specs/` if needed and write `.specs/project-context.md` and `.specs/implementation.md` from their templates, without duplicating content between them (stack, commands and structure in the former; conventions in the latter). Fill the dates with `date +%Y-%m-%d`. Keep it concise and factual, drop sections that do not apply, and do not create `features/`, `bugs/`, or any other file.
2. Show the user a short summary of what was recorded, the assumptions, and the open questions, and ask them to correct anything wrong; apply corrections in this same execution. Unconfirmed items stay marked as assumptions.
3. Suggest, without doing it unless the user agrees, adding one line to the project's agent-rules file pointing to `.specs/project-context.md`, `.specs/implementation.md` and `$sdd-lite`. Deliver the links, mode used, assumptions, and open questions. Do not commit. Stop.
