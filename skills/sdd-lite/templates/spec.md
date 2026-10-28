# SPEC — <feature name>

**ID:** NNN-name · **Status:** decision pending | proposed · **Date:** YYYY-MM-DD

## Problem, baseline, and goal

<who is affected; verified current behavior and code/contract reference; expected outcome>

## Scope and constraints

- **Included:** <outcomes in this Spec>
- **Out of scope:** <explicit boundaries>
- **Constraints:** <compatibility, stack, deployment, dependencies, and relevant data; see project-context>

## Decision brief — complete before asking the user to choose

**Verified baseline:** <observed behavior and repository/code evidence>

**Feature decision drivers:** <desired outcomes, scope boundaries, hard constraints, priorities, and explicit preferences; identify which are hard constraints and cite relevant Feature requirement IDs>

### Option cards

#### Option A — <name>

- **Approach:** <what changes or stays>
- **Affected components:** <components>
- **Estimated code impact:** low | moderate | high
- **Fit to Feature:** <requirement IDs and how this meets them; explicitly state any partial or failed fit and its evidence>
- **Benefits:** <concrete benefits>
- **Costs and risks:** <concrete costs, risks, and implications>
- **Constraints or conditions:** <conditions, or “None”>
- **Evidence:** <repository paths, observed contracts, or authoritative sources>

<Repeat for each real, materially different option that satisfies every hard constraint; two or three viable options by default when meaningful tradeoffs exist. Do not invent options to reach a count.>

### Viability matrix

<For multiple viable options only: include the matrix below using relevant, decision-distinguishing Feature criteria as rows and viable options as columns. Add or remove columns to match the real options. Every cell contains exactly one symbol and nothing else. Omit this entire section when only one option is viable or no option fits.>

| Criterion | Option A | Option B |
|---|---:|---:|
| <relevant criterion / requirement ID> | ✓ | ⚠ |

**Legend:** ✓ meets · ✗ does not meet · ⚠ partial or conditional fit. The option cards explain the evidence and implications behind every ⚠ and ✗. No scores or totals.

**Recommendation:** <for multiple options, recommend only an option compatible with all hard constraints and explicit preferences; name decisive Feature criteria and accepted tradeoffs. If no option fits, state that and ask the minimum decision. For one evident solution, state its evidence-based justification and why relevant alternatives fail.>

**Decision requested:** <for multiple options, ask the user to choose or adjust; if no option fits, ask only the decision needed to resolve the conflict; for one evident solution, write “None — proceed with the only viable solution.” This does not approve the Spec.>

<When only one solution is viable, state verified evidence and why hard constraints rule out relevant alternatives; omit fake cards and matrix. Present this explanation in the user-facing delivery too, and proceed without asking the user to choose. For multiple viable options, the delivery must reproduce the complete cards and matrix from this brief before asking for a choice.>

## Technical solution

**Technical decision:** <while pending, write “Pending user choice”; after choice, record the user's choice and date. For one clearly evident solution, give the date and code-based reason. Do not attribute a choice to the user without their statement.>

<Summarize only real options: the clearly evident solution or the selected option and relevant alternatives, in separate blocks. For each, record estimated code impact (low, moderate, or high), affected components, and decision-relevant fit or caveats. Identify criteria that do not apply. Avoid extensive comparison without a real tradeoff.>

**Reason for the decision:** <verified evidence, decisive benefit, and accepted cost; for a single solution, explain why no relevant alternative exists>.

## Open product questions

<List product decisions or Feature deviations the user still needs to assess. For each, cite the prior contract, real options, impact, and current proposal. If none remain, write “None” so the check is visible before approval. An earlier technical choice does not approve the Spec.>

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
