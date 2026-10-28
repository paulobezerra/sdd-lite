# SDD Lite · Review

Audit a feature or a bug after its Code tasks, or re-audit requested corrections. Resolve the target from the ID or context (`.specs/features/NNN-name/` or `.specs/bugs/NNN-name/`; ask if ambiguous) and write `review.md` **inside that folder**. Read `.specs/project-context.md` (if missing, suggest `$sdd-lite init`), [workflow](../guidelines/workflow.md), [review](../guidelines/review.md), [quality](../guidelines/quality.md), `.specs/implementation.md` (the conventions the work is audited against), the [template](../templates/review.md), then the source artifacts: Feature, Spec, Plan, and `execution.md` for a feature, or `bug.md` and `execution.md` for a bug. This step records evidence and corrections in `review.md`; it does not implement corrections in the same execution.


## 1. Fix the audit baseline

1. Identify the audited scope and check the Plan task criteria (or Bug task contract), the relevant `execution.md` entries, and the actual diff. Treat execution entries as evidence, not approval or proof: independently compare each claimed status, changed path, check, and remaining-work statement with approved criteria, repository code/diff, and applicable check results. A `SUCCESS` entry with missing or contradictory evidence remains unverified; a `PENDING` entry identifies claimed open work to assess against its criteria. **Review does not require validation of each Code iteration.** Separate pre-existing changes from feature changes. Confirm later decisions that replaced earlier contracts without rewriting Feature or Spec.
2. Check the local branch, `git status --short`, `HEAD`, and the remote when accessible. Record what could be verified; missing commit, push, or network access is an audit limitation, not an automatic publication task. Do not commit or push.
3. Trace requirement → task criteria → execution claim → code and checks. Check the diff against the project's `observed` and `decided` conventions in `.specs/implementation.md` (not its assumptions), and report deviations as findings. Look for requirements without delivery, unsupported or contradictory execution claims, divergent implementation, and contract regressions. For older Plans that actually use task checkboxes, verify their state against implementation and tests. Check affected boundaries as relevant.

## 2. Gather evidence for the audit

1. On the first audit, run the complete suite and applicable aggregate quality gates, plus focused checks that can confirm or refute the main risks. On later audits, verify corrections and affected behavior; repeat broad gates only when the impact invalidates earlier evidence or creates a concrete risk. Follow `quality.md` and the project's execution instructions. Record command, result, and environment/date. Distinguish tests run now, direct code observations, evidence inherited from an earlier review, and inference. An old test is not a rerun; an unrun test is not a pass.
2. For a failure, record reproduction conditions and effect. For missing evidence, state what remains uncertain and whether it blocks acceptance; do not automatically call it a proven defect. Prioritize integrity and security, then contract and predictability.

## 3. Record the conclusion

1. Create `review.md` for the first audit; for re-audits, update that same file, preserving relevant IDs and decisions. Give each finding a stable ID, evidence, impact, sufficient correction, acceptance, and test. Reassess earlier findings in the file using current evidence. Do not commit or push during Review.
2. **Do not change Feature, Spec, Plan, Bug, or `execution.md`.** Record proven and pending requirements in `review.md`; if there are no findings, record the conclusion and its limits. Do not ask the user to validate every correction or Code round. Deliver the link, state, and checks. Continue into Code corrections only when the user explicitly included them in the requested scope.
