# Discovery PRD — Worked Example

## 1. Document Control

| Field | Value |
|-------|-------|
| Artifact ID | DPRD-TASKFLOW-NOTIF-001 |
| Version | 1.0 |
| Date | 2026-02-18 |
| Author | AI-generated, human-reviewed |
| Status | Frozen |
| Upstream PFD | PFD-TASKFLOW-NOTIF-001 |
| Upstream VH | VH-TASKFLOW-NOTIF-001 |
| Upstream AR | AR-TASKFLOW-NOTIF-001 |
| Upstream EL | EL-TASKFLOW-NOTIF-001 |

---

## 2. Problem Statement

Project managers and team contributors on TaskFlow's mid-market accounts miss critical task updates because the notification system delivers high volumes of undifferentiated notifications without priority or role differentiation. This forces users to either disable notifications entirely (12% of users) or endure notification fatigue (41% have disabled at least one channel). The result is missed deadlines, dropped handoffs, and erosion of platform trust. This is the #2 cited reason for mid-market customer churn (34% of churned accounts, Q3 data), and a key competitor has launched intelligent notifications as a differentiator.

Source: PFD-TASKFLOW-NOTIF-001

---

## 3. Goals (What "Success" Means)

| Goal ID | Goal | Success Criterion | VH Trace |
|---------|------|-------------------|----------|
| G-1 | Reduce notification fatigue for mid-market users | Percentage of users with all notifications disabled decreases from 12% to below 6% within 60 days of launch | HYP-1 |
| G-2 | Increase notification actionability across user roles | PM self-reported notification actionability increases from <20% to >50% within 60 days | HYP-2 |
| G-3 | Reduce notification-related support burden | Notification-related support tickets decrease by at least 40% (from ~120/month to ~72/month) | HYP-1, HYP-2 |
| G-4 | Contribute to mid-market churn reduction | Mid-market churn rate decreases by at least 1 percentage point within two quarters of launch | HYP-3 |

---

## 4. Non-Goals (Hard Exclusions)

- **NG-1:** Enterprise-specific notification features (SSO-gated notification policies, admin-controlled rules) — these are a separate initiative for enterprise accounts and must not be included in this scope.
- **NG-2:** Pricing or packaging changes — notification improvements are not tied to plan tier changes.
- **NG-3:** Notification infrastructure re-architecture — this initiative defines what the notification system should do, not how it should be built. Infrastructure decisions belong to downstream engineering artifacts.
- **NG-4:** Activity Feed Redesign — the planned Q3 activity feed work is a separate initiative. This initiative must not depend on or duplicate that work.
- **NG-5:** Per-user custom priority rules — users will not define their own priority rules in this initiative. The system will apply a standard priority taxonomy. Per-user customization is a potential future enhancement.

---

## 5. Users / Personas

| PFD Reference | User / Persona | Context for Engineering |
|---------------|---------------|----------------------|
| UG-1 | Project Managers (Mid-Market) | Manage 3-8 concurrent projects. Need to quickly distinguish urgent updates (deadline risks, blockers, assignment changes) from informational noise. Currently receive 80-150 notifications/day. |
| UG-2 | Team Contributors | Individual contributors on project teams. Need timely notification of task assignments, blocker resolutions, and handoff requests. Currently receive 30-60 notifications/day. |
| UG-3 | Executive Stakeholders | Review project status periodically. Need high-level progress and risk alerts, not task-level events. Currently receive too-frequent, too-granular notifications. |

---

## 6. Requirements

### Functional Requirements

**FR-1:** The system SHALL classify each notification event into a priority level (Critical, Important, Informational) based on event type and context.
- VH Trace: HYP-1

**FR-2:** The system SHALL deliver Critical-priority notifications immediately through all enabled channels.
- VH Trace: HYP-1

**FR-3:** The system SHALL batch Important-priority notifications and deliver them at configurable intervals (default: every 2 hours during working hours).
- VH Trace: HYP-1

**FR-4:** The system SHALL aggregate Informational-priority notifications into a daily digest.
- VH Trace: HYP-1

**FR-5:** The system SHALL apply role-appropriate notification rules based on the user's role (Project Manager, Contributor, Executive).
- VH Trace: HYP-2

**FR-6:** The system SHALL provide Project Managers with real-time delivery of deadline-risk, blocker, and assignment-change notifications.
- VH Trace: HYP-2

**FR-7:** The system SHALL provide Contributors with prompt delivery of task-assignment and blocker-resolution notifications, with other updates batched.
- VH Trace: HYP-2

**FR-8:** The system SHALL provide Executive Stakeholders with a weekly project risk and progress digest, suppressing task-level notifications.
- VH Trace: HYP-2

**FR-9:** The system SHALL preserve existing user notification preferences (channel toggles and event-type toggles) — users must not lose their current settings.
- VH Trace: HYP-1 (constraint from PFD §8)

**FR-10:** The system SHALL allow users to override the default priority classification for specific event types.
- VH Trace: HYP-1

**FR-11:** The system SHALL default to Contributor notification rules for users whose role field is not set, ensuring no user is excluded from priority-filtered notifications.
- VH Trace: HYP-2 (informed by EL EXP-4)

### Non-Functional Requirements

**NFR-1:** The system SHALL process notification priority classification within 500ms of event generation so that Critical notifications are not delayed.
- VH Trace: Cross-cutting

**NFR-2:** The system SHALL handle the current notification volume (~2M events/day) without degradation in delivery latency.
- VH Trace: Cross-cutting

**NFR-3:** The system SHALL comply with existing data privacy requirements — notification filtering logic must not expose user data across account boundaries.
- VH Trace: Cross-cutting

**NFR-4:** The system SHALL provide notification delivery audit logs for troubleshooting (what was sent, to whom, through which channel, at what priority level).
- VH Trace: Cross-cutting

---

## 7. Constraints (Hard Guardrails)

- **C-1:** Must not break existing notification preferences — users who have configured toggles must not lose their settings. — Source: PFD §8
- **C-2:** Budget is within existing Q1-Q2 product engineering capacity — no additional headcount. — Source: PFD §8
- **C-3:** Solution must be defined by end of Q1; delivery target mid-Q2. — Source: PFD §8
- **C-4:** Priority taxonomy must work without per-user customization rules in this release (per NG-5). — Source: AR ASM-5
- **C-5:** Role determination must use existing user profile role data, with fallback to "Contributor" behavior for users without role data (22% of users per EL EXP-4). — Source: AR ASM-4, EL EXP-4

---

## 8. Assumptions

| ID | Assumption | Validation Status | Impact if False | AR Source | EL Source |
|----|-----------|------------------|----------------|-----------|-----------|
| A-1 | Notification overload is correlated with mid-market churn (causal link not fully established) | Partially Confirmed | Business case ($180K-$300K ARR) is an upper bound; initiative still justified on UX grounds | ASM-1 | EXP-1 |
| A-2 | Users who disabled notifications will re-enable them if quality improves (67% stated intent) | Confirmed | HYP-1's re-enablement success metric would fail; need to reframe success around fatigue reduction | ASM-2 | EXP-2 |
| A-3 | Existing notification event metadata supports priority classification without infrastructure changes | Confirmed | Timeline and budget constraints (C-2, C-3) may be violated | ASM-3 | EXP-3 |
| A-4 | User role data is 78% complete; 22% of users need fallback behavior | Partially Confirmed | Role-based delivery (FR-5 through FR-8) requires fallback rule for users without role data | ASM-4 | EXP-4 |
| A-5 | A standard priority taxonomy works for most users without per-user customization | Confirmed | Need per-user customization (violates NG-5) | ASM-5 | EXP-5 |
| A-6 | Notification improvements can be delivered without UX redesign | Untested | UX redesign extends scope and timeline; may need phased delivery | ASM-6 | — |
| A-7 | This initiative is independent of the Q3 Activity Feed Redesign | Untested | Work may be duplicated or need coordination | ASM-7 | — |

---

## 9. Out of Scope by Default

Anything not explicitly listed in §3 (Goals) and §6 (Requirements) is out of scope by default. This is the default rule — no implied scope exists.

Notable items that are explicitly **not** in scope:
- Machine learning or AI-based notification personalization
- Notification analytics dashboard for end users
- Slack, Teams, or third-party channel integrations for notifications
- Retrospective notification cleanup (clearing old notification backlogs)

---

## 10. Open Questions

**OQ-1: What is the specific priority taxonomy for notification classification?**
- **Status:** Unresolved
- **Blocking:** No — the taxonomy (Critical/Important/Informational) is defined at a category level. Specific event-type-to-priority mappings will be defined during engineering design and are implementation details.

**OQ-2: How should role be determined when the user profile role field is incomplete?**
- **Status:** Resolved
- **Blocking:** No
- **Resolution:** EL EXP-4 confirmed 22% of users have no role set. Default to "Contributor" behavior for unset roles. Whether to prompt users to set their role is deferred to a future enhancement.

**OQ-3: What is the optimal digest frequency for Informational notifications?**
- **Status:** Unresolved
- **Blocking:** No — FR-4 specifies daily digest as default. Exact timing is an implementation decision.

All blocking questions from upstream artifacts have been resolved or determined to be non-blocking for this document's purposes.

---

## 11. Acceptance / Success Criteria

| ID | Criterion | Measurement Method | VH Metric Trace |
|----|----------|-------------------|-----------------|
| AC-1 | Percentage of users with all notifications disabled decreases from 12% to below 6% within 60 days of launch | In-app analytics — notification preferences dashboard | SM-1 |
| AC-2 | >30% of users who previously disabled all notifications re-enable at least one channel within 60 days | In-app analytics — track users who had all channels disabled at launch | SM-2 |
| AC-3 | PM self-reported notification actionability increases from <20% to >50% within 60 days | Post-launch in-app survey at 30 and 60 days | SM-3 |
| AC-4 | Notification-related support tickets decrease by at least 40% within 60 days | Helpdesk analytics — notification category tag | SM-4 |
| AC-5 | Mid-market churn rate decreases by at least 1 percentage point within two quarters of launch | Standard quarterly churn reporting | SM-5 |
| AC-6 | "Notification overload" drops from top 3 reasons in mid-market exit surveys | Exit survey analysis — quarterly | SM-6 |

---

## 12. Freeze Declaration

| Field | Value |
|-------|-------|
| Frozen | Yes |
| Freeze Date | 2026-02-20 |
| Approved By | Sarah Chen, VP of Product |

This Discovery PRD has been validated against the Product Intelligence Kit's specification (including all Engineering Execution Kit downstream hard gates), reviewed, and approved. It is now the authoritative requirements document for the TaskFlow notification improvement initiative and is ready for handoff to the Engineering Execution Kit.
