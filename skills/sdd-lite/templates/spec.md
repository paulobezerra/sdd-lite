# SPEC — <feature name>

**ID:** NNN-name · **Status:** decision pending | proposed · **Date:** YYYY-MM-DD

**User validation for Plan:** pending. After an explicit statement, record it here with the user's supplied name and the date obtained from the OS, without changing requirements or decisions. The technical decision below is not validation.

## Problem, baseline, and goal

<who is affected; verified current behavior and code/contract reference; expected outcome>

## Scope and constraints

- **Included:** <outcomes in this Spec>
- **Out of scope:** <explicit boundaries>
- **Constraints:** <compatibility, stack, deployment, dependencies, and relevant data; see project-context>

## Decision brief — complete before asking the user to choose

**Verified baseline:** <observed behavior and repository/code evidence>

**Decision drivers:** <relevant Feature requirement IDs and constraints>

### Option cards

#### Option A — <name>

- **Approach:** <what changes or stays>
- **Affected components:** <components>
- **Estimated code impact:** low | moderate | high
- **Fit to Feature:** <requirement IDs and how this meets them>
- **Benefits:** <concrete benefits>
- **Costs and risks:** <concrete costs, risks, and implications>
- **Constraints or conditions:** <conditions, or “None”>
- **Evidence:** <repository paths, observed contracts, or authoritative sources>

<Repeat for each real option; two or three materially different viable options by default. Do not invent options to reach a count.>

### Viability matrix

<Use only criteria relevant to this decision and add Feature-specific drivers as needed. Options are columns; criteria are rows. Add or remove option columns to match the real options. Every cell contains exactly one symbol and nothing else.>

| Criterion | Option A | Option B |
|---|---:|---:|
| <relevant criterion / requirement ID> | ✓ | ⚠ |

**Legend:** ✓ meets · ✗ does not meet · ⚠ partial or conditional fit. The option cards explain the evidence and implications behind every ⚠ and ✗. No scores or totals.

**Recommendation (not approval):** <for multiple options, name the recommended option and decisive criteria; for one evident solution, state its evidence-based justification>

**Decision requested:** <for multiple options, ask the user to choose or adjust; for one evident solution, write “None — proceed with the only viable solution.” This is not Spec validation.>

<For a clearly evident single viable solution, state the verified evidence and why constraints rule out relevant alternatives; omit fake cards and matrix and proceed without asking the user to choose.>

## Technical solution

**Technical decision:** <while pending, write “Pending user choice”; after choice, record the user's choice and date. For one clearly evident solution, give the date and code-based reason. Do not attribute a choice to the user without their statement.>

<Summarize only real options: the clearly evident solution or the selected option and relevant alternatives, in separate blocks. For each, record estimated code impact (low, moderate, or high), affected components, and decision-relevant fit or caveats. Identify criteria that do not apply. Avoid extensive comparison without a real tradeoff.>

**Reason for the decision:** <verified evidence, decisive benefit, and accepted cost; for a single solution, explain why no relevant alternative exists>.

## Open questions for validation

<List product decisions or Feature deviations the user still needs to assess. For each, cite the prior contract, real options, impact, and current proposal. If none remain, write “None” so the check is visible before validation. Do not treat an earlier technical choice as Spec validation.>

## Requirements

- **SNNN-01** — <observable outcome; affected consumers: API, UI, API docs, database, operations>
- **SNNN-02** — <another outcome; dependency on SNNN-01, if any>

<Plan will turn these requirements into deliverable tasks. Code and Review track progress outside this Spec.>

## Contracts, data, and security

<Existing routes/payloads/statuses, invariants, authentication/authorization/CSRF, secrets/sessions, migrations, and compatibility. Omit irrelevant areas and justify decisions that change contracts.>

## Acceptance and verification criteria

- **Success:** given <initial state>, when <action>, then <observable result>. Test: <level and scenario>.
- **Failure/boundary:** given <relevant invalid input, denied access, or partial failure>, when <action>, then <response/preserved state>. Test: <level and scenario>.
- **Integration/compatibility:** <affected existing data, API, UI, API docs, or clean installation>. Test: <scenario and environment>.

**Applicable gate:** <commands from ../guidelines/quality.md and risk-based additional checks; consult `.specs/implementation.md` and record execution/limits in Review>.

## Decisions and history

- YYYY-MM-DD — <decision, reason, prior contract replaced, effects, and reference to earlier Review/Spec; do not rewrite history>
