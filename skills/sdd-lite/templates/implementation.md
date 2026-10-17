# IMPLEMENTATION CONVENTIONS — <project name>

**Updated:** YYYY-MM-DD · **Origin:** <observed in code | decided with the user | both>

Starting point for Spec, Code, Bug and Review; the feature Spec defines the contract and justifies exceptions. Each rule carries its **status**: `observed` (found in code/tests, cite the evidence), `decided` (confirmed by the user, with date), or `assumption` (unconfirmed; do not enforce in Review). Keep rules short and testable; drop sections that do not apply. Stack, commands and structure live in [project-context.md](project-context.md), not here.

## Boundaries and composition

- <layering and dependency direction; where contracts vs. implementations live; how new modules are wired in; rules about thin adapters, no I/O in the domain, etc.> — `<status>`, `<evidence: path or test>`

## Contracts and security

- <input validation and error mapping; authentication/authorization rules; session/CSRF/rate-limit practices; secrets handling; output encoding; API documentation upkeep> — `<status>`, `<evidence>`

## Data and persistence

- <query practices; migration policy (additive, never edit applied ones); transactions; money/time/ID representation; data preservation expectations> — `<status>`, `<evidence>`

## Client and interface

- <frontend/CLI/UI structure and constraints (e.g. no build step); how calls to the backend are organized; error and loading handling> — `<status>`, `<evidence>`

## Testing and quality gates

- <test levels and layout; what a unit test may and may not prove; boundary/integration expectations; the aggregate gate and which checks write files> — `<status>`, `<evidence>`

## Prohibited patterns

- <things the project explicitly avoids: custom frameworks, unnecessary abstractions, unsafe APIs, dependency policy> — `<status>`, `<evidence>`

## Open questions

<conventions that could not be established; remove if none>
