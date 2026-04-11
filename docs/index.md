# Product Intelligence Kit — Documentation Index

The Product Intelligence Kit governs the transformation of strategic intent into engineering-ready product requirements. It produces five artifact types in sequence, culminating in a Discovery PRD that satisfies the Engineering Execution Kit's intake requirements.

---

## Quick Navigation

### Process
- [Playbook](playbook.md) — Artifact flow, freeze points, re-entry protocol

### Principles (Organizational Policy)
- [Product Discovery Principles](principles/product-discovery-principles.md)
- [Hypothesis-Driven Development](principles/hypothesis-driven-development.md)
- [Compliance Discovery Principles](principles/compliance-discovery-principles.md) — Interpretive guidance for regulatory/compliance initiatives

### Artifact Types

#### Problem Framing Document (PFD)
- [Spec](specs/problem-framing-spec.md) — Content rules and hard gates
- [Template](artifacts/problem-framing-template.md) — Document structure
- [Prompt](prompts/problem-framing-prompt.md) — AI generation instructions
- [Validator](validators/problem-framing-validator.md) — Quality gate evaluation

#### Value Hypothesis (VH)
- [Spec](specs/value-hypothesis-spec.md)
- [Template](artifacts/value-hypothesis-template.md)
- [Prompt](prompts/value-hypothesis-prompt.md)
- [Validator](validators/value-hypothesis-validator.md)

#### Assumption Register (AR)
- [Spec](specs/assumption-register-spec.md)
- [Template](artifacts/assumption-register-template.md)
- [Prompt](prompts/assumption-register-prompt.md)
- [Validator](validators/assumption-register-validator.md)

#### Experiment Log (EL)
- [Spec](specs/experiment-log-spec.md)
- [Template](artifacts/experiment-log-template.md)
- [Prompt](prompts/experiment-log-prompt.md)
- [Validator](validators/experiment-log-validator.md)

#### Discovery PRD (DPRD)
- [Spec](specs/discovery-prd-spec.md)
- [Template](artifacts/discovery-prd-template.md)
- [Prompt](prompts/discovery-prd-prompt.md)
- [Validator](validators/discovery-prd-validator.md)

### Utility Prompts
- [Work Classification](prompts/work-classification-prompt.md) — Classify and route incoming work requests
- [Brownfield Analysis](prompts/brownfield-analysis-prompt.md) — Analyze existing systems to pre-fill intake forms
- [Stakeholder Alignment](prompts/stakeholder-alignment-prompt.md) — Surface and classify stakeholder conflicts
- [Assumption Stress Test](prompts/assumption-stress-test-prompt.md) — Adversarial analysis of assumptions
- [Cross-Initiative Conflict Detection](prompts/cross-initiative-conflict-prompt.md) — Identify assumption conflicts across initiatives
- [Initiative Prioritization](prompts/initiative-prioritization-prompt.md) — Compare and rank competing initiatives

### Intake Forms
- [Discovery Intake Form](artifacts/discovery-intake-template.md) — Human input for starting the discovery flow
- [Intake Spec](specs/discovery-intake-spec.md) — Upstream boundary contract (hard gates for valid intake)
- [Intake Validator](validators/discovery-intake-validator.md) — Validates intake form completeness

### Guides
- [How to Adapt](how-to-adapt.md) — Organizational adoption guidance
- [How to Use with AI](how-to-use-with-ai.md) — AI tool usage guide
- [Session Setup](session-setup.md) — Per-artifact setup checklists, pre-flight gate checks, and common failure reminders
- [Troubleshooting](troubleshooting.md) — Gate failure remediation guide
- [Entry from IEK](entry-from-iek.md) — Boundary briefing when arriving from the Insight & Evolution Kit (re-discover signal)

### Reference
- [Governance Model](governance-model.md) — AIEOS structural rules
- [Examples](../examples/) — Worked example of the full flow
- [Tests](../tests/) — Structural integrity checks
