# Product Intelligence Kit — Playbook

This playbook defines the end-to-end process for transforming strategic intent into engineering-ready product requirements. It is the authoritative process definition for the Product Intelligence Kit.

---

## Artifact Flow

The Product Intelligence Kit produces five artifact types in a strict linear sequence. Each artifact must be generated, validated, and frozen before the next can begin.

An optional pre-intake classification step routes work to the appropriate process depth.

```
Work Request (incoming)
        │
        ▼
┌─────────────────────────┐
│  Work Classification    │  Step 0a: Classify and route (utility prompt)
│  (optional)             │
└────────┬────────────────┘
         │ route to discovery
         ▼
Discovery Intake (human input)
        │
        ▼
┌─────────────────────────┐
│  Problem Framing        │  Step 1: Structure the problem space
│  Document (PFD)         │
└────────┬────────────────┘
         │ validate → freeze
         ▼
┌─────────────────────────┐
│  Value Hypothesis (VH)  │  Step 2: Define testable value bets
└────────┬────────────────┘
         │ validate → freeze
         ▼
┌─────────────────────────┐
│  Assumption Register    │  Step 3: Catalog and risk-assess assumptions
│  (AR)                   │
└────────┬────────────────┘
         │ validate → freeze
         │
         ├──── Stress Test (optional utility prompt)
         │
         ▼
┌─────────────────────────┐
│  Experiment Log (EL)    │  Step 4: Validate assumptions with evidence
└────────┬────────────────┘
         │ validate → freeze
         ▼
┌─────────────────────────┐
│  Discovery PRD (DPRD)   │  Step 5: Synthesize into engineering-ready PRD
└────────┬────────────────┘
         │ validate → freeze
         ▼
   Handoff to Engineering
   Execution Kit
```

---

## Utility Prompts

The kit includes utility prompts that support the artifact flow but do not produce governed artifacts.

### Work Classification

**Prompt:** `docs/prompts/work-classification-prompt.md`

**When to use:** Before filling the Discovery Intake Form. Determines whether incoming work needs full discovery, targeted discovery, or should be routed elsewhere (engineering triage, incident management, etc.).

**Output:** Classification (Feature / Enhancement / Bug / Compliance / Tech Debt / Incident Response / Research), recommended discovery depth, and routing decision.

Not all work needs full discovery. Bugs, tech debt, and incident response bypass this kit entirely.

### Brownfield Analysis

**Prompt:** `docs/prompts/brownfield-analysis-prompt.md`

**When to use:** Before filling the Discovery Intake Form, when the initiative involves an existing system. Analyzes system documentation and produces structured output mapped to intake form sections.

**Output:** Draft intake content based on existing system documentation. Human review is mandatory before use.

### Stakeholder Alignment Analysis

**Prompt:** `docs/prompts/stakeholder-alignment-prompt.md`

**When to use:** Before or during PFD generation, when multiple stakeholders have provided input and alignment is uncertain. Also useful before freeze if stakeholder buy-in is in question.

**Output:** Convergence/divergence analysis across stakeholder perspectives, with divergences classified as resolvable, negotiable, or blocking.

### Assumption Stress Test

**Prompt:** `docs/prompts/assumption-stress-test-prompt.md`

**When to use:** After the Assumption Register is frozen, before conducting experiments. Identifies weaknesses, blind spots, missing assumptions, and validation gaps.

**Output:** Individual assumption analysis, missing assumptions, correlated risks, and survivability assessment.

This helps teams design better experiments and catch assumptions they missed.

### Cross-Initiative Conflict Detection

**Prompt:** `docs/prompts/cross-initiative-conflict-prompt.md`

**When to use:** After freezing an AR, when multiple initiatives are active in parallel. Identifies assumption conflicts, resource competition, and cascade dependencies across initiatives.

**Output:** Conflict table, shared assumptions, cascade dependencies, and survivability assessment for parallel initiatives.

### Initiative Prioritization

**Prompt:** `docs/prompts/initiative-prioritization-prompt.md`

**When to use:** When multiple validated DPRDs compete for engineering capacity, or during planning cycles when choosing which initiatives to fund.

**Output:** Comparative analysis across initiatives covering problem severity, value confidence, risk profile, strategic alignment, and sequencing recommendations.

---

## Steps

### Step 0a: Work Classification (Optional)

**Type:** Utility prompt output (not a governed artifact)

**What happens:**
- An incoming work request is analyzed using `docs/prompts/work-classification-prompt.md`
- The prompt classifies the work type and recommends discovery depth
- Work classified as Bug, Tech Debt, or Incident Response bypasses this kit

**Output:** Classification and routing decision

**No validation or freeze** — this is a routing decision, not a governed artifact.

---

### Step 0b: Discovery Intake

**Type:** Human input with boundary contract validation

**What happens:**
- A human fills out the Discovery Intake Form (`docs/artifacts/discovery-intake-template.md`)
- The form captures: problem context, affected users, opportunity sizing, strategic alignment, known constraints
- For brownfield scenarios, use `docs/prompts/brownfield-analysis-prompt.md` to pre-fill the intake from existing system documentation, then review and approve before use

**Output:** Completed Discovery Intake Form

**Validation:**
- Use `docs/validators/discovery-intake-validator.md` in an AI session
- The validator evaluates against `docs/specs/discovery-intake-spec.md`
- All 6 hard gates must PASS before proceeding to PFD generation
- If FAIL: address blocking issues and re-validate

**No freeze** — the intake form is not a governed artifact and does not enter the freeze/re-entry protocol. However, validation is required to ensure sufficient input quality for downstream artifact generation. This validation serves as the **upstream boundary contract** for the kit.

---

### Step 1: Problem Framing Document (PFD)

**Artifact ID format:** `PFD-{PROJECT}-{NNN}`

**Inputs:**
- Validated Discovery Intake Form (must pass intake validator)
- `docs/principles/product-discovery-principles.md` (organizational policy)
- For compliance initiatives: `docs/principles/compliance-discovery-principles.md`

**Optional: Stakeholder Alignment**
- If multiple stakeholders have provided conflicting input, run `docs/prompts/stakeholder-alignment-prompt.md` before or during PFD generation
- Resolve blocking divergences before freezing the PFD

**Generation:**
- Use `docs/prompts/problem-framing-prompt.md` in a dedicated AI session
- The prompt references `docs/specs/problem-framing-spec.md` for content rules
- The prompt references `docs/artifacts/problem-framing-template.md` for structure
- Output: a Problem Framing Document

**Validation:**
- In a **separate AI session**, use `docs/validators/problem-framing-validator.md`
- The validator references `docs/specs/problem-framing-spec.md` for hard gates
- All hard gates must PASS

**Freeze:**
- Human reviews the validated PFD
- Human approves the freeze
- The PFD is now immutable and authoritative input for downstream artifacts

---

### Step 2: Value Hypothesis (VH)

**Artifact ID format:** `VH-{PROJECT}-{NNN}`

**Inputs:**
- Frozen Problem Framing Document
- `docs/principles/hypothesis-driven-development.md` (organizational policy)

**Generation:**
- Use `docs/prompts/value-hypothesis-prompt.md` in a dedicated AI session
- Include the **full frozen PFD** — do not summarize
- Output: a Value Hypothesis document

**Validation:**
- In a **separate AI session**, use `docs/validators/value-hypothesis-validator.md`
- All hard gates must PASS

**Freeze:**
- Human reviews the validated VH
- Human approves the freeze

---

### Step 3: Assumption Register (AR)

**Artifact ID format:** `AR-{PROJECT}-{NNN}`

**Inputs:**
- Frozen Problem Framing Document
- Frozen Value Hypothesis

**Generation:**
- Use `docs/prompts/assumption-register-prompt.md` in a dedicated AI session
- Include the **full frozen PFD and VH** — do not summarize
- Output: an Assumption Register

**Validation:**
- In a **separate AI session**, use `docs/validators/assumption-register-validator.md`
- All hard gates must PASS

**Freeze:**
- Human reviews the validated AR
- Human approves the freeze

**Optional: Stress Test**
- After freezing the AR, optionally run `docs/prompts/assumption-stress-test-prompt.md`
- Use the stress test output to inform experiment design (Step 4)
- This does not change the frozen AR — it is analytical input for the team

**Optional: Cross-Initiative Conflict Check**
- If multiple initiatives are active, run `docs/prompts/cross-initiative-conflict-prompt.md` with this AR and other frozen ARs
- Resolve critical conflicts before committing resources to experiments

---

### Step 4: Experiment Log (EL)

**Artifact ID format:** `EL-{PROJECT}-{NNN}`

**Inputs:**
- Frozen Problem Framing Document
- Frozen Value Hypothesis
- Frozen Assumption Register
- Experiment results data (human-provided: research findings, analysis results, interview notes, survey responses)

**Generation:**
- Use `docs/prompts/experiment-log-prompt.md` in a dedicated AI session
- Include the **full frozen PFD, VH, and AR** — do not summarize
- Include all experiment results data gathered during validation activities
- Output: an Experiment Log documenting what was tested, what was found, and how it affects assumptions

**Validation:**
- In a **separate AI session**, use `docs/validators/experiment-log-validator.md`
- All hard gates must PASS

**Freeze:**
- Human reviews the validated EL
- Human reviews the proceed/pivot/pause recommendation
- Human approves the freeze
- If the EL recommends pivot or pause, the team addresses this before proceeding to Step 5

---

### Step 5: Discovery PRD (DPRD)

**Artifact ID format:** `DPRD-{PROJECT}-{NNN}`

**Inputs:**
- Frozen Problem Framing Document
- Frozen Value Hypothesis
- Frozen Assumption Register
- Frozen Experiment Log

**Generation:**
- Use `docs/prompts/discovery-prd-prompt.md` in a dedicated AI session
- Include the **full frozen PFD, VH, AR, and EL** — do not summarize
- Output: a Discovery PRD that satisfies the Engineering Execution Kit's PRD specification

**Validation:**
- In a **separate AI session**, use `docs/validators/discovery-prd-validator.md`
- All hard gates must PASS (8 total: 6 downstream Engineering Execution Kit gates + 2 traceability gates)

**Freeze:**
- Human reviews the validated DPRD
- Human approves the freeze
- The DPRD is now the handoff artifact to the Engineering Execution Kit

---

**Optional: Initiative Prioritization**
- If multiple DPRDs are ready for handoff, run `docs/prompts/initiative-prioritization-prompt.md` to compare initiatives
- The analysis supports portfolio decisions about which initiatives to fund and in what order

---

## Downstream Handoff

### Delivery

The frozen Discovery PRD is delivered to the Engineering Execution Kit as its entry-point PRD.

**File placement:** Place the frozen DPRD as `docs/sdlc/01-prd.md` in the consuming project's repository. This is the PRD slot in the Engineering Execution Kit's artifact flow.

**Acceptance check:** The Engineering Execution Kit team runs `prd-validator.md` against the placed DPRD in a fresh AI session (using the EEK's `prd-spec.md` and `prd-validator.md`). This confirms the DPRD satisfies the EEK's 6 PRD hard gates.

A DPRD that has passed the DPRD validator will satisfy all 6 EEK PRD gates because the 6 EEK gates (`problem_definition`, `goals`, `scope`, `requirements`, `constraints`, `readiness`) are a proper subset of the 8 DPRD gates — they are included verbatim as the "Engineering Execution Kit Gates" in `discovery-prd-spec.md`. Passing the superset (8 gates) necessarily means passing the subset (6 gates). The acceptance check is a handoff confirmation, not a re-evaluation.

Extra DPRD sections (upstream artifact references: PFD, VH, AR, EL traceability) are not referenced by `prd-spec.md` and therefore not evaluated by `prd-validator.md`. They do not cause failures.

**No regeneration:** The DPRD is not re-processed through the EEK's `prd-prompt.md`. It is placed and validated as-is.

### Engineering Execution Kit Dependencies

The Engineering Execution Kit depends on these sections of the DPRD:

- §2 Problem Statement
- §3 Goals (What "Success" Means)
- §4 Non-Goals (Hard Exclusions)
- §6 Requirements (Functional and Non-Functional)
- §11 Acceptance / Success Criteria

### Cross-Kit Re-Entry Protocol

If a frozen DPRD must change **after** the Engineering Execution Kit has begun work on downstream artifacts (ACF, SAD, TDD, WDD, etc.):

> **Note:** This protocol governs changes that cross the kit boundary. For changes to upstream PIK artifacts (PFD, VH, AR, EL) that cascade to the DPRD but have not yet been handed off, use the standard PIK Re-Entry Protocol instead.

1. **Notify immediately** — Send the proposed change description to the Engineering Execution Kit team before any re-validation begins. Include: what section is changing, what is changing, and why. Do not silently re-validate and re-deliver.

2. **EEK runs impact analysis on the proposal** — The EEK team runs `impact-analysis-prompt.md` using the proposed change description (not the final updated DPRD) against all frozen EEK artifacts. This assesses downstream cost before the PIK commits. The EEK reports back: which artifacts are affected, which work items are impacted, and at what severity.

3. **Joint decision to proceed** — Both teams (human leads) review the impact report and agree to proceed with the change. If impact is too large or the change is contested, this is the decision point to pause or reframe.

4. **PIK re-entry** — Follow the PIK Re-Entry Protocol: update the DPRD, re-validate (all 8 gates), obtain human approval, re-freeze.

5. **Deliver updated DPRD** — Re-deliver as `docs/sdlc/01-prd.md`. The EEK team re-runs the acceptance check (`prd-validator.md`) and saves result as `01-prd-validation.json`.

6. **EEK cascade** — The EEK team re-validates affected downstream artifacts (SAD, TDD, WDD) top-down. Follows the standard EEK Re-Entry Protocol for cascade rules and in-progress work item handling.

7. **Human approval at each step** — Required in both kits. Neither kit self-approves cross-kit changes.

**Re-entry trigger:** Any change to DPRD §2 Problem Statement, §3 Goals, §4 Non-Goals, §6 Requirements, or §11 Acceptance Criteria requires cross-kit re-entry. Changes to §8 Assumptions or §10 Open Questions require EEK notification but may not require cascade re-validation — the EEK team assesses impact using the trigger table in the EEK playbook.

---

## Upstream Interface

This kit accepts strategic direction as informal input. There is no formal upstream handoff contract at this time. The Discovery Intake Form structures whatever strategic context is available.

When the Strategic Direction Kit is implemented, a formal handoff contract should be established.

---

## Freeze Points

| Artifact | Freeze Point | What It Unlocks |
|----------|-------------|-----------------|
| PFD | After validation PASS + human approval | VH generation |
| VH | After validation PASS + human approval | AR generation |
| AR | After validation PASS + human approval | EL generation (+ optional stress test) |
| EL | After validation PASS + human approval | DPRD generation (or pivot/pause decision) |
| DPRD | After validation PASS + human approval | Handoff to Engineering Execution Kit |

---

## Re-Entry Protocol

> **Scope:** This protocol governs changes to PIK-internal artifacts (PFD, VH, AR, EL, DPRD) **before handoff** or when the DPRD changes and has not yet been delivered to the Engineering Execution Kit. For changes to a DPRD that has **already been handed off**, use the Cross-Kit Re-Entry Protocol in the Downstream Handoff section above.

### Steps

When a frozen artifact must change:

1. **Impact analysis** — Before making any change, determine which downstream artifacts are affected using the trigger table below.

2. **Assess change severity** — Determine whether the change is minor (typo, clarification) or substantive (new content, changed requirements, removed sections). See Minor vs. Substantive Changes below.

3. **Modify** — Update the artifact in a new AI session.

4. **Re-validate** — Run the artifact's validator. All hard gates must PASS.

5. **Human approval** — Approve the re-validated artifact before proceeding to cascade.

6. **Cascade** — Re-validate all affected downstream artifacts top-down. If any fail re-validation, they must be regenerated from the updated upstream artifact. Human approval required at each step.

### Trigger Table

This table defines which downstream artifacts are affected when a frozen artifact changes.

| Changed Artifact | Affected Downstream Artifacts | Re-Validation Required |
|-----------------|-------------------------------|------------------------|
| PFD | VH, AR, EL, DPRD | All four must be re-validated. If VH fails, regenerate before re-validating AR. |
| VH | AR, EL, DPRD | AR must be re-validated. If it fails, regenerate before re-validating EL. |
| AR | EL, DPRD | EL must be re-validated. If it fails, regenerate or conduct new experiments (see EL note). |
| EL | DPRD | DPRD must be re-validated. If it fails, regenerate. |
| DPRD (pre-handoff) | None (terminal artifact) | Re-validate DPRD only. |
| DPRD (post-handoff) | EEK artifacts | Use Cross-Kit Re-Entry Protocol — not this protocol. |

**Cascade rule:** Re-validation runs strictly top-down. Do not re-validate AR before re-validating VH. Do not re-validate DPRD before re-validating EL.

### Minor vs. Substantive Changes

**Minor changes** (typo corrections, phrasing clarifications, formatting):
- Both team leads must agree the change is minor and does not alter meaning
- Minor changes to PFD or VH: re-validate only the changed artifact; cascade if downstream artifacts reference the corrected content by section
- If either team lead disagrees that the change is minor, treat it as substantive

**Substantive changes** (new user groups, updated goals, changed assumptions, new or removed requirements):
- Full re-entry protocol applies
- All downstream artifacts affected per the trigger table above must be re-validated

### In-Progress Downstream Work

If downstream artifacts are actively being generated when a re-entry is triggered:

- **Stop** generating the in-progress artifact immediately
- Complete the re-entry cascade first
- Restart downstream generation from the updated upstream artifacts

Do not attempt to merge in-progress changes with re-entry changes. Discard in-progress work and regenerate from the updated upstream artifact after the cascade is complete.

### EL Re-Entry Note

The Experiment Log has a unique dependency: it records results from real-world experiments (data analysis, surveys, interviews, technical assessments). If an upstream change (PFD, VH, or AR) affects which assumptions were tested or how they should be interpreted:

- **If existing experiments are still relevant:** Regenerate the EL from the same experiment data plus the updated upstream artifacts.
- **If existing experiments are no longer relevant:** New experiments must be conducted by the team before the EL can be regenerated. This is human work that cannot be skipped or simulated by AI.
- **Determining relevance:** The team — not the AI — makes this determination. Err toward conducting new experiments if there is any doubt.

### Re-Entry Initiated by Downstream Generation

If generating a downstream artifact reveals a problem in an upstream artifact (e.g., generating the AR exposes an inconsistency in the VH):

1. Stop generating the downstream artifact
2. Trigger re-entry on the upstream artifact (VH in this example)
3. Complete the full re-entry cascade before resuming downstream generation
4. Do **not** modify the downstream artifact to work around the upstream problem

---

## Iteration Rules

### Within a Step

If validation fails:
1. Review the blocking issues in the validator output
2. Regenerate the artifact in a **new AI session** with the validator feedback
3. Re-validate in a **separate AI session**
4. Repeat until all hard gates PASS

### Across Steps

If generating a downstream artifact reveals problems with an upstream artifact:
1. Do **not** modify the downstream artifact to work around the problem
2. Trigger the re-entry protocol on the upstream artifact
3. Cascade re-validation downstream

### Experiment-Driven Iteration

If the Experiment Log reveals invalidated assumptions:
1. Review the EL's impact assessment and recommendation
2. If **proceed**: continue to DPRD generation, incorporating validated/invalidated status
3. If **pivot**: trigger re-entry on the affected upstream artifact (PFD, VH, or AR), then regenerate downstream
4. If **pause**: halt the initiative until the blocking issue is resolved

---

## Session Discipline

- **One artifact per generation session** — do not generate multiple artifacts in one session
- **Separate generation and validation sessions** — prevents self-validation bias
- **Include full frozen upstream artifacts** — do not summarize or paraphrase
- **Include the spec, prompt, and template** for generation sessions
- **Include the spec and validator** for validation sessions
- **Utility prompts are independent sessions** — they do not produce governed artifacts
