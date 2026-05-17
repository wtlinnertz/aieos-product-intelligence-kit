# Structural Integrity Tests

This document defines the structural verification checks for the Product Intelligence Kit. These checks confirm compliance with the AIEOS governance model.

---

## 1. Four-File Completeness

Every artifact type must have exactly four files: spec, template, prompt, validator.

| Artifact Type | Spec | Template | Prompt | Validator | Status |
|--------------|------|----------|--------|-----------|--------|
| Problem Framing Document | `specs/problem-framing-spec.md` | `artifacts/problem-framing-template.md` | `prompts/problem-framing-prompt.md` | `validators/problem-framing-validator.md` | PASS |
| Value Hypothesis | `specs/value-hypothesis-spec.md` | `artifacts/value-hypothesis-template.md` | `prompts/value-hypothesis-prompt.md` | `validators/value-hypothesis-validator.md` | PASS |
| Assumption Register | `specs/assumption-register-spec.md` | `artifacts/assumption-register-template.md` | `prompts/assumption-register-prompt.md` | `validators/assumption-register-validator.md` | PASS |
| Experiment Log | `specs/experiment-log-spec.md` | `artifacts/experiment-log-template.md` | `prompts/experiment-log-prompt.md` | `validators/experiment-log-validator.md` | PASS |
| Discovery PRD | `specs/discovery-prd-spec.md` | `artifacts/discovery-prd-template.md` | `prompts/discovery-prd-prompt.md` | `validators/discovery-prd-validator.md` | PASS |

---

## 2. Naming Convention Compliance

### File Naming (Governance Model §4)

| File | Expected Pattern | Actual Name | Status |
|------|-----------------|-------------|--------|
| PFD Spec | `{type}-spec.md` | `problem-framing-spec.md` | PASS |
| PFD Template | `{type}-template.md` | `problem-framing-template.md` | PASS |
| PFD Prompt | `{type}-prompt.md` | `problem-framing-prompt.md` | PASS |
| PFD Validator | `{type}-validator.md` | `problem-framing-validator.md` | PASS |
| VH Spec | `{type}-spec.md` | `value-hypothesis-spec.md` | PASS |
| VH Template | `{type}-template.md` | `value-hypothesis-template.md` | PASS |
| VH Prompt | `{type}-prompt.md` | `value-hypothesis-prompt.md` | PASS |
| VH Validator | `{type}-validator.md` | `value-hypothesis-validator.md` | PASS |
| AR Spec | `{type}-spec.md` | `assumption-register-spec.md` | PASS |
| AR Template | `{type}-template.md` | `assumption-register-template.md` | PASS |
| AR Prompt | `{type}-prompt.md` | `assumption-register-prompt.md` | PASS |
| AR Validator | `{type}-validator.md` | `assumption-register-validator.md` | PASS |
| EL Spec | `{type}-spec.md` | `experiment-log-spec.md` | PASS |
| EL Template | `{type}-template.md` | `experiment-log-template.md` | PASS |
| EL Prompt | `{type}-prompt.md` | `experiment-log-prompt.md` | PASS |
| EL Validator | `{type}-validator.md` | `experiment-log-validator.md` | PASS |
| DPRD Spec | `{type}-spec.md` | `discovery-prd-spec.md` | PASS |
| DPRD Template | `{type}-template.md` | `discovery-prd-template.md` | PASS |
| DPRD Prompt | `{type}-prompt.md` | `discovery-prd-prompt.md` | PASS |
| DPRD Validator | `{type}-validator.md` | `discovery-prd-validator.md` | PASS |
| Intake Form | `{context}-template.md` | `discovery-intake-template.md` | PASS |
| Intake Spec | `{type}-spec.md` | `discovery-intake-spec.md` | PASS |
| Intake Validator | `{type}-validator.md` | `discovery-intake-validator.md` | PASS |
| Stress Test Utility | `{function}-prompt.md` | `assumption-stress-test-prompt.md` | PASS |
| Classification Utility | `{function}-prompt.md` | `work-classification-prompt.md` | PASS |

### Kit Naming

| Check | Expected | Actual | Status |
|-------|----------|--------|--------|
| Repository name | `aieos-product-intelligence-kit` | `aieos-product-intelligence-kit` | PASS |

---

## 3. Directory Structure Compliance (Governance Model §3)

| Directory | Expected | Exists | Status |
|-----------|----------|--------|--------|
| `docs/` | Yes | Yes | PASS |
| `docs/principles/` | Yes | Yes | PASS |
| `docs/specs/` | Yes | Yes | PASS |
| `docs/artifacts/` | Yes | Yes | PASS |
| `docs/prompts/` | Yes | Yes | PASS |
| `docs/validators/` | Yes | Yes | PASS |
| `docs/playbook.md` | Yes | Yes | PASS |
| `docs/index.md` | Yes | Yes | PASS |
| `docs/how-to-adapt.md` | Yes | Yes | PASS |
| `docs/how-to-use-with-ai.md` | Yes | Yes | PASS |
| `examples/` | Yes | Yes | PASS |
| `examples/validator-outputs/` | Yes | Yes | PASS |
| `examples/cross-kit/` | Yes | Yes | PASS |
| `tests/` | Yes | Yes | PASS |
| `tests/scenario-tests.md` | Yes | Yes | PASS |
| `CLAUDE.md` | Yes | Yes | PASS |
| `README.md` | Yes | Yes | PASS |
| `CONTRIBUTING.md` | Yes | Yes | PASS |
| `ANONYMIZATION.md` | Yes | Yes | PASS |
| `TERMS.md` | Yes | Yes | PASS |

---

## 4. Cross-Reference Verification

### Permitted Cross-References (Governance Model §2)

| Reference | Expected | Verified | Status |
|-----------|----------|----------|--------|
| Prompts → Specs | Prompts reference specs for content rules | All 5 generation prompts reference their spec | PASS |
| Prompts → Templates | Prompts reference templates for structure | All 5 generation prompts reference their template | PASS |
| Validators → Specs | Validators reference specs for hard gates | All 5 validators reference their spec | PASS |

### Prohibited Cross-References

| Check | Expected | Verified | Status |
|-------|----------|----------|--------|
| Templates do not reference specs | No spec references in templates | Confirmed | PASS |
| Validators do not reference prompts | No prompt references in validators | Confirmed | PASS |
| Specs do not inline in prompts | Prompts reference specs, not copy rules | Confirmed | PASS |
| Specs do not inline in validators | Validators reference specs, not copy rules | Confirmed | PASS |

---

## 5. Downstream Contract Compliance

### Discovery PRD vs. Engineering Execution Kit PRD Spec

| Requirement | Covered in DPRD Spec | Status |
|------------|---------------------|--------|
| 12 required sections present | Yes — all 12 sections listed | PASS |
| "The system SHALL ..." language for FRs | Yes — format requirement specified | PASS |
| Unique identifiers (FR-N, NFR-N) | Yes — format requirement specified | PASS |
| 6 hard gates (problem_definition, goals, scope, requirements, constraints, readiness) | Yes — all 6 included as "Engineering Execution Kit Gates" | PASS |
| Problem must answer what, who, why | Yes — content rule specified | PASS |
| At least 1 FR and 1 NFR | Yes — completeness rule specified | PASS |
| Non-goals must be present | Yes — completeness rule specified | PASS |
| No solution design or architecture | Yes — relationship rule specified | PASS |
| No implementation details | Yes — relationship rule specified | PASS |
| Internal consistency required | Yes — readiness gate covers this | PASS |

---

## 6. Upstream Boundary Contract

The Discovery Intake Form has a spec and validator that serve as the upstream boundary contract. This is not a full four-file governed artifact (no AI generation prompt), but a validated input contract per governance model §10.

| Check | Expected | Verified | Status |
|-------|----------|----------|--------|
| Intake spec exists | `discovery-intake-spec.md` in `docs/specs/` | Yes | PASS |
| Intake validator exists | `discovery-intake-validator.md` in `docs/validators/` | Yes | PASS |
| Spec defines 6 hard gates | problem_defined, users_identified, urgency_stated, evidence_present, scope_bounded, no_solutions | Yes — all 6 present | PASS |
| Validator references spec | Validator evaluates against intake spec | Yes | PASS |
| Hard gates map to template checklist | Spec gates correspond to template's 6 completeness checklist items | Yes | PASS |
| Playbook requires intake validation | Step 0b includes validation before PFD generation | Yes | PASS |

---

## 7. Utility Prompt Compliance

Utility prompts are not governed artifacts — they do not require the four-file system. They must follow the `{function}-prompt.md` naming convention.

| Utility Prompt | Naming Compliant | Purpose | Status |
|---------------|-----------------|---------|--------|
| `assumption-stress-test-prompt.md` | Yes | Adversarial analysis of assumptions | PASS |
| `work-classification-prompt.md` | Yes | Classify and route incoming work | PASS |
| `brownfield-analysis-prompt.md` | Yes | Analyze existing systems for intake pre-fill | PASS |
| `stakeholder-alignment-prompt.md` | Yes | Surface and classify stakeholder conflicts | PASS |
| `cross-initiative-conflict-prompt.md` | Yes | Detect assumption conflicts across initiatives | PASS |
| `initiative-prioritization-prompt.md` | Yes | Compare and rank competing initiatives | PASS |

---

## 8. Worked Example Completeness

| Example | File | Covers | Status |
|---------|------|--------|--------|
| Discovery Intake | `examples/01-discovery-intake.md` | Completed intake form | PASS |
| Problem Framing | `examples/02-problem-framing.md` | Full PFD with all sections, frozen | PASS |
| Value Hypothesis | `examples/03-value-hypothesis.md` | Full VH with all sections, frozen | PASS |
| Assumption Register | `examples/04-assumption-register.md` | Full AR with all sections, frozen | PASS |
| Experiment Log | `examples/05-experiment-log.md` | Full EL with all sections, frozen | PASS |
| Discovery PRD | `examples/06-discovery-prd.md` | Full DPRD with all 12 sections, frozen, EL references | PASS |
| Cross-Kit Handoff | `examples/cross-kit/README.md` | Step-by-step handoff from DPRD to EEK, acceptance check output | PASS |
| Acceptance Check Output | `examples/cross-kit/01-prd-validation.json` | Sample PRD validator output for DPRD-TASKFLOW-NOTIF-001 | PASS |
| Validator Output Examples | `examples/validator-outputs/` | PASS and FAIL examples for all 6 artifact types (12 JSON files + README) | PASS |

---

---

## 9. Cross-Kit Handoff Tests

These checks verify the interface between the Product Intelligence Kit and the Engineering Execution Kit (aieos-engineering-execution). They must pass for the inter-kit handoff to be trustworthy.

### 9.1 Downstream Handoff Mechanics Documented

| Check | Expected | Verified | Status |
|-------|----------|----------|--------|
| Playbook documents DPRD file placement | `docs/playbook.md` Downstream Handoff section specifies DPRD is placed as `01-prd.md` in consuming project's `docs/sdlc/` | Yes | PASS |
| Playbook documents acceptance validation procedure | Playbook specifies EEK team runs `prd-validator.md` against the placed DPRD as acceptance check | Yes | PASS |
| Playbook documents cross-kit re-entry trigger | Playbook specifies that changes to §2, §3, §4, §6, or §11 of DPRD post-handoff require notification to EEK team before re-validation | Yes | PASS |
| Playbook documents cross-kit re-entry protocol | Playbook specifies EEK runs impact analysis before DPRD re-entry begins | Yes | PASS |

### 9.2 Hard Gate Alignment with EEK PRD Spec

| Gate Name | Present in DPRD Spec (EEK Gates) | Present in EEK prd-spec.md | Match |
|-----------|-----------------------------------|----------------------------|-------|
| `problem_definition` | Yes | Yes | PASS |
| `goals` | Yes | Yes | PASS |
| `scope` | Yes | Yes | PASS |
| `requirements` | Yes | Yes | PASS |
| `constraints` | Yes | Yes | PASS |
| `readiness` | Yes | Yes | PASS |
| `upstream_traceability` | Yes (PIK gate only) | No (not required by EEK) | PASS — PIK-only gate, not a mismatch |
| `no_scope_expansion` | Yes (PIK gate only) | No (not required by EEK) | PASS — PIK-only gate, not a mismatch |

**Conclusion:** A DPRD that passes all 8 DPRD gates will necessarily pass all 6 EEK PRD gates. The 2 additional PIK gates are stricter requirements — not contradictions.

### 9.3 EEK Dual Entry Path Documentation

| Check | Expected | Verified | Status |
|-------|----------|----------|--------|
| EEK prd-spec.md lists DPRD as valid upstream input | `prd-spec.md` Upstream Dependencies section explicitly lists Path A (DPRD) and Path B (Product Brief) | Yes | PASS |
| EEK prd-prompt.md handles DPRD input | `prd-prompt.md` contains conditional: if DPRD, do not regenerate; if Product Brief, generate | Yes | PASS |
| EEK playbook documents Path A (Discovery entry) | EEK `playbook.md` Canonical Artifact Flow shows DPRD → validate → freeze path | Yes | PASS |
| EEK playbook documents cross-kit re-entry protocol | EEK `playbook.md` documents what happens when upstream DPRD changes post-handoff | Yes | PASS |

### 9.4 Kickoff Document Placement

| Check | Expected | Verified | Status |
|-------|----------|----------|--------|
| Kickoff document exists in PIK | `docs/meta/kit-kickoff-prompt.md` exists in this repo | Yes | PASS |
| Kickoff document is NOT in EEK | `aieos-engineering-execution/docs/product-intelligence-kit-kickoff.md` does not exist | Yes | PASS |

### 9.5 Governance Model Sync

| Check | Expected | Verified | Status |
|-------|----------|----------|--------|
| Governance model sync rule in PIK CLAUDE.md | `CLAUDE.md` contains governance model sync requirement | Yes | PASS |
| Governance model sync rule in EEK CLAUDE.md | `aieos-engineering-execution/CLAUDE.md` contains governance model sync requirement | Yes | PASS |
| Governance model files are structurally equivalent | Both `governance-model.md` files define the same 15 sections with same content | Yes | PASS |

### 9.6 Cross-Kit Example Completeness

| Check | Expected | Verified | Status |
|-------|----------|----------|--------|
| Cross-kit example README exists | `examples/cross-kit/README.md` exists and covers the full handoff sequence | Yes | PASS |
| Acceptance check output example exists | `examples/cross-kit/01-prd-validation.json` exists with correct JSON schema | Yes | PASS |
| Example uses same scenario as PIK examples | README references `examples/06-discovery-prd.md` (DPRD-TASKFLOW-NOTIF-001) as handoff artifact | Yes | PASS |
| Example covers PASS and FAIL branches | README documents both paths: PASS → freeze + continue; FAIL → return to PIK | Yes | PASS |
| Example documents 01-prd-validation.json placement | README specifies file is saved in consuming project's `docs/sdlc/` | Yes | PASS |
| Example references EEK end-to-end example | README points readers to `aieos-engineering-execution/examples/end-to-end/example-01-generic-service/` | Yes | PASS |

---

## Summary

| Category | Checks | Passed | Failed |
|----------|--------|--------|--------|
| Four-File Completeness | 5 | 5 | 0 |
| Naming Conventions | 26 | 26 | 0 |
| Directory Structure | 20 | 20 | 0 |
| Cross-References | 7 | 7 | 0 |
| Downstream Contract | 10 | 10 | 0 |
| Upstream Boundary Contract | 6 | 6 | 0 |
| Utility Prompts | 6 | 6 | 0 |
| Worked Example | 9 | 9 | 0 |
| Cross-Kit Handoff | 22 | 22 | 0 |
| **Total** | **115** | **115** | **0** |
