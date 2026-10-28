# Code execution record — 003-context-isolation

## B003-01 — Make clean context documentation-only guidance (attempt 1)

- **Kind:** bug task
- **Requirements / task / finding:** B003-01; AC1–AC14
- **Status:** SUCCESS
- **Changed paths:** `skills/sdd-lite/guidelines/workflow.md`; all seven `skills/sdd-lite/commands/*.md`; `skills/sdd-lite/SKILL.md`; `README.md`; `docs/index.html`; `.specs/bugs/003-context-isolation/execution.md`. The approved `bug.md` was pre-existing and left unchanged during Code.
- **Checks and results:** Manual consistency review of AC1–AC14 against the updated workflow, seven commands, router, README, and public documentation: PASS. Search for prior operational context gates and warnings in command procedures: none found. Local Markdown link check for SKILL.md, command files, and workflow.md: PASS. `git diff --check`: PASS.
- **Limits:** No automated conversation harness or repository test runner is defined; AC1–AC14 were verified by instruction and documentation inspection, not agent replay. An unrelated untracked `bug_pt_br.md` appeared during the work and was left untouched.
- **Remaining work / next step:** None for B003-01; B003-02 remains a separate task.

## B003-02 — Use artifact Status as the only approval state (attempt 1)

- **Kind:** bug task
- **Requirements / task / finding:** B003-02; AC15–AC22
- **Status:** SUCCESS
- **Changed paths:** `README.md`; `docs/index.html`; `skills/sdd-lite/SKILL.md`; `skills/sdd-lite/commands/{bug,code,feature,plan,spec}.md`; `skills/sdd-lite/guidelines/{specification,workflow}.md`; `skills/sdd-lite/templates/{bug,feature,plan,spec}.md`; `.specs/bugs/003-context-isolation/execution.md`. The earlier B003-01 changes in `commands/{init,review}.md` and other listed shared files were preserved.
- **Checks and results:** Inspected all eight files in `skills/sdd-lite/templates/` and searched the command producers/consumers, guidelines, SKILL.md, README, and public docs for duplicate approval state and name/date/prose requirements: PASS. Audited the Feature → Spec, Spec → Plan, Plan → Code, and Bug → Code approval gates against `Status: approved`; confirmed legacy explicit-approval normalization and that a pending legacy field cannot grant approval: PASS by manual procedure inspection. Markdown local-link check: PASS. HTML local-link check: PASS. `git diff --check`: PASS.
- **Limits:** No automated workflow harness or repository test runner is defined.
- **Remaining work / next step:** None for B003-02. No agent replay or automated workflow harness was available; the transition and legacy-field scenarios were verified by inspecting procedures, not by replaying each workflow.
