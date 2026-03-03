# Compliance Discovery Principles

This document provides interpretive guidance for using the Product Intelligence Kit when the initiative is driven by regulatory, legal, or policy requirements. It is input material for artifact generation — not a governed artifact itself.

These principles do not replace or override the standard product discovery principles. They provide additional context for how standard artifact sections should be interpreted when the initiative is compliance-driven.

---

## When to Use This Document

Include this document in AI generation sessions when the Work Classification prompt has classified the initiative as "Compliance" or when the initiative is driven by:

- Regulatory requirements (GDPR, CCPA, SOX, HIPAA, PCI-DSS, etc.)
- Legal mandates (court orders, consent decrees, contractual obligations)
- Policy changes (internal governance, security policies, data handling policies)
- Audit findings (gaps identified during compliance audits)
- Enforcement actions (regulatory warnings, fines, or remediation orders)

---

## Artifact Interpretation for Compliance Initiatives

### Problem Framing Document (PFD)

**Problem Statement:** Frame the problem as the regulatory gap or non-compliance risk. "What regulation or requirement are we not meeting, and what is the exposure?"

**Why Now:** Compliance initiatives often have concrete urgency drivers:
- Regulatory enforcement deadline
- Audit finding with remediation timeline
- New regulation effective date
- Contractual obligation milestone
- Enforcement action or warning from regulators

**Opportunity Sizing:** For compliance work, opportunity sizing focuses on risk exposure rather than revenue opportunity:
- Financial exposure (fines, penalties, legal costs)
- Market access risk (inability to operate in regulated markets)
- Reputational risk (public disclosure of non-compliance)
- Operational risk (forced shutdown of non-compliant systems)
- Competitive disadvantage (competitors already compliant)

This reframing preserves the spec's requirement for "opportunity sizing with stated basis" while fitting the compliance context.

**Pain Points:** Compliance pain points may be forward-looking (risks of non-compliance) rather than current experience. This is acceptable — frame as: "If we do not address this, [specific consequence] will occur by [date/trigger]."

**Current State:** Describe the current compliance posture: what is compliant, what is not, what gaps exist, and what interim measures are in place.

### Value Hypothesis (VH)

**Hypothesis Structure:** Compliance hypotheses can follow this adapted pattern:

> "We believe that [implementation approach] will satisfy [regulatory requirement / compliance standard] as measured by [compliance metric / audit criteria]."

This preserves the falsifiable structure required by the spec while fitting compliance context. Examples:
- "We believe that implementing field-level encryption for PII will satisfy GDPR Article 32 data protection requirements as measured by passing the annual DPA audit."
- "We believe that adding a data subject rights API will satisfy CCPA §1798.100 within the 45-day response window as measured by automated compliance testing."

**Success Metrics:** Map to compliance acceptance criteria rather than user engagement:
- Audit pass/fail results
- Regulatory certification status
- Compliance test coverage
- Response time SLAs mandated by regulation
- Data accuracy standards required by regulation

**Falsification:** Compliance hypotheses are falsifiable when framed around implementation approach, not regulatory intent. The regulation itself is non-negotiable — but whether a specific approach satisfies it is testable.

### Assumption Register (AR)

**Assumption Categories:** For compliance initiatives, the "Regulatory" category becomes primary. Typical compliance assumptions include:

- **Legal interpretation assumptions:** "We interpret 'deletion' under GDPR Art. 17 to include soft-delete with anonymization" — these carry risk because regulators may interpret differently
- **Implementation feasibility assumptions:** "We can meet the 30-day data deletion SLA with our current infrastructure" — these are technical but driven by regulatory requirements
- **Scope interpretation assumptions:** "Our B2B customers' employee data is covered under this regulation" — these determine which data/systems are in scope
- **Timeline assumptions:** "The regulatory enforcement date will not be moved earlier" — these affect planning
- **Organizational assumptions:** "Legal and engineering will agree on the definition of 'reasonable security measures'" — these affect cross-functional work

**Risk Assessment:** Regulatory assumptions often carry higher baseline risk than product assumptions because the consequences of being wrong include legal liability, not just product underperformance.

### Experiment Log (EL)

**Validation Methods:** Compliance assumptions may be validated through methods different from standard product assumptions:

- **Legal review:** Outside counsel or internal legal team reviews interpretation assumptions
- **Regulatory consultation:** Pre-submission review or regulatory sandbox testing
- **Compliance audit:** Internal or third-party audit against the relevant standard
- **Technical proof-of-concept:** Testing whether implementation satisfies specific regulatory criteria
- **Benchmarking:** How have other organizations in the same regulatory context implemented this?

These are legitimate "experiments" under the EL spec — they have hypotheses, methods, findings, and conclusions.

### Discovery PRD (DPRD)

**Requirements Traceability:** Requirements should trace to both VH hypotheses AND specific regulatory clauses. Example:
- FR-1 traces to HYP-1 AND GDPR Art. 17(1)
- NFR-3 traces to HYP-2 AND PCI-DSS Requirement 3.4

**Non-Negotiable Requirements:** Some requirements in compliance DPRDs are non-negotiable — they are direct translations of regulatory mandates. Flag these explicitly:
- Mark as "Regulatory mandate — not subject to scope negotiation"
- These are different from requirements that emerge from product hypotheses (which can be deprioritized)
- The DPRD's non-goals section should clarify which regulatory requirements are explicitly out of scope for this initiative vs. covered by other initiatives

**Constraints:** Compliance DPRDs often have hard external constraints (deadlines, audit schedules, certification timelines) that product DPRDs don't. Document these as constraints, not as aspirational goals.

---

## Principles Specific to Compliance Discovery

### 1. Regulation Is Input, Not Output

The regulatory requirement is a given — it is not subject to the "pivot/pause" analysis that product hypotheses undergo. What IS subject to analysis: the interpretation of the regulation, the approach to satisfying it, and the scope of what's covered.

### 2. Legal Interpretation Is an Assumption

How the organization interprets a regulation is an assumption that belongs in the AR. Different legal teams may interpret the same regulation differently. Document the interpretation, the source (internal counsel, external counsel, regulatory guidance), and the risk of the interpretation being challenged.

### 3. Compliance Has External Deadlines

Unlike product initiatives where timelines are internally set, compliance initiatives often have hard external deadlines. These deadlines are constraints, not goals — they cannot be negotiated. The PFD's "why now" and the DPRD's constraints section must capture these.

### 4. Over-Compliance Is Waste

Just as the product discovery principles warn against "efficient waste" (building the wrong thing efficiently), compliance discovery must guard against over-compliance — implementing more than the regulation requires. The AR should include assumptions about scope: "We assume the regulation requires X but not Y."

### 5. Evidence Standards May Differ

Compliance evidence often comes from legal review and regulatory guidance rather than user research. This is acceptable — the EL spec requires "evidence-based conclusions," not specifically "user research-based conclusions." A legal opinion from qualified counsel is valid evidence.

---

## What This Document Does NOT Change

- **Specs are unchanged** — all hard gates still apply; compliance initiatives must still pass the same validators
- **Templates are unchanged** — all required sections are still required
- **Validators are unchanged** — compliance artifacts are judged by the same standards
- **The artifact flow is unchanged** — PFD → VH → AR → EL → DPRD sequence is required

This document provides interpretive guidance for how to fill the standard sections with compliance-appropriate content. It does not create exceptions to the governance model.
