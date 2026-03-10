# Assumption Register

## 1. Document Control

| Field | Value |
|-------|-------|
| Artifact ID | AR-{PROJECT}-{NNN} |
| Version | {version} |
| Date | {date} |
| Author | {author} |
| Status | Draft / Validated / Freeze Pending / Frozen |
| Upstream PFD | {PFD artifact ID} |
| Upstream VH | {VH artifact ID} |
| Governance Model Version | 1.0 |
| Prompt Version | {prompt version} |
| Spec Version | {spec version} |
| Principles Version | {principles file versions} |

---

## 2. Upstream References

**Problem Framing Document:** {PFD artifact ID} — {brief problem statement reference}

**Value Hypothesis:** {VH artifact ID} — {brief hypothesis summary reference}

---

## 3. Assumption Inventory

### ASM-1: {Assumption Title}

| Field | Value |
|-------|-------|
| Statement | {What is being assumed to be true} |
| Source | {PFD or VH reference — e.g., "PFD §4 PP-2" or "VH HYP-1"} |
| Category | {User Behavior / Market / Technical / Organizational / Regulatory / Data} |
| Risk Level | {High / Medium / Low} |
| Impact if False | {What happens to the initiative if this assumption is wrong} |
| Current Evidence | {What evidence supports this assumption, or "None"} |
| Validation Method | {How this assumption will be tested or verified} |

{Repeat for each assumption}

---

## 4. Risk Assessment Summary

| Risk Level | Count | Assumptions |
|-----------|-------|-------------|
| High | {n} | {ASM-N, ASM-N, ...} |
| Medium | {n} | {ASM-N, ASM-N, ...} |
| Low | {n} | {ASM-N, ASM-N, ...} |

**Highest-risk assumptions:** {list the most critical assumptions}

**Unvalidated high-risk assumptions:** {list any high-risk assumptions with no current evidence, or "None"}

---

## 5. Validation Plan

| Assumption | Method | Expected Timeline | Owner |
|-----------|--------|-------------------|-------|
| ASM-N | {concrete validation approach} | {when} | {who, or "TBD"} |

{Must include entries for all high-risk assumptions. Medium-risk assumptions recommended.}

---

## 6. Dependency Map

### Inter-Assumption Dependencies

{Describe dependencies between assumptions, or state "No inter-assumption dependencies identified"}

### Cascade Analysis

{Which assumptions, if invalidated, would cascade to invalidate other assumptions?}

---

## 7. Open Questions

**OQ-1: {Question}**
- **Category:** Blocking / Non-blocking
- **Related assumption:** ASM-N
- **Owner / Resolution plan:** {who will resolve this, or how}

{Repeat for each open question, or state "All questions resolved"}

---

## 8. Freeze Declaration

| Field | Value |
|-------|-------|
| Frozen | Yes / No |
| Freeze Date | {date} |
| Approved By | {approver} |

{Freeze declaration statement}
