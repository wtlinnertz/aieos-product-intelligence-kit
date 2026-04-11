# Work Classification — Specification

Version: v1.0

The Work Classification Record captures the routing decision for an incoming work request before any discovery or execution artifacts are produced. It is the entry gate for the Product Intelligence Kit — it must exist and pass validation before the Discovery Intake Form is completed.

This is a **boundary contract**, not a governed artifact. The classification record is human-authored (AI-assisted via `work-classification-prompt.md`). It is validated against this spec to confirm the routing decision is explicit, justified, and free of solution content.

---

## Purpose

The classification spec serves two roles:

1. **Routing gate** — Ensures work is directed to the appropriate process depth before investment begins; prevents heavyweight discovery being applied to work that does not need it, and prevents execution-ready work from bypassing discovery when discovery is required
2. **Decision record** — Freezes the classification decision so it is traceable and cannot silently change mid-flow

---

## Upstream Dependencies

- None — this is the entry point for the Product Intelligence Kit and the precursor to the Discovery Intake Form

---

## Required Sections

1. Document Control
2. Classification Decision (type, confidence, depth, routing)
3. Justification
4. Artifact Requirements
5. Risk Flags
6. Freeze Declaration

---

## Content Rules

### Document Control
**Rules**
- Record ID must be present
- Date must be present
- A description of the incoming work request must be present (1-2 sentences)

**Failure Examples**
- Missing Record ID
- Work request summary absent or empty

### Classification Decision
**Rules**
- Primary type must be exactly one value from the taxonomy: Feature, Enhancement, Bug, Compliance, Tech Debt, Incident Response, Research
- Composite or ambiguous types are not permitted — if genuinely ambiguous, classify as Research
- Confidence must be stated: High, Medium, or Low
- Discovery depth must be explicitly stated: Full, Targeted, or None
- Route To must name exactly one destination: Product Intelligence Kit, Engineering Execution Kit (direct), Engineering Triage, or Incident Management

**Failure Examples**
- "Feature / Enhancement" — composite type, not permitted
- Discovery depth absent or stated as "TBD"
- Route To is vague ("engineering team") rather than a named kit or process

### Justification
**Rules**
- Must explain why this classification was chosen — not just restate the classification decision
- Must reference at least one characteristic of the work request that drove the type selection
- Must not be a single sentence that merely restates the classification table entry

**Failure Examples**
- "This is a bug because it is a bug fix" — circular, not a justification
- Justification section empty or absent

### Artifact Requirements
**Rules**
- Must list each PIK artifact type and state whether it is required (Yes / No)
- If Discovery Depth is None, all five artifacts must be marked No with rationale
- If Discovery Depth is Full or Targeted, all five artifacts must be marked Yes
- Artifact requirements must be consistent with the declared Discovery Depth

**Failure Examples**
- Discovery Depth is Full but some artifacts marked No without explanation
- Discovery Depth is None but artifacts marked Yes

### Risk Flags
**Rules**
- Must address the risk of under-classification
- Must either identify specific under-classification risks for this work, or explicitly state "None identified"
- Absence of this section is a failure — the check must be performed and recorded even if the result is none

**Failure Examples**
- Risk Flags section missing
- Section present but empty

### No Solution Content
**Rules**
- The classification record must not contain solution proposals, architecture, or implementation details
- The record must not contain functional or non-functional requirements
- The record may describe what the work is — it must not describe how it will be solved

**Failure Examples**
- "Route to PIK; the solution will use a microservices architecture" — implementation detail
- Requirements listed in the justification

---

## Format Requirements

- Classification Decision fields must be presented in a table or structured list — not prose
- Artifact Requirements must be in a table with Required (Yes/No) and Rationale columns
- The Freeze Declaration must be present and completed before the record is used as a gate

---

## Completeness Rules

- All six sections must be present and non-empty (Risk Flags may contain "None identified")
- Classification Decision fields must all be filled — no blank or TBD values
- Justification must go beyond restating the type
- Artifact Requirements table must cover all five artifact types

---

## Relationship Rules

- The classification record precedes and gates the Discovery Intake Form — the intake form must not be completed until the classification record exists and passes validation
- The classification record must not be modified after freeze — if the classification changes, a new record must be created
- The EEK Kit Entry Gate references the frozen classification record as a prerequisite check

---

## Hard Gates

1. **document_control** — Record ID, date, and work request summary present
2. **type_declared** — Primary type is exactly one value from the taxonomy; no composite or ambiguous types
3. **routing_complete** — Discovery depth and Route To destination are explicitly stated; no TBD values
4. **justification_present** — Justification explains the reasoning, not just restates the classification
5. **risk_flags_addressed** — Risk Flags section present with content or explicit "None identified"
6. **no_solution_content** — No solution proposals, requirements, or implementation details anywhere in the record
