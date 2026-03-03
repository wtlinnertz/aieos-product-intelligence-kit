# Value Hypothesis — Worked Example

## 1. Document Control

| Field | Value |
|-------|-------|
| Artifact ID | VH-TASKFLOW-NOTIF-001 |
| Version | 1.0 |
| Date | 2026-01-20 |
| Author | AI-generated, human-reviewed |
| Status | Frozen |
| Upstream PFD | PFD-TASKFLOW-NOTIF-001 |

---

## 2. Problem Summary

TaskFlow's notification system delivers high volumes of undifferentiated notifications, forcing mid-market users to either disable notifications (missing critical updates) or endure fatigue (reduced productivity and trust). This is the #2 cited reason for mid-market churn.

Source: PFD-TASKFLOW-NOTIF-001

---

## 3. Target Users

| PFD Reference | User Group | Relevance to Hypotheses |
|---------------|-----------|------------------------|
| UG-1 | Project Managers (Mid-Market) | Primary beneficiaries — receive highest notification volume (80-150/day), most affected by lack of prioritization |
| UG-2 | Team Contributors | Significant beneficiaries — miss assignment and blocker notifications buried in noise |
| UG-3 | Executive Stakeholders | Secondary beneficiaries — receive inappropriate notification granularity for their role |

---

## 4. Value Hypotheses

### HYP-1: Priority-Based Notification Filtering Reduces Fatigue

**We believe that** filtering notifications by urgency and relevance **for** project managers (UG-1) and team contributors (UG-2) **will achieve** a significant reduction in notification fatigue and a measurable decrease in missed critical updates.

- **Belief:** Users are overwhelmed not by notifications as a concept, but by the inability to distinguish urgent from informational. If the system surfaces high-priority notifications (deadline risks, assignment changes, blocker alerts) prominently and reduces noise from low-priority events (comments on completed tasks, minor status updates), users will engage with notifications rather than disabling them.
- **Target users:** UG-1 (Project Managers), UG-2 (Team Contributors)
- **Expected outcome:** Users who receive priority-filtered notifications will re-enable previously disabled notification channels and report lower fatigue levels. The percentage of users with all notifications disabled will decrease.
- **Evidence criteria:** The percentage of users with all notifications disabled decreases from 12% to below 6% within 60 days of launch. Users who receive filtered notifications report lower notification fatigue in post-launch survey (target: >60% report improvement).
- **Falsification criteria:** If fewer than 30% of users who previously disabled all notifications re-enable any channel within 60 days, this hypothesis is false. If notification-related support tickets do not decrease by at least 25%, the filtering is not solving the core problem.

### HYP-2: Role-Appropriate Notification Delivery Improves Actionability

**We believe that** tailoring notification content and frequency to user role (PM vs. contributor vs. executive) **for** all three user groups (UG-1, UG-2, UG-3) **will achieve** higher notification actionability rates and fewer redundant communication requests.

- **Belief:** Different roles need different information at different frequencies. PMs need blocker and deadline alerts in real-time; contributors need assignment and handoff notifications promptly but can batch other updates; executives need weekly risk digests, not task-level events. Matching delivery to role will make each notification more likely to drive action.
- **Target users:** UG-1 (Project Managers), UG-2 (Team Contributors), UG-3 (Executive Stakeholders)
- **Expected outcome:** Users report that a higher percentage of received notifications are actionable. PMs reduce time spent manually checking the platform. Contributors stop asking PMs for assignment status.
- **Evidence criteria:** Self-reported notification actionability increases from <20% (PMs) to >50%. Platform check frequency for PMs decreases measurably (analytics). Support tickets related to "missed notifications" decrease by at least 40%.
- **Falsification criteria:** If self-reported actionability does not exceed 35% for PMs within 60 days, role-based tailoring is insufficient. If contributors' behavior (asking PMs for status) does not change as measured by a follow-up interview sample, the hypothesis is false.

### HYP-3: Improved Notification Quality Reduces Mid-Market Churn

**We believe that** addressing notification overload **for** mid-market account users (UG-1, UG-2) **will achieve** a measurable reduction in mid-market churn rate.

- **Belief:** Notification overload is a causal factor in churn, not just a correlated complaint. Users who have a better notification experience will derive more value from the platform, reducing their likelihood of churning. Since notifications are the #2 cited churn reason, improving them should move the churn metric.
- **Target users:** UG-1 (Project Managers), UG-2 (Team Contributors)
- **Expected outcome:** Mid-market churn rate decreases measurably after notification improvements are delivered.
- **Evidence criteria:** Mid-market churn rate decreases by at least 1 percentage point (from 8.2%) within two quarters of launch. "Notification overload" drops from the top 3 reasons in exit surveys.
- **Falsification criteria:** If mid-market churn rate does not decrease by at least 0.5 percentage points within two quarters, or if "notification overload" remains in the top 3 exit survey reasons at the same or higher percentage, this hypothesis is false.

---

## 5. Hypothesis Prioritization

| Rank | Hypothesis | Expected Impact | Confidence Level | Rationale |
|------|-----------|----------------|-----------------|-----------|
| 1 | HYP-1 | High | Medium | Directly addresses the core pain point (PP-1, PP-2). High impact because it attacks the root cause — undifferentiated volume. Medium confidence because we assume users will re-engage once filtering exists, which is unvalidated. |
| 2 | HYP-2 | Medium | Medium | Addresses role mismatch (PP-3). Medium impact because it complements HYP-1 but may not move metrics alone. Medium confidence because role-based needs are inferred from interviews, not validated quantitatively. |
| 3 | HYP-3 | High | Low | Highest business impact (churn reduction) but lowest confidence because the causal link between notifications and churn is assumed, not proven. This hypothesis depends on HYP-1 and HYP-2 succeeding. |

**Prioritization basis:** Impact assessed by potential business value (ARR retention, pipeline conversion). Confidence assessed by strength of evidence supporting the causal mechanism. HYP-1 ranked first because it is the most direct intervention with the most evidence; HYP-3 ranked last because it is an outcome hypothesis dependent on HYP-1 and HYP-2.

---

## 6. Success Metrics

**SM-1: Notification Disable Rate**
- **Hypothesis:** HYP-1
- **Metric:** Percentage of users with all notification channels disabled
- **Target:** Decrease from 12% to below 6% within 60 days of launch
- **Measurement method:** In-app analytics — notification preferences dashboard

**SM-2: Notification Re-enablement Rate**
- **Hypothesis:** HYP-1
- **Metric:** Percentage of previously-all-disabled users who re-enable at least one channel
- **Target:** >30% re-enable within 60 days
- **Measurement method:** In-app analytics — track users who had all channels disabled at launch

**SM-3: Self-Reported Actionability**
- **Hypothesis:** HYP-2
- **Metric:** Percentage of notifications users report as actionable
- **Target:** PMs: >50% (from <20%). Contributors: >40%.
- **Measurement method:** Post-launch in-app survey (30 days and 60 days post-launch)

**SM-4: Notification-Related Support Tickets**
- **Hypothesis:** HYP-1, HYP-2
- **Metric:** Monthly notification-related support ticket volume
- **Target:** Decrease by at least 40% (from ~120/month to ~72/month)
- **Measurement method:** Helpdesk analytics — notification category tag

**SM-5: Mid-Market Churn Rate**
- **Hypothesis:** HYP-3
- **Metric:** Quarterly mid-market account churn rate
- **Target:** Decrease by at least 1 percentage point (from 8.2%) within two quarters
- **Measurement method:** Finance/analytics — standard churn reporting

**SM-6: Exit Survey Notification Mentions**
- **Hypothesis:** HYP-3
- **Metric:** Percentage of churned mid-market accounts citing "notification overload" in exit surveys
- **Target:** Drop from 34% to below 20%
- **Measurement method:** Exit survey analysis — quarterly

---

## 7. Falsification Criteria

| Hypothesis | Falsification Condition | Evidence Required |
|-----------|------------------------|-------------------|
| HYP-1 | <30% of previously-disabled users re-enable any channel within 60 days, OR notification support tickets do not decrease by 25% | In-app analytics + helpdesk data at 60-day mark |
| HYP-2 | PM self-reported actionability does not exceed 35% within 60 days, OR contributor behavior (asking PMs for status) unchanged in follow-up interviews | Post-launch survey + 5-8 contributor interviews at 60-day mark |
| HYP-3 | Mid-market churn rate does not decrease by 0.5pp within two quarters, OR "notification overload" remains in top 3 exit survey reasons at same/higher percentage | Quarterly churn report + exit survey analysis |

---

## 8. Dependencies and Risks

### Hypothesis Dependencies
- HYP-3 (churn reduction) is dependent on HYP-1 and HYP-2 succeeding. If notifications are not meaningfully improved (HYP-1, HYP-2 fail), churn reduction from notifications cannot occur.
- HYP-1 and HYP-2 are independent of each other — either could succeed alone, though both succeeding amplifies the effect.

### Hypothesis Conflicts
- No conflicts identified between hypotheses. They are complementary.

### Risks to Validity
- **Confounding churn factors:** Other product changes or market conditions during the measurement period could affect churn independently, making HYP-3 difficult to isolate.
- **Behavior inertia:** Users who have disabled notifications may not re-check or re-enable even if improvements are made, requiring active communication or re-onboarding.
- **Sample size for HYP-2 qualitative measure:** Follow-up interviews may not be representative. Self-reported actionability is subjective.

---

## 9. Open Questions

**OQ-1: What constitutes "high priority" for notification filtering?**
- **Category:** Non-blocking (can be defined during requirements generation based on event metadata)
- **Relevant hypothesis:** HYP-1
- **Owner / Resolution plan:** Product team to define priority taxonomy during DPRD generation, informed by PM interview data on which notification types are "must-see."

**OQ-2: How should "role" be determined for role-based delivery?**
- **Category:** Non-blocking (can be defined during requirements — role data exists in user profiles)
- **Relevant hypothesis:** HYP-2
- **Owner / Resolution plan:** Engineering to confirm role data availability and granularity. Product to define role-notification mapping.

---

## 10. Freeze Declaration

| Field | Value |
|-------|-------|
| Frozen | Yes |
| Freeze Date | 2026-01-22 |
| Approved By | Sarah Chen, VP of Product |

This Value Hypothesis document has been validated, reviewed, and approved. It is now the authoritative set of value bets for the TaskFlow notification improvement initiative and the required input for Assumption Register generation.
