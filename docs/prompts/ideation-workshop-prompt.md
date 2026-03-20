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

## Relationship to Pipeline

The Ideation Workshop Record is **not a governed artifact** — it has no spec, validator, or hard gates. It is an operational input to the pipeline:

- **Selected idea → WCR (Step 0):** The idea description feeds the work request
- **Ideas table → Discovery Intake §1:** Problem context drawn from the workshop findings
- **Signal inputs → Discovery Intake §2:** Prior organizational learning referenced
- **Discarded ideas → ER Notes:** Recorded as context for future ideation sessions

The workshop record is saved as `00-ideation-workshop.md` in the SDLC directory, numbered before the routing record (`00-routing-record.md`) to preserve chronological order. If both exist, the routing record references the workshop as its input source.
