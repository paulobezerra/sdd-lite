# SDD Lite · Feature

Turn a product need into `.specs/features/NNN-name/feature.md`. Read `.specs/project-context.md` (if missing, suggest `$sdd-lite init`), [workflow](../guidelines/workflow.md), and the [template](../templates/feature.md). This step defines **why**, **for whom**, and **what outcome**; it does not choose architecture. By default it ends after Feature; continue into later stages only when the user explicitly included them in the requested scope and their gates pass.


## 1. Triage and understand the request

0. If the request is really a pinpoint defect (existing behavior is wrong, the fix is small and local, and no product decision is needed), say so and recommend `$sdd-lite bug`, which skips Spec and Plan; continue here only for a genuine new capability or if the user insists.

1. Identify the affected user or operator, the current problem, its consequence, and the desired outcome. Separate observed product facts from assumptions. Consult only the necessary context; if the idea concerns already specified behavior, find the existing feature/spec before opening another ID.
2. Define what is included now and what is excluded. Record known product and compatibility constraints without turning implementation details into product requirements. When product paths differ, clarify only the choice that prevents defining the outcome; other questions may remain explicitly open.

## 2. Prepare the branch, write, and check

1. Use the ID/folder supplied by the user or the next free `NNN` in `.specs/features/`; preserve existing files. Check the branch and workspace state. Before writing `feature.md`, identify the origin integration branch declared in `.specs/project-context.md`. If it is not declared, stop before creating the branch and ask the user which origin branch to use; do not infer it from the current checkout. Refresh that branch's remote-tracking ref from `origin` (for example, fetch the declared branch) and base a new `feature/NNN-name` branch on the resulting current `origin/<branch>` tip. If the remote cannot be reached, do not create the branch from a potentially stale local ref; report the issue and wait for direction. Reuse the correct feature branch if it exists; do not mix another task's changes. Record the effective branch in the artifact. If an older Feature was delivered without a branch, establish it using these same base checks and complete this metadata in `feature.md` without changing decisions.
2. Fill the template with the need, outcome, boundaries, observable success signals, and open questions. A success signal should show the effect on a user or operator without prescribing a class, library, or technical test.
3. Check whether someone outside the conversation can tell who benefits and how, what is excluded, and which product choices remain. Remove premature technical solutions, vague promises, and duplicate features. Set `Status: proposed` until the user explicitly approves the completed Feature; approval changes only `Status` to `approved`. Creating or refining the Feature does not imply approval. Deliver the link, branch, expected outcome, and pending questions.
