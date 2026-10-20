# BUG — Spec sem opções técnicas estruturadas

**ID:** 001-spec-opcoes-matriz · **Status:** open · **Date:** 2026-10-20

**Branch:** `fix/001-spec-opcoes-matriz`.

**User validation to start Code:** validated. **Statement:** “aprovar”. **Name:** Paulo Bezerra · **Date:** 2026-10-20.

## Problem

When a Feature has meaningful technical alternatives, the current Spec flow can ask for a choice without a durable, complete comparison. This loses part of the former contract: the old command required two or three viable options and the template contained a criteria-by-option matrix. Users need consistently formatted option descriptions and a traceable comparison before choosing. They also need the pending decision recorded so the reasoning survives the conversation and can be completed into the technical contract after their choice.

## Reproduction

1. Run `$sdd-lite spec <ID>` for a validated Feature with a meaningful technical tradeoff, such as a coverage requirement spanning PHP and JavaScript.
2. Let repository inspection identify multiple viable ways to meet the requirement.
3. Observe that the command may present short prose options and ask for a choice, but does not require the former option format or a decision-criteria matrix, and leaves no `spec.md` decision brief while waiting.

The supplied conversation demonstrates the missing durable comparison. The command procedure is prompt-driven; this repository has no automated workflow runner.

## Root cause

- The former `.specs/commands/spec.md` at `beb6ea0` and `c1b2021` required two or three viable solutions and comparison across security/data integrity, performance, compatibility/migration, simplicity, maintenance/patterns, and operations. It required a recommendation without mechanical scoring.
- The former `.specs/templates/spec.md` at `beb6ea0` and `c1b2021` contained a Markdown matrix with those criteria as rows and option columns, adding a third option column when needed.
- Commit `9534153` (2026-10-16, `feat: add bilingual localization and English docs`) changed the command from “two or three” options to “one or more,” moved the comparison to free-form vertical text, and replaced the template matrix with a prose placeholder. This is where the versioned option/matrix contract was lost.
- Commit `04a7bcb` (2026-10-18, `feat: adopt standalone SDD Lite workflow`) deleted the local command and template while adopting the standalone skill. It migrated the already-simplified version; it did not originate the matrix removal.
- The rule against writing the **final** `spec.md` before the choice is present in the pre-migration command as well as the current command. That behavior was not lost in migration. However, it leaves no durable decision brief, which this correction should address while preserving the rule that the technical contract is not finalized or approved before the choice.
- The migrated `skills/sdd-lite/commands/spec.md` and `skills/sdd-lite/templates/spec.md` preserve the prose-only option description and have no viability matrix. The specification guideline likewise does not restore the former matrix.

These commit objects are present in the local `sandbox_php` checkout, and its `origin/main` resolves to the same head as local `main` (`2723c544e4993d293eb9699ddda0a2194f79e034`). The historic Portuguese command and template were inspected directly. This establishes the change's location and the exact former matrix dimensions.

## Fix

Restore the former option cards and viability matrix in the Spec command, specification guideline, and template, then add a pending-decision state to address the missing durable brief. Before asking the user, create or update `spec.md` as a **decision brief**, containing the verified baseline, constraints, real option cards, icon-only comparison matrix, evidence-based recommendation, and the exact decision requested. Mark the decision as pending; do not present unchosen design details as a final contract.

For a real tradeoff, present two or three materially different, viable options by default, including retaining the current design when it meets the Feature; add an option when it adds a genuine choice. Do not fabricate alternatives to reach a count. If only one solution meets the verified constraints, explain that evidence and do not ask the user to choose. Each option card records: approach, affected components, estimated code impact (low/moderate/high), fit to Feature requirements, concrete benefits, costs and risks, constraints or conditions, and supporting repository or authoritative evidence.

The matrix is a visual summary: options are columns, broad decision criteria are rows, and every cell contains exactly one symbol. Use **✓** for meets the criterion, **✗** for does not meet it, and **⚠** for partial or conditional fit. Define the legend immediately beside the matrix. Do not put prose, numeric scores, or totals in cells. Use the following broad criterion catalog as a checklist, then include only criteria that are relevant and distinguish the options; add Feature-specific drivers as needed:

- Functional fit: requirement coverage and correctness.
- Security and data integrity; safety where harm to people, property, or environment is in scope.
- Reliability: availability, resilience, fault tolerance, and recovery.
- Performance efficiency: latency, resource use, capacity, and scaling.
- Compatibility: interoperability with existing consumers, data, and deployment environments.
- Interaction capability for user-facing changes; include accessibility needs when applicable.
- Maintainability: modularity, testability, diagnosis, and ease of change.
- Flexibility: ability to adapt to likely changes without disproportionate redesign.
- Operational excellence: observability, deployment, support, and incident response.
- Cost and effort: implementation, migration, dependencies, and ongoing operation; include sustainability when relevant.

This is a reusable catalog, not a mandatory ten-row matrix. Omit criteria that do not affect the decision. The option cards carry the evidence and explain every ⚠ and ✗ so the compact matrix never hides why a mark was chosen. Link criteria to Feature requirement IDs where practical. The agent must give an explicit, evidence-based recommendation and identify which criteria drive it; label it as a recommendation, ask the user to choose or adjust, and never treat it as approval. Do not rank options by counting symbols or total scores.

After the user chooses or adjusts an option, update that same `spec.md` with the recorded decision, accepted tradeoffs, and completed technical contract, requirements, and verification criteria. Keep Spec validation for Plan pending until separately stated. The choice must not be treated as validation or as approval of a divergence from the Feature.

Do not change Feature immutability, the requirement for explicit user approval of a divergent contract, the separate Spec validation gate for Plan, or the rule that Spec does not start Plan/Code. Do not edit existing Feature or Spec artifacts as part of the command behavior change.

## Tasks

- [x] **B001-01 — Restore structured options, an explicit nonbinding recommendation, and a visual viability matrix in a durable pending-decision brief.** **Acceptance:** given a validated Feature with meaningful technical tradeoffs, when Spec identifies viable solutions, then before asking the user to choose it records a decision-pending brief in `spec.md`, presents two or three distinct viable options by default in a consistent card format, and includes a criterion-by-option matrix using only relevant criteria from a broad quality/architecture catalog plus Feature-specific drivers. Every matrix cell contains only ✓, ✗, or ⚠, with a nearby legend; the cards explain the evidence and implications behind each mark. The matrix has no scores or totals. The agent explicitly recommends an option and names the criteria that support it, while asking the user to make or adjust the final choice. After the user's choice, the same file records the decision and completes the technical contract, while Plan validation remains pending. Given a verified single viable solution, when Spec finds no real alternative, then it records the evidence and proceeds without fabricated options or a fake comparison. **Test:** manual prompt-procedure review using (a) a multi-stack coverage decision with different native metrics and (b) a Feature whose constraints leave one evident solution; confirm the pending brief, icon matrix, and nonbinding recommendation precede the choice request, and technical choice, Feature deviation approval, and Spec validation remain separate. The repository has no automated runner for this documentation workflow. **Gate:** inspect command, guideline, template, and links; review the historical-to-current behavior against commits `c1b2021`, `9534153`, and `04a7bcb`; check cross-file consistency and the diff.

## Notes

The user explicitly invoked `$sdd-lite bug` and supplied the prior Spec conversation as context. This work changes workflow behavior and adds a decision-brief state, so it does not meet the pinpoint-bug criteria; the recommended flow is Feature → Spec → Plan. Continuing in the requested Bug flow is recorded as the user's authorized workflow exception. The context-isolation recommendation is also waived for this execution because the user explicitly supplied the prior execution context to diagnose this report.

History reviewed: `beb6ea0` and `c1b2021` contain the prior option requirement and matrix; `9534153` removes the matrix and relaxes the option count; `04a7bcb` moves to the standalone workflow after that removal. The matrix is a confirmed prior artifact; a pre-choice persistent `spec.md` brief is a new behavior requested to make the options reviewable and traceable, not a recovered historical behavior.

Format research: MADR supports a structured decision record with context, considered options, and rationale. ISO/IEC 25010:2023 defines nine product-quality characteristics; the official AWS and Azure Well-Architected Frameworks add broad architecture concerns such as operational excellence, reliability, cost optimization, and sustainability. These models provide a more complete source catalog than the former six-row matrix, but a single Spec should select only criteria relevant to the particular decision. The matrix remains icon-only by user preference; its symbols are qualitative summaries, not a scoring model. The agent recommendation must be explicit and explain which criteria drive it, while the user's choice remains final. Sources: [MADR](https://adr.github.io/madr/), [ISO/IEC 25010:2023](https://www.iso.org/standard/78176.html), [AWS Well-Architected pillars](https://docs.aws.amazon.com/wellarchitected/2024-06-27/framework/the-pillars-of-the-framework.html), and [Azure Well-Architected pillars](https://learn.microsoft.com/azure/well-architected/pillars).
