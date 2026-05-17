# aieos-product-intelligence-kit

The **Product Intelligence Kit** governs the space between strategic intent and engineering-ready product requirements. It's part of the [AIEOS](https://github.com/your-org/aieos) system.

## What this kit does

This kit transforms a product problem into a validated, engineering-ready Product Requirements Document (PRD) through a structured discovery process. It produces five artifacts in sequence:

1. **Problem Framing Document** — Structures the problem space, users, pain points, and opportunity
2. **Value Hypothesis** — Defines testable bets about what will create value
3. **Assumption Register** — Catalogs assumptions with risk levels and validation plans
4. **Experiment Log** — Records assumption validation results and evidence
5. **Discovery PRD** — Engineering-ready requirements that satisfy the Engineering Execution Kit's PRD specification

Two utility prompts support the flow:

- **Work Classification** — Routes incoming work to the right process (avoids busywork)
- **Assumption Stress Test** — Adversarial analysis to strengthen assumptions before experiments

## Quick start

1. Optionally run the [Work Classification Prompt](docs/prompts/work-classification-prompt.md) to determine if this work needs full discovery
2. Fill out the [Discovery Intake Form](docs/artifacts/discovery-intake-template.md)
3. Follow the [Playbook](docs/playbook.md) to generate, validate, and freeze each artifact in sequence
4. See [How to Use with AI](docs/how-to-use-with-ai.md) for step-by-step AI session instructions
5. Review the [worked example](examples/) for a complete flow

## Documentation

| Document | Description |
|----------|-------------|
| [Playbook](docs/playbook.md) | Artifact flow, freeze points, re-entry protocol |
| [Index](docs/index.md) | Full documentation navigation |
| [How to Adapt](docs/how-to-adapt.md) | Customize the kit for your organization |
| [How to Use with AI](docs/how-to-use-with-ai.md) | AI session setup and workflow |
| [Governance Model](docs/governance-model.md) | AIEOS structural rules |

## Artifact specifications

| Artifact | Spec | Template | Prompt | Validator |
|----------|------|----------|--------|-----------|
| Problem Framing | [spec](docs/specs/problem-framing-spec.md) | [template](docs/artifacts/problem-framing-template.md) | [prompt](docs/prompts/problem-framing-prompt.md) | [validator](docs/validators/problem-framing-validator.md) |
| Value Hypothesis | [spec](docs/specs/value-hypothesis-spec.md) | [template](docs/artifacts/value-hypothesis-template.md) | [prompt](docs/prompts/value-hypothesis-prompt.md) | [validator](docs/validators/value-hypothesis-validator.md) |
| Assumption Register | [spec](docs/specs/assumption-register-spec.md) | [template](docs/artifacts/assumption-register-template.md) | [prompt](docs/prompts/assumption-register-prompt.md) | [validator](docs/validators/assumption-register-validator.md) |
| Experiment Log | [spec](docs/specs/experiment-log-spec.md) | [template](docs/artifacts/experiment-log-template.md) | [prompt](docs/prompts/experiment-log-prompt.md) | [validator](docs/validators/experiment-log-validator.md) |
| Discovery PRD | [spec](docs/specs/discovery-prd-spec.md) | [template](docs/artifacts/discovery-prd-template.md) | [prompt](docs/prompts/discovery-prd-prompt.md) | [validator](docs/validators/discovery-prd-validator.md) |

## Utility prompts

| Prompt | Purpose |
|--------|---------|
| [Work Classification](docs/prompts/work-classification-prompt.md) | Classify incoming work and route to appropriate process |
| [Brownfield Analysis](docs/prompts/brownfield-analysis-prompt.md) | Analyze existing systems to pre-fill intake forms |
| [Stakeholder Alignment](docs/prompts/stakeholder-alignment-prompt.md) | Surface and resolve conflicting stakeholder perspectives |
| [Assumption Stress Test](docs/prompts/assumption-stress-test-prompt.md) | Adversarial analysis of assumptions before experiments |
| [Cross-Initiative Conflict](docs/prompts/cross-initiative-conflict-prompt.md) | Detect assumption conflicts across parallel initiatives |
| [Initiative Prioritization](docs/prompts/initiative-prioritization-prompt.md) | Compare and rank competing initiatives for resource decisions |

## Boundary contracts

- **Upstream:** Discovery Intake Form validated against [intake spec](docs/specs/discovery-intake-spec.md) (6 hard gates)
- **Downstream:** Produces a frozen Discovery PRD for the [Engineering Execution Kit](https://github.com/your-org/aieos-engineering-execution) (8 hard gates)

## License

See [LICENSE](LICENSE).
