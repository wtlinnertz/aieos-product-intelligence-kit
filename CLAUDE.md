# CLAUDE.md — Product Intelligence Kit

## What This Repository Is

This is the **Product Intelligence Kit** — an AIEOS kit that governs the transformation of strategic intent into engineering-ready product requirements. It follows the AIEOS governance model.

## Repository Structure

```
docs/
  principles/          # Organizational policy (input material)
  specs/               # Content rules and hard gates per artifact type
  artifacts/           # Templates and intake forms
  prompts/             # AI generation + utility prompts
  validators/          # Quality gate definitions
  meta/                # Non-governed meta documents (kit genesis, bootstrapping records)
  playbook.md          # End-to-end process definition
  index.md             # Documentation entry point
  how-to-adapt.md      # Organizational adoption guidance
  how-to-use-with-ai.md # AI tool usage guide
  governance-model.md  # AIEOS structural rules (reference)
examples/              # Worked example (TaskFlow notification scenario)
tests/                 # Structural integrity checks
```

## Artifact Types

This kit produces five artifact types in sequence:

1. **Problem Framing Document (PFD)** — Structures the problem space
2. **Value Hypothesis (VH)** — Defines testable value bets
3. **Assumption Register (AR)** — Catalogs and risk-assesses assumptions
4. **Experiment Log (EL)** — Records assumption validation results
5. **Discovery PRD (DPRD)** — Engineering-ready requirements (handoff to Engineering Execution Kit)

Each artifact type has exactly four governing files: spec, template, prompt, validator.

## Utility Prompts

Five utility prompts support the flow but do not produce governed artifacts:

- **Brownfield Analysis** (`brownfield-analysis-prompt.md`) — Analyzes existing systems to pre-fill intake forms
- **Stakeholder Alignment** (`stakeholder-alignment-prompt.md`) — Surfaces and classifies stakeholder conflicts
- **Assumption Stress Test** (`assumption-stress-test-prompt.md`) — Adversarial analysis of assumptions before experiments
- **Cross-Initiative Conflict** (`cross-initiative-conflict-prompt.md`) — Detects assumption conflicts across parallel initiatives
- **Initiative Prioritization** (`initiative-prioritization-prompt.md`) — Compares and ranks competing initiatives

Note: Work Classification is a **governed artifact** (Step 0), not a utility prompt. It has a spec, template, prompt, and validator. See Artifact Flow below.

## Key Rules

- **Specs are the source of truth** — prompts and validators reference specs, never inline rules
- **Validators judge, they do not help** — no suggestions, no redesign
- **Freeze before promote** — upstream artifacts must be frozen before downstream generation
- **Separate generation and validation** — different AI sessions to prevent self-validation bias
- **No scope expansion** — downstream artifacts must not expand scope beyond upstream
- **No inferred information** — mark missing information explicitly, do not fill gaps
- **Governance model sync** — `docs/governance-model.md` is a synchronized copy of `aieos-spec/governance-model.md`, which is the canonical authority. Do not edit the kit copy directly — update `aieos-spec` first, then sync all kit copies to match exactly. See governance-model.md §15 for versioning and change protocol.
- **Engagement Record** — PIK creates the ER (`docs/engagement/er-{initiative}.md` in the consuming project) when Discovery Intake is validated, and updates it as each Layer 2 artifact freezes. See `docs/playbook.md §Maintaining the Engagement Record` and `aieos-spec/docs/engagement-record-spec.md`.

## Artifact Flow

```
Step 0: Work Classification Record → validate → freeze → route
Discovery Intake (human) → validate intake → PFD → validate → freeze
                    → VH → validate → freeze
                    → AR → validate → freeze → [stress test]
                    → EL → validate → freeze → [proceed/pivot/pause]
                    → DPRD → validate → freeze → handoff
```

## Boundary Contracts

- **Upstream:** Discovery Intake Form validated against `docs/specs/discovery-intake-spec.md` (6 hard gates). This is the upstream boundary contract — upstream teams can produce validated intake artifacts independently.
- **Downstream:** Produces a frozen Discovery PRD that satisfies the Engineering Execution Kit's PRD specification (8 hard gates). The DPRD is delivered as `docs/sdlc/01-prd.md` in the consuming project and validated by the EEK's `prd-validator.md` as an acceptance check. See `docs/playbook.md` §Downstream Handoff for full mechanics and cross-kit re-entry protocol. Note: EEK requires a **Kit Entry Record** (Step 0 gate) before artifact generation begins — teams receiving the DPRD via Path A should expect this gate and have a classification record or justification ready.

## File Naming

| Type | Pattern |
|------|---------|
| Spec | `{type}-spec.md` |
| Template | `{type}-template.md` |
| Prompt | `{type}-prompt.md` |
| Validator | `{type}-validator.md` |
| Utility Prompt | `{function}-prompt.md` |

## When Working on This Kit

- Read the playbook (`docs/playbook.md`) for the full process definition
- Read the governance model (`docs/governance-model.md`) for structural rules
- Check `docs/how-to-use-with-ai.md` for session setup instructions
- Reference `examples/` for a complete worked example

## Building or Auditing AIEOS Kits

- `aieos-spec/docs/kit-structure-standard.md` — compliance checklist for building and auditing kits
- `aieos-spec/docs/philosophy.md` — design rationale for governance model decisions
- `aieos-spec/docs/layer-model.md` — seven-layer model and kit registry
