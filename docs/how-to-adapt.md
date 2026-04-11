# How to Adapt the Product Intelligence Kit

This guide helps organizations adopt and customize the Product Intelligence Kit for their context.

---

## What Can Be Adapted

### Principles (Fully Customizable)
The files in `docs/principles/` represent your organization's product discovery standards. These are input material — they inform artifact generation but are not governed artifacts. Modify them freely to reflect your organization's values and practices.

Examples of customization:
- Adjust the evidence standards to match your research maturity
- Modify opportunity sizing expectations for your industry
- Add domain-specific hypothesis formation guidelines

### Templates (Structure Customizable, Section Headings Fixed)
Templates define document structure. You may:
- Add guidance text within placeholder sections
- Add sub-sections within existing sections
- Adjust table column headers for clarity

You must not:
- Remove required sections
- Rename section headings (these are referenced by prompts and validators)
- Add content rules to templates (those belong in specs)

### Prompts (Behavior Customizable)
Prompts define how AI generates artifacts. You may:
- Add domain-specific extraction guidance
- Adjust tone and style instructions
- Add examples of good output
- Add organization-specific terminology

You must not:
- Inline content rules (those belong in specs)
- Remove references to specs and templates
- Add instructions that contradict the spec

---

## What Must Not Be Adapted

### Specs (Core Rules Fixed)
Specs define the hard gates and content rules. Modifying specs changes what "good" means for the entire system. Changes to specs require:
- Impact analysis on prompts and validators that reference the spec
- Re-validation of any existing artifacts produced under the old spec
- Version bump (minor for new gates, major for changed gates)

### Validators (Judgment Logic Fixed)
Validators must evaluate against specs exactly. If you change a spec, update the corresponding validator. Never make validators "helpful" or "lenient."

### Artifact Flow (Sequence Fixed)
The five-artifact sequence (PFD → VH → AR → EL → DPRD) and the freeze-before-promote rule are structural. Changing the flow requires understanding the dependency chain — each downstream artifact has hard-gate dependencies on all upstream artifacts.

### Hard Gates (Quality Bar Fixed)
Hard gates define the minimum quality bar. Removing a hard gate lowers the quality floor for all artifacts. Add gates if your organization needs stricter standards, but do not remove existing ones.

---

## Common Adaptations

### Lightweight Mode
For smaller initiatives where full rigor is excessive:
- The playbook still applies — do not skip artifacts
- Artifacts may be shorter, but all required sections and hard gates still apply
- The Discovery Intake Form must still pass intake validation (6 hard gates), but responses can be concise
- The Discovery Intake Form may have many optional sections marked "Not applicable"
- The Experiment Log may document a single rapid validation (e.g., one data pull or three quick interviews) rather than a multi-week research program
- Use the Work Classification prompt to confirm that full discovery is warranted
- Consider this the minimum viable discovery process

### Enterprise Mode
For large, high-stakes initiatives:
- Add more detailed intake questions to the Discovery Intake Form
- Add additional principles files for domain-specific policy (e.g., `regulatory-discovery.md`)
- Consider splitting the Assumption Register into domain-specific registers (but each must still follow the four-file system)
- Add stakeholder review gates between artifacts (document in your playbook adaptation)

### Compliance Mode
For regulatory, legal, or policy-driven initiatives:
- Include `docs/principles/compliance-discovery-principles.md` in all generation sessions
- The principles file provides interpretive guidance for each artifact type (e.g., "Opportunity Sizing" becomes "Risk Exposure," hypotheses reference regulatory clauses)
- All specs, templates, and hard gates remain unchanged — the principles file guides how to fill them appropriately
- See the compliance principles file for detailed guidance on PFD, VH, AR, EL, and DPRD adaptation

### Brownfield Adaptation
For initiatives involving existing systems:
- Use `docs/prompts/brownfield-analysis-prompt.md` to analyze existing system documentation
- The analysis output maps to Discovery Intake Form sections
- Human review of pre-filled intake is mandatory
- The PFD's "Current State" section becomes especially important

### Adding Tool Bindings
When mapping kit concepts to specific tools (Jira, Notion, Confluence, etc.):
- Create files in `docs/bindings/` (create the directory if needed)
- Keep bindings out of specs, templates, prompts, and validators
- Example: `docs/bindings/jira-mapping.md` maps PFD/VH/AR/DPRD to Jira issue types

---

## Versioning Your Adaptations

Follow semantic versioning:
- **Major**: Changes to hard gates, required sections, or artifact flow
- **Minor**: New principles files, template sub-sections, prompt enhancements
- **Patch**: Typo fixes, clarifications, example updates

Track your version in the repository's release tags or changelog.
