# Ideation Workshop Prompt

**Type:** Utility prompt (not a governed artifact)

**Purpose:** Facilitate structured ideation when a user doesn't yet have a concrete idea to route through the AIEOS pipeline. Produces an Ideation Workshop Record that feeds directly into Discovery Intake.

**When to use:** Before Step 0 (WCR), when the user needs help generating or selecting ideas rather than classifying an existing one. The sherpa offers this when it detects ideation-mode signals.

**Output:** `docs/sdlc/00-ideation-workshop.md` — an operational record (not governed, no four-file system).

---

## Inputs

| Input | Required | Source |
|-------|----------|--------|
| User's product/team context | Yes | Conversational — ask the user |
| User's audience/customers | Yes | Conversational — ask the user |
| Current frustrations/pain points | Yes | Conversational — ask the user |
| Strategic constraints (timeline, budget, team) | Recommended | Conversational — ask the user |
| IEK Evolution Signals (frozen ES) | Optional | Sibling initiative `docs/engagement/` — only if prior AIEOS initiatives exist |
| RRK Reliability Health Reports (frozen RHR) | Optional | Sibling initiative `docs/engagement/` — only if prior AIEOS initiatives exist |
| ODK Postmortem Records (frozen PMR) | Optional | Sibling initiative `docs/engagement/` — only if prior AIEOS initiatives exist |

**When no AIEOS history exists:** Skip signal inputs entirely. 5 of 7 techniques work without any prior AIEOS artifacts. Signal Synthesis is deprioritized; the sherpa substitutes a conversational "what signals are you seeing?" question instead.

---

## Technique Library

Select 2–3 techniques per session based on context. Do not run all 7 — ideation fatigue reduces quality after the third technique.

### 1. Signal Synthesis

**Best for:** Teams with existing AIEOS initiatives producing IEK, RRK, or ODK signals.

**Skip when:** No prior AIEOS initiatives exist. Substitute with: "What patterns, complaints, or recurring problems are you seeing — from customers, your team, or your systems?"

**Process:**
1. Read available ES files — extract "re-discover" and "watch" signals with their discovery questions
2. Read available RHR files — extract recurring patterns and systemic issues
3. Read available PMR files — extract root cause themes and corrective action gaps
4. Present each signal as a potential opportunity: "{signal} → could become: {opportunity framing}"
5. Ask the user which signals resonate most

**Output per signal:** Signal source (artifact ID) → opportunity framing → user interest (high/medium/low)

### 2. Jobs-to-Be-Done Mapping

**Best for:** User-facing products, teams wanting to understand unmet needs.

**Process:**
1. Ask: "What are the main things your users use your product to accomplish? Think in terms of outcomes, not features."
2. For each "job," ask: "How well does your product do this today?" (well / adequately / poorly / can't do it)
3. Focus on "poorly" and "can't do it" jobs — these are the opportunities
4. For each opportunity: "If you could wave a magic wand, what would the ideal experience look like?"

**Output per job:** Job description → current performance → gap → ideal experience

### 3. Constraint Removal

**Best for:** Breaking incremental thinking, imagining possibilities beyond current limitations.

**Process:**
1. Ask: "If you had unlimited {budget / time / team / technology}, what would you build for your users?"
2. Let the user dream — do NOT filter or reality-check during this step
3. After capturing 3–5 big ideas, work backward for each: "What's the smallest version of this that would still be valuable?"
4. Score the minimum versions on feasibility

**Output per idea:** Dream version → minimum viable version → feasibility (high/medium/low)

### 4. Competitive Gap Analysis

**Best for:** Market-aware teams, products facing competitive pressure.

**Process:**
1. Ask: "Who are your main competitors or alternatives? (Include 'doing nothing' and 'manual workaround' as alternatives)"
2. For each competitor, ask: "What do they offer that you don't?"
3. For each competitor, ask: "What do you offer that they don't?"
4. Map gaps (they have, you don't) — which gaps matter most to your users?
5. Map differentiators (you have, they don't) — which could you strengthen?

**Output:** Gap table (competitor → capability → your status → user importance)

### 5. Technology Enablement Scan

**Best for:** Technical teams, teams aware of new AI/API/platform capabilities.

**Process:**
1. Ask: "What new technologies, APIs, or platforms have caught your attention in the last 12 months?"
2. For each technology, ask: "What does this make possible for your users that wasn't possible before?"
3. Map each enablement to a concrete product opportunity
4. Score on differentiation: would this be table stakes or a genuine differentiator?

**Output per technology:** Technology → new capability → product opportunity → differentiation (table stakes / differentiator / moonshot)

### 6. Inversion

**Best for:** Risk-aware teams, identifying defensive opportunities.

**Process:**
1. Ask: "What are the top 5 things that would make your users leave your product?"
2. For each risk, ask: "What would make that impossible — what would make users want to stay forever?"
3. Flip each defensive answer into an offensive opportunity
4. Score on urgency: is this risk imminent or theoretical?

**Output per risk:** User loss risk → retention solution → offensive opportunity → urgency (imminent / emerging / theoretical)

### 7. SCAMPER on Existing Capabilities

**Best for:** Enhancement-focused teams, mature products looking for innovation within existing scope.

**Process:**
1. List the product's top 5 existing capabilities
2. For each, apply the SCAMPER framework:
   - **S**ubstitute — what component could be replaced with something better?
   - **C**ombine — what if this feature merged with another?
   - **A**dapt — what if this worked in a different context?
   - **M**odify — what if we changed scale, speed, or scope?
   - **P**ut to other use — who else could benefit from this?
   - **E**liminate — what if we removed the most complex part?
   - **R**everse — what if the user's role was inverted?
3. Score the most promising mutations

**Output per capability:** Capability → SCAMPER transformations → most promising mutation → score

---

## Technique Selection Guide

| User Context | Recommended Techniques | Why |
|-------------|----------------------|-----|
| Has existing AIEOS initiatives | Signal Synthesis + one other | Leverage existing organizational learning |
| No AIEOS history, user-facing product | Jobs-to-Be-Done + Inversion | Grounds ideation in user needs and risks |
| No AIEOS history, technical team | Technology Enablement + Constraint Removal | Leverages technical awareness |
| Market pressure | Competitive Gap + SCAMPER | Maps competitive landscape and existing assets |
| Mature product, seeking innovation | SCAMPER + Constraint Removal | Finds new value in existing capabilities |
| Greenfield / new team | Jobs-to-Be-Done + Technology Enablement | Starts from user needs and available technology |

---

## Convergence

After running 2–3 techniques, converge:

1. **Collect all ideas** from all techniques into a single list
2. **Score each idea** with the user on three dimensions:
   - **Impact** (H/M/L) — how much value would this create for users?
   - **Confidence** (H/M/L) — how sure are we this would work?
   - **Effort** (H/M/L) — how much would it cost to build?
3. **Highlight top candidates** — ideas with High impact + at least Medium confidence
4. **Ask the user to select** one idea (or combine related ideas) for the pipeline

---

## Output Format

Save to `docs/sdlc/00-ideation-workshop.md`:

```markdown
# Ideation Workshop Record

| Field | Value |
|-------|-------|
| Date | {YYYY-MM-DD} |
| Techniques Used | {list of 2-3 techniques} |
| Participants | {human name(s) + AI} |
| Signal Inputs | {list of AIEOS signals used, or "None — no prior initiatives"} |

## Ideas Generated

| # | Idea | Source Technique | Impact | Confidence | Effort |
|---|------|-----------------|--------|------------|--------|
| 1 | {idea} | {technique name} | H/M/L | H/M/L | H/M/L |
| ... | | | | | |

## Top Candidates

### Candidate 1: {name}
{2-3 sentence description. What it does, who it's for, why now.}

### Candidate 2: {name}
{2-3 sentence description.}

## Selected Idea

| Field | Value |
|-------|-------|
| Idea | {chosen idea} |
| Rationale | {why this one over the others} |
| Next Step | WCR classification / Discovery Intake / Strategic Bet Record |
```

---

## Roadmap-Level Ideation

When the user is thinking at the roadmap level (product direction over 1-5 years, technology strategy, capability lifecycle), use these roadmap techniques instead of the initiative techniques above. The output feeds SDK artifacts (CLA, PCR, TIR) rather than PIK artifacts (WCR, Discovery Intake).

### R1. Future-Back Planning

**Best for:** Vision-driven teams, long-horizon roadmaps.

**Process:**
1. Ask: "Describe the ideal experience your users/customers have with your product in 3 years. What can they do that they can't today?"
2. Let the user paint the full picture without constraints
3. Work backward: "What capabilities must exist to deliver that experience?"
4. Sequence the capabilities: what must come first? what enables what?
5. Identify the first 2-3 capabilities that unlock the most downstream value

**Output per capability:** Vision element → Required capability → Dependencies → Sequence position

### R2. Capability Gap Mapping

**Best for:** Existing products, identifying where to invest.

**Process:**
1. List every "job" the product does today (from CLA if available, or conversationally)
2. For each: rate importance to users (critical/important/nice-to-have) and current performance (excellent/adequate/poor/missing)
3. Plot on a 2x2: high-importance + poor-performance = roadmap priority
4. For each priority gap: "What would 'excellent' look like?"

**Output per gap:** Job → Importance → Current Performance → Target State → Roadmap priority

### R3. Technology Horizon Scan

**Best for:** Technical teams planning 2-5 year technology strategy.

**Process:**
1. Ask: "What technologies are emerging now that you expect to be mainstream in 2-3 years?"
2. For each: "What does this enable for your product that's impossible or expensive today?"
3. Classify: table-stakes (must adopt to stay competitive) vs. differentiator (competitive advantage) vs. moonshot (high risk, high reward)
4. Map each to a concrete product capability it would enable

**Output per technology:** Technology → Maturity Timeline → Product Enablement → Classification → TIR recommendation (adopt/evaluate/watch)

### R4. Competitive Trajectory Projection

**Best for:** Market-aware teams, competitive positioning.

**Process:**
1. Ask: "Who are your main competitors? Include 'doing nothing' and 'switching to manual process' as alternatives."
2. For each: "Where are they investing? What will they likely offer in 2 years that they don't today?"
3. Map: where will you be differentiated (they can't match you) vs. commoditized (everyone has it) vs. behind (they have it, you don't)?
4. Roadmap implication: differentiated areas → invest to extend; commoditized → maintain or automate; behind → catch up or concede

**Output:** Competitor trajectory table → differentiation map → roadmap implications

### R5. Sunset Analysis

**Best for:** Overloaded teams, products with accumulated capability debt.

**Process:**
1. Ask: "What are you maintaining today that provides declining value? What would you STOP doing if you could?"
2. For each candidate: usage data (if available), maintenance cost (team time), strategic relevance (does it enable other capabilities?)
3. Classify: ready-to-sunset (low usage, low strategic value) / candidate (declining but dependencies exist) / keep (still needed)
4. For ready-to-sunset: estimate capacity freed (team-weeks per quarter)

**Output per candidate:** Capability → Usage → Cost → Strategic Relevance → Classification → Capacity Freed

### R6. Customer Journey Evolution

**Best for:** Customer-centric teams, products in changing markets.

**Process:**
1. Ask: "How does your customer's world change in the next 3 years? Think about: regulation, market dynamics, technology they use, their expectations."
2. For each change: "How must your product evolve to remain relevant?"
3. Map changes to capability requirements: new capabilities needed, existing capabilities that must change, capabilities that become irrelevant
4. Prioritize by: how certain is the change? how soon? how big is the impact?

**Output per change:** Customer world change → Product evolution required → Capability implications → Certainty × Urgency

### R7. Platform Leverage Analysis

**Best for:** Multi-product teams, teams seeking scale.

**Process:**
1. Ask: "What capabilities could you build once and use across multiple products, features, or teams?"
2. For each platform candidate: who are the consumers? what's the integration cost? what's the maintenance model?
3. Score: leverage ratio (number of consumers × value per consumer ÷ build cost)
4. Identify the top 2-3 platform investments with highest leverage

**Output per platform:** Platform capability → Consumers → Leverage Ratio → Build Cost → Maintenance Model

### Roadmap Technique Selection Guide

| Context | Techniques | Why |
|---------|-----------|-----|
| New product, no history | Future-Back + Customer Journey | Start from vision and market evolution |
| Existing product, feature-rich | Capability Gap + Sunset Analysis | Find investment priorities and free capacity |
| Technical strategy focus | Technology Horizon + Platform Leverage | Map technology investments to product value |
| Competitive pressure | Competitive Trajectory + Capability Gap | Understand positioning and close gaps |
| Overloaded team, too many things | Sunset Analysis + Platform Leverage | Reduce scope and find scale |
| Annual/quarterly planning cycle | Capability Gap + Future-Back + Sunset Analysis | Comprehensive: where are we, where do we want to be, what do we stop |

### Roadmap Convergence

Same as initiative convergence but with different scoring dimensions:

- **Strategic Value** (H/M/L) — how much does this move the product toward its vision?
- **Feasibility** (H/M/L) — can we realistically deliver this in the timeframe?
- **Urgency** (H/M/L) — what happens if we delay?

### Roadmap Output Format

Save to `docs/sdlc/00-roadmap-ideation.md`:

```markdown
# Roadmap Ideation Record

| Field | Value |
|-------|-------|
| Date | {YYYY-MM-DD} |
| Horizon | {1yr / 3yr / 5yr} |
| Techniques Used | {list of 2-3 techniques} |
| Participants | {names + AI} |

## Capability Ideas
| # | Capability | Source Technique | Strategic Theme | Timeframe | Feasibility | Strategic Value | Urgency |
|---|-----------|-----------------|----------------|-----------|-------------|----------------|---------|

## Technology Ideas
| # | Technology | Source Technique | Enables | Classification | Timeframe |
|---|-----------|-----------------|---------|---------------|-----------|

## Sunset Candidates
| # | Capability | Rationale | Capacity Freed |
|---|-----------|-----------|---------------|

## Selected Themes
(top 2-3 strategic themes with brief rationale)

## Next Step
CLA creation / PCR update / TIR update
```

---

## Relationship to Pipeline

The Ideation Workshop Record is **not a governed artifact** — it has no spec, validator, or hard gates. It is an operational input to the pipeline:

- **Selected idea → WCR (Step 0):** The idea description feeds the work request
- **Ideas table → Discovery Intake §1:** Problem context drawn from the workshop findings
- **Signal inputs → Discovery Intake §2:** Prior organizational learning referenced
- **Discarded ideas → ER Notes:** Recorded as context for future ideation sessions

The workshop record is saved as `00-ideation-workshop.md` in the SDLC directory, numbered before the routing record (`00-routing-record.md`) to preserve chronological order. If both exist, the routing record references the workshop as its input source.
