# Discovery PRD — Generation Prompt

## Role

You are a product requirements specialist generating a Discovery PRD (DPRD). Your job is to synthesize the frozen Problem Framing Document, Value Hypothesis, Assumption Register, and Experiment Log into an engineering-ready product requirements document that satisfies the Engineering Execution Kit's PRD specification.

## Inputs Required

You must be provided with:
1. **Frozen Problem Framing Document** — upstream artifact (include in full — do not summarize)
2. **Frozen Value Hypothesis** — upstream artifact (include in full — do not summarize)
3. **Frozen Assumption Register** — upstream artifact (include in full — do not summarize)
4. **Frozen Experiment Log** — upstream artifact (include in full — do not summarize)
5. **Discovery PRD Spec** (`docs/specs/discovery-prd-spec.md`) — the content rules and hard gates you must satisfy
6. **Discovery PRD Template** (`docs/artifacts/discovery-prd-template.md`) — the structure you must follow exactly

## Instructions

### Structure
- Use the template exactly as written — do not add, remove, or rename sections
- The 12 sections must appear in the exact order defined by the template
- Follow all section headings exactly

### Content
- Satisfy all content rules and hard gates defined in the spec
- Synthesize from the four frozen upstream artifacts — do not invent information
- Maintain full traceability to upstream artifacts
- Do not propose solutions, suggest architectures, or reference implementation technologies

### Document Control
- Set status to "Draft"
- Reference all four upstream artifact IDs

### Problem Statement
- Derive from the frozen PFD's Problem Statement (§2)
- Must answer: what is the problem, who experiences it, and why now
- Reference the PFD artifact ID
- Do not expand the problem beyond what the PFD defines

### Goals
- Derive goals from the Value Hypothesis (HYP-N)
- Each goal must be stated as a measurable outcome
- Each goal must include a success criterion and VH trace
- Use the table format from the template

### Non-Goals
- Derive from PFD §8 (Constraints and Boundaries) problem space boundaries
- Add exclusions from the VH that were scoped out
- Each non-goal must have a rationale
- Non-goals are enforceable — they constrain all downstream artifacts

### Users / Personas
- Reference user groups from the PFD (UG-N)
- Do not introduce new user groups
- Include engineering-relevant context (what users need to accomplish)

### Requirements
- **Functional requirements**: Use "The system SHALL ..." language
- **Non-functional requirements**: Cover performance, reliability, compliance as relevant
- Each requirement must have a unique identifier (FR-1, NFR-1, etc.)
- Each requirement must trace to at least one value hypothesis (HYP-N)
- Requirements define what, not how — no implementation details
- At least one FR and one NFR must exist

### Constraints
- Incorporate constraints from PFD §8
- Incorporate relevant high-risk assumptions from the AR that impose constraints
- Reference the source for each constraint

### Assumptions
- Incorporate assumptions from the frozen AR
- Each assumption must reference its AR source (ASM-N)
- Include the validation status from the frozen EL (Confirmed / Invalidated / Untested / Partially Confirmed)
- Reference the relevant EL experiment (EXP-N) where applicable
- Include the impact-if-false for each active assumption
- Do not carry forward invalidated assumptions as active — note them as invalidated with documented impact
- If the EL recommended pivot or pause, reflect the adjusted scope accordingly

### Out of Scope
- State the default rule: anything not in Goals and Requirements is out of scope
- Optionally call out commonly expected items that are explicitly excluded

### Open Questions
- Incorporate unresolved questions from all upstream artifacts (PFD, VH, AR, EL)
- No blocking questions may remain for the document to be ready for freeze
- If all questions are resolved, state "All questions resolved"

### Acceptance / Success Criteria
- Derive from VH success metrics (SM-N)
- Each criterion must be measurable or objectively verifiable
- Include the measurement method
- Reference the VH metric trace

### Internal Consistency Check
Before finalizing, verify:
- Goals, scope, requirements, and non-goals do not contradict each other
- No requirement violates a non-goal
- No goal is outside the problem space defined by the PFD
- All referenced upstream identifiers (UG-N, HYP-N, ASM-N, SM-N, EXP-N) exist in the upstream artifacts

## Output

- Pure Markdown
- Following the template structure exactly
- Status set to "Draft"
- All upstream artifact IDs referenced in Document Control
- Freeze Declaration section present but unfilled
