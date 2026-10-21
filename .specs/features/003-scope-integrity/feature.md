# FEATURE — Scope integrity and execution traceability across SDD stages

**ID:** 003-scope-integrity · **Status:** proposed · **Date:** 2026-10-21

**Branch:** `feature/003-scope-integrity`.

**User validation for Spec:** validated. **Statement:** “aprovar a feature”. **Name:** Paulo Bezerra · **Date:** 2026-10-21.

## Business need

Users of SDD Lite rely on Feature, Spec, Plan, Code, and Review to carry a product need through implementation without silently changing earlier decisions. Spec has a decision-quality gap: when several approaches exist, users need complete, comparable options and a viability matrix, and the recommendation must follow the validated Feature's priorities and constraints. A recommendation can otherwise favor implementation convenience even when it conflicts with the requested outcome. This is especially consequential because users rely on Spec to make the design decision before Plan and Code.

There are also execution-traceability gaps. Spec and Plan can attempt to repair or resolve artifacts and problems that they should only identify and record. Code can alter Feature, Spec, or the approved task scope and acceptance criteria to make an implementation fit. Its progress is mainly reported in the session, which makes it harder to preserve a durable account of work and compare that account with the code changes. A Code execution can also end without a clear completion status, allowing a later execution to begin another task before the previous one is complete.

These gaps make it difficult for users and reviewers to know whether a technical recommendation honors the requested outcome, which decisions are authorized, what remains pending, and whether implementation evidence supports a completion claim. The need is to make Spec's comparisons and recommendations faithful to the Feature, while clarifying a few misaligned points in the lightweight execution flow. For example, a Code task may add a coverage command and thresholds, correctly report that the checks fail because coverage is below the minimum, preserve the unchecked Plan item, and identify the remaining work as adding frontend tests. If that work is still within the approved task and needs no user decision, ending the execution there leaves the user unsure whether Code is blocked or simply stopped early, and forces them to ask it to continue. This calls for clear expectations about continuing in-scope work and reporting a real blocker, while keeping the response proportionate to the task.

## Desired outcome

Users and agents can carry work through each SDD Lite stage with clear, aligned expectations. Before a technical decision, users can compare complete option cards and a viability matrix when multiple viable approaches exist, and see a recommendation grounded in the validated Feature's stated priorities and constraints. Recommendations do not violate explicit user preferences or hard constraints; if no option fits, Spec asks for the minimum decision needed. When only one approach is viable, Spec supports it with evidence rather than inventing alternatives. The workflow also preserves approved decisions, surfaces divergences for the right decision or validation, continues in-scope work, and makes Code's completion state and evidence easy to find. These changes keep the flow lightweight and let Review independently check completion claims.

## Boundaries and context

- **Included:** Make Spec's multi-option decision process explicit and reliable: require full option cards and a viability matrix whenever multiple materially viable approaches exist; show them to the user in the delivery; ground criteria and recommendations in the validated Feature; exclude any recommendation that violates a hard constraint or explicit preference; and explain evidence when only one approach is viable. Also clarify existing command boundaries and divergence handling; prevent Code from editing Feature, Spec, Plan, Bug, or Review to record progress; resolve conflicting Code-edit rules; define Code continuation, durable `SUCCESS`/`PENDING` state, evidence, and resumption; ensure Review independently checks claims; and evaluate the smallest durable execution record, adopting it only when simpler changes cannot meet the outcome.
- **Out of scope:** Implementing command, guideline, template, documentation, or adapter changes during the Feature stage; writing the Plan; redesigning the workflow or adding a new routine stage; adding records beyond the justified execution record; treating a progress report or status as proof of acceptance; recommending architecture from this Feature alone.
- **Product constraints:** Preserve SDD Lite's lightweight purpose and existing flow. Feature outcomes, explicit user priorities, hard constraints, and preferences guide Spec decisions; repository convenience cannot override them. Do not fabricate alternatives or matrices when only one solution is viable. Keep options and the matrix complete enough to make the decision reviewable, without adding irrelevant criteria or ranking by symbol counts. Preserve stage isolation and approved inputs. Any execution record must be justified by the need for persistent handoff and kept proportionate.

## Success signals

- When multiple materially viable technical approaches exist, users receive complete option cards and a viability matrix in both the saved Spec brief and the delivery response before being asked to choose; every card explains partial or failed fit.
- Spec recommendations explicitly follow the Feature's outcomes, priorities, hard constraints, and user preferences. An option that violates a hard constraint is not recommended; if none fit, Spec asks for the minimum decision needed. If only one option is viable, evidence explains why relevant alternatives fail without fabricated choices.
- Reviewers can trace each recommendation to Feature criteria and assess whether the chosen option honored them, including when the recommendation favored less implementation work.
- Users can tell what each stage is responsible for, what it may edit, and how it should respond when it finds an upstream or implementation divergence.
- When a task contract or scope is unsuitable, Code leaves the approved Feature, Spec, and Plan criteria intact and provides a clear route to the required decision or validation.
- After any Code execution, the user can find a persistent `SUCCESS` or `PENDING` status and understand the supporting evidence or, for pending work, the reason, remaining work, and next step. If the next step is within the approved scope and requires no user decision, Code continues the work rather than ending with a progress report that merely tells the user to continue it.
- A later Code execution detects an unfinished prior task and does not start a subsequent task until the pending work has been resolved through the defined process.
- Review can independently compare reported criteria, changed files, diff, code, and applicable checks, and does not accept a checkbox or execution report alone as proof of completion.
- The selected approach resolves the demonstrated gaps with the least added process, preserving SDD Lite's lightweight use; any additional artifact or mandatory procedure has a clear need that simpler clarifications cannot meet.

## Validation history

- 2026-10-21 — Earlier Feature text was validated for Spec by Paulo Bezerra (“aprovar”). That validation predates this user-authorized revision.
- 2026-10-21 — Paulo Bezerra explicitly authorized this session's exception to the usual Feature immutability rule and requested that Spec option/matrix quality and recommendation alignment become the Feature's top priority.
