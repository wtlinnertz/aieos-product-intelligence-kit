# Cross-Kit Handoff Example — TaskFlow Notification Feature

This example demonstrates the complete handoff from the Product Intelligence Kit to the Engineering Execution Kit. It uses the TaskFlow Notification Feature scenario — the same initiative traced through all five PIK artifact examples.

---

## Scenario

**Initiative:** TaskFlow Intelligent Notification System
**Stage at handoff:** All five PIK artifacts are validated and frozen. The Discovery PRD is the terminal artifact and is ready for engineering.

**PIK artifacts (all frozen):**

| Step | Artifact | Example File |
|------|----------|-------------|
| 0b | Discovery Intake | `examples/01-discovery-intake.md` |
| 1 | Problem Framing Document | `examples/02-problem-framing.md` |
| 2 | Value Hypothesis | `examples/03-value-hypothesis.md` |
| 3 | Assumption Register | `examples/04-assumption-register.md` |
| 4 | Experiment Log | `examples/05-experiment-log.md` |
| 5 | Discovery PRD | `examples/06-discovery-prd.md` ← **handoff artifact** |

---

## What the Handoff Looks Like

### Step 1 — PIK ships the frozen DPRD

The PIK team delivers `DPRD-TASKFLOW-NOTIF-001` (frozen, validated, human-approved) to the EEK team. This is the file at `examples/06-discovery-prd.md` in this repository.

The DPRD has already passed the DPRD validator (8 hard gates). It carries full traceability back to upstream PIK artifacts in §7 (Upstream Artifact References) and §8 (Assumptions).

---

### Step 2 — EEK team places the DPRD

The EEK team places the frozen DPRD in the consuming project's repository:

```
<consuming-project>/
  docs/
    sdlc/
      01-prd.md    ← frozen DPRD placed here, no edits
```

The file is placed **as-is**. The EEK does not edit, reformat, or regenerate it. Extra DPRD sections (upstream artifact references, PIK traceability metadata) are not referenced by the EEK PRD spec and will not cause validator failures.

---

### Step 3 — EEK team runs the acceptance check

In a fresh AI session, the EEK team opens:
- `docs/specs/prd-spec.md` (from the Engineering Execution Kit)
- `docs/validators/prd-validator.md` (from the Engineering Execution Kit)
- `docs/sdlc/01-prd.md` (the placed DPRD)

The prd-validator evaluates the DPRD against the 6 EEK PRD hard gates. No generation occurs — this is a confirmation-only check.

**Why it passes:** The 6 EEK PRD gates (`problem_definition`, `goals`, `scope`, `requirements`, `constraints`, `readiness`) are a proper subset of the 8 DPRD gates. They are included verbatim as the "Engineering Execution Kit Gates" in `discovery-prd-spec.md`. A DPRD that passes all 8 DPRD gates necessarily passes all 6 EEK gates.

**Sample acceptance check output:** See `examples/cross-kit/01-prd-validation.json` in this directory.

---

### Step 4 — Save the acceptance check result

The EEK team saves the validator output:

```
<consuming-project>/
  docs/
    sdlc/
      01-prd.md
      01-prd-validation.json    ← acceptance check result saved here
```

---

### Step 5 — Freeze the PRD slot and begin engineering

If the acceptance check result is `"status": "PASS"`, the PRD slot is frozen. The EEK flow continues:

```
01-prd.md (frozen DPRD)
  → Architecture Context (intake form) → ACF → validate → freeze
  → PRD + ACF → SAD → validate → freeze
  → Design Context (intake form) → DCF → validate → freeze
  → SAD + DCF → TDD → validate → freeze
  → TDD → WDD → validate → DoR check → human approval → freeze
  → Execute per work item (Tests → Plan → Code → Review)
  → ORD → validate → production ready
```

If the acceptance check result is `"status": "FAIL"`, the EEK team does **not** begin ACF. They return the failing validator output to the PIK team for correction. The PIK team re-enters the DPRD through the PIK Re-Entry Protocol and re-delivers after re-validation.

---

## Acceptance Check Output (Annotated)

The file `01-prd-validation.json` in this directory shows the expected acceptance check output for `DPRD-TASKFLOW-NOTIF-001`.

Key points:
- `"status": "PASS"` — DPRD clears the EEK acceptance check
- All 6 EEK PRD hard gates pass
- `completeness_score` reflects EEK-relevant content only (extra DPRD traceability sections are not penalized)
- `warnings` may note the presence of PIK-specific sections — these are informational, not blocking

---

## If the DPRD Must Change After Engineering Begins

Once the EEK has started work on downstream artifacts (ACF, SAD, TDD, WDD), a DPRD change triggers the **Cross-Kit Re-Entry Protocol** — not the standard PIK Re-Entry Protocol.

**Trigger sections:** §2 Problem Statement, §3 Goals, §4 Non-Goals, §6 Requirements, §11 Acceptance Criteria

The protocol requires joint notification, EEK impact analysis on the proposed change, a joint decision to proceed, PIK re-entry and re-delivery, and EEK cascade re-validation.

Full protocol is documented in:
- PIK: `docs/playbook.md` → Downstream Handoff → Cross-Kit Re-Entry Protocol
- EEK: `docs/playbook.md` → Cross-Kit Re-Entry Protocol (Upstream PRD Change)

---

## EEK End-to-End Example

The Engineering Execution Kit includes a complete worked example for a different scenario (a generic internal reference data service). It demonstrates the full EEK artifact flow from PRD through ORD, including validator outputs at each step.

**Location:** `aieos-engineering-execution-kit/examples/end-to-end/example-01-generic-service/`

That example uses Path B entry (direct Product Brief → PRD generation). The TaskFlow handoff above uses Path A entry (frozen DPRD placed directly). The EEK artifact flow after the PRD slot is identical for both paths.

---

## Summary

| Step | Action | Actor | Output |
|------|--------|-------|--------|
| 1 | Ship frozen DPRD | PIK team | `DPRD-TASKFLOW-NOTIF-001` (this repository, `examples/06-discovery-prd.md`) |
| 2 | Place DPRD | EEK team | `docs/sdlc/01-prd.md` in consuming project |
| 3 | Run acceptance check | EEK team (AI session) | Validator output |
| 4 | Save result | EEK team | `docs/sdlc/01-prd-validation.json` |
| 5a | Freeze + continue | EEK team | ACF step begins |
| 5b | Return to PIK (if FAIL) | EEK team | Failing validator output → PIK corrects and re-delivers |
