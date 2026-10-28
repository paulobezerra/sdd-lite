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

Earlier decisions are not rewritten by later stages: **Spec does not change Feature; Plan does not change Feature or Spec; Code does not change Feature, Spec, Plan, Bug, or Review; Review does not change Feature, Spec, Plan, or Bug.** Approval is represented only by the validated artifact's `Status`. Plan and Bug define task scope and acceptance; Code records status and evidence only in the workflow folder's `execution.md`. Review may update `review.md` during re-audits or correction tracking.

If the current step finds a conflict, gap, or later decision that contradicts an input, record it **in the current step's artifact**: source, divergence, impact, and rationale. Obtain the user's explicit approval before treating a changed contract as current; represent approval only with that artifact's Status. Code records a needed decision and its impact in `execution.md`, without changing the original requirement text. Review records new findings and re-audit results in the same `review.md`.

For Feature, Spec, Plan, and Bug, the artifact header `Status` is the only approval state. Before approval, use a non-approved value such as `proposed`, `decision pending`, or `open`. When the user explicitly approves the completed artifact, change only its Status to `approved`; do not add approval prose, a separate field, name/date, quotation, history, or log. A technical choice, silence, clarification, or request for the next command is not approval. Downstream commands pass the approval gate when Status is `approved`; preserve independent technical prerequisites and dependencies. For legacy artifacts, at the consuming stage normalize an unambiguous explicit approval in the old validation field by setting Status to `approved` and removing that field. Status already `approved` is sufficient even if a redundant field says pending; remove the obsolete field. A pending legacy field alone does not grant approval. This metadata-only normalization is permitted in the validated upstream artifact at stage entry; it does not permit contract edits. **Code does not require approval for every task.** Its progress, changed paths, checks, and handoff are recorded in the workflow folder's `execution.md`; Code may update an upstream artifact only for this legacy metadata normalization, otherwise it may edit only its workflow folder's `execution.md` among SDD artifacts.

**User-authorized exceptions:** do not use an SDD Lite preference or stage to block an explicit request. For any request that breaks the workflow, explain the rule, why the recommended path protects quality, and the concrete risk of the exception. If the user explicitly insists, proceed within the authorized scope and state in the delivery that the workflow was broken with their authorization. Do not invent validation, choices, tests, or passed gates; keep unproven items pending and describe the real limitation. This does not authorize destructive operations or waive restrictions outside SDD Lite.

### Code execution records

Every feature or bug workflow folder has one `execution.md`, owned by Code. Append one entry per invocation and ID, including Review corrections in the folder containing `review.md`. Each entry identifies the Code ID, work kind, linked requirement/task/finding IDs, status, changed paths, checks with actual results, environment limits, and remaining work/next step. Begin each attempt as `PENDING`; update that active entry to `SUCCESS` only after all acceptance criteria and applicable gates pass. Keep prior attempts intact. If an ID is pending and a later ID is requested, resume the pending ID first; a resumed invocation appends a new attempt for it. Continue recoverable in-scope work; stop for a real external blocker or product/scope decision and describe the handoff. The latest entry is authoritative for current status, but Review independently checks every claim against approved criteria and repository evidence.

## Context guidance and request scope

The README and public documentation may recommend starting a command in a new chat or after clearing context. This is advice only. Procedures must not inspect whether conversation context is clean, infer it from execution records or other artifacts, warn or ask permission based on it, or record an isolation exception. If conversation history is unclear, proceed using the current request and repository artifacts. Accept a user's correction about their chat without recording an exception. Artifact approval and dependency gates remain independent and must still be enforced.

By default, perform only the command or Code task the user requested. An explicit request may cover multiple commands, multiple Code IDs, or the whole Plan; then work in dependency order, preserve every stage gate, and create a separate execution entry for each Code ID. Completing one task never authorizes the rest of the Plan by itself.

## Stage write boundaries

Feature, Spec, Plan, Bug, and Review may write only their stage-owned artifact(s) within `.specs/features/` or `.specs/bugs/`. Init may write only `.specs/project-context.md` and `.specs/implementation.md`. Code may change implementation files in its approved task scope and may update only its workflow folder's `execution.md` among SDD artifacts. A clarification during Bug updates only `bug.md`; it does not switch stages. Preserve each stage's approval and dependency rules.

## Approval gate for stage transitions

Before Spec, Plan, or the first Code task, require the previous delivery artifact to have `Status: approved`: Feature → Spec, Spec → Plan, Plan → Code, and Bug → Code. Do not ask for another approval when Status is already approved. A checkbox, technical choice, silence, clarification, or request for the next command does not change Status. Feature starts the lifecycle and requires no prior approval.

Between Code IDs, follow Plan order and dependencies. Before starting a task, confirm that prerequisites are recorded complete in `execution.md` and that code, diff, and applicable checks support the claim. A status alone is insufficient. If an earlier ID's latest entry is `PENDING`, resume it before a later task. If the requested task is not ready, explain the actual dependency and do not proceed; without an ID, choose the first eligible task. For Review corrections, use findings in `review.md` and record execution in `execution.md`.

## Feature and bug branches; publication before Review

At the start of Feature or Bug, after choosing the ID and before writing its artifact, identify the origin integration branch declared in `.specs/project-context.md`. If it is missing, stop before branch creation and ask the user which origin branch to use; do not infer it from the current checkout. Refresh the declared remote-tracking ref from `origin` and create a new local `feature/NNN-name` or `fix/NNN-name` branch, respectively, from the current `origin/<branch>` tip. If the remote cannot be reached, do not create the branch from a potentially stale local ref; report the issue and wait for direction. Reuse the correct task branch if it already exists. Check workspace state before switching branches to avoid mixing other work. Record the effective branch in `feature.md` or `bug.md`, respectively. Creating the branch is preparation, not a functional task; use the same branch through the flow. For an older Feature or Bug without a recorded branch, establish it and record it in the corresponding artifact, applying these same base checks without changing validated decisions.

Before Review, check branch state, diff, local commit, and remote when accessible. Record whether publication is proven; if remote access is unavailable or no push is verified, state that as an audit limit. Review does not create commits or push. Do not create an automatic publication task or require push for a Code task.

## Change policy and economy

- Do not create a PR, commit, publish, send messages, change a remote environment, or deploy without an explicit request. No destructive operations (database reset, volume cleanup, force operations, file deletion) without authorization and target verification.
- Do not add credentials, a real `.env`, tokens, sensitive logs, or dumps to the repository. Do not add dependencies without checking need, compatibility and support, and reporting the decision. Do not start subagents or autonomous loops without explicit authorization.
- If a Spec or bug diagnosis conflicts with code, identify the conflict, explain it, and propose the smallest change; do not silently fix everything at once. Do not ask for details already present in the artifacts.
- Work on a bounded task; locate with search tools before opening large files; do not read vendored or generated directories, lock files, or `.git` in full; avoid cosmetic edits outside scope and keep formatting-only diffs separate; do not repeat passed checks without a change; say when a test was not run.
