# Problem Framing Document — Specification

The Problem Framing Document (PFD) structures the problem space for a product initiative. It defines what problem exists, who experiences it, why it matters now, and how large the opportunity is. It is the first governed artifact in the Product Intelligence Kit.

---

## Upstream Dependencies

- Completed Discovery Intake Form

---

## Required Sections

1. Document Control
2. Problem Statement
3. User Landscape
4. Pain Points and Impact
5. Opportunity Sizing
6. Strategic Alignment
7. Current State
8. Constraints and Boundaries
9. Open Questions
10. Freeze Declaration

---

## Content Rules

### Document Control
- Must include artifact ID in format `PFD-{PROJECT}-{NNN}`
- Must include version, date, author, and status (Draft / Validated / Frozen)

### Problem Statement
- Must contain a clear, concise problem statement (1-3 sentences)
- Must identify who experiences the problem (specific user groups or personas)
- Must include rationale for why this problem matters now ("why now")
- Must not contain solution proposals or implementation ideas
- Must not use vague language ("improve the experience", "make it better")

### User Landscape
- Must identify all affected user groups or personas
- Each user group must include: who they are, what they do, and how the problem affects them
- Must distinguish between primary users (directly affected) and secondary users (indirectly affected)
- Must not include demographic profiles unless directly relevant to the problem

### Pain Points and Impact
- Must enumerate specific pain points experienced by identified users
- Each pain point must describe: the problem behavior, its frequency, and its impact
- Impact must be stated in concrete terms (time lost, errors caused, revenue affected, tasks abandoned)
- Must not speculate about pain points without evidence basis — clearly label what is known vs. assumed

### Opportunity Sizing
- Must include an estimate of the opportunity magnitude
- Sizing may be quantitative (revenue impact, time savings, user count) or qualitative (strategic importance, competitive necessity) but must be explicit
- Must state the basis for the sizing estimate (data source, calculation method, or reasoning)
- Must acknowledge uncertainty where it exists

### Strategic Alignment
- Must explain how addressing this problem aligns with organizational strategy
- Must identify which strategic objectives this initiative supports
- If strategic context is not available, must state "Strategic context not provided" rather than inferring

### Current State
- Must describe how the problem is currently handled (workarounds, existing solutions, manual processes)
- Must describe what has been tried before, if anything, and why it was insufficient
- For brownfield scenarios: must describe the existing system and its limitations
- For greenfield scenarios: must describe the absence of a solution and its consequences

### Constraints and Boundaries
- Must document known constraints (regulatory, technical, budgetary, timeline)
- Must document known boundaries on the problem space (what adjacent problems are explicitly excluded)
- Must not include implementation constraints — those belong in downstream artifacts

### Open Questions
- Must list unresolved questions that could affect problem understanding
- Each question must be categorized as: blocking (must resolve before proceeding) or non-blocking (can proceed with assumption)
- Blocking questions must have an owner or plan for resolution

### Freeze Declaration
- Must include a freeze declaration statement when the artifact is frozen
- Must include the date of freeze and the approver

---

## Format Requirements

- Pain points should be numbered (PP-1, PP-2, etc.)
- User groups should be labeled (UG-1, UG-2, etc.)
- Open questions should be numbered (OQ-1, OQ-2, etc.)
- All sections must use the headings exactly as defined in the template

---

## Completeness Rules

- All required sections must be present
- Problem statement must answer what, who, and why now
- At least one user group must be identified with description and impact
- At least one pain point must be documented with frequency and impact
- Opportunity sizing must be present (even if qualitative)
- Open questions section must exist (may be empty if all questions are resolved)

---

## Relationship Rules

- PFD must not contain solution proposals or architecture
- PFD must not reference implementation technologies or design patterns
- PFD defines the problem space that downstream artifacts (VH, AR, DPRD) must not expand
- Constraints in the PFD are inherited by all downstream artifacts

---

## Hard Gates

1. **problem_definition** — Clear problem statement with identified users and "why now" rationale
2. **user_landscape** — At least one user group identified with description and impact
3. **pain_points** — At least one pain point documented with frequency and concrete impact
4. **opportunity** — Opportunity sizing present with stated basis
5. **current_state** — Current state described (existing solutions, workarounds, or absence thereof)
6. **no_solutions** — No solution proposals, architecture, or implementation details present
