# Experiment Log — Worked Example

## 1. Document Control

| Field | Value |
|-------|-------|
| Artifact ID | EL-TASKFLOW-NOTIF-001 |
| Version | 1.0 |
| Date | 2026-02-14 |
| Author | AI-generated, human-reviewed |
| Status | Frozen |
| Upstream PFD | PFD-TASKFLOW-NOTIF-001 |
| Upstream VH | VH-TASKFLOW-NOTIF-001 |
| Upstream AR | AR-TASKFLOW-NOTIF-001 |

---

## 2. Upstream References

**Problem Framing Document:** PFD-TASKFLOW-NOTIF-001

**Value Hypothesis:** VH-TASKFLOW-NOTIF-001

**Assumption Register:** AR-TASKFLOW-NOTIF-001 — 7 assumptions targeted for validation

---

## 3. Experiment Inventory

### EXP-1: Notification-Churn Cohort Analysis

| Field | Value |
|-------|-------|
| Target Assumption | ASM-1 (Notification overload is causal to churn) |
| Hypothesis Tested | Users who disable notifications churn at a higher rate than users who keep them enabled, after controlling for account age and plan tier |
| Method | Cohort analysis comparing churn rates between notification-disabled vs. notification-enabled users across mid-market accounts, controlling for account age and plan tier |
| Sample / Scope | All mid-market accounts active in Q2-Q3 2025 (n=312 accounts, 1,847 users). Cohorts: all-disabled (n=221), partially-disabled (n=758), all-enabled (n=868) |
| Conclusion | Partially Confirmed |
| Confidence Level | Medium |

**Raw Findings:**
- Users with all notifications disabled churned at 14.2% (quarterly), vs. 7.8% for all-enabled users and 9.1% for partially-disabled users
- After controlling for account age and plan tier, the difference remained significant (p<0.05) between all-disabled and all-enabled cohorts
- However, the direction of causation is unclear: users may disable notifications because they are already disengaging (reverse causality)
- Account-level churn showed a weaker signal: accounts where >50% of users disabled notifications churned at 11.3% vs. 7.4% for accounts where <20% disabled

**Limitations:**
- Observational study — cannot establish causation, only correlation
- Reverse causality is plausible: users may disable notifications as part of disengagement, not as a cause of it
- Q2-Q3 2025 data may not reflect current conditions (competitive landscape has changed since ProjectPro launch)

### EXP-2: Notification Re-enablement Survey

| Field | Value |
|-------|-------|
| Target Assumption | ASM-2 (Users will re-enable notifications if quality improves) |
| Hypothesis Tested | Users who have disabled all notifications would re-enable them if notifications were filtered by priority |
| Method | In-app survey targeting users with all notification channels disabled. Presented a description of priority-filtered notifications with examples, then asked about willingness to re-enable |
| Sample / Scope | 43 responses from users with all notifications disabled (target was 50; 43 achieved from 120 invitations, 36% response rate) |
| Conclusion | Confirmed |
| Confidence Level | Medium |

**Raw Findings:**
- 67% (29/43) said they would "definitely" or "probably" re-enable notifications if they only received high-priority items
- 23% (10/43) said "maybe — depends on how well it works"
- 9% (4/43) said "no — I prefer checking the app directly"
- When asked what "high priority" means, the top answers were: "tasks assigned to me" (88%), "deadlines at risk" (81%), "blockers on my tasks" (74%), "someone needs my input" (67%)
- Free-text responses frequently mentioned "I turned them off because everything looked urgent" and "I'd try it again if I could trust it to only show important things"

**Limitations:**
- Stated intent does not reliably predict actual behavior — 67% saying "yes" in a survey may translate to far fewer actually re-enabling
- Self-selection bias: users who responded to the survey may be more engaged than non-respondents
- Sample size (43) is modest; results should be interpreted as directional, not precise

### EXP-3: Notification Event Metadata Assessment

| Field | Value |
|-------|-------|
| Target Assumption | ASM-3 (Notification event metadata supports intelligent filtering) |
| Hypothesis Tested | The existing notification event metadata fields are sufficient to determine notification priority without significant infrastructure changes |
| Method | Engineering review of the notification event schema, with assessment against a draft priority taxonomy (Critical/Important/Informational). Identified required fields for each priority determination rule. |
| Sample / Scope | Full notification event schema (23 event types, 12 metadata fields per event). Reviewed against 8 proposed priority rules. |
| Conclusion | Confirmed |
| Confidence Level | High |

**Raw Findings:**
- All 8 proposed priority rules can be evaluated using existing metadata fields (action_type, task_status, assignee_id, due_date, blocker_flag, project_id, actor_id, mentioned_users)
- No new data sources or infrastructure changes are required for basic priority classification
- The existing event pipeline can support a classification step with <100ms added latency (well within the 500ms budget)
- One gap identified: "deadline at risk" detection requires comparing due_date against current date, which is simple but currently not computed in the event pipeline — minor addition needed

**Limitations:**
- Assessment is based on the current 8 priority rules; more complex future rules may require additional metadata
- Performance estimate is theoretical — not load-tested

### EXP-4: Role Data Completeness Audit

| Field | Value |
|-------|-------|
| Target Assumption | ASM-4 (Role data exists and is accurate) |
| Hypothesis Tested | User role field is sufficiently complete and accurate for role-based notification delivery |
| Method | Data audit of role field across all mid-market accounts. Compared self-reported roles against actual platform usage patterns (project creation, task management, reporting views). |
| Sample / Scope | All users on mid-market accounts (n=1,847 users across 312 accounts) |
| Conclusion | Partially Confirmed |
| Confidence Level | High |

**Raw Findings:**
- Role field completeness: 78% of users have a role set (1,441/1,847)
- 22% have no role set (406 users) — these would need a fallback
- Role accuracy (comparing self-reported role to usage patterns): 89% match for "Project Manager" role (high confidence), 72% match for "Contributor" role (moderate — some contributors have PM-like usage patterns), "Executive" role is rare (only 34 users) and 91% match
- The 22% with no role set show mixed usage patterns: 65% look like contributors, 25% look like PMs, 10% are inactive

**Limitations:**
- "Accuracy" is defined by usage pattern matching, which is itself an assumption — some PMs may delegate project creation to admins
- Executive role sample is very small (34 users)

### EXP-5: Priority Need Convergence Interviews

| Field | Value |
|-------|-------|
| Target Assumption | ASM-5 (Users can articulate priority needs consistently) |
| Hypothesis Tested | Users across roles converge on a consistent set of notification priorities that can be served by a standard taxonomy |
| Method | Semi-structured interviews with PMs, contributors, and executives from mid-market accounts. Asked to sort 15 notification scenarios into "must see immediately", "can wait", and "don't need" |
| Sample / Scope | 14 interviews: 6 PMs, 5 contributors, 3 executives from 9 different accounts |
| Conclusion | Confirmed |
| Confidence Level | Medium |

**Raw Findings:**
- Strong convergence on "must see immediately": task assignment (100%), deadline at risk (93%), blocker reported (93%), someone needs my input (86%)
- Strong convergence on "don't need" for PMs and contributors: comment on completed task (100%), team member updated their status (86%)
- Role-based differences emerged as expected: executives ranked "project milestone reached" and "budget threshold crossed" as must-see; PMs and contributors did not
- A standard three-tier taxonomy (Critical/Important/Informational) maps well to the convergence data
- The 15 notification scenarios covered all current event types; no interviewee identified a scenario we missed

**Limitations:**
- 14 interviews is directionally useful but not statistically representative
- All interviewees were from accounts in good standing — churned account users may have different priority needs
- Scenarios were presented in controlled conditions; real-world priority needs may differ when notifications arrive in context

---

## 4. Results Summary

| Conclusion | Count | Experiments |
|-----------|-------|-------------|
| Confirmed | 3 | EXP-2, EXP-3, EXP-5 |
| Invalidated | 0 | — |
| Inconclusive | 0 | — |
| Partially Confirmed | 2 | EXP-1, EXP-4 |

### High-Risk Assumption Coverage

| AR Assumption | Risk Level | Tested By | Result |
|--------------|-----------|-----------|--------|
| ASM-1 | High | EXP-1 | Partially Confirmed — correlation exists but causation not established |
| ASM-2 | High | EXP-2 | Confirmed — 67% state intent to re-enable |
| ASM-3 | Medium | EXP-3 | Confirmed — metadata sufficient |
| ASM-4 | Medium | EXP-4 | Partially Confirmed — 78% complete, 22% need fallback |
| ASM-5 | Medium | EXP-5 | Confirmed — consistent priority taxonomy viable |
| ASM-6 | Low | Not tested | Untested — design review deferred |
| ASM-7 | Low | Not tested | Untested — coordination meeting not yet held |

---

## 5. Assumption Status Update

| AR Assumption | Original Risk | Experiment | Updated Status | Notes |
|--------------|--------------|------------|---------------|-------|
| ASM-1 | High | EXP-1 | Partially Confirmed | Correlation exists; causation not proven. Proceed with awareness that churn impact may be smaller than estimated. |
| ASM-2 | High | EXP-2 | Confirmed | 67% stated re-enablement intent. Actual behavior will need post-launch monitoring. |
| ASM-3 | Medium | EXP-3 | Confirmed | Metadata sufficient. Minor addition needed for deadline-at-risk detection. |
| ASM-4 | Medium | EXP-4 | Partially Confirmed | 78% have roles set. Need fallback for 22% without roles (default to Contributor recommended). |
| ASM-5 | Medium | EXP-5 | Confirmed | Standard three-tier taxonomy works across roles. |
| ASM-6 | Low | Not tested | Untested | Low risk; design review planned but not blocking. |
| ASM-7 | Low | Not tested | Untested | Low risk; coordination meeting not blocking. |

---

## 6. Impact Assessment

### Invalidated Assumptions

No assumptions were invalidated.

### Partially Confirmed Assumptions

**ASM-1: Notification overload is causal to churn**
- **What was confirmed:** Significant correlation between notification disablement and higher churn rates (14.2% vs. 7.8%)
- **What was not confirmed:** Causal direction — disablement may be a symptom of disengagement, not a cause
- **Impact on initiative:** The business case ($180K-$300K ARR retention) should be treated as an upper bound, not a guaranteed outcome. The initiative remains justified on user experience grounds even if the churn impact is smaller than projected.
- **Affected hypotheses:** VH HYP-3 (churn reduction) — confidence level should be adjusted downward

**ASM-4: Role data exists and is accurate**
- **What was confirmed:** 78% of users have role data; accuracy is high for PM (89%) and Executive (91%), moderate for Contributor (72%)
- **What was not confirmed:** Full completeness — 22% of users have no role set
- **Impact on initiative:** Role-based delivery (VH HYP-2) is feasible but needs a fallback rule for users without role data. Recommendation: default to "Contributor" behavior for unset roles, with a prompt for users to set their role.
- **Affected hypotheses:** VH HYP-2 (role-appropriate delivery) — feasible with fallback

### Confirmed Assumptions (De-Risk Notes)

- **ASM-2 confirmed:** Users express clear willingness to re-enable notifications under improved conditions. This de-risks the primary success metric for HYP-1.
- **ASM-3 confirmed:** No infrastructure blockers. The existing metadata and pipeline can support priority classification within performance constraints. This de-risks timeline and budget assumptions.
- **ASM-5 confirmed:** A standard priority taxonomy is viable across roles. This means NG-5 (no per-user custom rules) is appropriate — a standard taxonomy is sufficient for this phase.

---

## 7. Recommendations

**Proceed / Pivot / Pause:** Proceed

**Rationale:** No assumptions were invalidated. Both high-risk assumptions (ASM-1, ASM-2) showed positive signals, though ASM-1's causal link is weaker than hoped. The technical feasibility assumption (ASM-3) was confirmed with high confidence, removing the main delivery risk. The role data gap (ASM-4) is manageable with a fallback rule.

The initiative should proceed to Discovery PRD generation with two adjustments:
1. Frame the churn reduction goal (G-4 in the PRD) with appropriate uncertainty — the impact may be smaller than the upper-bound estimate
2. Include a fallback requirement for users without role data

**Remaining validation needed:**
- ASM-6 (no UX redesign needed) — low risk, can be validated during engineering design
- ASM-7 (independence from Activity Feed Redesign) — low risk, coordination meeting should happen but is not blocking

---

## 8. Open Questions

**OQ-1: Should we actively prompt users without role data to set their role?**
- **Category:** Non-blocking
- **Raised by:** EXP-4
- **Owner / Resolution plan:** Product team to decide during DPRD generation whether role-setting is in scope or deferred. Recommendation: add as a non-blocking enhancement.

---

## 9. Freeze Declaration

| Field | Value |
|-------|-------|
| Frozen | Yes |
| Freeze Date | 2026-02-16 |
| Approved By | Sarah Chen, VP of Product |

This Experiment Log has been validated, reviewed, and approved. The recommendation is to proceed. It is now the authoritative experiment evidence for the TaskFlow notification improvement initiative and the required input for Discovery PRD generation.
