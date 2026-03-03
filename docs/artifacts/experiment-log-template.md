# Experiment Log

## 1. Document Control

| Field | Value |
|-------|-------|
| Artifact ID | EL-{PROJECT}-{NNN} |
| Version | {version} |
| Date | {date} |
| Author | {author} |
| Status | Draft / Validated / Frozen |
| Upstream PFD | {PFD artifact ID} |
| Upstream VH | {VH artifact ID} |
| Upstream AR | {AR artifact ID} |

---

## 2. Upstream References

**Problem Framing Document:** {PFD artifact ID}

**Value Hypothesis:** {VH artifact ID}

**Assumption Register:** {AR artifact ID} — {N} assumptions targeted for validation

---

## 3. Experiment Inventory

### EXP-1: {Experiment Title}

| Field | Value |
|-------|-------|
| Target Assumption | {ASM-N from AR} |
| Hypothesis Tested | {What this experiment aimed to confirm or disprove} |
| Method | {How the experiment was conducted} |
| Sample / Scope | {Size, selection criteria, representativeness} |
| Conclusion | {Confirmed / Invalidated / Inconclusive / Partially Confirmed} |
| Confidence Level | {High / Medium / Low} |

**Raw Findings:**
{Factual observations — what was observed or measured, without interpretation}

**Limitations:**
{What could affect the reliability of this result}

{Repeat for each experiment}

---

## 4. Results Summary

| Conclusion | Count | Experiments |
|-----------|-------|-------------|
| Confirmed | {n} | {EXP-N, ...} |
| Invalidated | {n} | {EXP-N, ...} |
| Inconclusive | {n} | {EXP-N, ...} |
| Partially Confirmed | {n} | {EXP-N, ...} |

### High-Risk Assumption Coverage

| AR Assumption | Risk Level | Tested By | Result |
|--------------|-----------|-----------|--------|
| ASM-N | {High/Medium/Low} | {EXP-N or "Not tested"} | {conclusion or "Untested"} |

---

## 5. Assumption Status Update

| AR Assumption | Original Risk | Experiment | Updated Status | Notes |
|--------------|--------------|------------|---------------|-------|
| ASM-N | {High/Medium/Low} | {EXP-N or "Not tested"} | {Confirmed / Invalidated / Inconclusive / Untested / Partially Confirmed} | {brief note} |

---

## 6. Impact Assessment

### Invalidated Assumptions

**{ASM-N}: {assumption title}**
- **Impact on initiative:** {what this means for the initiative}
- **Affected hypotheses:** {VH HYP-N references}
- **Re-entry required:** {Yes / No — does this require re-entry on upstream artifacts?}

{Repeat for each invalidated assumption}

### Partially Confirmed Assumptions

**{ASM-N}: {assumption title}**
- **What was confirmed:** {the part that held}
- **What was not confirmed:** {the part that didn't hold}
- **Impact on initiative:** {what this means}
- **Affected hypotheses:** {VH HYP-N references}

{Repeat for each partially confirmed assumption}

### Confirmed Assumptions (De-Risk Notes)

{Brief notes on how confirmed assumptions reduce initiative risk, or "No assumptions confirmed"}

---

## 7. Recommendations

**Proceed / Pivot / Pause:** {recommendation}

**Rationale:** {evidence-based reasoning for the recommendation}

**Remaining validation needed:**
- {Any assumptions that still require validation before proceeding to the Discovery PRD}

---

## 8. Open Questions

**OQ-1: {Question}**
- **Category:** Blocking / Non-blocking
- **Raised by:** {EXP-N}
- **Owner / Resolution plan:** {who will resolve this, or how}

{Repeat for each open question, or state "No new questions raised"}

---

## 9. Freeze Declaration

| Field | Value |
|-------|-------|
| Frozen | Yes / No |
| Freeze Date | {date} |
| Approved By | {approver} |

{Freeze declaration statement}
