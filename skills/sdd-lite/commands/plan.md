# SDD Lite · Plan

Turn a selected `spec.md` into deliverable `TNNN-XX` tasks. Read `.specs/project-context.md` (if missing, suggest `$sdd-lite init`), [workflow](../guidelines/workflow.md), [quality](../guidelines/quality.md), the [template](../templates/plan.md), Feature, Spec, and relevant code/tests. By default, perform Plan only; continue to Code only when the user explicitly included it in the requested scope and its gates pass.


## 1. Check prerequisites

1. Require `spec.md` to have `Status: approved`; if not, stop and identify the missing approval. Confirm the technical choice is recorded, requirements have IDs, and acceptance criteria are observable. Check conflicts with Feature, current code, project-context, and `.specs/implementation.md`. Do not change Feature or Spec. Record any deviation and its impact in the Plan, request explicit user approval for a contract change, and leave affected dependencies pending until decided.
2. Make a short inventory of requirements, consumers, and risks that require work: data/migration, domain, API, UI, security, and operations as applicable. Do not create tasks for layers the feature does not touch.

## 2. Divide into increments

1. Order tasks by dependency and risk. Each ID must deliver usable, verifiable behavior with prerequisites, success, relevant failure, and preservation of the prior contract. Include everything needed to complete that slice: migration, backend, API, UI, tests, and documentation. Technical preparation belongs in the first task that uses it; branches, isolated scaffolding, and formatters are not functional increments.
2. Cite requirements covered by each task and dependencies between IDs. State the test expected to fail before implementation and the applicable gate; for non-behavioral changes, specify a real check instead of a trivial test. If a task is too large for one Code session, divide it into slices that each deliver a usable result.

## 3. Audit the Plan before delivery

1. Check requirement → task → acceptance/verification: every implementable requirement needs a task, and every task must deliver a Spec outcome. Check dependency order and final integration risks, especially data preservation, HTTP contract, authorization, and browser behavior where affected.
2. Write `plan.md` from the template with stable IDs. Keep Plan Status non-approved until the user explicitly approves the completed Plan. Approval changes only Status to `approved`; creating or refining the Plan does not imply approval. Deliver the link, execution order, and any gaps that still prevent Code.
