# Discovery PRD

## 1. Document Control

| Field | Value |
|-------|-------|
| Artifact ID | DPRD-{PROJECT}-{NNN} |
| Version | {version} |
| Date | {date} |
| Author | {author} |
| Status | Draft / Validated / Frozen |
| Upstream PFD | {PFD artifact ID} |
| Upstream VH | {VH artifact ID} |
| Upstream AR | {AR artifact ID} |
| Upstream EL | {EL artifact ID} |

---

## 2. Problem Statement

{Clear problem statement derived from the frozen PFD. Must identify who experiences the problem, what the problem is, and why it matters now.}

Source: {PFD artifact ID}

---

## 3. Goals (What "Success" Means)

{Explicit goals stated as measurable outcomes. Each goal traces to a value hypothesis.}

| Goal ID | Goal | Success Criterion | VH Trace |
|---------|------|-------------------|----------|
| G-1 | {goal} | {measurable criterion} | {HYP-N} |

---

## 4. Non-Goals (Hard Exclusions)

The following are explicitly excluded from this initiative. These are enforceable constraints on all downstream artifacts.

- **NG-1:** {exclusion} — {rationale}

---

## 5. Users / Personas

{Users and personas referenced from the frozen PFD.}

| PFD Reference | User / Persona | Context for Engineering |
|---------------|---------------|----------------------|
| UG-1 | {name} | {what they need to accomplish} |

---

## 6. Requirements

### Functional Requirements

**FR-1:** The system SHALL {requirement}
- VH Trace: {HYP-N}

{Repeat for each functional requirement}

### Non-Functional Requirements

**NFR-1:** The system SHALL {requirement}
- VH Trace: {HYP-N, or "Cross-cutting"}

{Repeat for each non-functional requirement}

---

## 7. Constraints (Hard Guardrails)

{Constraints inherited from PFD and informed by AR.}

- **C-1:** {constraint} — Source: {PFD §8 / AR ASM-N}

---

## 8. Assumptions

{Assumptions inherited from the frozen AR, with validation status from the frozen EL. If any active assumption is false, it changes scope or direction.}

| ID | Assumption | Validation Status | Impact if False | AR Source | EL Source |
|----|-----------|------------------|----------------|-----------|-----------|
| A-1 | {assumption} | {Confirmed / Invalidated / Untested / Partially Confirmed} | {impact} | {ASM-N} | {EXP-N or "—"} |

---

## 9. Out of Scope by Default

Anything not explicitly listed in §3 (Goals) and §6 (Requirements) is out of scope by default. This is not a list of exclusions — it is the default rule. Specific exclusions are listed in §4 (Non-Goals).

{Optional: call out commonly expected items that are explicitly not in scope for this initiative}

---

## 10. Open Questions

{Unresolved questions. No blocking questions may remain if this document is to be frozen.}

**OQ-1: {Question}**
- **Status:** Resolved / Unresolved
- **Blocking:** Yes / No
- **Resolution:** {answer, if resolved}

{Repeat for each open question, or state "All questions resolved"}

---

## 11. Acceptance / Success Criteria

{Measurable or objectively verifiable criteria that define when the initiative is complete and successful.}

| ID | Criterion | Measurement Method | VH Metric Trace |
|----|----------|-------------------|-----------------|
| AC-1 | {criterion} | {how measured} | {SM-N} |

---

## 12. Freeze Declaration

| Field | Value |
|-------|-------|
| Frozen | Yes / No |
| Freeze Date | {date} |
| Approved By | {approver} |

{Freeze declaration statement}
