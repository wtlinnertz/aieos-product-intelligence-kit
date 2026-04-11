# Troubleshooting Guide: Product Intelligence Kit

## How to Use This Guide

When a validator returns FAIL, find the failing gate in the table below. The Remediation column describes the specific fix required. Reopen the artifact, apply the remediation, and rerun the validator in a new session.

Validators and generation are separate sessions. Don't embed fix attempts in your validation session.

---

## Work Classification Record (WCR)

This is a human-completed artifact. Fill all fields directly in the template before running the validator.

| Gate | What Failure Looks Like | Typical Cause | Remediation |
|------|------------------------|---------------|-------------|
| document_control | Missing ID, owner, date, or status field | Incomplete template fill | Add all required fields from template §1; no field may be blank |
| type_declared | Composite type stated (e.g., "Feature / Enhancement") | Ambiguity in classification | Use exactly one type from the enumerated list; composite entries are not permitted |
| routing_complete | No routing decision recorded | Classification done without completing the routing step | Complete §3 routing decision: name which kit receives the work and which entry path applies |
| justification_present | Type selection has no explanation | Classification treated as self-evident | Add 2–3 sentences explaining why this work type was chosen over the alternatives |
| risk_flags_addressed | Risk flags section blank or missing | Template section skipped | Assess each risk flag explicitly; "None identified" must be written out, not left blank |
| no_solution_content | Solution proposals or implementation details present | Habit of combining problem framing with solution design | Remove all solution content; the WCR classifies work, it does not design it |

---

## Discovery Intake Form (boundary contract)

This is a human-completed artifact. It is the upstream boundary contract for PIK. Validate before passing to PIK for processing.

| Gate | What Failure Looks Like | Typical Cause | Remediation |
|------|------------------------|---------------|-------------|
| problem_defined | Problem statement absent, or describes a feature or solution | Solution written instead of problem | Rewrite to describe the observed gap, pain, or constraint: not what to build |
| users_identified | User group absent or described only as "all users" | Insufficient specificity in audience definition | Name the specific user segment(s) with observable characteristics that distinguish them |
| urgency_stated | Business urgency or timing not present | Field treated as optional | Add urgency context: the driver (deadline, competitor move, regulation), timing, and consequences of delay |
| evidence_present | No supporting data cited | Assumption that the problem is widely understood | Attach at least one piece of evidence: a research finding, support ticket volume, or a specific metric |
| scope_bounded | Scope described as open-ended or left for engineering to define | Scope boundary not established by submitter | State what is in scope and what is explicitly out of scope |
| no_solutions | Solution, technology choice, or implementation detail present | Natural habit when thinking about a problem | Remove all solution content; the intake describes the problem, not the approach |

---

## Problem Framing Document (PFD-{PROJECT}-{NNN})

| Gate | What Failure Looks Like | Typical Cause | Remediation |
|------|------------------------|---------------|-------------|
| problem_definition | Problem statement contains a solution direction (e.g., "We need to improve X by building Y") | Framing written from a solution mindset | Rewrite as an observable gap: who is affected, what they cannot do, and what consequence follows |
| user_landscape | User types described without pain attribution | User research summary pasted without framing it to the problem | Connect each user type to a specific pain point in their workflow |
| pain_points | Pain points listed without evidence linkage | Pain invented or assumed rather than observed | Cite the evidence source for each pain point (intake form reference, research finding, metric) |
| opportunity | Opportunity section states a solution or product | Solution-first thinking | State the opportunity as the gap that could be closed, not the product that could close it |
| current_state | Current state section absent or too vague to be useful | Assumed shared knowledge among the team | Document the current behavior, workaround, or state with enough specificity that an outsider understands it |
| no_solutions | Solution, technology choice, or architectural direction present | Habit of moving toward solutions during framing | Remove all solution content; PFD describes what is true today, not what to build |

---

## Value Hypothesis (VH-{PROJECT}-{NNN})

| Gate | What Failure Looks Like | Typical Cause | Remediation |
|------|------------------------|---------------|-------------|
| hypothesis_present | No falsifiable hypothesis statement present | Hypothesis written as a statement of intent or goal | Rewrite in "If [condition], then [measurable outcome]" form |
| falsifiable | Hypothesis cannot be proven true or false with observable data | Vague outcome language ("users will be happier") | Define a specific metric and threshold that would constitute proof or disproof |
| user_traceability | Hypothesis references user types not established in PFD | New user group introduced during hypothesis writing | Hypothesis must reference user types established in PFD §2; introduce no new groups |
| no_scope_expansion | New problems or user groups introduced beyond PFD scope | Scope creep during hypothesis formulation | Remove additions; the VH tests a hypothesis within the scope of the PFD |
| no_solutions | Implementation or technology choice present | Build-forward thinking during hypothesis work | Remove solution content; VH tests whether value would be delivered, not how |
| metrics_defined | Metric section names a metric with no measurement method | Metric defined without a measurement plan | Define what to measure, how to measure it, and what threshold constitutes success |

---

## Assumption Register (AR-{PROJECT}-{NNN})

| Gate | What Failure Looks Like | Typical Cause | Remediation |
|------|------------------------|---------------|-------------|
| assumption_inventory | Fewer than 3 assumptions cataloged for a non-trivial hypothesis | Assumptions not fully surfaced | Run `assumption-stress-test-prompt.md` before freezing; aim for complete coverage of user, market, and feasibility assumptions |
| source_traceability | Assumptions cite "PFD" without a section reference (should be "PFD §3 UG-1") | Lazy referencing during register population | Update each assumption's Source field to include the specific section number and item ID |
| risk_assessment | Risk ratings absent or every assumption rated "low" | Risk-aversion in self-assessment | Apply the risk rating criteria from the spec honestly; high-risk assumptions are expected and acceptable |
| high_risk_validation | High-risk assumptions have no validation plan | Validation planning deferred | Add an explicit validation approach for each high-risk assumption before freezing the AR |
| no_scope_expansion | New assumptions reference problems not established in PFD or VH | Scope drift during assumption surfacing | Remove out-of-scope assumptions; the AR catalogs assumptions about the established problem only |
| no_solutions | Assumptions describe implementation choices rather than unknowns | Solution thinking reframed as assumptions | Reframe as assumptions about user behavior, market conditions, or feasibility: not design choices |

---

## Experiment Log (EL-{PROJECT}-{NNN})

| Gate | What Failure Looks Like | Typical Cause | Remediation |
|------|------------------------|---------------|-------------|
| experiment_present | Experiment section missing, or describes planned experiments only | Log written before experiments ran | Complete actual experiments before generating the EL; the EL records outcomes, not plans |
| assumption_traceability | Experiments not linked to specific AR assumptions | Experiments designed and run without tracking which assumption each tests | Each experiment entry must reference the AR assumption ID it was designed to validate |
| evidence_based_conclusions | Conclusions stated without supporting observations | Interpretation produced before evidence is documented | Separate §Observations (factual record) from §Conclusions (interpretation); support every conclusion with at least one observation |
| impact_assessed | Impact of results on upstream artifacts not addressed | Downstream consequence analysis skipped | For each experiment, explicitly assess whether the outcome requires PFD, VH, or AR updates |
| no_scope_expansion | New problems or assumptions introduced based on experiment findings | Experiments surfaced new issues that were added to scope | Do not expand scope; document new findings in a note for a future engagement |
| no_solutions | EL includes solution design or implementation detail | Engineers contributed build proposals during experiment review | Remove all solution content; the EL records what was learned, not what to build |

---

## Discovery PRD (DPRD-{PROJECT}-{NNN})

| Gate | What Failure Looks Like | Typical Cause | Remediation |
|------|------------------------|---------------|-------------|
| problem_definition | Problem definition contradicts or rephrases PFD §1 | Drift from upstream framing during generation | Align §1 with PFD §1 exactly; do not rephrase or expand |
| goals | Goals not traceable to VH metrics or hypothesis | Goals invented during DPRD generation | Each goal must cite the VH metric or hypothesis statement it fulfills |
| scope | Scope contains items not present in PFD, VH, AR, or EL | Scope expansion during requirements writing | Remove scope additions; DPRD scope is bounded by the frozen upstream artifact chain |
| requirements | Requirements prescribe implementation (e.g., "SHALL use microservices") | Engineers contributing to requirements during generation | Rewrite as outcome or capability requirements; remove how, keep what |
| constraints | Constraints section empty or states aspirations rather than real constraints | Constraints treated as optional or filled with goals | Document actual constraints from the intake form and AR; "None" requires explicit written justification |
| readiness | Readiness checklist items unchecked with no explanation | Readiness checklist not reviewed before freeze | Address each unchecked item; provide explicit justification for any item intentionally skipped |
| upstream_traceability | Requirements not traceable to upstream artifact IDs | Traceability added as afterthought or omitted | Add a source reference to each requirement (e.g., "VH-TASKFLOW-001 §2") |
| no_scope_expansion | DPRD introduces new problems, user groups, or capabilities | Discovery findings tempted scope additions during writing | Remove all additions; content not present in the frozen upstream chain does not belong in the DPRD |
