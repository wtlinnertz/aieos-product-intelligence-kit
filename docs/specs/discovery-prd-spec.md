# Discovery PRD — Specification

The Discovery PRD (DPRD) is the terminal artifact of the Product Intelligence Kit. It synthesizes the problem framing, value hypotheses, validated assumptions, and experiment results into an engineering-ready product requirements document. It must satisfy the Engineering Execution Kit's PRD specification exactly, as it serves as the handoff artifact to that kit.

---

## What This Artifact Is Not

- **Not a technical design document.** The DPRD defines what to build and why. How the system accomplishes it belongs in the SAD and TDD (downstream in the Engineering Execution Kit).
- **Not a backlog of tasks.** The DPRD defines requirements, not a work breakdown structure or sprint plan.
- **Not a project plan.** The DPRD defines product intent. Delivery planning belongs in downstream engineering artifacts.

---

## Upstream Dependencies

- Frozen Problem Framing Document (PFD)
- Frozen Value Hypothesis (VH)
- Frozen Assumption Register (AR)
- Frozen Experiment Log (EL)

---

## Required Sections

These sections are mandated by the Engineering Execution Kit's PRD specification. They must appear exactly as listed.

1. Document Control
2. Problem Statement
3. Goals (What "Success" Means)
4. Non-Goals (Hard Exclusions)
5. Users / Personas
6. Requirements (Functional and Non-Functional)
7. Constraints (Hard Guardrails)
8. Assumptions
9. Out of Scope by Default
10. Open Questions
11. Acceptance / Success Criteria
12. Freeze Declaration

---

## Content Rules

### Document Control
- Must include artifact ID in format `DPRD-{PROJECT}-{NNN}`
- Must include version, date, author, and status (Draft / Validated / Frozen)
- Must reference all upstream artifact IDs (PFD, VH, AR, EL)

### Problem Statement
- Must contain a clear problem statement
- Must identify who experiences the problem (users or personas)
- Must include rationale ("why now")
- Content must be derived from the frozen PFD — must not redefine or expand the problem

### Goals (What "Success" Means)
- Goals must be explicit and stated as measurable outcomes
- Success criteria must be measurable or objectively verifiable
- Goals must trace to value hypotheses in the frozen VH

### Non-Goals (Hard Exclusions)
- Non-goals must be explicitly listed as hard exclusions
- Non-goals are enforceable constraints on all downstream artifacts
- Must include boundaries from PFD §8 (Constraints and Boundaries)
- Empty non-goals section is a failure unless justified

### Users / Personas
- Must reference user groups from the frozen PFD
- Must not introduce new user groups not present in the PFD
- Each user/persona must include relevant context for engineering (what they need to accomplish)

### Requirements (Functional and Non-Functional)
- Functional requirements must be explicitly stated
- Non-functional requirements must be explicitly stated (performance, reliability, compliance, etc.)
- Requirements must not contain implementation details or solution design — DPRDs that prescribe solutions undermine the engineering team's architecture authority and create false requirements
- Functional requirements must use "The system SHALL ..." language
- Each requirement must have a unique identifier (FR-1, NFR-1, etc.)
- At least one functional requirement and one non-functional requirement must exist
- Requirements must trace to at least one value hypothesis (VH HYP-N reference)

**Failure examples:** "The system SHALL use a microservices architecture" (implementation prescription, not a requirement). "The system SHALL be fast" (not measurable). "FR-1: Support notifications" (no "SHALL" language, no VH trace, no measurable criterion). Valid: "FR-1: The system SHALL deliver notifications to UG-1 users within 60 seconds of the triggering event. [HYP-2]"

### Constraints (Hard Guardrails)
- Constraints must be documented (regulatory, technical, delivery)
- Must incorporate constraints from PFD §8
- Must incorporate relevant high-risk assumptions from the AR

### Assumptions
- Assumptions must be documented with note that if false, they change scope or direction
- Must incorporate assumptions from the frozen AR
- Each assumption must reference its AR source (ASM-N)
- Must reflect the validated/invalidated status from the frozen EL where available
- Invalidated assumptions must not be carried forward as active assumptions — they must be noted as invalidated with impact documented

### Out of Scope by Default
- Must state the default scope rule: anything not listed in Goals and Requirements is out of scope
- No implied scope — anything not explicitly included is excluded

### Open Questions
- Must list any unresolved questions
- No unresolved critical questions that would block architecture
- Must incorporate unresolved blocking questions from PFD, VH, AR, and EL
- May be empty if all questions are resolved

### Acceptance / Success Criteria
- Must define acceptance criteria that are measurable or objectively verifiable
- Must trace to success metrics from the frozen VH (SM-N references)

### Freeze Declaration
- Must include a freeze declaration statement when the artifact is frozen
- Must include the date of freeze and the approver

---

## Format Requirements

- Functional requirements must use "The system SHALL ..." language
- Each functional requirement must have a unique identifier (FR-1, FR-2, etc.)
- Each non-functional requirement must have a unique identifier (NFR-1, NFR-2, etc.)
- All sections must use the headings exactly as defined in the template

---

## Completeness Rules

- All 12 required sections must be present
- Problem statement must answer what, who, and why
- At least one functional requirement and one non-functional requirement must exist
- Non-goals must be present (empty non-goals section is a failure unless justified)
- Open questions section must exist (may be empty if all questions are resolved)
- PRD must be internally consistent (goals, scope, requirements, and non-goals do not contradict)

---

## Relationship Rules

- DPRD is downstream of all four PIK artifacts (PFD, VH, AR, EL) — all must be Frozen before the DPRD is generated
- DPRD must not contain solution design or architecture
- DPRD must not reference implementation details
- DPRD defines intent that downstream artifacts (SAD, TDD) must not reinterpret or expand
- Non-goals are enforceable constraints on all downstream artifacts
- DPRD must not expand scope beyond what the PFD, VH, AR, and EL collectively define
- Requirements must trace to value hypotheses (HYP-N references)
- Assumptions must trace to the Assumption Register (ASM-N references) and carry EL validation status
- When delivered to the Engineering Execution Kit via Path A, the DPRD is placed as `docs/sdlc/01-prd.md` and validated against the EEK's PRD specification — it must not be regenerated or modified by the EEK

---

## Traceability Rules (Product Intelligence Kit Extension)

These rules extend the base PRD specification with traceability requirements specific to the Product Intelligence Kit's artifact flow.

- Problem statement must be derived from the frozen PFD
- Goals must trace to value hypotheses in the frozen VH
- Requirements must trace to at least one hypothesis (VH HYP-N reference)
- Assumptions must reference their AR source (ASM-N) and reflect EL validation status
- Acceptance criteria must trace to VH success metrics (SM-N)
- User groups must reference PFD identifiers (UG-N)
- Assumption validation status must reflect EL experiment results (EXP-N references where applicable)

---

## Hard Gates

### Engineering Execution Kit Gates (Downstream Contract)

These 6 gates are mandated by the downstream Engineering Execution Kit. All must PASS for the DPRD to be accepted as a valid PRD.

1. **problem_definition** — Clear problem statement with identified users and rationale
2. **goals** — Explicit goals with measurable success criteria
3. **scope** — In-scope clearly defined, explicit non-goals, no implied scope
4. **requirements** — Functional and non-functional requirements explicitly stated
5. **constraints** — Constraints and assumptions documented
6. **readiness** — No unresolved critical questions, internally consistent

### Product Intelligence Kit Gates (Traceability)

These gates ensure the DPRD is properly grounded in the upstream discovery artifacts.

7. **upstream_traceability** — Problem traces to PFD, goals trace to VH, assumptions trace to AR, validation status reflects EL
8. **no_scope_expansion** — No expansion beyond the collective scope of PFD, VH, AR, and EL
