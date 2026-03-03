# Product Discovery Principles

This document defines the organizational standards for product discovery. It is input material for artifact generation — not a governed artifact itself.

---

## 1. Problem Before Solution

Every product initiative begins with a structured understanding of the problem. Teams must articulate what problem exists, who experiences it, and why it matters before proposing solutions. Jumping to solutions without validated problem understanding is the most common cause of wasted engineering effort.

## 2. Evidence Over Opinion

Product decisions are grounded in evidence: user research, behavioral data, market analysis, and validated experiments. Where evidence is unavailable, the gap must be acknowledged explicitly and a plan to obtain evidence must be defined.

## 3. Explicit Assumptions

All assumptions must be made visible. Hidden assumptions are the primary source of product risk. Every assumption must be documented with:
- What is being assumed
- Why it is believed to be true
- What happens if it is false
- How it will be validated

## 4. Progressive Certainty

Discovery follows a deliberate progression from uncertainty to confidence:
- **Problem Framing**: Do we understand the problem?
- **Value Hypotheses**: Do we have testable bets about value?
- **Assumption Validation**: Have we identified and risk-assessed our assumptions?
- **Requirements Definition**: Can we define what to build with enough clarity to drive architecture?

Each stage reduces uncertainty. Skipping stages increases the risk of building the wrong thing.

## 5. Scope Discipline

Scope is defined by what is explicitly included and explicitly excluded. There is no implied scope. Non-goals are as important as goals — they prevent scope creep and protect engineering focus. Once scope is frozen, it may not be expanded without triggering the re-entry protocol.

## 6. User-Centered Framing

Problems are framed from the user's perspective. Requirements describe what users need to accomplish, not how the system should be built. Personas are not demographic profiles — they represent distinct need patterns and behavioral contexts.

## 7. Measurable Outcomes

Goals must be stated as measurable outcomes. "Improve the user experience" is not a goal. "Reduce task completion time by 30% for the primary workflow" is a goal. Success criteria must be objectively verifiable — if two reasonable people could disagree about whether a criterion is met, it is not specific enough.

## 8. Intellectual Honesty

Teams must distinguish between what they know, what they believe, and what they are guessing. Discovery artifacts make these distinctions explicit:
- **Known**: Supported by evidence or direct observation
- **Believed**: Supported by indirect evidence or experience
- **Assumed**: Taken as true without evidence, requiring validation

## 9. Appropriate Depth

The depth of discovery should match the stakes. A minor feature enhancement does not need the same rigor as a new product line. However, the minimum bar is always: clear problem statement, explicit scope, at least one functional and non-functional requirement, and documented assumptions.

## 10. Independence from Implementation

Discovery artifacts define intent, not implementation. They describe what problem to solve and what success looks like — never how to build it. Architecture and design are the domain of downstream kits. Discovery artifacts that prescribe solutions constrain engineering unnecessarily and are considered defective.
