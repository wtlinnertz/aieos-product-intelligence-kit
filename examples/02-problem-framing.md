# Problem Framing Document — Worked Example

## 1. Document Control

| Field | Value |
|-------|-------|
| Artifact ID | PFD-TASKFLOW-NOTIF-001 |
| Version | 1.0 |
| Date | 2026-01-15 |
| Author | AI-generated, human-reviewed |
| Status | Frozen |

---

## 2. Problem Statement

Project managers and team contributors on TaskFlow's mid-market accounts miss critical task updates because the notification system delivers high volumes of undifferentiated notifications, forcing users to either disable notifications entirely or endure notification fatigue. This results in missed deadlines, dropped handoffs, and is the #2 cited reason for mid-market customer churn (34% of churned accounts, Q3 data). This problem requires attention now because churn data quantifies its business impact, a key competitor has launched intelligent notifications as a differentiator, and three enterprise prospects have flagged notification quality during active sales evaluations.

---

## 3. User Landscape

### Primary Users

**UG-1: Project Managers (Mid-Market)**
- **Who they are:** Project managers on mid-market accounts (3-8 concurrent projects, 5-25 team members per project)
- **What they do:** Monitor project status, identify blockers, manage deadlines, coordinate team handoffs
- **How the problem affects them:** Receive 80-150 notifications/day with fewer than 20% being actionable. Many have resorted to constant manual checking of the platform rather than relying on notifications, consuming significant time and attention.

**UG-2: Team Contributors**
- **Who they are:** Individual contributors on project teams
- **What they do:** Execute assigned tasks, report blockers, hand off completed work
- **How the problem affects them:** Receive 30-60 notifications/day. Frequently miss assignment notifications and blocker resolution updates buried in noise. Cope by asking PMs directly for status, creating redundant communication.

### Secondary Users

**UG-3: Executive Stakeholders**
- **Who they are:** Executives or senior leaders who periodically review project status
- **What they do:** Monitor portfolio health, identify at-risk projects, make resource decisions
- **How the problem affects them:** Receive summary notifications that are too frequent and not focused on decision-relevant information. Cope by requesting verbal updates from PMs, bypassing the platform.

---

## 4. Pain Points and Impact

**PP-1: Notification Volume Overwhelms Signal**
- **Problem behavior:** All enabled notification types generate immediate individual notifications regardless of relevance or urgency, creating a high-volume, undifferentiated stream
- **Frequency:** Continuous — PMs receive 80-150/day, contributors receive 30-60/day
- **Impact:** 41% of users have disabled at least one notification channel; 12% have disabled all notifications. Users who leave notifications on report "notification fatigue."
- **Evidence basis:** Known (in-app analytics, Q3 data)

**PP-2: No Priority Differentiation**
- **Problem behavior:** A deadline-at-risk alert looks identical to a comment on a completed task. Users cannot distinguish urgent from informational without opening each notification.
- **Frequency:** Every notification delivery
- **Impact:** Critical updates (blocker alerts, deadline risks, assignment changes) are buried in low-value notifications. Users miss actionable items.
- **Evidence basis:** Known (user interviews — 7 of 8 PMs described this as a "daily frustration")

**PP-3: Binary Control Model**
- **Problem behavior:** Users can only toggle notification types on or off. There is no middle ground — no filtering by relevance, no batching, no priority-based delivery.
- **Frequency:** Ongoing — the 30-toggle preference page was introduced in 2024 Q1 and did not durably reduce complaints
- **Impact:** Users default to "all on" (and suffer fatigue) or "all off" (and miss critical updates). The 2024 Q1 granular toggles reduced support tickets by 15% initially but returned to baseline within 2 months.
- **Evidence basis:** Known (support ticket data, adoption analytics)

**PP-4: Missed Handoffs and Deadlines**
- **Problem behavior:** When contributors miss assignment or blocker-resolution notifications, handoffs stall. When PMs miss deadline-risk notifications, corrective action is delayed.
- **Frequency:** Support data shows notification-related tickets are 8% of all tickets (~120/month), and PM interviews indicate missed handoffs occur "multiple times per week"
- **Impact:** Missed deadlines, rework, and erosion of trust in the platform as a coordination tool. Contributes directly to churn (34% of churned mid-market accounts cite notification overload).
- **Evidence basis:** Known (exit surveys, support tickets, user interviews)

---

## 5. Opportunity Sizing

**Churn reduction:** Addressing the #2 churn driver could retain 15-25% of mid-market accounts that would otherwise churn, estimated at $180K-$300K ARR annually.

**Pipeline conversion:** Three active enterprise prospects ($420K combined deal value) have specifically asked about notification improvements.

**Support cost reduction:** A 50% reduction in notification-related support tickets (~120/month → ~60/month) would save approximately 60 support hours/month.

**Basis:** Churn estimate derived from Q3 exit survey data (34% of 47 churned accounts cited notifications) and mid-market account ACV. Pipeline data from CRM. Support ticket volume from helpdesk analytics.

**Uncertainty acknowledgment:** The churn reduction estimate assumes notification overload is a causal factor, not merely a correlated complaint. The actual retention impact could be higher or lower depending on whether addressing notifications changes the churn decision or whether other factors dominate.

---

## 6. Strategic Alignment

Addressing notification overload directly supports two organizational priorities:

**Strategic objectives supported:**
- FY26 priority: "Reduce mid-market churn rate from 8.2% to 5.5%" — notifications are the #2 cited churn reason
- Product roadmap theme: "Intelligence layer" — making the platform smarter about what surfaces to users

---

## 7. Current State

### How the Problem Is Currently Handled

- **Channel toggles:** Users can enable/disable email, in-app, and mobile push notifications at the account level
- **Event type toggles:** A preference page offers ~30 toggles for specific event types (task assigned, comment added, status changed, etc.)
- **No filtering or prioritization:** All enabled notifications are delivered immediately and identically
- **No batching or digesting:** Each event generates a separate notification

### What Has Been Tried Before

- **2024 Q1 — Granular toggle page:** Added ~30 event-type toggles. Support tickets decreased 15% initially but returned to baseline within 2 months. Post-mortem: toggles were too complex (users didn't understand the categories) and the fundamental problem (volume without prioritization) was unchanged.

### Existing System Context

- Notification service is an internal microservice processing ~2M events/day
- Events have structured metadata: project ID, task ID, user ID, action type, timestamp, actor
- Current architecture supports channel routing (which channel to send through) but not content-based filtering or priority assessment
- No user behavior data is currently used in notification decisions

---

## 8. Constraints and Boundaries

### Known Constraints
- Budget is within existing Q1-Q2 product engineering capacity — no additional headcount
- Timeline: solution must be defined by end of Q1, delivery target mid-Q2
- Must not break existing notification preferences — users who have configured toggles must not lose their settings
- Standard data privacy requirements apply (no notification-specific regulatory constraints)

### Problem Space Boundaries
- Enterprise-specific notification features (SSO-gated policies, admin-controlled rules) are excluded — separate initiative
- Pricing and packaging changes are excluded
- The notification infrastructure architecture is not in scope for this problem framing — this document defines the problem, not the technical approach

---

## 9. Open Questions

**OQ-1: Is notification overload causal to churn or merely correlated?**
- **Category:** Non-blocking (we have sufficient evidence to proceed, but this affects expected impact)
- **Owner / Resolution plan:** Product Analytics team will conduct cohort analysis comparing churn rates between users who disabled notifications and those who didn't. Expected by end of January.

**OQ-2: Would users re-enable notifications if they were more relevant?**
- **Category:** Non-blocking (we believe yes based on interview data, but not validated)
- **Owner / Resolution plan:** Include in upcoming user research sprint. Plan: survey users who have disabled notifications about conditions for re-enabling.

**OQ-3: Is the existing notification event metadata sufficient for intelligent filtering?**
- **Category:** Non-blocking (engineering assessment needed, but does not block problem framing or hypothesis formation)
- **Owner / Resolution plan:** Engineering lead to assess metadata richness against filtering requirements. Expected by mid-February.

---

## 10. Freeze Declaration

| Field | Value |
|-------|-------|
| Frozen | Yes |
| Freeze Date | 2026-01-17 |
| Approved By | Sarah Chen, VP of Product |

This Problem Framing Document has been validated, reviewed, and approved. It is now the authoritative problem definition for the TaskFlow notification improvement initiative and the required input for Value Hypothesis generation.
