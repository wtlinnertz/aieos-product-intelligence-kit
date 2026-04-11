# Product Intelligence Kit — Playbook

This playbook defines the end-to-end process for transforming strategic intent into engineering-ready product requirements. It is the authoritative process definition for the Product Intelligence Kit.

---

## Artifact Flow

The Product Intelligence Kit produces five artifact types in a strict linear sequence. Each artifact must be generated, validated, and frozen before the next can begin.

A mandatory classification step routes incoming work before any discovery investment begins.

```
Work Request (incoming)
        │
        ▼
┌─────────────────────────┐
│  Work Classification    │  Step 0: Classify and route (required)
│  Record                 │  prompt → validate → freeze
└────────┬────────────────┘
         │ routes to discovery (Full or Targeted depth)
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

## Step 0: Work Classification

**What:** Classify the incoming work request and produce a frozen routing decision before any discovery investment begins.

**Prompt:** `docs/prompts/work-classification-prompt.md`
**Spec:** `docs/specs/work-classification-spec.md`
**Template:** `docs/artifacts/work-classification-template.md`
**Validator:** `docs/validators/work-classification-validator.md`
**Gate:** Validator PASS + human freeze
**Output:** Frozen Work Classification Record

### Steps

1. Provide the work request to `work-classification-prompt.md` — it produces a completed `work-classification-template.md`
2. Human reviews the AI-produced record and corrects any errors
3. Run `work-classification-validator.md` against the record
4. Fix any blocking issues; re-run until PASS
5. Human completes the Freeze Declaration
6. **Route based on Discovery Depth:**
   - **Full or Targeted** → proceed to Discovery Intake Form (this kit)
   - **None** → route to Engineering Execution Kit, Engineering Triage, or Incident Management as declared; stop here

Not all work enters this kit. Bugs, tech debt, and incident response bypass PIK entirely. The classification record is the evidence that the routing decision was made deliberately.

The frozen classification record is referenced by the EEK Kit Entry Gate as confirmation that the work was classified before entering EEK.

---

## Utility Prompts

The kit includes utility prompts that support the artifact flow but do not produce governed artifacts.

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

### Ideation Workshop

**Prompt:** `docs/prompts/ideation-workshop-prompt.md`

**When to use:** Before Step 0 (WCR), when the user doesn't yet have a concrete idea to classify. The sherpa offers this when it detects ideation-mode signals ("I don't know what to build", "help me brainstorm", "what should we work on").

**Techniques:** 7 named techniques (Signal Synthesis, Jobs-to-Be-Done, Constraint Removal, Competitive Gap Analysis, Technology Enablement Scan, Inversion, SCAMPER). Select 2–3 per session based on context.

**No AIEOS history required:** 5 of 7 techniques work without prior initiatives. Signal Synthesis is skipped when no sibling ERs exist.

**Output:** Ideation Workshop Record (`docs/sdlc/00-ideation-workshop.md`) — an operational record containing all ideas generated, scoring (impact/confidence/effort), and the selected idea for pipeline entry. Feeds directly into WCR and Discovery Intake.

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

**Pre-flight check:** Confirm the Engagement Record exists at `docs/engagement/er-{INITIATIVE}-{NNN}.md` in the consuming project. If it does not exist, create it now — fill in §1 Document Control and leave §2–§7 as stubs. Do not proceed with PFD generation until the ER exists. This check prevents retroactive ER creation, which leads to lost decisions and incomplete records.

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

### From Strategic Direction Kit (SDK) — Layer 1

When the initiative originates from a funded strategic bet:

1. The frozen PPR identifies the above-the-line SBR
2. The frozen SBR provides: thesis (§2), success signal (§3), failure signal (§4), investment envelope (§6)
3. Reference these when filling the Discovery Intake Form — the SBR's thesis becomes strategic context, the signals inform the Value Hypothesis, and the investment envelope constrains the engagement scope

See `docs/entry-from-sdk.md` for the full boundary briefing.

### Without SDK

Not all PIK engagements require SDK artifacts. SDK is optional when:
- The initiative is an enhancement within an existing bet's scope (Preset 2)
- The strategic direction is informal but clear
- The initiative is triggered by IEK re-discover within an existing bet's scope

When entering PIK without SDK artifacts, the Discovery Intake Form structures whatever strategic context is available informally.

---

## Freeze Points

| Artifact | Freeze Point | What It Unlocks |
|----------|-------------|-----------------|
| PFD | After validation PASS + human approval | VH generation |
| VH | After validation PASS + human approval | AR generation |
| AR | After validation PASS + human approval | EL generation (+ optional stress test) |
| EL | After validation PASS + human approval | DPRD generation (or pivot/pause decision) |
| DPRD | After validation PASS + human approval | Handoff to Engineering Execution Kit |

> **Freeze semantics:** A freeze is a human commitment, not a technical lock. Nothing prevents editing a Markdown file after it is frozen. The enforcement mechanism is the Git commit that immediately follows the freeze declaration — that commit is the audit trail. **Frozen artifacts must be committed immediately on approval.** The commit message should identify the artifact and its status (e.g., `docs: freeze PFD-PAYMENTS-001`). If a frozen artifact is edited without following the re-entry protocol, the Git history exposes the deviation.

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
3. If **pivot**: identify which upstream artifact needs revision — see Discovery Iteration Patterns below for the three pivot types and their artifact chains
4. If **pause**: halt the initiative until the blocking issue is resolved; document the blocking issue and minimum evidence required before resuming

---

## Discovery Iteration Patterns

Real discovery is not a pipeline. Learning changes earlier conclusions. This section defines the three patterns that arise when EL experiments or AR analysis reveal that upstream framing needs revision.

These patterns are distinct from the Re-Entry Protocol:
- **Re-Entry Protocol** — governs changes to frozen artifacts due to external events (new requirements, changed constraints)
- **Discovery Iteration Patterns** — govern the normal case of learning within a live discovery engagement that changes upstream framing before the DPRD is generated

The key difference: iteration is expected. Re-entry is exceptional. Treat them differently.

---

### Pattern 1: Problem Reframe

**Trigger:** EL experiment results show the problem in the PFD was incorrectly framed. The team discovers a different problem than the one they were investigating — different in scope, user group, or root cause.

**Examples:**
- Experiments reveal the problem affects a different user group than PFD identified
- Evidence shows the root cause is upstream of what PFD described
- Experiments reveal the problem is a symptom of a more fundamental issue

**Artifact chain:**
1. Record the learning in the EL (add an experiment entry or update the impact assessment)
2. Author a **Pivot Decision Record** (one page — see template below) naming what changed and why
3. Unfreeze the PFD — apply re-entry to the PFD
4. Revise the PFD to reflect the corrected problem framing
5. Re-validate PFD — all hard gates must PASS
6. Re-validate VH for consistency with revised PFD (if VH hypotheses are no longer coherent, revise VH as well)
7. Re-validate AR for consistency (assumptions may change with the problem framing)
8. Re-validate EL — confirm experiment entries are still consistent with the revised framing
9. Generate DPRD from the revised upstream chain

**Cost note:** Problem Reframe is the most expensive iteration pattern — it potentially affects all five upstream artifacts. If the problem reframe is so significant that the initiative should be reconsidered entirely, treat this as a pause decision, not a reframe.

---

### Pattern 2: Hypothesis Revision

**Trigger:** AR risk analysis or EL experiments show the value mechanism is wrong — the hypothesis about how value is created for users is incorrect — but the problem framing in the PFD is still correct.

**Examples:**
- The proposed capability was tested and users don't value it the way the team expected
- A technical constraint invalidated a key assumption about how the hypothesis could be delivered
- Experiments confirmed the problem exists but revealed a different mechanism for solving it

**Artifact chain:**
1. Record the learning in the EL (update the experiment entry with results and interpretation)
2. Author a **Pivot Decision Record** naming what changed and why
3. Unfreeze the VH — apply re-entry to the VH
4. Revise the VH to reflect the corrected value hypothesis (new hypothesis, revised confidence levels, updated success metrics)
5. Re-validate VH — all hard gates must PASS
6. Re-validate AR — if new hypothesis introduces new assumptions, add them; if invalidated assumptions are now irrelevant, remove them
7. Re-validate EL — confirm experiment entries and recommendations are consistent with revised VH
8. Generate DPRD from the revised upstream chain

**Cost note:** Hypothesis Revision does not require revisiting the PFD. If the PFD must also change, treat this as a Problem Reframe (Pattern 1).

---

### Pattern 3: Assumption Invalidation

**Trigger:** EL invalidates a specific assumption, but the problem framing and hypothesis are still correct. The scope or approach needs adjustment, but the core direction holds.

**Examples:**
- A technical integration assumed to be straightforward proved infeasible; the approach must change
- A user behavior assumption was wrong, but the problem and value hypothesis remain valid
- A market assumption was incorrect in a way that changes scope but not direction

**Artifact chain:**
1. Record the learning in the EL (mark assumption as Invalidated, document the evidence, update the impact assessment and recommendation)
2. Determine whether the invalidation:
   - **(a) Changes the scope or constraints of the work** — update the AR assumption status, assess downstream DPRD scope impact, then proceed to DPRD generation with adjusted constraints documented
   - **(b) Invalidates the hypothesis mechanism** — treat as Hypothesis Revision (Pattern 2)
   - **(c) Invalidates the problem framing itself** — treat as Problem Reframe (Pattern 1)
3. If path (a): no upstream artifact revision is required. The DPRD will reflect the invalidated assumption status from the EL. Document the scope adjustment in the DPRD Constraints section.
4. If additional experiments are needed before any path can be determined: add new experiments to the EL, conduct them, then re-evaluate.

**Cost note:** Pattern 3 is the lightest iteration pattern. It often resolves without artifact revision — the DPRD naturally incorporates the invalidated assumption status from the EL per the DPRD spec.

---

### Pivot Decision Record

When triggering Pattern 1 or Pattern 2, author a one-page Pivot Decision Record before making any artifact changes. This record is not a governed artifact — it does not have a validator or freeze point. It exists to make the iteration traceable.

**Format:**

```markdown
## Pivot Decision Record

- Date:
- Engagement:
- Artifact to revise: (PFD | VH)
- Pattern: (Problem Reframe | Hypothesis Revision)

### What changed

(1-2 sentences: what did experiments reveal that changes the upstream framing?)

### Evidence

(Reference to the EL entry that triggered this pivot — EXP-N identifier and brief summary)

### What is being revised

(Specific sections or content in the artifact that will change. Be concrete.)

### What remains unchanged

(What is NOT changing — to confirm the scope of the revision is bounded)

### Human approval

Approved by: ____________  Date: ____________
```

File this as `pivot-decision-{date}.md` in the engagement's working directory. It becomes part of the discovery record.

---

### When to Use Re-Entry vs. Iteration Patterns

| Situation | Use |
|-----------|-----|
| EL experiments change problem framing | Pattern 1 (Problem Reframe) |
| EL/AR analysis changes value hypothesis | Pattern 2 (Hypothesis Revision) |
| EL invalidates an assumption, scope adjusts | Pattern 3 (Assumption Invalidation) |
| External requirement changes after freeze | Re-Entry Protocol |
| DPRD already handed off to EEK and must change | Cross-Kit Re-Entry Protocol |
| Downstream generation reveals upstream inconsistency | Re-Entry Protocol (see Re-Entry Initiated by Downstream Generation) |

If the situation involves a frozen artifact that must change due to external input (not discovery learning), use the Re-Entry Protocol. If it involves discovery learning changing upstream framing, use the iteration patterns. When in doubt, use the iteration patterns — they are lighter and designed for the normal discovery flow.

---

## Amendment Procedure

A frozen artifact may be corrected in place without re-validation when **all** of the following criteria are met:

1. The correction does not affect any field evaluated by a hard gate.
2. The correction does not change scope, decisions, owners, or technical specifications.
3. The correction does not affect any field referenced by a downstream artifact.

**Procedure:** Make the correction and add an Amendment Log entry to the artifact's Document Control section: date, what changed, materiality criterion cited, and who authorized the change. No re-validation is required.

**If there is any ambiguity** about whether a change is non-material, treat it as material and use the Re-Entry Protocol. The amendment path must not become a workaround for the re-entry protocol.

---

## Receiving Escalations

This kit may receive escalations from downstream layers. Escalation is an assessed recommendation — it is not an automatic re-entry trigger.

### Trigger 2 — Recurring Reliability Pattern (from RRK)

**Signal:** The Reliability & Resilience Kit (Layer 6) has identified a recurring root cause class across three or more review periods for a service that traces to a product decision in scope of this kit.

**What to do:**
1. Receive the escalation record from the RRK team. It will include: trigger type, triggering artifact ID (an RHR or IR), signal description, and recommended action.
2. Run a new Work Classification against the escalation description. The question is: does this recurring pattern warrant a new discovery engagement, or is it within the scope of an active/pending engagement?
3. If a new discovery engagement is warranted: create a new Work Classification Record (Step 0), use the escalation record as intake context, and begin a fresh PFD.
4. If it falls within an existing engagement: assess whether any frozen DPRD or upstream artifact needs re-entry. Use the Cross-Kit Re-Entry Protocol if the affected DPRD has already been handed off.
5. A human must authorize the decision to open a new engagement or decline. Declining is valid — document the rationale.

### Trigger 4 — Release Rollback Revealing Wrong Feature (from REK)

**Signal:** The Release & Exposure Kit (Layer 5) has identified that a release rollback was caused by a fundamental product direction problem — the feature should not have been built as specified, not merely that the build or release was flawed.

**What to do:**
1. Receive the escalation record from the REK team.
2. Retrieve the DPRD that generated the feature in question.
3. Assess whether the DPRD goals, requirements, or value hypotheses are at fault. This requires reviewing the upstream PIK artifact chain (PFD, VH, AR, EL).
4. If the discovery chain is at fault: open a new discovery engagement. The prior DPRD and its upstream chain are superseded; they are not re-entered — a fresh engagement is more appropriate when the fundamental direction was wrong.
5. If the DPRD was correct but implementation diverged: the issue belongs in EEK, not PIK. Return the escalation record to the REK team with this assessment.
6. A human must authorize the decision at step 4 or 5.

---

## Principle File Revision

When a principle file in `docs/principles/` changes, use the change categories defined in `aieos-governance-foundation/docs/principle-file-standard.md`:

| Change Category | Version Bump | Re-Entry Impact |
|----------------|-------------|-----------------|
| **Minor** (clarification only) | `v_.x → v_.x+1` | No re-entry required; already-frozen artifacts remain valid |
| **Significant** (new requirement or tightened constraint) | `v1.x → v1.x+1` | Review artifacts generated after the change against updated principles; already-frozen artifacts are grandfathered |
| **Breaking** (removal or loosening) | `vN.x → vN+1.0` | Requires service owner authorization and documented business justification; re-entry may be warranted |

Every change to a principle file must bump the version field, even minor clarifications.

---

## Deprecation and Sunset

When a discovery initiative ends — either by completion, cancellation, or strategic redirect — the artifacts it produced transition to terminal lifecycle states. See the full protocol in `aieos-governance-foundation/docs/deprecation-protocol.md`.

### When to Deprecate or Abandon

| Situation | Action |
|-----------|--------|
| Discovery completed; DPRD frozen and handed off; initiative concluded | `Deprecated` on all frozen artifacts after system reaches end of operational life |
| Initiative cancelled after one or more artifacts are Frozen | `Deprecated` on frozen artifacts; `Abandoned` on any non-frozen artifacts |
| Initiative cancelled before any artifact is Frozen | `Abandoned` on all in-progress artifacts |
| Discovery concluded with a Pause or stop signal at EL; no DPRD produced | `Abandoned` on all artifacts in the series |

### Who Authorizes

A product owner, team lead, or equivalent role must authorize the terminal state transition. Do not move to `Deprecated` or `Abandoned` without an authorizing name and role recorded in the Deprecation Notice.

### How to Issue a Deprecation Notice (DN)

1. Confirm the cancellation or conclusion decision is authorized.
2. List all artifacts in the discovery series with their current status.
3. For each artifact: if Frozen → `Deprecated`; if not Frozen → `Abandoned`.
4. Create a DN record at `docs/sdlc/dn-{initiative-id}-{NNN}.md` using the format in `aieos-governance-foundation/docs/deprecation-protocol.md`.
5. Update each artifact's Status field to its terminal state (non-material amendment; add Amendment Log entry per governance model §6).

### What Does Not Change

- Artifacts are retained — never deleted.
- Terminal state does not require re-validation.
- If the initiative restarts, new artifacts with new IDs are produced. Terminal-state artifacts are not reactivated.

---

## Maintaining the Engagement Record

The Engagement Record (ER) is a project-level artifact that lives in the consuming project at `docs/engagement/er-{initiative}.md`. It spans all AIEOS layers and is maintained by each kit's operators as work passes through. The ER spec and format are defined in `aieos-governance-foundation/docs/engagement-record-spec.md`.

**PIK creates the ER and maintains its Layer 2 section.**

### When to Create the ER

Create the ER when the Discovery Intake is validated — at the beginning of Step 1 (PFD generation). Create the file at `docs/engagement/er-{INITIATIVE}-{NNN}.md` in the consuming project. Fill in §1 Document Control and leave §2–§7 as stubs. The ER must exist before the first governed artifact is generated.

### What to Update During Discovery

| Trigger | ER update |
|---------|-----------|
| WCR frozen | Add WCR ID to §2 artifact table |
| Discovery Intake validated | Record intake date in §2 |
| PFD frozen | Add PFD ID to §2 |
| VH frozen | Add VH ID to §2 |
| AR frozen | Add AR ID to §2 |
| EL frozen | Add EL ID to §2 |
| Pivot decision made | Add PDR ID to §2; record pivot in §2 Key Decisions with the AR assumption ID that was invalidated |
| DPRD frozen | Add DPRD ID to §2 |

### On Initiative End

When issuing a Deprecation Notice: update §1 Status to `Deprecated` or `Abandoned`, add the DN ID to §7 Initiative Outcome, and record the final VH verdict in §7 if known.

---

## Session Discipline

- **One artifact per generation session** — do not generate multiple artifacts in one session
- **Separate generation and validation sessions** — prevents self-validation bias
- **Include full frozen upstream artifacts** — do not summarize or paraphrase
- **Include the spec, prompt, and template** for generation sessions
- **Include the spec and validator** for validation sessions
- **Utility prompts are independent sessions** — they do not produce governed artifacts
