# Code execution record — NNN-name

Append one entry for each Code invocation and ID. Start each attempt as `PENDING`; update that entry to `SUCCESS` only after the task's acceptance criteria and applicable gates pass. Keep earlier entries intact. A resumed invocation adds a new attempt for the pending ID. Do not duplicate approved acceptance text.

## TNNN-01 — <task or finding title> (attempt 1)

- **Kind:** feature task | bug task | Review correction
- **Requirements / task / finding:** <linked IDs>
- **Status:** PENDING | SUCCESS
- **Changed paths:** <actual paths, or `none`>
- **Checks and results:** <commands or manual procedures actually run and their results; include environment limits>
- **Limits:** <relevant environment or verification limits, or `None`>
- **Remaining work / next step:** <what remains and how to proceed, or `None`>
