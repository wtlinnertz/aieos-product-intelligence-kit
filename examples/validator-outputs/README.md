# Validator Output Examples

This directory contains sample validator outputs for all PIK artifact types.

These files demonstrate:
- What a PASS looks like
- What a FAIL looks like and why
- How validators report blocking issues
- How completeness scores are expressed

All outputs:
- Follow the standardized validator JSON schema
- Contain no suggestions or redesign — only observations about what is present or absent
- Reference only missing, ambiguous, or non-compliant content

---

## Included Validators

| Artifact | PASS | FAIL |
|----------|------|------|
| Discovery Intake | `discovery-intake-validator-pass.json` | `discovery-intake-validator-fail.json` |
| Problem Framing Document | `problem-framing-validator-pass.json` | `problem-framing-validator-fail.json` |
| Value Hypothesis | `value-hypothesis-validator-pass.json` | `value-hypothesis-validator-fail.json` |
| Assumption Register | `assumption-register-validator-pass.json` | `assumption-register-validator-fail.json` |
| Experiment Log | `experiment-log-validator-pass.json` | `experiment-log-validator-fail.json` |
| Discovery PRD | `discovery-prd-validator-pass.json` | `discovery-prd-validator-fail.json` |

All examples use the TaskFlow Intelligent Notification System scenario — the same scenario traced through `examples/01-discovery-intake.md` through `examples/06-discovery-prd.md`.

---

## How to Use These Examples

- Compare your validator output to these samples to calibrate expected behavior
- Use FAIL examples to understand what a blocking issue looks like before running your first validation
- Use them to calibrate AI agent behavior when running validators
- Use them to explain validator enforcement to stakeholders unfamiliar with the system

These outputs are illustrative, not exhaustive.
