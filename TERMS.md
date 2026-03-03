# TERMS

This document defines common terms used throughout the **Product Intelligence Kit**.

These definitions are intentionally **tool-agnostic**, **employer-neutral**, and **AI-friendly**.

---

## Core Concepts

### Discovery
The process of defining a problem, understanding affected users, forming value hypotheses, and validating assumptions — before committing to engineering solutions. Discovery precedes specification.

---

### Artifact
A persisted document produced at a specific stage of the discovery process. Artifacts are promoted, not rewritten, as work progresses downstream.

Examples: PFD, VH, AR, EL, DPRD.

---

### Artifact Promotion
The formal progression of an artifact to the next stage after passing validation. Once promoted, an artifact is considered frozen.

---

### Freeze
A state indicating an artifact is approved and may not be reinterpreted, expanded, or redesigned by downstream artifacts without explicit re-entry. Freeze requires human approval after validation.

---

### Hard Gate
A validation criterion that must pass for an artifact to be promoted. Any hard gate failure results in a FAIL status — there is no partial pass. Hard gates are defined in specs and evaluated by validators.

---

### Re-Entry Protocol
The process by which a frozen artifact is reopened for modification. Re-entry requires impact analysis, modification, re-validation, cascade re-validation of downstream artifacts, and human approval at each step.

---

## Discovery Artifacts

### Discovery Intake Form
A human-authored intake document that captures problem context before discovery begins. It is the upstream boundary contract for the kit. Not a governed artifact — it has no generation prompt. Must be validated before PFD generation begins.

---

### Problem Framing Document (PFD)
Defines the problem space: the specific problem being addressed, affected users, pain points, opportunity sizing, current state, and constraints. Does not propose solutions.

---

### Value Hypothesis (VH)
Defines testable beliefs about the value that solving the problem will deliver. Each hypothesis specifies a belief, target users, expected outcome, evidence criteria, and falsification criteria. Does not propose solutions or architecture.

---

### Assumption Register (AR)
Catalogs the assumptions that underlie the PFD and VH, assesses their risk level, and defines a validation plan. Risk levels: High, Medium, Low.

---

### Experiment Log (EL)
Records the results of assumption validation activities (research, interviews, surveys, technical assessments). Documents what was tested, what was found, and what the evidence means for each assumption. Ends with a proceed/pivot/pause recommendation.

---

### Discovery PRD (DPRD)
Synthesizes all upstream discovery artifacts into an engineering-ready product requirements document. Satisfies the Engineering Execution Kit's PRD specification. Terminal artifact of the Product Intelligence Kit — the handoff to engineering.

---

## Validation Concepts

### Validator
A document that defines the judgment procedure for evaluating an artifact against its spec. Validators produce PASS or FAIL in structured JSON. They do not suggest improvements or redesign.

---

### Blocking Issue
A validator finding that causes a hard gate to FAIL. Must be resolved before the artifact can be promoted. Blocking issues are reported under `blocking_issues` in the validator output.

---

### Warning
A validator observation that does not cause a FAIL but flags a potential risk, ambiguity, or gap worth attention. Warnings do not prevent promotion.

---

### Completeness Score
A 0–100 score included in validator output indicating the overall completeness of the artifact's content. A high completeness score does not mean PASS — hard gate failures override the score. A FAIL artifact may have a high completeness score if most content is present but one gate is definitively unmet.

---

## Process Concepts

### Session Discipline
The practice of using separate AI sessions for generation and validation of the same artifact, to prevent self-validation bias. One artifact per generation session.

---

### Upstream Boundary Contract
The validated Discovery Intake Form. Upstream teams may produce and validate intake artifacts independently, without access to PIK internals, as long as the intake form satisfies all 6 hard gates.

---

### Downstream Contract
The frozen Discovery PRD. It satisfies the Engineering Execution Kit's PRD specification (6 hard gates), enabling the EEK to begin engineering without any re-generation of the PRD.

---

### Utility Prompt
A prompt that supports the discovery flow but does not produce a governed artifact. Utility prompts do not require the four-file system (no spec, template, or validator). Examples: work-classification-prompt.md, assumption-stress-test-prompt.md.

---

### Four-File System
The AIEOS governance pattern in which each artifact type is defined by exactly four files:
- **Spec** — authoritative content rules and hard gates
- **Template** — structure only, no content rules
- **Prompt** — AI behavior for generation
- **Validator** — judgment procedure for quality gates

---

## Hypothesis Concepts

### Belief
The core assertion in a value hypothesis — what the team believes to be true about user behavior, market dynamics, or product impact.

---

### Falsification Criteria
The specific, observable conditions under which a hypothesis would be considered false. Hypotheses without falsification criteria cannot be tested and are not permitted.

---

### Evidence Criteria
The evidence that would be considered sufficient to confirm a hypothesis. Paired with falsification criteria to bound the hypothesis from both directions.

---

### Proceed / Pivot / Pause
The three possible recommendations from a validated Experiment Log:
- **Proceed** — Evidence supports moving to DPRD generation
- **Pivot** — Evidence invalidates upstream assumptions; re-entry required before proceeding
- **Pause** — A blocking uncertainty must be resolved by the team before any path is clear
