# PROJECT CONTEXT — <project name>

**Updated:** YYYY-MM-DD · **Origin:** <new project (user-provided) | existing project (analyzed) | both> · **Artifact language:** <e.g. pt-BR, en>

<Keep this file short and factual. Mark every unverified statement as "assumption". Never include secrets.>

## Purpose

<what the project is, for whom, and the problem it solves>

## Stack and constraints

- **Languages/frameworks/runtime:** <versions>
- **Data/infrastructure:** <databases, services, deployment model>
- **Hard constraints:** <e.g. no build step, compatibility, hosting limits, compliance>

## Structure and boundaries

<key directories and what lives where; dependency direction and layering rules; where new code of each kind goes>

## Commands

<verified commands only; say how to run them (host, container, etc.) and what needs to be running>

- Install: `<cmd>`
- Run: `<cmd>`
- Test: `<cmd>` · focused: `<cmd>`
- Lint/format/static analysis: `<cmd>`
- Full quality gate: `<cmd>`

## Conventions

Implementation rules (boundaries, contracts, security, data, testing) live in [implementation.md](implementation.md); do not duplicate them here.

## Authorization limits

<operations agents must not do without authorization: destructive DB commands, deploys, etc.>

## Current state and known risks

<existing features/areas in one line each, tech debt, fragile areas, missing tests; omit for an empty project>

## Open questions

<unknowns to resolve; remove if none>
