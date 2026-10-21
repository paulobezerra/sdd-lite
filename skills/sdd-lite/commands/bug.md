# SDD Lite · Bug

Short flow for a **pinpoint bug**: **Bug → Code → Review**, with one artifact, `.specs/bugs/NNN-name/bug.md`, in place of Feature → Spec → Plan. Read `.specs/project-context.md` (if missing, suggest `$sdd-lite init`), [workflow](../guidelines/workflow.md), [quality](../guidelines/quality.md), and the [template](../templates/bug.md). Read `.specs/implementation.md` for the project's conventions. This flow exists to save tokens and steps: do not add spec or plan files, and do not explore beyond the suspected area. This step diagnoses and writes the task list; it does not fix the bug. End after Bug.

Before starting, apply the [context isolation rule](../guidelines/workflow.md#recommended-isolation-clean-context-for-each-execution). If a previous execution's context is still present, briefly warn about the quality and traceability risk and recommend clearing the context, either here or in a new conversation. Do not block the user; if they explicitly insist on continuing with accumulated context, proceed and state in the delivery that they authorized the exception. Reconstruct state from versioned artifacts and the actual repository.

## 1. Triage: is it really a pinpoint bug?

It is a pinpoint bug only if **all** of these hold:

1. Existing behavior contradicts an expectation that is already clear (a spec, a test, documented behavior, or an obvious invariant); nothing about the desired behavior is a new product decision.
2. The cause is probably local: one area, a few files.
3. The fix needs no public contract change (API, schema, events, CLI), no data migration, and no choice between design alternatives.
4. It does not hide a missing capability, a security or data-integrity redesign, or a cross-cutting refactor.

If any criterion fails, **do not continue**: explain which one failed and recommend `$sdd-lite feature` (Feature → Spec → Plan). If the user explicitly insists on the bug flow, proceed and record the exception in `bug.md` **Notes**, following the workflow exception rule. If the report is vague, ask only the minimum needed to reproduce: expected versus actual behavior, steps, input, and environment. If the item turns out to be a bug already covered by a feature's open Review finding, point to that finding instead of opening a bug.

## 2. Diagnose with minimal cost

1. Reproduce or locate the failing path in the cheapest way: search for the symptom, read the relevant function and its tests, and run the failing test or command from project-context when safe. Do not read or analyze the whole repository.
2. Establish the **root cause** with file and line evidence. Separate verified facts from assumptions, and say what you did not manage to verify. Do not stop at the symptom.
3. Define the **smallest fix** that addresses the cause, and list what must not change: public contracts, existing data, behavior covered by existing tests. Check for the same defect elsewhere (same pattern, same helper) and either include it in scope when it is the same root cause or note it as out of scope.
4. If the investigation shows the bug is larger than triaged (more areas, a contract or data change, real design alternatives), stop and recommend the feature flow, summarizing what you found so it is not lost.

## 3. Branch, write, check

1. Use the ID or folder supplied by the user, or the next free `NNN` in `.specs/bugs/`; preserve existing files. Check the branch and workspace state. Before writing `bug.md`, identify the origin integration branch declared in `.specs/project-context.md`. If it is not declared, stop before creating the branch and ask the user which origin branch to use; do not infer it from the current checkout. Refresh that branch's remote-tracking ref from `origin` and base a new `fix/NNN-name` branch on the resulting current `origin/<branch>` tip. If the remote cannot be reached, do not create the branch from a potentially stale local ref; report the issue and wait for direction. Reuse the correct bug branch if it exists, and do not mix another task's changes. Record the effective branch in the artifact.
2. Fill `bug.md` from the template: problem (observed versus expected, who is affected, severity), reproduction, root cause with evidence, fix and what must not change, and the task list. Usually there is **one** task `BNNN-01`; add more only when they are independently verifiable. Each task has an acceptance criterion (given/when/then), a regression test **expected to fail before the fix**, and the focused gate from project-context. For a bug whose behavior cannot be tested automatically, specify the real manual or environment check instead, and say why.
3. Check that someone outside the conversation can follow the diagnosis, that the fix is the smallest sufficient one, and that no spec or plan content crept in. Leave "validation to start Code" pending: the user's single explicit validation of `bug.md`, recorded with their name and the OS date, replaces the three feature validations. Deliver the link, branch, root cause, task list, and pending questions. Stop; do not fix, commit, or start Code.

## 4. What happens next

- `$sdd-lite code BNNN-01` executes the task and only ticks its checkbox in `bug.md`.
- `$sdd-lite review <ID>` audits it and creates `review.md` in the same bug folder. Corrections found there go through `code` again.
