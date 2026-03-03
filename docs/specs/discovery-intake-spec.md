# Discovery Intake Form — Specification

The Discovery Intake Form captures human intent and context before AI-generated artifact production begins. It is the upstream boundary contract for the Product Intelligence Kit — it defines what constitutes valid input for this kit's artifact flow.

This is a **boundary contract**, not a governed artifact. The intake form is human-authored (no AI generation prompt exists). It is validated against this spec to ensure completeness before downstream artifact generation begins.

---

## Purpose

The intake spec serves two roles:

1. **Internal quality gate** — Ensures the PFD generation step has sufficient input material to work with
2. **Upstream boundary contract** — Enables an upstream team (e.g., a future Strategic Direction Kit) to produce validated intake artifacts independently, knowing exactly what this kit requires

---

## Upstream Dependencies

- None — this is the entry point for the Product Intelligence Kit
- When a Strategic Direction Kit exists, its output should map to the sections defined here

---

## Required Sections

1. Problem Context
2. Users and Stakeholders
3. Opportunity
4. Current State
5. Scope and Boundaries
6. Assumptions and Risks
7. Additional Context (optional — no hard gate)

---

## Content Rules

### Problem Context
- Must describe the problem in concrete terms — specific behaviors, gaps, or inefficiencies
- Must not use vague language ("improve the experience", "make things better", "optimize the flow")
- Must identify who experiences the problem (specific user groups, roles, or personas)
- Must provide a "why now" rationale — what has changed, what is the cost of inaction, or what deadline exists
- Must include some evidence basis — data, research, user feedback, or observation that supports the problem's existence
- Evidence may be limited but must be explicitly stated; "no evidence available" is acceptable if acknowledged

### Users and Stakeholders
- Must identify at least one primary user group affected by the problem
- Each user group should describe how they experience the problem (not just who they are)
- Secondary users and sponsor are encouraged but not required for the hard gate

### Opportunity
- Must include an estimate of impact (quantitative or qualitative)
- Must state what is uncertain about the estimate
- Strategic alignment is encouraged but not required for the hard gate

### Current State
- Must describe how the problem is currently handled — workarounds, manual processes, existing tools, or absence of a solution
- For brownfield initiatives: must describe the existing system context
- For greenfield initiatives: must describe what happens in the absence of a solution

### Scope and Boundaries
- Must state what is in scope for this initiative
- Must state what is explicitly out of scope
- Must document known constraints (regulatory, budgetary, timeline, technical)
- If no constraints are known, must state "No known constraints" rather than leaving blank

### Assumptions and Risks
- Must list conditions assumed to be true that, if false, would change the initiative's direction
- Must list potential blockers or risks
- May be brief but must not be empty — if no assumptions or risks are identified, state "None identified" explicitly

### Additional Context
- Optional — no hard gate applies
- Reference documents and related initiatives may be listed here

---

## Format Requirements

- The form must use the section headings defined in the template (`docs/artifacts/discovery-intake-template.md`)
- Sections may be filled in any order
- Blank sections must remain present with the heading intact — do not remove sections
- Evidence should be labeled with its source type where possible (e.g., "user interviews", "support ticket analysis", "competitive research")

---

## Completeness Rules

- All required sections (1-6) must be present and non-empty
- Problem context must answer three questions: what is the problem, who experiences it, and why now
- At least one user group must be identified with a description of how they experience the problem
- Scope must include both in-scope and out-of-scope statements
- Constraints must be documented or explicitly stated as "none known"
- Evidence basis must exist — even if limited or low-confidence

---

## Relationship Rules

- The intake form feeds PFD generation — PFD content rules draw from the information captured here
- The intake form must NOT contain solution proposals, architecture, or implementation details
- The intake form must NOT contain requirements — those emerge through the artifact flow
- The intake form must NOT assign priority or make build/no-build decisions — those emerge from VH and AR analysis
- Information missing from the intake will be marked as "Not provided" in the PFD — missing information does not block intake validation as long as the hard gates are met

---

## Hard Gates

1. **problem_defined** — Problem is described in concrete terms (not vague or abstract); answers what is wrong, broken, or missing
2. **users_identified** — At least one affected user group is identified with a description of how they experience the problem
3. **urgency_stated** — "Why now" rationale is provided (triggering event, cost of inaction, deadline, or strategic shift)
4. **evidence_present** — Some evidence basis exists for the problem's existence (data, research, user feedback, or observation); evidence may be limited but must be explicitly stated
5. **scope_bounded** — Both in-scope and out-of-scope boundaries are stated; known constraints are documented or explicitly noted as "none known"
6. **no_solutions** — No solution proposals, architecture, implementation details, or requirements are present in the intake form
