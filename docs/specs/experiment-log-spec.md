# Experiment Log — Specification

Version: v1.0

The Experiment Log (EL) records the execution and results of assumption validation activities defined in the Assumption Register. It closes the loop between validation plans and actual evidence, ensuring that the Discovery PRD is informed by validated (or invalidated) assumptions rather than untested beliefs. It is the fourth governed artifact in the Product Intelligence Kit, sitting between the Assumption Register and the Discovery PRD.

---

## What This Artifact Is Not

- **Not a product experiment backlog.** The EL documents experiments already conducted, not planned experiments. If an experiment has not been run, it does not appear in the EL.
- **Not a plan for future experiments.** Future validation belongs in the AR Validation Plan. The EL records what happened.
- **Not a retrospective or recommendations document.** The EL records what was observed. Recommendations are a bounded section grounded in evidence — not the primary purpose of the artifact.

---

## Upstream Dependencies

- Frozen Problem Framing Document (PFD)
- Frozen Value Hypothesis (VH)
- Frozen Assumption Register (AR)

---

## Required Sections

1. Document Control
2. Upstream References
3. Experiment Inventory
4. Results Summary
5. Assumption Status Update
6. Impact Assessment
7. Recommendations
8. Open Questions
9. Freeze Declaration

---

## Content Rules

### Document Control
- Must include artifact ID in format `EL-{PROJECT}-{NNN}`
- Must include version, date, author, and status (Draft / Validated / Frozen)
- Must reference the frozen PFD, VH, and AR artifact IDs

### Upstream References
- Must reference the frozen PFD, VH, and AR by artifact ID
- Must state how many assumptions from the AR were targeted for validation

### Experiment Inventory
- Must contain at least one experiment entry
- Each experiment must include:
  - **Identifier**: EXP-N format
  - **Target assumption**: Reference to AR assumption (ASM-N)
  - **Hypothesis tested**: What the experiment aimed to confirm or disprove
  - **Method**: How the experiment was conducted (user interviews, data analysis, prototype test, survey, market research, etc.)
  - **Sample / scope**: Size, selection criteria, and representativeness of the sample or analysis scope
  - **Raw findings**: What was observed or measured — factual, without interpretation
  - **Conclusion**: Confirmed, Invalidated, Inconclusive, or Partially Confirmed
  - **Confidence level**: High, Medium, or Low — how much weight the conclusion should carry
  - **Limitations**: What could affect the reliability of this result
- Experiments must trace to specific assumptions in the AR
- Findings must be factual observations, not interpretations or recommendations
- Experiments must not propose solutions or implementation details

**Failure examples:** Raw finding reads "users found the process helpful" (interpretation, not observation — what did they say or do?). Raw finding reads "the experiment confirmed our hypothesis" (conclusion, not finding). Conclusion present without supporting findings. Valid raw finding: "7 of 8 interviewed users described a weekly reconciliation task taking 2–4 hours; 1 user automated this with a script."

### Results Summary
- Must provide an aggregate view of experiment outcomes
- Must count experiments by conclusion (Confirmed / Invalidated / Inconclusive / Partially Confirmed)
- Must identify which high-risk assumptions (from AR) have been tested and which remain untested

### Assumption Status Update
- Must provide an updated status for every assumption in the AR based on experiment results
- Each assumption must show: original risk level, experiment reference (or "Not tested"), updated status (Confirmed / Invalidated / Inconclusive / Untested / Partially Confirmed)
- Must not modify the assumption statements themselves — this is a status overlay, not a rewrite

### Impact Assessment
- For any invalidated or partially confirmed assumptions: must describe the impact on the initiative
- Must identify which value hypotheses (VH HYP-N) are affected by invalidated assumptions
- Must identify whether any invalidated assumptions should trigger re-entry on upstream artifacts
- For confirmed assumptions: may note that they de-risk the initiative

### Recommendations
- Must state whether the initiative should proceed, pivot, or pause based on experiment results
- Must identify any assumptions that still require validation before proceeding to the Discovery PRD
- Recommendations must be grounded in experiment evidence — not opinions
- Must not propose solutions or implementation approaches

### Open Questions
- Must list questions raised by experiment results
- Each question must be categorized as blocking or non-blocking

### Freeze Declaration
- Must include a freeze declaration statement when the artifact is frozen
- Must include the date of freeze and the approver

---

## Format Requirements

- Experiments must be numbered (EXP-1, EXP-2, etc.)
- Open questions must be numbered (OQ-1, OQ-2, etc.)
- Conclusions must use exactly one of: Confirmed, Invalidated, Inconclusive, Partially Confirmed
- Confidence levels must use exactly: High, Medium, or Low
- All sections must use the headings exactly as defined in the template

---

## Completeness Rules

- All required sections must be present
- At least one experiment must be documented with full structure
- Every high-risk assumption from the AR must be addressed (tested or explicitly noted as untested with justification)
- Assumption status update must cover all AR assumptions
- Impact assessment must address all invalidated or partially confirmed assumptions
- Results summary must be present
- Recommendations must be present and grounded in evidence
- Open questions section must exist (may be empty)

---

## Relationship Rules

- EL is downstream of the frozen PFD, VH, and AR — all three must be Frozen before the EL is generated
- EL must not expand the problem space beyond what the PFD defines
- EL must not introduce new hypotheses not present in the VH
- EL must not modify assumption statements from the AR — it reports on them (the AR is frozen; modifying its assumptions would be retroactive editing of a frozen artifact)
- EL must not contain solution proposals, architecture, or implementation details
- EL experiment references must trace to AR assumption identifiers (ASM-N)
- EL feeds the Discovery PRD by providing validated/invalidated assumption status — the DPRD carries forward only what the EL confirms or notes as Invalidated

---

## Hard Gates

1. **experiment_present** — At least one experiment documented with complete structure (target assumption, method, sample, findings, conclusion, confidence, limitations)
2. **assumption_traceability** — Every experiment traces to a specific AR assumption (ASM-N); every high-risk AR assumption is addressed
3. **evidence_based_conclusions** — Conclusions are supported by documented findings; no unsupported claims
4. **impact_assessed** — All invalidated or partially confirmed assumptions have documented impact on the initiative
5. **no_scope_expansion** — No expansion beyond the scope of upstream artifacts
6. **no_solutions** — No solution proposals, architecture, or implementation details present
