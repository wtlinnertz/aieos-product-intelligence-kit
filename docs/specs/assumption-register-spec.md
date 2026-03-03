# Assumption Register — Specification

The Assumption Register (AR) catalogs all assumptions underlying the product initiative, assigns risk levels, and defines validation plans. It makes hidden assumptions visible before requirements are written. It is the third governed artifact in the Product Intelligence Kit.

---

## Upstream Dependencies

- Frozen Problem Framing Document (PFD)
- Frozen Value Hypothesis (VH)

---

## Required Sections

1. Document Control
2. Upstream References
3. Assumption Inventory
4. Risk Assessment Summary
5. Validation Plan
6. Dependency Map
7. Open Questions
8. Freeze Declaration

---

## Content Rules

### Document Control
- Must include artifact ID in format `AR-{PROJECT}-{NNN}`
- Must include version, date, author, and status (Draft / Validated / Frozen)
- Must reference the frozen PFD and VH artifact IDs

### Upstream References
- Must reference the frozen PFD and VH by artifact ID
- Must provide a brief statement of what problem and hypotheses the assumptions relate to

### Assumption Inventory
- Must contain at least three assumptions (product initiatives always carry multiple assumptions)
- Each assumption must include:
  - **Identifier**: ASM-N format
  - **Statement**: What is being assumed to be true
  - **Source**: Which upstream artifact and section this assumption originates from (PFD or VH reference)
  - **Category**: One of: User Behavior, Market, Technical, Organizational, Regulatory, Data
  - **Risk level**: High, Medium, or Low
  - **Impact if false**: What happens to the initiative if this assumption is wrong
  - **Current evidence**: What evidence supports this assumption (or "None")
  - **Validation method**: How this assumption will be tested or verified
- Assumptions must not contain solution proposals or implementation details
- Assumptions must trace to specific content in the PFD or VH

### Risk Assessment Summary
- Must provide an aggregate view of assumption risk
- Must count assumptions by risk level (High / Medium / Low)
- Must identify the highest-risk assumptions explicitly
- Must state whether any high-risk assumptions are unvalidated

### Validation Plan
- Must define a validation approach for every high-risk assumption
- Medium-risk assumptions should have validation approaches (warning if missing, not a gate failure)
- Each validation entry must include: assumption reference, method, expected timeline, owner (or "TBD")
- Validation methods must be concrete (not "we will validate this later")

### Dependency Map
- Must identify dependencies between assumptions (if any exist)
- Must identify which assumptions, if invalidated, would cascade to other assumptions
- May state "No inter-assumption dependencies identified" if none exist

### Open Questions
- Must list unresolved questions about assumptions
- Each question must be categorized as blocking or non-blocking

### Freeze Declaration
- Must include a freeze declaration statement when the artifact is frozen
- Must include the date of freeze and the approver

---

## Format Requirements

- Assumptions must be numbered (ASM-1, ASM-2, etc.)
- Open questions must be numbered (OQ-1, OQ-2, etc.)
- Risk levels must use exactly: High, Medium, or Low
- Categories must use exactly one of: User Behavior, Market, Technical, Organizational, Regulatory, Data
- All sections must use the headings exactly as defined in the template

---

## Completeness Rules

- All required sections must be present
- At least three assumptions must be documented with full structure
- Every assumption must have a source reference to PFD or VH
- Every assumption must have a risk level and impact-if-false statement
- Every high-risk assumption must have a validation plan entry
- Risk assessment summary must be present
- Open questions section must exist (may be empty)

---

## Relationship Rules

- AR must not expand the problem space beyond what the PFD defines
- AR must not introduce hypotheses not present in the VH
- AR must not contain solution proposals, architecture, or implementation details
- AR assumptions must trace to content in the PFD or VH
- The AR feeds the Discovery PRD's Assumptions and Constraints sections

---

## Hard Gates

1. **assumption_inventory** — At least three assumptions documented with complete structure (statement, source, category, risk level, impact if false, evidence, validation method)
2. **source_traceability** — Every assumption traces to specific content in the frozen PFD or VH
3. **risk_assessment** — All assumptions have risk levels; risk assessment summary is present
4. **high_risk_validation** — Every high-risk assumption has a concrete validation plan entry
5. **no_scope_expansion** — No expansion beyond the problem space and hypotheses defined in upstream artifacts
6. **no_solutions** — No solution proposals, architecture, or implementation details present
