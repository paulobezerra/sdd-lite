# Specification guidelines

Spec turns a validated product Feature into a technical contract. It does not implement the feature or divide it into Plan tasks.

## Understand before choosing

- Read the Feature, `.specs/project-context.md`, `.specs/implementation.md`, and the current code/tests/contracts directly affected. Separate verified current behavior, assumptions, and the requested result.
- Clarify only missing product decisions that change the behavior, permissions, data, compatibility, or boundaries. Do not invent a contract from silence.
- Present real technical alternatives only when meaningful tradeoffs exist. Include retaining the current design when viable; do not fabricate options or rank them mechanically. If one solution is clearly indicated, briefly justify it with repository evidence and proceed.
- For a meaningful tradeoff, present two or three materially different, viable options by default. Add options only when they offer a genuine choice. If only one solution meets verified constraints, explain the evidence and do not fabricate alternatives or ask for a choice.
- Before asking for a choice, save `spec.md` as a decision-pending brief containing the verified baseline, constraints, option cards, comparison matrix, recommendation, and exact decision requested. Cards state approach, affected components, low/moderate/high code impact, fit to Feature requirements, benefits, costs and risks, constraints or conditions, and supporting repository or authoritative evidence.
- Use options as matrix columns and only relevant, distinguishing criteria as rows. Use this catalog as a checklist, adding Feature-specific drivers when useful: functional fit; security, data integrity, and safety where relevant; reliability; performance efficiency; compatibility; user interaction and accessibility; maintainability; flexibility; operational excellence; cost and effort, including sustainability when relevant. Link criteria to Feature requirement IDs where practical.
- Each matrix cell contains exactly one symbol: ✓ means meets, ✗ means does not meet, and ⚠ means partial or conditional fit. Place this legend beside the matrix. No prose, scores, or totals belong in cells. Option cards explain the evidence and implications behind every ⚠ and ✗. Never rank options by counting symbols.
- For multiple viable options, state an explicit, nonbinding recommendation and name its decisive criteria; ask the user to choose or adjust. A recommendation is not approval. For one clearly evident solution, state the evidence-based recommendation and proceed without asking for a choice. When waiting for a choice, do not present unchosen design details as a final contract or proceed to Plan/Code. After the user's choice, update that same `spec.md` with the decision, accepted tradeoffs, and completed contract. A choice does not approve a Feature deviation or validate Spec for Plan.

## Write a verifiable contract

- Give requirements stable IDs and describe initial state, action, observable result, relevant failures, and data that must remain unchanged.
- Define routes, payloads, status codes, permissions, session/CSRF behavior where the project uses them, persistence, migrations, and consumers only to the level needed for acceptance.
- Link every requirement to a verification appropriate to its risk. Include browser or database integration when unit tests cannot prove the boundary.
- Keep Feature immutable. Record later decisions that diverge from it in Spec with source, impact, and explicit user validation; do not silently rewrite the original requirement.
- Record the technical decision and reasoning, then leave validation for Plan pending until the user explicitly validates the Spec. The choice itself does not count as that validation.
