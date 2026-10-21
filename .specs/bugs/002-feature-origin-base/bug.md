# BUG — Feature branch pode partir de uma base local desatualizada

**ID:** 002-feature-origin-base · **Status:** open · **Date:** 2026-10-20

**Branch:** `fix/002-feature-origin-base`.

**User validation to start Code:** validated. **Statement:** “aprove o bug”. **Name:** Paulo Bezerra · **Date:** 2026-10-20.

## Problem

When a user runs `$sdd-lite feature`, the command tells the agent to create its branch from the “integration branch” without requiring it to identify the project's remote integration branch or verify that the local base is current. If the project does not declare which branch tracks the origin, the agent can silently choose a stale local branch. The resulting Feature and later Spec may omit code already present on the remote branch. This affects every user starting a feature in a project whose local base may lag behind its remote.

## Reproduction

1. Use a project where the local integration branch is behind its remote counterpart, or where project context does not identify the integration branch.
2. Run `$sdd-lite feature <description>`.
3. The current procedure permits creating the feature branch from the unspecified or stale local integration branch without asking the user or checking the remote.

The procedure is prompt-driven and has no automated runner. In this repository, local `origin/main` was at `e9c4806738f8dc43f2adf74149ec3e986985409c`; a read-only remote check found `main` at `cdc41944efba97ac49e12f969f7cd8ac5db6a502`, confirming that the local reference can be stale.

## Root cause

- `skills/sdd-lite/commands/feature.md:16` requires creating the feature branch “from the integration branch” but does not require determining which remote branch that means, checking whether it is declared in project context, or confirming its current remote tip.
- `skills/sdd-lite/guidelines/workflow.md:50` repeats the same underspecified base rule for Feature and Bug branches.
- No step tells the agent to stop and ask the user when the project does not specify its origin integration branch, or to avoid using an out-of-date local base.

## Fix

Update the Feature branch preparation procedure and its shared workflow rule so the agent identifies the project's declared origin integration branch and verifies its base is current before creating the feature branch. If the project does not specify the branch, stop before branch creation and ask the user which origin branch to use. Keep the change limited to branch-base selection and freshness checks; do not alter Feature content, validation gates, branch naming, or the Bug flow beyond shared rules needed to prevent contradictory instructions.

## Tasks

- [x] **B002-01 — Require an explicit, current origin base before creating a Feature branch.** **Acceptance:** given a project that declares its origin integration branch, when `$sdd-lite feature` prepares a branch, then it uses that branch's current remote tip as the base; given a project that does not declare the branch, when the command reaches branch preparation, then it stops before creating the branch and asks the user which origin branch to use. **Test:** manual procedure review with (a) a project whose local integration branch is behind its declared remote and (b) a project with no declared origin integration branch; confirm the stale base is refreshed before branch creation and the missing-base case waits for the user's answer. The documentation workflow has no automated test runner. **Gate:** review the command and shared workflow for consistent branch rules; verify links, examples, and diff; no automated gate is defined in project-context.
- [x] **B002-02 — Apply the explicit, current origin base rule to Bug branches.** **Acceptance:** given a project that declares its origin integration branch, when `$sdd-lite bug` prepares a new branch, then it refreshes and uses the current `origin/<branch>` tip; given a project without a declared branch, it stops before branch creation and asks the user which origin branch to use; if the remote cannot be reached, it does not use a potentially stale local base. **Test:** manual procedure review of the declared-and-stale, undeclared, and unreachable-remote cases. The documentation workflow has no automated test runner. **Gate:** review the Bug command and shared workflow for consistent branch rules, then inspect links, examples, and diff; no automated gate is defined in project-context.

## Notes

The user explicitly invoked `$sdd-lite bug` and then said “continue,” authorizing continuation in this flow. The requested behavior is treated as a pinpoint correction to the existing Feature branch procedure; no Spec or Plan is added.

**Authorized scope extension:** On 2026-10-21, Paulo Bezerra explicitly requested: “implemente a correção para o fluxo de bug tbm”. This extends the original Feature-only scope to cover the same stale-base cause in Bug branch preparation. B002-02 records the added requirement; the original diagnosis and B002-01 acceptance remain unchanged.
