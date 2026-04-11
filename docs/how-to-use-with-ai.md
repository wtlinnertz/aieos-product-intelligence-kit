# How to Use the Product Intelligence Kit with AI

This guide explains how to use AI assistants to generate and validate Product Intelligence Kit artifacts.

---

## General Principles

1. **One artifact per session**. Generate each artifact in its own AI session
2. **Separate generation and validation**. Never generate and validate in the same session
3. **Include full inputs**. Always include complete frozen upstream artifacts; do not summarize
4. **Human in the loop**. AI generates and validates; humans review and freeze


## Session Setup

### For Generation Sessions

Include these files in the AI session context:
1. The **prompt** for the artifact type you're generating
2. The **spec** referenced by the prompt
3. The **template** referenced by the prompt
4. Any **principles** files referenced by the prompt
5. All **frozen upstream artifacts** (full text, not summaries)

### For Validation Sessions

Include these files in the AI session context:
1. The **validator** for the artifact type you're validating
2. The **spec** referenced by the validator
3. The **artifact** to be validated
4. All **frozen upstream artifacts** (for traceability checks)

#### Starting a Validation Session. Step by Step

Separate sessions is the rule. Here is what "separate session" means operationally:

1. **End the generation session.** Close the conversation or start a new one. Do not continue in the same thread.
2. **Open a fresh conversation.** No prior context should carry over. If your AI tool has project-level instructions (CLAUDE.md), those are fine. They don't contain artifact content.
3. **Do not paste generation inputs.** The generation session included the prompt, spec, template, and principles. Do not include any of these in the validation session. The validator is the only behavior instruction needed.
4. **Paste in this order:**
   - The spec (`{type}-spec.md`)
   - The validator (`{type}-validator.md`)
   - The frozen upstream artifacts (PFD, VH, AR, EL as applicable for traceability checks)
   - The artifact to validate
5. **Give a single instruction:** "Validate this artifact against the spec and validator. Output JSON only."
6. **Review the output**. If status is fail, fix only the blocking issues listed. do not redesign.
7. **Re-run in a new session** if you make fixes (same rules apply).

### For Utility Prompt Sessions

Include these files in the AI session context:
1. The **utility prompt** you're using
2. The **inputs** specified by the prompt (e.g., work request, frozen artifacts)

Utility prompts do not produce governed artifacts. Their output is analysis for human consumption.


## Step-by-Step Workflow

### Pre-Step: Classify Incoming Work (Optional)

**When to use:** Before filling the Discovery Intake Form, to determine whether this work needs full discovery or should be routed elsewhere.

**Session. Include:**
- `docs/prompts/work-classification-prompt.md`
- The incoming work request description

**Instruction to AI:**
> Classify this work request. Determine the work type, recommended discovery depth, and routing.

**Possible outcomes:**
- **Full discovery**: Proceed to Step 0 (fill Discovery Intake Form)
- **Targeted discovery**: Proceed to Step 0, but note which artifacts can be abbreviated
- **No discovery**: Route to engineering triage, incident management, or backlog: this kit is not needed

### Pre-Step: Brownfield Analysis (Optional)

**When to use:** Before filling the Discovery Intake Form, when the initiative involves an existing system and you have system documentation available.

**Session. Include:**
- `docs/prompts/brownfield-analysis-prompt.md`
- Existing system documentation (architecture docs, API specs, user guides, support ticket data, etc.)
- Optional: focus area description

**Instruction to AI:**
> Analyze this system documentation and produce structured output mapped to Discovery Intake Form sections. Identify current capabilities, user groups, pain points, and constraints.

**Output:** Draft intake content. A human MUST review, correct, and complete the output before using it as the Discovery Intake Form.

### Step 0: Fill and Validate the Discovery Intake Form

1. Open `docs/artifacts/discovery-intake-template.md`
2. Fill in what you know. Leave unknowns blank (or start from brownfield analysis output if available)
3. Complete the checklist at the bottom
4. This is human work. Do not use ai to fill the intake form (except for brownfield analysis output, which must be human-reviewed)

**Validation session. Include:**
- `docs/validators/discovery-intake-validator.md`
- `docs/specs/discovery-intake-spec.md`
- Your completed Discovery Intake Form

**Instruction to AI:**
> Validate this Discovery Intake Form against its specification. Produce the standard validator JSON output.

**If PASS:** Proceed to Step 1 (PFD generation)
**If FAIL:** Address blocking issues in the intake form and re-validate

### Step 0.5: Stakeholder Alignment Analysis (Optional)

**When to use:** When multiple stakeholders have provided input and their views may conflict. Run before PFD generation to surface and resolve disagreements.

**Session. Include:**
- `docs/prompts/stakeholder-alignment-prompt.md`
- Each stakeholder's input (labeled by stakeholder name/role)
- Optional: draft PFD (if one exists)

**Instruction to AI:**
> Analyze these stakeholder inputs. Identify where they converge and diverge on the problem definition, priorities, scope, and success criteria. Classify each divergence as resolvable, negotiable, or blocking.

**Output:** Use the analysis to resolve blocking divergences before PFD generation. Negotiable divergences may inform the PFD's Open Questions section.

### Step 1: Generate Problem Framing Document

**Generation session. Include:**
- `docs/prompts/problem-framing-prompt.md`
- `docs/specs/problem-framing-spec.md`
- `docs/artifacts/problem-framing-template.md`
- `docs/principles/product-discovery-principles.md`
- For compliance initiatives: `docs/principles/compliance-discovery-principles.md`
- Your validated Discovery Intake Form

**Instruction to AI:**
> Generate a Problem Framing Document from the provided Discovery Intake Form. Follow the prompt instructions, satisfy all spec requirements, and use the template structure exactly.

**Validation session (new session). Include:**
- `docs/validators/problem-framing-validator.md`
- `docs/specs/problem-framing-spec.md`
- The generated PFD

**Instruction to AI:**
> Validate this Problem Framing Document against its specification. Produce the standard validator JSON output.

**If PASS:** Human reviews → approves → freezes
**If FAIL:** Review blocking issues → regenerate in a new session with feedback → revalidate

### Step 2: Generate Value Hypothesis

**Generation session. Include:**
- `docs/prompts/value-hypothesis-prompt.md`
- `docs/specs/value-hypothesis-spec.md`
- `docs/artifacts/value-hypothesis-template.md`
- `docs/principles/hypothesis-driven-development.md`
- Frozen PFD (full text)

**Instruction to AI:**
> Generate a Value Hypothesis document from the provided frozen Problem Framing Document. Follow the prompt instructions, satisfy all spec requirements, and use the template structure exactly.

**Validation session (new session). Include:**
- `docs/validators/value-hypothesis-validator.md`
- `docs/specs/value-hypothesis-spec.md`
- The generated VH
- Frozen PFD (for traceability checks)

**If PASS:** Human reviews → approves → freezes
**If FAIL:** Review blocking issues → regenerate → revalidate

### Step 3: Generate Assumption Register

**Generation session. Include:**
- `docs/prompts/assumption-register-prompt.md`
- `docs/specs/assumption-register-spec.md`
- `docs/artifacts/assumption-register-template.md`
- Frozen PFD (full text)
- Frozen VH (full text)

**Instruction to AI:**
> Generate an Assumption Register from the provided frozen Problem Framing Document and Value Hypothesis. Follow the prompt instructions, satisfy all spec requirements, and use the template structure exactly.

**Validation session (new session). Include:**
- `docs/validators/assumption-register-validator.md`
- `docs/specs/assumption-register-spec.md`
- The generated AR
- Frozen PFD (for traceability checks)
- Frozen VH (for traceability checks)

**If PASS:** Human reviews → approves → freezes
**If FAIL:** Review blocking issues → regenerate → revalidate

### Step 3.5: Stress Test Assumptions (Optional)

**When to use:** After freezing the AR, before conducting experiments. Helps design better experiments and catch blind spots.

**Session. Include:**
- `docs/prompts/assumption-stress-test-prompt.md`
- Frozen AR
- Frozen PFD
- Frozen VH

**Instruction to AI:**
> Stress-test the assumptions in this Assumption Register. Challenge each assumption, identify hidden dependencies, assess evidence quality, and identify missing assumptions.

**Output:** Use the analysis to inform experiment design. This does not change the frozen AR.

### Step 3.6: Cross-Initiative Conflict Check (Optional)

**When to use:** After freezing the AR, when other initiatives are also active with frozen ARs. Identifies conflicts before committing resources to experiments.

**Session. Include:**
- `docs/prompts/cross-initiative-conflict-prompt.md`
- This initiative's frozen AR
- Other initiatives' frozen ARs
- Optional: frozen PFDs for each initiative (for scope context)

**Instruction to AI:**
> Analyze these Assumption Registers from different initiatives. Identify direct conflicts, resource competition, shared assumptions, and cascade dependencies. Assess which initiatives can safely proceed in parallel.

**Output:** Use the analysis to resolve critical conflicts before committing to experiments. Shared assumptions may present validation efficiency opportunities.

### Step 4: Generate Experiment Log

**Prerequisites:** The team has conducted validation experiments based on the AR's validation plans. Experiment results data must be gathered before this step.

**Generation session. Include:**
- `docs/prompts/experiment-log-prompt.md`
- `docs/specs/experiment-log-spec.md`
- `docs/artifacts/experiment-log-template.md`
- Frozen PFD (full text)
- Frozen VH (full text)
- Frozen AR (full text)
- Experiment results data (research findings, analysis results, interview notes, survey responses)

**Instruction to AI:**
> Generate an Experiment Log from the provided frozen upstream artifacts and experiment results data. Follow the prompt instructions, satisfy all spec requirements, and use the template structure exactly.

**Validation session (new session). Include:**
- `docs/validators/experiment-log-validator.md`
- `docs/specs/experiment-log-spec.md`
- The generated EL
- Frozen AR (for assumption traceability checks)
- Frozen VH (for hypothesis traceability and scope checks)
- Frozen PFD (for scope checks)

**If PASS:** Human reviews → reviews proceed/pivot/pause recommendation → approves → freezes
**If FAIL:** Review blocking issues → regenerate → revalidate

**Important:** If the EL recommends **pivot** or **pause**, address this before proceeding to Step 5. A pivot triggers re-entry on affected upstream artifacts.

### Step 5: Generate Discovery PRD

**Generation session. Include:**
- `docs/prompts/discovery-prd-prompt.md`
- `docs/specs/discovery-prd-spec.md`
- `docs/artifacts/discovery-prd-template.md`
- Frozen PFD (full text)
- Frozen VH (full text)
- Frozen AR (full text)
- Frozen EL (full text)

**Instruction to AI:**
> Generate a Discovery PRD from the provided frozen upstream artifacts. Follow the prompt instructions, satisfy all spec requirements (including all Engineering Execution Kit downstream gates), and use the template structure exactly.

**Validation session (new session). Include:**
- `docs/validators/discovery-prd-validator.md`
- `docs/specs/discovery-prd-spec.md`
- The generated DPRD
- Frozen PFD (for traceability checks)
- Frozen VH (for traceability checks)
- Frozen AR (for traceability checks)
- Frozen EL (for traceability checks)

**If PASS:** Human reviews → approves → freezes → hand off to Engineering Execution Kit
**If FAIL:** Review blocking issues → regenerate → revalidate

### Step 6: Initiative Prioritization (Optional)

**When to use:** When multiple initiatives have frozen DPRDs and the organization must decide which to fund or sequence.

**Session. Include:**
- `docs/prompts/initiative-prioritization-prompt.md`
- Frozen DPRDs (and their upstream artifacts) for each initiative being compared
- Optional: resource constraints, strategic priorities, cross-initiative conflict analysis output

**Instruction to AI:**
> Compare these initiatives across problem severity, value confidence, risk profile, strategic alignment, and scope. Produce a comparison matrix, sequencing recommendations, and risk-adjusted ranking.

**Output:** Use the analysis to support portfolio prioritization decisions. The prompt does not make the decision. It presents structured evidence for human decision-makers.


## Tips

### Context Window Management
The downstream sessions (EL, DPRD) require multiple frozen artifacts as input. If context window limits are a concern:
- Use AI models with larger context windows for later artifacts
- Ensure all upstream artifacts are included in full, partial inclusion violates session discipline

### Iteration
- Each regeneration attempt should be in a **new session** with the validator feedback included as additional context
- Do not ask the AI to "fix" an artifact in the same session that generated it
- Include the validator's `blocking_issues` as explicit requirements for the regeneration

### Handling Validation Failures
When a validator returns FAIL:
1. Read the `blocking_issues`. these tell you exactly what failed
2. Check if the issue is in the artifact or in the upstream input
3. If upstream: trigger re-entry protocol (see playbook)
4. If in the artifact: regenerate with the blocking issues as additional constraints

### Freezing
When you freeze an artifact:
1. Update the Document Control status to "Frozen"
2. Fill in the Freeze Declaration section (date, approver, statement)
3. The artifact is now immutable. Changes require re-entry protocol

### Experiment Timing
The Experiment Log requires actual experiment results. The team must conduct validation activities between step 3 (ar freeze) and step 4 (el generation). this is the part of the process where human research, data analysis, and testing happen. the ai structures and documents the results; it does not conduct the experiments.
