# Product Intelligence Kit — Scenario Tests

This document defines executable test scenarios for the Product Intelligence Kit. Each scenario specifies a path through the kit, the inputs required, expected behavior at each step, and key verifications.

Structural integrity checks are in `tests/structural-integrity.md`. This document covers **flow scenarios** — how the kit behaves end-to-end under different conditions.

---

## Coverage Matrix

| Dimension | S-01 | S-02 | S-03 | S-04 | S-05 | S-06 | S-07 | S-08 | S-09 |
|-----------|------|------|------|------|------|------|------|------|------|
| Happy path (full discovery → DPRD) | x | | | | | | | | |
| Failed validation → fix cycle | | x | | | | | | x | |
| Re-entry (upstream artifact change) | | | x | x | | | | | |
| Experiment-driven pivot | | | | | x | | | | x |
| Cross-kit handoff (Path A) | | | | | | x | | | |
| Work classification routing | | | | | | | x | | |
| Greenfield intake | x | x | | | | x | x | x | x |
| Brownfield intake | | | | | | | | | |
| Multi-stakeholder input | | | | | | | | | |
| Compliance initiative | | | | | | | | | |
| Validator behavioral test (gate-level) | | | | | | | | x | |
| Discovery iteration pattern (Pattern 1) | | | | | | | | | x |

---

## Scenarios

---

### S-01: Happy Path — Full Discovery to Handoff

**What:** Complete end-to-end flow with no failures, no re-entry, and a proceed recommendation from the Experiment Log. This is the baseline path — validate it first.

**Preconditions:** No existing artifacts for this initiative.

**Flow:**

| Step | Action | Inputs | Expected Output | Key Verifications |
|------|--------|--------|-----------------|-------------------|
| 0a | (Optional) Run work classification | `work-classification-prompt.md` + work request | Classification: Feature or Enhancement | Routed to full discovery; not bypassed |
| 0b | Human fills Discovery Intake Form | `discovery-intake-template.md` | Completed intake form | All 6 required sections present |
| 0b | Validate intake form | `discovery-intake-spec.md` + `discovery-intake-validator.md` + intake form | JSON: `"status": "PASS"` | All 6 hard gates pass; proceed to PFD |
| 1 | Generate PFD | `problem-framing-prompt.md` + `problem-framing-spec.md` + `problem-framing-template.md` + validated intake | PFD draft | Output follows template exactly; no solution proposals |
| 1 | Validate PFD | `problem-framing-spec.md` + `problem-framing-validator.md` + PFD draft | JSON: `"status": "PASS"` | All 6 hard gates pass |
| 1 | Freeze PFD | Human review + approval | Frozen PFD with Artifact ID (PFD-{PROJECT}-{NNN}) | Human has approved; status marked Frozen |
| 2 | Generate VH | `value-hypothesis-prompt.md` + `value-hypothesis-spec.md` + `value-hypothesis-template.md` + frozen PFD | VH draft | All user groups trace to PFD UG-N identifiers; no solutions |
| 2 | Validate VH | `value-hypothesis-spec.md` + `value-hypothesis-validator.md` + VH draft | JSON: `"status": "PASS"` | All 6 hard gates pass; falsification criteria present for all hypotheses |
| 2 | Freeze VH | Human review + approval | Frozen VH | Human has approved |
| 3 | Generate AR | `assumption-register-prompt.md` + `assumption-register-spec.md` + `assumption-register-template.md` + frozen PFD + frozen VH | AR draft | All assumptions trace to PFD or VH; high-risk assumptions have validation plans |
| 3 | Validate AR | `assumption-register-spec.md` + `assumption-register-validator.md` + AR draft | JSON: `"status": "PASS"` | All 6 hard gates pass |
| 3 | Freeze AR | Human review + approval | Frozen AR | Human has approved |
| 3 | (Optional) Run assumption stress test | `assumption-stress-test-prompt.md` + frozen AR | Stress test analysis | Not a governed artifact; used to inform experiment design |
| 4 | Team conducts experiments | Human work: interviews, surveys, analysis | Experiment results data | Real-world data gathered; cannot be AI-simulated |
| 4 | Generate EL | `experiment-log-prompt.md` + `experiment-log-spec.md` + `experiment-log-template.md` + frozen PFD + VH + AR + experiment data | EL draft | All experiments trace to AR assumptions; conclusions match findings |
| 4 | Validate EL | `experiment-log-spec.md` + `experiment-log-validator.md` + EL draft | JSON: `"status": "PASS"` | All 6 hard gates pass; recommendation is `proceed` |
| 4 | Freeze EL | Human review + approval | Frozen EL with `proceed` recommendation | Human has reviewed recommendation and approved |
| 5 | Generate DPRD | `discovery-prd-prompt.md` + `discovery-prd-spec.md` + `discovery-prd-template.md` + all 4 frozen upstream artifacts | DPRD draft | All 12 sections present; FRs use SHALL language; upstream artifacts referenced in §7 |
| 5 | Validate DPRD | `discovery-prd-spec.md` + `discovery-prd-validator.md` + DPRD draft | JSON: `"status": "PASS"` | All 8 hard gates pass (6 EEK gates + 2 PIK traceability gates) |
| 5 | Freeze DPRD | Human review + approval | Frozen DPRD with Artifact ID | Human has approved; ready for handoff |
| 6 | Hand off to EEK | Place frozen DPRD as `docs/sdlc/01-prd.md` in consuming project | DPRD placed; EEK runs acceptance check | No regeneration; see `examples/cross-kit/README.md` |

**Key verifications:**
- Each step uses a **separate AI session** for generation and validation
- No artifact is generated before its upstream is frozen
- Validation is PASS before freeze at each step
- Human approval occurs at each freeze point
- No solution proposals appear in PFD, VH, or AR

---

### S-02: Validation Failure → Fix Cycle

**What:** Validation fails at one step. The team corrects the blocking issues and re-validates in a new session. Verifies that the fix cycle works as documented.

**Preconditions:** All steps up to the failed step have been completed successfully. This scenario can be applied at any step — PFD is used as the example.

**Flow:**

| Step | Action | Inputs | Expected Output | Key Verifications |
|------|--------|--------|-----------------|-------------------|
| 1 | Generate PFD | As in S-01 | PFD draft | Draft produced |
| 1 | Validate PFD (first attempt) | Spec + validator + PFD draft | JSON: `"status": "FAIL"` | Blocking issues listed with gate names and locations |
| 1 | Review blocking issues | Validator output | Human identifies required corrections | Corrections are limited to what is missing — do not rewrite the whole document |
| 1 | Regenerate PFD | **New AI session** with spec + prompt + template + upstream artifacts + validator output | Corrected PFD draft | Validator feedback explicitly passed to new session |
| 1 | Validate PFD (second attempt) | **Separate AI session** with spec + validator + corrected PFD | JSON: `"status": "PASS"` | All previously failing gates now pass |
| 1 | Freeze PFD | Human review + approval | Frozen PFD | Human confirms corrections are complete |

**Key verifications:**
- Regeneration uses a **new AI session** — not a continuation of the generation session
- Validation uses a **separate AI session** from regeneration
- The fix targets the specific blocking issues — do not regenerate from scratch unless all content is invalid
- FAIL validator output contains actionable `blocking_issues` with gate names and locations
- Second validation confirms all gates pass before freeze

---

### S-03: Re-Entry — PFD Change After VH Is Frozen

**What:** A frozen PFD must change (e.g., a significant new user group is discovered after the PFD was frozen). Verifies that the re-entry cascade works correctly.

**Preconditions:** PFD, VH are both frozen. AR generation has not yet begun.

**Flow:**

| Step | Action | Inputs | Expected Output | Key Verifications |
|------|--------|--------|-----------------|-------------------|
| — | Impact analysis | Proposed PFD change description | List of downstream artifacts affected: VH (user traceability will break) | Impact confirmed before any modification begins |
| 1 | Modify PFD | PFD + proposed change | Updated PFD draft | Change is minimal and specific — not a full rewrite |
| 1 | Re-validate PFD | Spec + validator + updated PFD | JSON: `"status": "PASS"` | All 6 hard gates pass with new content |
| 1 | Re-freeze PFD | Human review + approval | Updated frozen PFD | Human confirms change is correct |
| 2 | Regenerate VH | New AI session: prompt + spec + template + **updated frozen PFD** | Updated VH draft | VH re-grounded in updated PFD; user groups may change |
| 2 | Re-validate VH | Spec + validator + updated VH | JSON: `"status": "PASS"` | All 6 hard gates pass; user traceability verified against updated PFD |
| 2 | Re-freeze VH | Human review + approval | Updated frozen VH | Human confirms cascade is complete |

**Key verifications:**
- Impact analysis occurs before any modification
- Cascade re-validation runs top-down (PFD → VH), not in parallel
- All downstream frozen artifacts are re-validated, not just the one that changed
- Human approval required at each freeze point in the cascade
- If AR, EL, or DPRD were also frozen, they must be re-validated (or regenerated if they fail) before the initiative can continue

---

### S-04: Re-Entry — EL Reveals Invalidated Assumption, Upstream AR Change Required

**What:** Experiment results invalidate a core assumption in the AR. The team must re-enter the AR (and cascade through EL → DPRD). Verifies that experiment-driven re-entry works correctly.

**Preconditions:** PFD, VH, AR all frozen. Experiments have been conducted. EL generation has revealed that a high-risk assumption is definitively false.

**Flow:**

| Step | Action | Inputs | Expected Output | Key Verifications |
|------|--------|--------|-----------------|-------------------|
| 4 | Generate EL (first attempt) | All frozen upstream artifacts + experiment data | EL draft with `pivot` recommendation | Validator will PASS but recommendation is pivot, not proceed |
| 4 | Validate EL | Spec + validator + EL | JSON: `"status": "PASS"` with pivot recommendation documented | Validator passes (EL is correct); pivot decision is human responsibility |
| — | Human decision | EL + recommendation | Decision: pivot; identify which upstream artifact to re-enter | Human determines which assumption changed and which artifact owns it |
| 3 | Re-enter AR | Modify AR to reflect updated assumption status | Updated AR draft | Invalidated assumption is updated with evidence; risk re-assessed |
| 3 | Re-validate AR | Spec + validator + updated AR | JSON: `"status": "PASS"` | All 6 hard gates pass |
| 3 | Re-freeze AR | Human approval | Updated frozen AR | Human confirms |
| 4 | Regenerate EL | New AI session with all updated frozen artifacts + experiment data | New EL draft | EL references updated AR assumptions; conclusions consistent |
| 4 | Re-validate EL | Spec + validator + new EL | JSON: `"status": "PASS"` with `proceed` or updated recommendation | Human reviews new recommendation |
| 4 | Re-freeze EL | Human approval | Updated frozen EL | Proceed to DPRD only if recommendation supports it |

**Key verifications:**
- A PASS EL with a pivot recommendation does NOT automatically block generation — it triggers a human decision
- Re-entry starts at the affected upstream artifact (AR), not at the EL
- EL is regenerated from the same experiment data with updated upstream artifacts — new experiments are NOT required unless the re-entered AR introduces new untested assumptions
- Cascade runs AR → EL → (optionally DPRD) in order

---

### S-05: Experiment Log Pause — Blocking Uncertainty

**What:** Experiment results are inconclusive and the EL recommends pause. A blocking uncertainty cannot be resolved without additional information that is not yet available. Verifies that the pause path is documented and followed correctly.

**Preconditions:** PFD, VH, AR all frozen. Experiments have been conducted but results are inconclusive.

**Flow:**

| Step | Action | Inputs | Expected Output | Key Verifications |
|------|--------|--------|-----------------|-------------------|
| 4 | Generate EL | All frozen upstream artifacts + experiment data | EL draft with `pause` recommendation | Validator will PASS; recommendation is pause |
| 4 | Validate EL | Spec + validator + EL | JSON: `"status": "PASS"` | PASS — the EL correctly documents the inconclusive state |
| 4 | Freeze EL | Human review + approval | Frozen EL with pause recommendation | Human acknowledges the pause; initiative is halted |
| — | Team resolves blocking uncertainty | Human work (new research, escalation, timeline) | Resolution or decision to abandon | No AI step; human responsibility |
| — | IF resolved: re-enter EL | New experiments → regenerate EL with updated data | Updated EL with proceed or pivot recommendation | New experiments are required; cannot re-generate from same data if question was about new information |
| — | IF abandoned: close initiative | Human decision | Initiative closed; no DPRD generated | Documented in team records |

**Key verifications:**
- A PASS EL with a pause recommendation does NOT mean the artifact is ready for DPRD generation
- The kit does not prescribe how to resolve a blocking uncertainty — that is human and organizational work
- If new experiments are conducted, the EL is regenerated from the combined original + new experiment data
- Abandoning an initiative is a valid outcome — the kit does not force a proceed

---

### S-06: Cross-Kit Handoff — Path A (DPRD → EEK)

**What:** Validates the complete handoff from PIK to the Engineering Execution Kit. Verifies that the DPRD is accepted as-is by the EEK without regeneration.

**Preconditions:** DPRD is frozen and validated (all 8 DPRD hard gates passed). Engineering Execution Kit is available in a consuming project.

**Flow:**

| Step | Action | Inputs | Expected Output | Key Verifications |
|------|--------|--------|-----------------|-------------------|
| — | Ship frozen DPRD | Frozen DPRD | DPRD delivered to EEK team | No edits made to DPRD before delivery |
| — | Place DPRD | Frozen DPRD | `docs/sdlc/01-prd.md` in consuming project | File placed exactly as-is; no reformatting |
| — | Run PRD acceptance check | EEK `prd-spec.md` + EEK `prd-validator.md` + `01-prd.md` | JSON: `"status": "PASS"` | All 6 EEK PRD hard gates pass; extra PIK traceability sections do not cause failures |
| — | Save acceptance check result | Acceptance check output | `docs/sdlc/01-prd-validation.json` in consuming project | Result saved; PASS confirmed |
| — | Freeze PRD slot | — | PRD slot frozen in EEK | EEK begins ACF step |

**Key verifications:**
- DPRD is **not** regenerated through `prd-prompt.md` — it is placed directly
- EEK `prd-validator.md` evaluates only the 6 EEK PRD gates — PIK-only gates (upstream_traceability, no_scope_expansion) are not evaluated and do not cause failures
- The acceptance check output is saved as `01-prd-validation.json`
- If acceptance check FAILS: the DPRD is returned to PIK for correction; EEK does NOT begin ACF
- See `examples/cross-kit/README.md` and `examples/cross-kit/01-prd-validation.json` for reference

---

### S-07: Work Classification Routing

**What:** Verifies that the work classification utility correctly routes non-discovery work away from the kit. The kit should not be applied to bugs, tech debt, or incident response.

**Preconditions:** Incoming work request of ambiguous type.

**Flow:**

| Step | Action | Inputs | Expected Output | Key Verifications |
|------|--------|--------|-----------------|-------------------|
| 0a | Run work classification | `work-classification-prompt.md` + work request | Classification output | Output includes: work type, recommended discovery depth, routing decision |
| — | IF classified as Feature/Enhancement with full discovery | Classification output | Route to intake form (begin S-01) | Discovery is appropriate |
| — | IF classified as Feature/Enhancement with targeted discovery | Classification output | Route to intake form with narrower scope | Targeted discovery only; not all 5 artifacts required |
| — | IF classified as Bug | Classification output | Route to engineering triage; bypass this kit | Kit does not apply to bugs |
| — | IF classified as Tech Debt | Classification output | Route to engineering triage; bypass this kit | Kit does not apply to tech debt |
| — | IF classified as Incident Response | Classification output | Route to incident management; bypass this kit | Kit does not apply to incidents |

**Key verifications:**
- Work classification is a routing decision, not a governed artifact — no freeze, no validation
- Classification output does not gate downstream steps (it is advisory)
- Bugs and tech debt bypass the entire kit — do not apply discovery to execution work
- Ambiguous cases should default to targeted discovery rather than full or none

---

### S-08: DPRD Validator — Upstream Traceability Gate Behavior

**What:** Tests gate 7 (`upstream_traceability`) of the DPRD validator by running it against two DPRD variants — one with EL experiment references present in the Assumptions section (PASS) and one with assumptions documented but no EXP-N references (FAIL). Exercises the spec-validator pair at the gate level.

**Preconditions:** Complete frozen discovery chain (PFD, VH, AR, EL). EL contains at least two experiment records with EXP-N identifiers. DPRD spec and validator available.

**Flow:**

| Step | Action | Inputs | Expected Output | Key Verifications |
|------|--------|--------|-----------------|-------------------|
| 1 | Generate DPRD — with EL traceability | `discovery-prd-prompt.md` + spec + template + all 4 frozen upstream artifacts | DPRD draft; Assumptions section references EXP-1, EXP-2... from EL | EXP-N identifiers from EL appear in DPRD Assumptions section |
| 2 | Validate DPRD (PASS variant) | **Separate AI session:** `discovery-prd-spec.md` + `discovery-prd-validator.md` + DPRD | JSON: `"status": "PASS"`, `upstream_traceability: "PASS"` | All 8 hard gates pass; gate 7 passes because EXP-N references are present |
| 3 | Produce DPRD variant — no EL references | Same DPRD content; Assumptions section revised to remove EXP-N identifiers (assumptions listed as statements only) | DPRD variant with no EXP-N references | Content is structurally complete except for missing traceability |
| 4 | Validate DPRD (FAIL variant) | **Separate AI session:** `discovery-prd-spec.md` + `discovery-prd-validator.md` + variant DPRD | JSON: `"status": "FAIL"`, `upstream_traceability: "FAIL"` | Gate 7 fails; `blocking_issues` references upstream_traceability with location pointing to Assumptions section |

**Key verifications:**
- Gate 7 is independently evaluable — it fails even when all other 7 gates would pass
- The validator evaluates only what is explicitly present — it does not infer EXP-N traceability from other sections
- A gate 7 failure is a blocking issue — DPRD cannot be frozen until EL is updated with EXP-N identifiers and DPRD is regenerated
- Generation (steps 1, 3) and validation (steps 2, 4) use separate AI sessions

---

### S-09: Discovery Iteration Pattern 1 — Problem Reframe

**What:** EL results reveal the core problem framing in the PFD is incorrect. Pattern 1 (Problem Reframe) is triggered: a Pivot Decision Record is filed and approved, the PFD is revised and re-validated, and the VH is checked for cascade consistency. Verifies the iteration model is distinct from re-entry and produces a coherent bounded revision.

**Preconditions:** PFD, VH, AR all frozen. Experiments conducted. EXP-3 result shows the assumed pain point exists in only 8% of users, not the broad audience defined in the PFD. This changes the problem scope, not just a hypothesis.

**Flow:**

| Step | Action | Inputs | Expected Output | Key Verifications |
|------|--------|--------|-----------------|-------------------|
| 4 | Generate EL | All frozen upstream artifacts + experiment data including EXP-3 | EL draft with `pivot` recommendation; EXP-3 finding documented | Recommendation is `pivot`; EXP-3 is traceable to an AR assumption |
| 4 | Validate EL | `experiment-log-spec.md` + `experiment-log-validator.md` + EL | JSON: `"status": "PASS"` with `pivot` recommendation | PASS — EL correctly documents the finding; pivot is the learning outcome |
| 4 | Freeze EL | Human review + approval | Frozen EL with `pivot` recommendation | Human acknowledges finding; iteration decision pending |
| — | File Pivot Decision Record | `pivot-decision-template.md` | EXP-3 finding + impacted artifact (PFD) + pattern (Pattern 1 — Problem Reframe) | Completed pivot-decision-{date}.md with Document Control, Evidence, Downstream Impact Assessment, and Human Approval all filled |
| — | Human approves Pivot Decision Record | Pivot Decision Record | Signed record | Revision authorized | Artifact revision may not begin before approval |
| 1 | Revise PFD | Frozen PFD + approved Pivot Decision Record | Revised PFD with narrowed user scope | User groups updated to reflect actual affected segment; change bounded to what the Pivot Decision Record specified |
| 1 | Re-validate PFD | `problem-framing-spec.md` + `problem-framing-validator.md` + revised PFD | JSON: `"status": "PASS"` | All 6 PFD hard gates pass |
| 1 | Re-freeze PFD | Human review + approval | Updated frozen PFD | Human confirms revision is bounded and correct |
| 2 | Assess VH cascade consistency | Revised PFD + frozen VH | Consistency check | All VH user group references (UG-N) must trace to revised PFD | If any VH user group references a UG-N no longer in PFD, VH must be revised |
| 2 | [If VH needs revision] Re-validate and re-freeze VH | Spec + validator + revised VH | JSON: `"status": "PASS"` | All 6 VH hard gates pass |
| — | Check AR and EL consistency | Revised PFD + re-checked VH + frozen AR + frozen EL | Consistency confirmed | AR assumptions must still be valid under revised problem scope; existing EL findings still apply |

**Key verifications:**
- Pattern 1 REQUIRES a Pivot Decision Record — no artifact revision begins without it
- Human approval of the Pivot Decision Record is a hard stop before revision
- The frozen EL (with `pivot` recommendation) is the evidence base — no new experiments are required
- Cascade is bounded: PFD → VH check → AR/EL consistency check; not a full re-run of the artifact chain
- **Distinction from Re-Entry (S-03, S-04):** Iteration is triggered by experimental learning (expected outcome of discovery); re-entry is triggered by external events. Iteration is bounded by what the experiment revealed.
- **Distinction from S-05 (Pause):** Pattern 1 triggers when learning is conclusive enough to justify revision; pause triggers when uncertainty cannot be resolved with available experiments.

---

## Execution Checklist

Before each run, confirm:

- [ ] Each generation step uses a **separate AI session** from validation
- [ ] Only one artifact is generated per session
- [ ] Full frozen upstream artifacts are included — not summaries or excerpts
- [ ] Human approval is obtained at each freeze point
- [ ] Validator outputs are saved (or referenced) alongside the artifact

---

## Known Gaps

The following dimensions are documented as out of scope for current scenario tests but should be added in future iterations:

| Dimension | Notes |
|-----------|-------|
| Brownfield intake (with brownfield analysis prompt) | Brownfield analysis utility exists but no scenario test covers it |
| Multi-stakeholder input with alignment prompt | Stakeholder alignment utility exists but no scenario test covers it |
| Compliance initiative (compliance-discovery-principles.md) | Compliance principles file exists; no scenario validates its integration |
| Cross-initiative conflict detection | Utility exists; no scenario covers parallel initiatives |
| Initiative prioritization | Utility exists; no scenario covers multi-DPRD portfolio decisions |
