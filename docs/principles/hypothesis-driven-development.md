# Hypothesis-Driven Development

This document defines the organizational standards for forming and testing hypotheses in product development. It is input material for artifact generation — not a governed artifact itself.

---

## 1. What a Value Hypothesis Is

A value hypothesis is a testable statement about what will create value for users or the business. It takes the form:

> **We believe that** [doing this thing] **for** [these people] **will achieve** [this outcome]. **We will know this is true when** [we observe this evidence].

A value hypothesis is not a feature request, a solution proposal, or a project description. It is a bet — an explicit statement of expected cause and effect that can be proven or disproven.

## 2. Hypothesis Structure

Every value hypothesis must include:

- **Belief**: What we think will happen (the causal claim)
- **Target users**: Who will benefit
- **Expected outcome**: What measurable change we expect
- **Evidence criteria**: How we will know the hypothesis is true or false
- **Falsification criteria**: What evidence would disprove the hypothesis

A hypothesis without falsification criteria is not a hypothesis — it is a wish.

## 3. Types of Hypotheses

Product discovery typically involves three types of hypotheses:

| Type | Question | Example |
|------|----------|---------|
| **Value** | Will users find this valuable? | "Users will complete the workflow 40% faster with guided mode" |
| **Usability** | Can users figure out how to use it? | "Users will complete onboarding without support intervention" |
| **Feasibility** | Can we build it within constraints? | "The system can process requests within 200ms at expected load" |

This kit focuses on **value hypotheses**. Usability and feasibility hypotheses are addressed in downstream kits.

## 4. Hypothesis Quality Standards

**Strong hypotheses are:**
- Specific — they name concrete users, outcomes, and evidence
- Measurable — the outcome can be quantified or objectively verified
- Falsifiable — there is a clear condition under which the hypothesis is wrong
- Bounded — they specify the scope and timeframe of the expected effect
- Independent — each hypothesis can be evaluated on its own

**Weak hypotheses are:**
- Vague ("users will like it")
- Unfalsifiable ("this will improve the experience")
- Compound ("this will increase engagement AND reduce churn AND improve satisfaction")
- Solution-embedded ("adding a dashboard will help users")

## 5. From Hypothesis to Requirement

Value hypotheses are not requirements. They are the reasoning that justifies requirements. The relationship is:

```
Value Hypothesis: "We believe X will achieve Y"
    ↓
Assumption Register: "This requires assumptions A, B, C to be true"
    ↓
Requirements: "The system SHALL do Z" (where Z is what's needed to test or fulfill the hypothesis)
```

Requirements in the Discovery PRD must trace back to at least one value hypothesis. Requirements that exist without a value justification indicate either a missing hypothesis or scope creep.

## 6. Managing Multiple Hypotheses

A product initiative may have multiple value hypotheses. When this happens:
- Each hypothesis must be independently evaluable
- Hypotheses should be prioritized by risk and impact
- Conflicting hypotheses must be identified and resolved before requirements generation
- The Assumption Register must cover assumptions from all active hypotheses

## 7. When Hypotheses Fail

A hypothesis that is disproven is a success of the discovery process, not a failure. When a hypothesis fails:
- Document the evidence that disproved it
- Assess impact on downstream artifacts
- Trigger re-entry if the hypothesis was already embedded in frozen artifacts
- Do not modify evidence to fit the hypothesis

## 8. Hypothesis Iteration

Hypotheses may be refined during discovery. Refinement is expected. However:
- Refinement must be documented (what changed and why)
- A refined hypothesis is a new hypothesis — it replaces, not amends, the previous version
- Once a Value Hypothesis document is frozen, changes require the re-entry protocol
