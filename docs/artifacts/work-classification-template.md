# Work Classification Record

A structured record of the routing decision for an incoming work request. Complete this before filling the Discovery Intake Form.

This record is **human-authored** (optionally AI-assisted via `work-classification-prompt.md`). It is validated against `work-classification-spec.md` before the Discovery Intake Form is started.

---

## Document Control

- Record ID: (e.g., WCR-2026-001)
- Date:
- Classified By:
- Work Request Summary: (1-2 sentences describing the incoming work in concrete terms — what is being requested and by whom)

---

## Classification Decision

| Field | Value |
|-------|-------|
| Primary Type | Feature / Enhancement / Bug / Compliance / Tech Debt / Incident Response / Research |
| Confidence | High / Medium / Low |
| Discovery Depth | Full / Targeted / None |
| Route To | Product Intelligence Kit / Engineering Execution Kit (direct) / Engineering Triage / Incident Management |
| Intake Form | Discovery Intake Form / Product Brief / None |

**Type Definitions:**

| Type | Discovery Depth |
|------|----------------|
| Feature | Full — new capability that does not exist today |
| Enhancement | Targeted — improvement to existing capability |
| Bug | None — existing capability not working as designed |
| Compliance | Full — regulatory, legal, or policy-mandated change |
| Tech Debt | None — internal quality improvement, no user-facing change |
| Incident Response | None — urgent fix for production issue |
| Research | None (yet) — investigation needed before classification is possible; re-classify after research |

---

## Justification

(Why this classification was chosen. Must explain the reasoning, not restate the type. Reference at least one specific characteristic of the work request. 2-4 sentences.)

---

## Artifact Requirements

| Artifact | Required | Rationale |
|----------|----------|-----------|
| Problem Framing Document | Yes / No | |
| Value Hypothesis | Yes / No | |
| Assumption Register | Yes / No | |
| Experiment Log | Yes / No | |
| Discovery PRD | Yes / No | |

All five artifacts are required for Full and Targeted discovery depth. All five are excluded for None depth.

---

## Risk Flags

(Risks of under-classification — e.g., "This may be a design flaw requiring discovery rather than a simple bug fix." State "None identified" if none apply. This section must not be left blank.)

---

## Completeness Checklist

Before validating and freezing this record, confirm:

- [ ] Record ID and date are present
- [ ] Work request is summarized concisely
- [ ] Primary type is exactly one value from the taxonomy
- [ ] Confidence, Discovery Depth, and Route To are all filled
- [ ] Justification goes beyond restating the classification
- [ ] Artifact requirements are consistent with Discovery Depth
- [ ] Risk flags are addressed (or explicitly noted as none)
- [ ] No solution proposals or requirements are present

---

## Freeze Declaration

This classification record is validated and frozen. The routing decision is final. If the classification changes, a new record must be created.

- Validated Against: `work-classification-spec.md`
- Validation Result: PASS
- Frozen By:
- Date:
