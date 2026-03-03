# Value Hypothesis — Specification

The Value Hypothesis (VH) defines testable bets about what will create value for users and the business. It translates a structured problem understanding into explicit, falsifiable claims about value creation. It is the second governed artifact in the Product Intelligence Kit.

---

## Upstream Dependencies

- Frozen Problem Framing Document (PFD)

---

## Required Sections

1. Document Control
2. Problem Summary
3. Target Users
4. Value Hypotheses
5. Hypothesis Prioritization
6. Success Metrics
7. Falsification Criteria
8. Dependencies and Risks
9. Open Questions
10. Freeze Declaration

---

## Content Rules

### Document Control
- Must include artifact ID in format `VH-{PROJECT}-{NNN}`
- Must include version, date, author, and status (Draft / Validated / Frozen)
- Must reference the frozen PFD artifact ID

### Problem Summary
- Must contain a brief summary of the problem from the frozen PFD (1-3 sentences)
- Must not redefine or expand the problem — this is a reference, not a restatement
- Must reference the PFD artifact ID

### Target Users
- Must reference user groups from the frozen PFD by their identifiers (UG-N)
- Must not introduce new user groups not present in the PFD
- May refine user understanding but must not expand the user landscape

### Value Hypotheses
- Must contain at least one value hypothesis
- Each hypothesis must follow the structure: "We believe that [action] for [users] will achieve [outcome]"
- Each hypothesis must include:
  - **Belief**: The causal claim being made
  - **Target users**: Which user groups (referencing PFD identifiers)
  - **Expected outcome**: A measurable or verifiable result
  - **Evidence criteria**: How we will know the hypothesis is true
  - **Falsification criteria**: What evidence would disprove the hypothesis
- Hypotheses must not contain solution proposals or implementation details
- Hypotheses must be scoped within the problem space defined by the PFD

### Hypothesis Prioritization
- Hypotheses must be prioritized by a combination of expected impact and confidence level
- Each hypothesis must have an explicit priority ranking
- The basis for prioritization must be stated

### Success Metrics
- Must define at least one metric per hypothesis that will indicate success
- Metrics must be measurable or objectively verifiable
- Metrics must not require implementation knowledge to define (no "API response time" unless the PFD specifically discusses API performance)

### Falsification Criteria
- Each hypothesis must have explicit conditions under which it would be considered false
- Falsification criteria must be specific enough that two reasonable people would agree on whether the criterion is met

### Dependencies and Risks
- Must document risks to hypothesis validity
- Must document dependencies between hypotheses (if any)
- Must identify any conflicts between hypotheses

### Open Questions
- Must list unresolved questions about value assumptions
- Each question must be categorized as blocking or non-blocking

### Freeze Declaration
- Must include a freeze declaration statement when the artifact is frozen
- Must include the date of freeze and the approver

---

## Format Requirements

- Hypotheses should be numbered (HYP-1, HYP-2, etc.)
- Success metrics should be numbered (SM-1, SM-2, etc.)
- Open questions should be numbered (OQ-1, OQ-2, etc.)
- All sections must use the headings exactly as defined in the template

---

## Completeness Rules

- All required sections must be present
- At least one value hypothesis must exist with full structure (belief, users, outcome, evidence, falsification)
- At least one success metric must exist
- Falsification criteria must be present for every hypothesis
- Prioritization must be present with stated basis
- Open questions section must exist (may be empty)

---

## Relationship Rules

- VH must not expand the problem space beyond what the PFD defines
- VH must not introduce user groups not present in the PFD
- VH must not contain solution proposals, architecture, or implementation details
- VH must reference user groups by PFD identifiers
- Hypotheses define the value bets that the Assumption Register and Discovery PRD must not expand

---

## Hard Gates

1. **hypothesis_present** — At least one value hypothesis exists with complete structure (belief, users, outcome, evidence, falsification)
2. **falsifiable** — Every hypothesis has explicit falsification criteria that are specific and testable
3. **user_traceability** — All target users reference PFD user group identifiers; no new user groups introduced
4. **no_scope_expansion** — No expansion of the problem space beyond what the PFD defines
5. **no_solutions** — No solution proposals, architecture, or implementation details present
6. **metrics_defined** — At least one measurable success metric exists per hypothesis
