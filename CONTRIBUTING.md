# CONTRIBUTING

Thank you for your interest in contributing to the **Product Intelligence Kit**.

This repository is a **public, employer-neutral toolkit** for AI-assisted product discovery artifacts, validators, and workflows. Contributions are welcome, provided they follow the rules below.

---

## Guiding Principles

All contributions must uphold these principles:

- **AI generates, validators decide**
- **Specs are the source of truth — prompts and validators reference, never inline**
- **Validators judge; they do not help**
- **Freeze before promote — upstream artifacts must be frozen before downstream generation**
- **Ambiguity is a failure condition**
- **Anonymization is mandatory**

If a contribution weakens these principles, it will not be accepted.

---

## What You Can Contribute

### Documentation
- Clarifications or improvements to existing docs
- New explanations that improve understanding
- Diagrams that reflect the documented flow

### Templates
- Improvements to existing artifact templates
- Template refinements that improve structure clarity

### Validators
- Validator improvements that reduce false positives, improve determinism, or strengthen scope enforcement
- New hard gate definitions that are observable and unambiguous

### Prompts
- Generation prompt improvements that better reference specs and templates
- New utility prompts that support the discovery flow without producing governed artifacts

### Examples
- Anonymized examples demonstrating correct usage
- Full artifact traces through the discovery flow
- Validator PASS/FAIL examples

### Principles
- New organizational policy files that can be optionally included in discovery sessions
- Refinements to existing principles that reflect common discovery patterns

---

## What You Should NOT Contribute

The following will be rejected:

- Employer-specific content
- Proprietary system names, workflows, or terminology
- Tool-specific implementations disguised as standards
- Changes that weaken validator strictness or add "helpful" language to validators
- New artifact types without a corresponding four-file implementation (spec, template, prompt, validator)
- Large architectural rewrites without prior discussion

---

## Anonymization Requirements (MANDATORY)

All contributions must comply with **`ANONYMIZATION.md`**.

Before submitting a PR, confirm:
- No company names or internal acronyms appear
- No internal URLs, domains, or identifiers appear
- All examples use approved placeholders
- No screenshots or logs expose identifiers

Violations may result in immediate rejection or removal.

---

## Contribution Workflow

### 1. Fork and Branch
- Fork the repository
- Create a branch from `main`
- Use a descriptive branch name:
  - `docs/…`
  - `template/…`
  - `validator/…`
  - `prompt/…`
  - `example/…`

### 2. Make Your Changes
- Keep changes small and focused
- One logical improvement per PR
- Do not bundle unrelated changes

### 3. Validate Your Contribution
Before opening a PR, ensure:
- Content aligns with existing terminology (`TERMS.md`)
- Examples follow anonymization rules
- Templates and validators align with the playbook
- No contradictions or scope creep introduced
- If adding a new artifact type: all four files are present (spec, template, prompt, validator)

### 4. Open a Pull Request
Your PR description should include:
- What problem this change solves
- Which documents are affected
- Any intentional trade-offs
- AI Usage Disclosure (if AI tools assisted in drafting)

PRs without a clear purpose may be closed.

---

## Review Expectations

Maintainers will review contributions for:

- Alignment with the governance model and playbook
- Clarity and determinism
- Anonymization compliance
- Appropriateness for a public, reusable kit

Maintainers may request changes or reject PRs that:
- Introduce ambiguity
- Weaken validation strictness
- Embed organization-specific assumptions
- Violate the four-file system

---

## Style & Formatting

- Use Markdown
- Prefer bullet points over long prose
- Keep language precise and unambiguous
- Avoid marketing language
- Favor enforceable rules over guidance where possible

---

## AI Usage in Contributions

You may use AI tools to assist in drafting content, provided that:

- You review all AI-generated output
- You ensure anonymization compliance
- You do not paste proprietary material into AI tools
- You take responsibility for the final content

---

## Reporting Issues

If you find:
- Anonymization violations
- Ambiguities in templates or validators
- Inconsistencies across documents
- Cross-references that violate the governance model

Please open an issue with a clear description and reference to the affected file(s).

---

## Code of Conduct

This project follows the **Code of Conduct** defined in `CODE_OF_CONDUCT.md`.

---

## Final Note

This repository prioritizes **clarity, rigor, and reuse** over speed or novelty.

If you are unsure whether a contribution fits, open an issue first and start a discussion.
