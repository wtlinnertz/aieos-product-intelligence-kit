# Discovery Intake Form — Worked Example

**Scenario:** A B2B SaaS project management platform ("TaskFlow") is experiencing high churn among mid-market customers. The team believes poor notification management is a contributing factor.

---

## Problem Context

### What is the problem?
Project managers and team members on our platform miss critical task updates because our notification system sends too many low-value notifications. Users either disable notifications entirely (and miss important ones) or leave them on (and experience notification fatigue). This leads to missed deadlines, dropped handoffs, and frustrated users.

### Who experiences this problem?
- **Project managers** who need to stay aware of blockers, deadline risks, and team status changes. They receive 80-150 notifications per day and report that fewer than 20% are actionable.
- **Team contributors** who need to know when tasks are assigned, when blockers are cleared, and when their input is needed. They receive 30-60 notifications per day and frequently miss assignment notifications buried in noise.
- **Executive stakeholders** who check in on project status periodically. They receive summary-level notifications but report they are too frequent and not focused on what matters to them.

### Why does this matter now?
- Q3 churn analysis shows "notification overload" is the #2 reason cited in exit surveys (behind pricing), mentioned by 34% of churned mid-market accounts
- Three enterprise prospects in the current pipeline have specifically asked about notification customization during evaluations
- Competitor "ProjectPro" launched intelligent notifications last quarter and is using it as a primary differentiator in sales conversations

### What evidence do we have?
- Exit survey data: 34% of churned mid-market accounts cite notification overload (Q3 data, n=47)
- In-app analytics: 41% of users have disabled at least one notification channel; 12% have disabled all notifications
- Support ticket analysis: notification-related tickets are the 3rd most common category (8% of all tickets)
- User interviews: 8 interviews conducted in October with mid-market PMs, 7 of 8 described notification management as "a daily frustration"
- NPS comments: 23 verbatim mentions of notifications in Q3 detractor comments

---

## Users and Stakeholders

### Primary users
- **Project managers (mid-market accounts):** Manage 3-8 concurrent projects with 5-25 team members each. They need to quickly identify which updates require action vs. which are informational. Currently cope by checking the platform constantly rather than relying on notifications.
- **Team contributors:** Individual contributors on project teams. Need to know when something is assigned to them or when a blocker they reported is resolved. Currently cope by asking PMs directly rather than trusting notifications.

### Secondary users
- **Executive stakeholders:** Check project status weekly or bi-weekly. Want high-level progress and risk alerts, not task-level noise. Currently cope by asking PMs for verbal updates.

### Sponsor
- VP of Product, Sarah Chen

---

## Opportunity

### How big is this opportunity?
- **Churn reduction estimate:** If we address the #2 churn reason, we estimate retaining 15-25% of the mid-market accounts that would otherwise churn, worth approximately $180K-$300K ARR annually
- **Pipeline conversion:** 3 enterprise prospects with a combined deal value of $420K have asked about notification improvements
- **Support cost reduction:** Reducing notification-related support tickets (currently ~120/month) by 50% would save approximately 60 support hours/month

### Strategic alignment
- Aligns with FY26 strategic priority: "Reduce mid-market churn rate from 8.2% to 5.5%"
- Supports product roadmap theme: "Intelligence layer" — making the platform smarter about what surfaces to users

---

## Current State

### How is the problem handled today?
- Users can toggle notification channels on/off (email, in-app, mobile push) at the account level
- There is a single "notification preferences" page with ~30 toggles for different event types
- No priority or relevance filtering exists — all notifications of an enabled type are delivered
- No batching or digesting — each event generates an immediate notification

### What has been tried before?
- In 2024 Q1, we added the granular toggle page (30 toggles). Support tickets about notifications decreased by 15% initially but returned to previous levels within 2 months. Users reported the toggles were too complex and they defaulted to "all on" or "all off."
- We have not attempted any intelligent filtering, prioritization, or batching.

### Existing system context
- Notification service is an internal microservice processing ~2M notification events/day
- Event types are well-structured with metadata (project, task, user, action type, timestamp)
- Current architecture supports channel routing but not content-based filtering or prioritization

---

## Scope and Boundaries

### What is in scope?
- Understanding and addressing the notification overload problem for mid-market customers
- Improving notification relevance and reducing noise
- Supporting the three primary user types identified above

### What is explicitly out of scope?
- Enterprise-specific notification features (SSO-gated notification policies, admin-controlled rules) — these will be a separate initiative if needed
- Pricing changes or packaging adjustments
- Changes to the underlying notification infrastructure architecture (this initiative defines what, not how)

### Known constraints
- No regulatory or compliance constraints specific to notifications (standard data privacy applies)
- Budget: allocated within existing Q1-Q2 product engineering capacity (no additional headcount)
- Timeline: solution must be defined and ready for engineering by end of Q1; delivery target is mid-Q2
- Must not break existing notification preferences — users who have configured toggles must not lose their settings

---

## Assumptions and Risks

### What are we assuming to be true?
- Notification overload is a causal factor in churn, not just a correlated complaint
- Users would re-enable notifications if they were more relevant (rather than having permanently lost trust in the notification system)
- The existing notification event metadata is rich enough to support intelligent filtering without significant infrastructure changes

### What could go wrong?
- Churn may be driven primarily by pricing, and notification improvements may not move the needle
- Users may have already developed workarounds (checking the app directly) and may not change behavior even with better notifications
- Scope could expand if we discover the underlying notification infrastructure cannot support the required changes

---

## Additional Context

### Reference documents
- Q3 Churn Analysis Report (internal)
- October User Interview Synthesis (8 interviews)
- Notification Service Technical Overview (architecture doc)
- Competitor Analysis: ProjectPro Intelligent Notifications (competitive intel)

### Related initiatives
- "Activity Feed Redesign" — planned for Q3, focuses on the in-app activity feed. Notification improvements should be compatible with but not dependent on this initiative.

---

## Completeness Checklist

- [x] Problem is clearly described in concrete terms
- [x] At least one affected user group is identified
- [x] "Why now" rationale is provided
- [x] Some evidence basis exists (even if limited)
- [x] Scope boundaries are stated (in scope and out of scope)
- [x] Known constraints are listed
