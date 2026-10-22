# SDD Lite workflow

Paths here are relative to this skill; project artifacts live under `.specs/` in the user's repository.

There are two flows. Each execution performs only the requested step.

- **Feature:** **Feature → Spec → Plan → Code → Review**, followed by **Code → Review** for corrections. A feature folder has `feature.md`, `spec.md`, `plan.md`, `execution.md`, and `review.md`. Code records progress and evidence in `execution.md`; Review records findings and re-audits in the same `review.md`.
- **Bug:** **Bug → Code → Review**, for a pinpoint defect that needs no product decision, contract change, migration, or design alternatives. A bug folder has `bug.md` (problem, reproduction, root cause, fix, and task contract), `execution.md`, and `review.md`. The `bug` command triages first and redirects to the feature flow when the problem is not pinpoint. It exists to save tokens and steps, so do not add spec or plan files to a bug.

`code` and `review` serve both flows. The ID prefix (`T…` = feature task, `B…` = bug task) or the folder tells them which; Code writes only `execution.md` among SDD artifacts, and Review writes findings in `review.md` inside the item's folder.

`init` creates two project-level artifacts that hold everything project-specific: `.specs/project-context.md` (purpose, stack, structure, commands, authorization limits, artifact language), which every command reads first, and `.specs/implementation.md` (verified implementation conventions: boundaries, contracts, security, data, testing), which Spec, Code, Bug and Review also read. Conventions marked `assumption` are not enforced. Re-run `init` to refresh them; change a rule there, never inside a feature artifact. This skill contains no project-specific rules.

The executable procedures live in [commands](../commands/). [Guidelines](.) define shared rules and [templates](../templates/) define artifacts. Change workflow behavior here and in the relevant command; project-specific adapters must not duplicate rules.

**Multi-agent premise:** SDD Lite must work with any agent that can read repository commands and artifacts. Do not implement workflow rules only through hooks, plugins, session state, or agent-specific commands. Adapters may improve discovery, but cannot be the only way to enforce a rule, record a decision, or verify a gate.

## Immutable inputs between steps

Earlier decisions are not rewritten by later stages: **Spec does not change Feature; Plan does not change Feature or Spec; Code does not change Feature, Spec, Plan, Bug, or Review; Review does not change Feature, Spec, Plan, or Bug.** Explicit validation stays in the validated artifact. Plan and Bug define task scope and acceptance; Code records status and evidence only in the workflow folder's `execution.md`. Review may update `review.md` during re-audits or correction tracking.

If the current step finds a conflict, gap, or later decision that contradicts an input, record it **in the current step's artifact**: source, divergence, impact, and the user's explicit statement approving the change. Without that validation, leave it pending and do not treat the changed contract as approved. Code records a needed decision and its impact in `execution.md`, without changing the original requirement text. Review records new findings and re-audit results in the same `review.md`.

Validation is recorded only in the validated artifact: Feature in `feature.md`, Spec in `spec.md`, and Plan in `plan.md`. Record the explicit statement, the name supplied by the user, and the date obtained from the OS. **Code does not require user validation for every task.** Its progress, changed paths, checks, and handoff are recorded in the workflow folder's `execution.md`; Code may not edit other SDD artifacts. Existing validation fields remain valid.

**User-authorized exceptions:** do not use an SDD Lite preference or stage to block an explicit request. For any request that breaks the workflow, explain the rule, why the recommended path protects quality, and the concrete risk of the exception. If the user explicitly insists, proceed within the authorized scope and state in the delivery that the workflow was broken with their authorization. Do not invent validation, choices, tests, or passed gates; keep unproven items pending and describe the real limitation. This does not authorize destructive operations or waive restrictions outside SDD Lite.

### Code execution records

Every feature or bug workflow folder has one `execution.md`, owned by Code. Append one entry per invocation and ID, including Review corrections in the folder containing `review.md`. Each entry identifies the Code ID, work kind, linked requirement/task/finding IDs, status, changed paths, checks with actual results, environment limits, and remaining work/next step. Begin each attempt as `PENDING`; update that active entry to `SUCCESS` only after all acceptance criteria and applicable gates pass. Keep prior attempts intact. If an ID is pending and a later ID is requested, resume the pending ID first; a resumed invocation appends a new attempt for it. Continue recoverable in-scope work; stop for a real external blocker or product/scope decision and describe the handoff. The latest entry is authoritative for current status, but Review independently checks every claim against approved criteria and repository evidence.

## Recommended isolation: clean context for each execution

**Recommend starting each SDD Lite command or Code ID with clean context, and run only the requested step.** Clearing the current conversation's context (for example, with `/clear`) and opening a new conversation are equally valid ways to do this; SDD Lite does not prefer either. No automatic clearing is required. Reconstruct the required state from versioned artifacts and the actual repository state, regardless of how context was cleared. The current request supplies the scope and any new user decision; memory of an earlier execution is not evidence. A response needed to finish the current command, such as a technical choice during Spec or validation of the result, stays in the same execution.

**Check before each execution:** if the available conversation contains a completed or blocked Feature, Spec, Plan, Code, or Review execution and its context has not been cleared, warn before proceeding: **accumulated assumptions and provisional decisions may compromise the quality and traceability of the next step**. Briefly explain the risk and recommend clearing the context, either in the current conversation or by opening a new one. This warning is not a block. If the current request explicitly insists on continuing with accumulated context, proceed; otherwise wait for the user's decision. When proceeding, execute only the requested command, reconstruct inputs from versioned artifacts and actual repository state, and do not treat conversation history as validation, a technical choice, or implementation evidence. In the delivery, state that the recommended isolation was waived with the user's explicit authorization. The warning does not replace required validation between stages.

### Why isolate executions

Feature, Spec, Plan, Code, and Review have different inputs, decisions, and exit criteria. With context carried across executions, an agent may mistake assumptions or rejected alternatives for authorization for the next stage without checking repository state. Starting with clean context supports reconstruction from recorded evidence: Feature validation feeds Spec; validated Spec feeds Plan; approved task criteria and the latest execution record feed later Code work; completed tasks and diff feed Review. This reduces reliance on transient memory and makes decisions easier to audit.

Clearing context by either method is an isolation measure, not a technical guarantee. Each command still checks validation, branch, prerequisites, and evidence under its own rules. The cost is reconstructing context at each execution; the benefit is finding divergence before it spreads.

## Entry premise: explicit validation of the previous step

Before Spec, Plan, or the first Code task, check explicit user validation in the previous delivery artifact: Feature → Spec, Spec → Plan, Plan → Code. For a bug, a single validation recorded in `bug.md` covers Bug → Code. The record includes the **user-supplied name** and a **date obtained from the operating system when recording it**. A checkbox, gate, or lack of objection does not prove validation. A technical choice during Spec does not replace validation of the completed Spec.

If the record is missing, explain which delivery needs validation and wait for the user to explicitly say it is validated. Ask for their name if it has not been supplied; run `date +%Y-%m-%d` on the OS when recording the statement, and add it only to the validated artifact. Do not substitute a user-supplied date or file creation date. If the user insists on proceeding without validation, follow the exception rule above: do not claim the gate passed, and record the pending validation in the new artifact and delivery. Feature starts the lifecycle and requires no prior validation.

Between Code IDs, follow Plan order and dependencies. Before starting a task, confirm that prerequisites are recorded complete in `execution.md` and that code, diff, and applicable checks support the claim. A status alone is insufficient. If an earlier ID's latest entry is `PENDING`, resume it before a later task. If the requested task is not ready, explain the actual dependency and do not proceed; without an ID, choose the first eligible task. For Review corrections, use findings in `review.md` and record execution in `execution.md`.

## Feature and bug branches; publication before Review

At the start of Feature or Bug, after choosing the ID and before writing its artifact, identify the origin integration branch declared in `.specs/project-context.md`. If it is missing, stop before branch creation and ask the user which origin branch to use; do not infer it from the current checkout. Refresh the declared remote-tracking ref from `origin` and create a new local `feature/NNN-name` or `fix/NNN-name` branch, respectively, from the current `origin/<branch>` tip. If the remote cannot be reached, do not create the branch from a potentially stale local ref; report the issue and wait for direction. Reuse the correct task branch if it already exists. Check workspace state before switching branches to avoid mixing other work. Record the effective branch in `feature.md` or `bug.md`, respectively. Creating the branch is preparation, not a functional task; use the same branch through the flow. For an older Feature or Bug without a recorded branch, establish it and record it in the corresponding artifact, applying these same base checks without changing validated decisions.

Before Review, check branch state, diff, local commit, and remote when accessible. Record whether publication is proven; if remote access is unavailable or no push is verified, state that as an audit limit. Review does not create commits or push. Do not create an automatic publication task or require push for a Code task.

## Change policy and economy

- Do not create a PR, commit, publish, send messages, change a remote environment, or deploy without an explicit request. No destructive operations (database reset, volume cleanup, force operations, file deletion) without authorization and target verification.
- Do not add credentials, a real `.env`, tokens, sensitive logs, or dumps to the repository. Do not add dependencies without checking need, compatibility and support, and reporting the decision. Do not start subagents or autonomous loops without explicit authorization.
- If a Spec or bug diagnosis conflicts with code, identify the conflict, explain it, and propose the smallest change; do not silently fix everything at once. Do not ask for details already present in the artifacts.
- Work on a bounded task; locate with search tools before opening large files; do not read vendored or generated directories, lock files, or `.git` in full; avoid cosmetic edits outside scope and keep formatting-only diffs separate; do not repeat passed checks without a change; say when a test was not run.
