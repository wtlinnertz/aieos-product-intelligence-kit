# Session Setup: Product Intelligence Kit

Use this file to set up an AI session for each PIK artifact. Find the section for the artifact you're generating or validating. Follow the checklist before starting.

**Rule:** Generate and validate in separate sessions. Do not self-validate.

---

## Work Classification Record (WCR)

**What you're creating:** A formal classification of incoming work that determines routing, entry path, and whether discovery is required.

**Note:** The WCR is human-authored with AI assistance. The prompt provides classification guidance, not a generation template.

**Required Inputs (confirm before starting):**
- [ ] Work request or problem statement: Present?
- [ ] Stakeholder context (requestor, urgency, known constraints): Present?

**Pre-Flight Gate Check (verify before generating):**
- [ ] `document_control`: ID, owner, date, and status fields planned
- [ ] `type_declared`: One classification type ready to select from the enumerated list
- [ ] `routing_complete`: Know which kit and which entry path this work routes to
- [ ] `justification_present`: Can explain the classification choice in 2-3 sentences
- [ ] `risk_flags_addressed`: Have considered each risk flag category
- [ ] `no_solution_content`: Work request does not contain solution proposals

**Session Setup:**
1. Load: `docs/prompts/work-classification-prompt.md`
2. Provide: The incoming work request or problem statement (verbatim)
3. Provide: Any stakeholder context (requestor, timeline, urgency, constraints)
4. Validate in a separate session: `docs/validators/work-classification-validator.md`

**Common Failure to Avoid:**
Composite types (e.g., "Feature / Enhancement"): select exactly one type from the enumerated list.

---

## Discovery Intake Form (boundary contract)

**What you're creating:** A structured description of the problem that will gate discovery. This is a human-authored form: no AI generation.

**Note:** Validate the completed intake form before generating any discovery artifacts. Fixing intake gate failures later is expensive.

**Required Inputs (confirm before starting):**
- [ ] Completed WCR: Frozen?
- [ ] Problem statement: Present and free of solution language?
- [ ] User group description: Named and specific?
- [ ] Supporting evidence: At least one piece?

**Pre-Flight Gate Check (verify before generating):**
- [ ] `problem_defined`: Problem statement describes a gap or pain, not a feature
- [ ] `users_identified`: Specific user segment named (not "all users")
- [ ] `urgency_stated`: Business urgency, timing, and consequences present
- [ ] `evidence_present`: At least one evidence source cited
- [ ] `scope_bounded`: What is in scope and out of scope is stated
- [ ] `no_solutions`: No solutions, technology choices, or implementation details present

**Session Setup:**
1. Use: `docs/artifacts/discovery-intake-template.md`: fill manually, no prompt
2. Validate in a separate session: `docs/validators/discovery-intake-validator.md`
3. Do not generate PFD until the intake form passes validation

**Common Failure to Avoid:**
Solution language in the problem statement (e.g., "We need a notification service"): rewrite to describe the gap: who cannot do what, and what consequence follows.

---

## Problem Framing Document (PFD-{PROJECT}-{NNN})

**What you're creating:** A structured framing of the problem space: who is affected, what they cannot do, and what the opportunity represents. No solutions.

**Required Inputs (confirm before starting):**
- [ ] Validated Discovery Intake Form: Frozen?
- [ ] WCR: Frozen?

**Pre-Flight Gate Check (verify before generating):**
- [ ] `problem_definition`: Can state the problem as an observable gap (not a solution direction)
- [ ] `user_landscape`: User types are specific and traceable to intake
- [ ] `pain_points`: Each pain point has an evidence source from the intake
- [ ] `opportunity`: Opportunity can be stated as a gap to close, not a product to build
- [ ] `current_state`: Current behavior or workaround is documented with specificity
- [ ] `no_solutions`: No solution content, technology choices, or implementation details

**Session Setup:**
1. Load: `docs/prompts/problem-framing-prompt.md`
2. Provide: Full content of the validated Discovery Intake Form
3. Provide: `docs/specs/problem-framing-spec.md` (or confirm it is in context)
4. Validate in a separate session: `docs/validators/problem-framing-validator.md`

**Common Failure to Avoid:**
Solution-adjacent framing ("We need to improve onboarding"): rewrite as an observable gap: who is affected, what they cannot accomplish, what the consequence is.

---

## Value Hypothesis (VH-{PROJECT}-{NNN})

**What you're creating:** A falsifiable statement of what value would be delivered if the problem is solved: with measurable success criteria. No solutions.

**Required Inputs (confirm before starting):**
- [ ] Frozen PFD (PFD-{PROJECT}-{NNN}): Frozen?
- [ ] Frozen Discovery Intake Form: Frozen?

**Pre-Flight Gate Check (verify before generating):**
- [ ] `hypothesis_present`: Can state hypothesis in "If [condition], then [measurable outcome]" form
- [ ] `falsifiable`: Success criterion is a specific metric with a defined threshold
- [ ] `user_traceability`: Hypothesis user types come from PFD §2, not newly introduced
- [ ] `no_scope_expansion`: VH does not introduce new problems or user groups beyond PFD scope
- [ ] `no_solutions`: No implementation, technology, or design choices present
- [ ] `metrics_defined`: Measurement method, data source, and threshold are specified

**Session Setup:**
1. Load: `docs/prompts/value-hypothesis-prompt.md`
2. Provide: Full text of frozen PFD
3. Provide: `docs/specs/value-hypothesis-spec.md` (or confirm it is in context)
4. Validate in a separate session: `docs/validators/value-hypothesis-validator.md`

**Common Failure to Avoid:**
Hypothesis containing a solution ("We will build a wizard that will increase completions by 20%"): rewrite to test the value bet: "If users can complete onboarding in under 3 minutes, completion rate will increase by 20%."

---

## Assumption Register (AR-{PROJECT}-{NNN})

**What you're creating:** A catalog of all assumptions underlying the hypothesis, with risk assessment and validation plans for high-risk assumptions.

**Required Inputs (confirm before starting):**
- [ ] Frozen PFD: Frozen?
- [ ] Frozen VH: Frozen?

**Pre-Flight Gate Check (verify before generating):**
- [ ] `assumption_inventory`: Have identified ≥3 distinct assumptions (more for complex initiatives)
- [ ] `source_traceability`: Each assumption has a section-level source reference (e.g., "PFD §3 UG-1")
- [ ] `risk_assessment`: Risk rating criteria understood and will be applied honestly
- [ ] `high_risk_validation`: Validation plan ready for each assumption rated high-risk
- [ ] `no_scope_expansion`: Assumptions are about the established problem, not new problems
- [ ] `no_solutions`: No implementation choices embedded in assumption statements

**Session Setup:**
1. Load: `docs/prompts/assumption-register-prompt.md`
2. Provide: Full text of frozen PFD and frozen VH
3. Provide: `docs/specs/assumption-register-spec.md` (or confirm it is in context)
4. Consider running `docs/prompts/assumption-stress-test-prompt.md` before freezing to surface adversarial risks
5. Validate in a separate session: `docs/validators/assumption-register-validator.md`

**Common Failure to Avoid:**
Source references citing only "PFD" without section: use specific section and item IDs (e.g., "PFD §3 UG-1") so each assumption is independently traceable.

---

## Experiment Log (EL-{PROJECT}-{NNN})

**What you're creating:** A record of assumption validation experiments: what was tested, what was observed, and what conclusions follow. Generated after experiments are complete, not before.

**Required Inputs (confirm before starting):**
- [ ] Frozen PFD: Frozen?
- [ ] Frozen VH: Frozen?
- [ ] Frozen AR: Frozen?
- [ ] Actual experiment results: Complete? (Do not generate EL before experiments run)

**Pre-Flight Gate Check (verify before generating):**
- [ ] `experiment_present`: At least one experiment has been completed and results are in hand
- [ ] `assumption_traceability`: Each experiment maps to a specific AR assumption ID
- [ ] `evidence_based_conclusions`: Factual observations are separated from interpretations
- [ ] `impact_assessed`: Ready to assess whether results require upstream artifact updates
- [ ] `no_scope_expansion`: Experiments tested existing assumptions, did not expand scope
- [ ] `no_solutions`: EL records what was learned, not what to build

**Session Setup:**
1. Load: `docs/prompts/experiment-log-prompt.md`
2. Provide: Full text of frozen AR (assumption IDs and risk assessments)
3. Provide: Experiment results: organized by assumption ID, with raw observations separate from conclusions
4. Provide: `docs/specs/experiment-log-spec.md` (or confirm it is in context)
5. Validate in a separate session: `docs/validators/experiment-log-validator.md`

**Common Failure to Avoid:**
Conclusions stated without supporting observations ("users found the feature helpful"): separate what was observed (quotes, metrics, behaviors) from what it means (the interpretation).

---

## Discovery PRD (DPRD-{PROJECT}-{NNN})

**What you're creating:** Engineering-ready requirements that serve as the handoff artifact to the Engineering Execution Kit. Scope is bounded by all upstream frozen artifacts: no expansion permitted.

**Required Inputs (confirm before starting):**
- [ ] Frozen PFD: Frozen?
- [ ] Frozen VH: Frozen?
- [ ] Frozen AR: Frozen?
- [ ] Frozen EL: Frozen? (EL must show a "proceed" decision)

**Pre-Flight Gate Check (verify before generating):**
- [ ] `problem_definition`: PFD §1 problem statement ready to carry forward verbatim
- [ ] `goals`: VH metrics and hypotheses are the source of goals: not new goals
- [ ] `scope`: Can bound scope to what is traceable in upstream artifacts
- [ ] `requirements`: Requirements will describe outcomes/capabilities, not implementation
- [ ] `constraints`: Known constraints from intake and AR are ready to document
- [ ] `readiness`: All readiness checklist items are satisfiable
- [ ] `upstream_traceability`: Each requirement will cite its upstream source (PFD/VH/AR/EL ID + section)
- [ ] `no_scope_expansion`: No additions beyond what the upstream artifact chain established

**Session Setup:**
1. Load: `docs/prompts/discovery-prd-prompt.md`
2. Provide: Full text of all four frozen upstream artifacts (PFD, VH, AR, EL)
3. Provide: `docs/specs/discovery-prd-spec.md` (or confirm it is in context)
4. Validate in a separate session: `docs/validators/discovery-prd-validator.md`
5. After validation PASS: deliver to Engineering Execution Kit as `docs/sdlc/01-prd.md`

**Common Failure to Avoid:**
Requirements that prescribe implementation ("The system SHALL use microservices architecture"): rewrite as capability or outcome requirements: what the system must do, not how it does it.
