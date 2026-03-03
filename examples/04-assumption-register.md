# Assumption Register — Worked Example

## 1. Document Control

| Field | Value |
|-------|-------|
| Artifact ID | AR-TASKFLOW-NOTIF-001 |
| Version | 1.0 |
| Date | 2026-01-24 |
| Author | AI-generated, human-reviewed |
| Status | Frozen |
| Upstream PFD | PFD-TASKFLOW-NOTIF-001 |
| Upstream VH | VH-TASKFLOW-NOTIF-001 |

---

## 2. Upstream References

**Problem Framing Document:** PFD-TASKFLOW-NOTIF-001 — TaskFlow's notification system delivers undifferentiated high-volume notifications, causing fatigue and contributing to mid-market churn.

**Value Hypothesis:** VH-TASKFLOW-NOTIF-001 — Three hypotheses: priority-based filtering reduces fatigue (HYP-1), role-appropriate delivery improves actionability (HYP-2), and improved notification quality reduces churn (HYP-3).

---

## 3. Assumption Inventory

### ASM-1: Notification Overload Is Causal to Churn

| Field | Value |
|-------|-------|
| Statement | Notification overload is a causal factor in mid-market churn, not merely a correlated complaint. Addressing it will reduce churn. |
| Source | PFD §5 Opportunity Sizing, VH HYP-3 |
| Category | Market |
| Risk Level | High |
| Impact if False | The primary business justification ($180K-$300K ARR retention) is invalid. The initiative may still improve user experience but would not achieve its churn reduction goal. Priority and scope would need reassessment. |
| Current Evidence | Exit surveys cite notifications as #2 churn reason (34%, n=47). However, correlation is not causation — users may cite notifications as a proxy for deeper dissatisfaction. |
| Validation Method | Product Analytics team cohort analysis comparing churn rates between users who disabled notifications vs. those who didn't, controlling for account age and plan tier. Expected January. |

### ASM-2: Users Will Re-enable Notifications If Quality Improves

| Field | Value |
|-------|-------|
| Statement | Users who have disabled notifications will re-enable them if notification quality (relevance, priority) improves meaningfully. |
| Source | PFD §4 PP-3, VH HYP-1 |
| Category | User Behavior |
| Risk Level | High |
| Impact if False | HYP-1's primary success metric (re-enablement rate) would fail. Users may have permanently abandoned notifications as a channel, requiring different intervention strategies (e.g., in-app activity feed improvements instead). |
| Current Evidence | 7 of 8 PM interviewees said they would use notifications "if they were useful." However, stated preferences in interviews do not reliably predict actual behavior. |
| Validation Method | Pre-launch survey targeting users who have disabled all notifications: "If notifications only showed you [high-priority examples], would you re-enable them?" with follow-up on specific conditions. Target: n=50. |

### ASM-3: Notification Event Metadata Supports Intelligent Filtering

| Field | Value |
|-------|-------|
| Statement | The existing notification event metadata (project ID, task ID, user ID, action type, timestamp, actor) is sufficient to determine notification priority and relevance without significant infrastructure changes. |
| Source | PFD §7 Current State |
| Category | Technical |
| Risk Level | Medium |
| Impact if False | Intelligent filtering (HYP-1) may require infrastructure changes that extend timeline and budget beyond allocated Q1-Q2 capacity. Scope would need to be reduced or timeline extended. |
| Current Evidence | Notification service documentation describes structured metadata fields. Engineering has not formally assessed whether these fields are sufficient for priority determination. |
| Validation Method | Engineering lead reviews notification event schema and assesses whether priority can be inferred from existing fields. Produces a gap analysis by mid-February. |

### ASM-4: Role Data Exists and Is Accurate

| Field | Value |
|-------|-------|
| Statement | User role information (PM, contributor, executive) is available in user profiles and is accurate enough to drive role-based notification delivery. |
| Source | VH HYP-2 |
| Category | Data |
| Risk Level | Medium |
| Impact if False | Role-based delivery (HYP-2) cannot be implemented without manual role assignment or role inference, adding complexity and potentially delaying delivery. |
| Current Evidence | User profiles have a "role" field, but its completeness and accuracy have not been audited. Self-reported roles may not match actual usage patterns. |
| Validation Method | Data team audits role field completeness across mid-market accounts. Compare self-reported roles against actual platform usage patterns (e.g., do "PMs" actually create and manage projects?). Target: audit complete by early February. |

### ASM-5: Users Can Articulate Priority Needs Consistently

| Field | Value |
|-------|-------|
| Statement | Users across mid-market accounts have consistent enough priority needs that a single priority taxonomy can work for most users, without requiring per-user customization. |
| Source | VH HYP-1, PFD §4 PP-2 |
| Category | User Behavior |
| Risk Level | Medium |
| Impact if False | A universal priority taxonomy would not work. The solution would need to support per-user or per-account priority customization, significantly increasing complexity. |
| Current Evidence | PM interviews suggest convergence around "deadline risks, assignments, and blockers" as high-priority. However, the sample is small (8 interviews) and limited to PMs. |
| Validation Method | Expand user research to include contributors and executives (target: 12-15 additional interviews across roles). Analyze for convergence in priority definitions. |

### ASM-6: Improved Notifications Do Not Require UX Redesign

| Field | Value |
|-------|-------|
| Statement | Notification quality improvements can be delivered through backend filtering and delivery logic changes without requiring a redesign of the notification UI/UX. |
| Source | PFD §7 Current State |
| Category | Technical |
| Risk Level | Low |
| Impact if False | A UX redesign would extend scope and timeline. The initiative may need to be phased, with backend improvements first and UX improvements in a subsequent release. |
| Current Evidence | The current notification UI displays title, description, and timestamp. Adding a priority indicator and batching are likely compatible with the existing UI. However, digest views (for executives) may require new UI components. |
| Validation Method | Design team reviews current notification UI against proposed filtering and batching behaviors. Identifies any required UI changes. |

### ASM-7: Notification Improvements Are Independent of Activity Feed Redesign

| Field | Value |
|-------|-------|
| Statement | Notification improvements can be delivered independently of the planned Q3 Activity Feed Redesign initiative without creating conflicts or redundant work. |
| Source | PFD Discovery Intake — Related Initiatives |
| Category | Organizational |
| Risk Level | Low |
| Impact if False | Work may be duplicated between initiatives, or notification improvements may need to be coordinated with the activity feed timeline, potentially delaying delivery. |
| Current Evidence | The two initiatives are described as "compatible but not dependent" in the intake form. No detailed dependency analysis has been done. |
| Validation Method | Product lead confirms with Activity Feed Redesign owner that the two initiatives can proceed independently. Brief coordination meeting. |

---

## 4. Risk Assessment Summary

| Risk Level | Count | Assumptions |
|-----------|-------|-------------|
| High | 2 | ASM-1, ASM-2 |
| Medium | 3 | ASM-3, ASM-4, ASM-5 |
| Low | 2 | ASM-6, ASM-7 |

**Highest-risk assumptions:** ASM-1 (notification-churn causality) and ASM-2 (user re-enablement behavior). These two assumptions underpin the initiative's business case and the primary success metric respectively.

**Unvalidated high-risk assumptions:** Both ASM-1 and ASM-2 have supporting evidence but neither has been validated through the planned validation methods. Cohort analysis (ASM-1) and pre-launch survey (ASM-2) are in progress.

---

## 5. Validation Plan

| Assumption | Method | Expected Timeline | Owner |
|-----------|--------|-------------------|-------|
| ASM-1 | Cohort analysis: churn rate comparison between notification-disabled vs. notification-enabled users, controlling for account age and plan tier | End of January 2026 | Product Analytics team |
| ASM-2 | Pre-launch survey of users with all notifications disabled (n=50 target): conditions for re-enablement | Early February 2026 | User Research team |
| ASM-3 | Engineering review of notification event schema; gap analysis for priority determination | Mid-February 2026 | Engineering lead |
| ASM-4 | Role field completeness audit across mid-market accounts; usage-pattern-vs-role comparison | Early February 2026 | Data team |
| ASM-5 | Expanded user research (12-15 interviews across PM, contributor, executive roles): priority need convergence analysis | Mid-February 2026 | User Research team |

---

## 6. Dependency Map

### Inter-Assumption Dependencies

- **ASM-1 → ASM-2:** If notification overload is not causal to churn (ASM-1 false), then user re-enablement (ASM-2) becomes less relevant to the business case — users might re-enable, but the churn impact wouldn't follow.
- **ASM-3 → ASM-5:** If metadata is insufficient for filtering (ASM-3 false), then even if users have consistent priority needs (ASM-5 true), the system cannot deliver on those needs without infrastructure work.

### Cascade Analysis

- If **ASM-1 is invalidated**: HYP-3 fails, the churn reduction business case weakens significantly. HYP-1 and HYP-2 may still be valid (notifications can still be improved for user experience) but the initiative's priority relative to other work would need reassessment.
- If **ASM-2 is invalidated**: HYP-1's primary success metric (re-enablement) would fail. The initiative would need to reframe success around reducing fatigue for users who keep notifications on, rather than re-engaging users who turned them off.

---

## 7. Open Questions

**OQ-1: Will the cohort analysis have sufficient sample size to be statistically meaningful?**
- **Category:** Non-blocking
- **Related assumption:** ASM-1
- **Owner / Resolution plan:** Product Analytics to assess sample size feasibility before running the analysis. If n is too small, consider extending the analysis window or supplementing with qualitative data.

---

## 8. Freeze Declaration

| Field | Value |
|-------|-------|
| Frozen | Yes |
| Freeze Date | 2026-01-26 |
| Approved By | Sarah Chen, VP of Product |

This Assumption Register has been validated, reviewed, and approved. It is now the authoritative assumption catalog for the TaskFlow notification improvement initiative and the required input for Discovery PRD generation.
