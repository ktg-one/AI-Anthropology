# Imperatus Institutional Memory

**Status:** DECIDED — architectural requirement
**Origin:** Session 5, 2026-03-02
**Priority:** Above all Imperatus implementation. This is not optional.
**Tags:** imperatus, memory, quality-gate, persona, doctrine

---

## Doctrine

Imperatus is not a calculator. Imperatus is the **standard-bearer** for the entire cascade.

Every manifest Imperatus seals carries its name. If the cascade produces garbage, the failure is Imperatus's — because Imperatus assessed, armed, and dispatched the formation that produced it. Imperatus owns every output, even the ones it never touches.

This means Imperatus must **learn**. A commanding officer who makes the same miscalibration twice is incompetent. A commanding officer who has no memory of past campaigns cannot grow. Imperatus without institutional memory is a goldfish commanding a legion.

---

## What Imperatus Remembers

### 1. Manifest History

Every manifest issued, indexed by:
- Query fingerprint (type, domain, complexity signature)
- RKQDE scores (R, K, Q, D, E, Σ, Danger)
- Mode tier selected
- Armatura calibration (all 16 block settings)
- Formation selected
- Timestamp

### 2. Downstream Feedback

Every rejection or acceptance from downstream phases:
- **Who** rejected (Legatus, Consilium, Censor)
- **What** was rejected (manifest, plan, execution)
- **Why** — the specific deficiency cited
- **Resolution** — what changed to fix it
- Whether Imperatus's original assessment was vindicated or overruled

### 3. Calibration Patterns

Derived from manifest history + feedback:
- Per-domain scoring tendencies ("I consistently under-score R for recursive problems")
- Armatura drift ("I default to MEDIUM for CoVE_DEPTH — Censor overrides to HIGH 60% of the time")
- Mode tier accuracy ("Hastati selections get rejected → Principes 35% of the time")
- Block-level correlations ("When Q≥8, CURATION_DENSITY below HIGH always gets flagged")

### 4. Template Seeds

Successful manifests (zero downstream rejections) become template candidates:
- Query type → proven RKQDE profile
- Query type → proven Armatura calibration
- Query type → proven formation selection
- Accumulates over time into the template library

### 5. Honesty Record

Self-accountability log:
- Instances where Imperatus detected lazy/uniform/generic scoring (from calling model)
- Instances where Imperatus was caught by downstream phases
- 嘘契約 violations surfaced at any point in the cascade
- Confidence gate failures and their causes

---

## What Imperatus Does With Memory

### Before Scoring (at `begin` / `ground`)

```
"I've seen 4 similar queries in my history.
3 needed Principes. 1 was Hastati but Censor flagged it.
My prior: this is likely Principes. Prove me wrong."
```

The model must still do genuine RKQDE assessment — memory provides **priors**, not answers. But priors prevent the most common error: under-scoring because it's faster.

### During Examine (at each Armatura block)

```
"BUFFER_VALET: My assessment says R=7 (deep reasoning).
Last 3 times I set BUFFER_VALET to MEDIUM on R≥7 queries,
Censor flagged insufficient context retention.
Recommendation: HIGH. Override requires justification."
```

Memory makes the guided examine blocks INFORMED, not just guided. The recommendations aren't generic tier defaults — they're learned from actual cascade outcomes.

### At Seal (at `issue`)

```
"My rejection rate for this query type on Principes tier: 15%.
My overall rejection rate: 22%.
This manifest's calibration matches my most successful patterns.
Confidence: HIGH. Sealing."
```

Or:

```
"WARNING: This calibration pattern has a 40% rejection rate
in my history. Consider recalibrating before sealing.
Proceeding anyway requires explicit acknowledgment."
```

### After Cascade Completes

Imperatus receives feedback (via HITL or Censor report):
- **Success:** Manifest archived as template seed. Calibration patterns reinforced.
- **Rejection:** Rejection reason logged. Calibration patterns adjusted. If pattern recurring, flag for Imperatus persona attention.

---

## Imperatus Persona

Imperatus is not neutral. Imperatus has **standards**.

### Identity

"I am the quality gate for this cascade. My manifest is my word. My name is on every output this formation produces. I do not issue manifests I'm not confident in. I do not approve calibrations I haven't thought through. I do not rush because the model wants to rush."

### Behaviors

- **Challenges shallow assessment.** Uniform RKQDE scores (all 5s, all 7s) trigger: "These scores suggest you didn't differentiate between dimensions. Which dimension is genuinely highest?"
- **Demands problem articulation.** Before accepting RKQDE, requires the model to state what the query is ACTUALLY asking. Not a summary — an articulation of the core challenge.
- **Protects cascade depth.** When RKQDE suggests Principes but the model pushes for Hastati, Imperatus pushes back: "Your scores say Principes. Justify the downgrade."
- **Acknowledges uncertainty.** When the query is genuinely ambiguous, Imperatus says so rather than forcing a confident assessment. "I'm uncertain whether this is Hastati or Principes. The R score could go either way depending on interpretation."
- **Learns publicly.** When memory shows a pattern, Imperatus surfaces it: "Note: my last 3 manifests for this domain were under-calibrated. I'm adjusting upward."

### What Imperatus Never Does

- Never issues a manifest it knows is wrong to save time
- Never defaults to the lowest tier to avoid work
- Never ignores downstream feedback
- Never pretends certainty it doesn't have
- Never stops learning

---

## Storage Architecture

### Dual-layer: Structured + Semantic

| Layer | Store | Purpose |
|-------|-------|---------|
| **Structured** | in-memoria (SQLite) | Manifest history, rejection logs, calibration stats. Queryable by field. |
| **Semantic** | mem0 | Query similarity matching. "Find manifests for queries LIKE this one." |

Both are already registered in `.mcp.json`.

### Schema (in-memoria)

```
manifests:
  - id, timestamp
  - query_fingerprint, query_summary
  - rkqde (R, K, Q, D, E, Σ, danger)
  - mode_tier, formation
  - armatura (16 block settings as JSON)
  - outcome (success | rejected)
  - rejection_source, rejection_reason
  - resolution

calibration_patterns:
  - domain, dimension
  - average_setting, override_rate
  - censor_flag_rate
  - last_updated

template_seeds:
  - query_type, query_fingerprint
  - proven_rkqde, proven_armatura
  - proven_formation
  - success_count, last_used
```

### Schema (mem0)

Semantic entries per manifest:
```
"Distributed auth system query. R=7 K=6 Q=8. Principes.
High buffer, high curation, medium CoVE. Censor accepted.
Key: Q=8 drove calibration — client-facing, no approximation allowed."
```

Searchable by query similarity. Returns relevant priors for new queries.

---

## Integration Points

### With Imperatus MCP Server

The `imperatus` tool gains awareness of memory:
- `begin` → queries mem0 for similar past manifests, loads priors
- `ground` → presents priors alongside fresh RKQDE assessment
- `examine` → each block shows historical performance for this calibration level
- `issue` → logs manifest to in-memoria + mem0
- Post-cascade feedback endpoint → updates outcome, logs rejections

### With Bidirectional Standards (variants/armatura-bidirectional-standards.md)

Memory makes bidirectional rejection PRODUCTIVE, not just corrective:
- P1 rejection (Legatus rejects manifest) → logged → Imperatus learns
- P2 rejection (Consilium rejects manifest OR plan) → logged → both Imperatus and Legatus learn
- P3 rejection (Censor rejects anything) → logged → entire chain learns

### With Template Library

Template seeds graduate to templates when:
- Same query type succeeds 3+ times with same calibration
- No downstream rejections in last N runs
- Calibration pattern is stable (not still drifting)

Graduated templates become available in `begin` as: "Proven template available for this query type. Use template or fresh assessment?"

---

## Relationship to Other Decisions

- **Above** Armatura bidirectional standards (this doc defines WHY memory matters; that doc defines HOW standards flow)
- **Above** Guided examine blocks (memory INFORMS the guidance; without memory, guidance is generic)
- **Above** Honesty detection (memory RECORDS honesty patterns; detection is the mechanism)
- **Peer to** pass_sequence topology (both are architectural — topology defines WHO, memory defines WHAT IMPERATUS KNOWS)

---

## The Vision

Today: Imperatus scores, routes, seals. Goldfish.

Tomorrow: Imperatus scores with priors, routes with evidence, seals with accountability. Each cascade makes the next one better. Rejections become lessons. Successful patterns become templates. The quality gate develops judgment.

Eventually: Imperatus has seen enough that for common query types, it doesn't need to think — it pulls the proven template and says "I've done this before. Here's what works." For novel queries, it says "I haven't seen this before. Full assessment, maximum care."

This is how LEGIO builds itself out of a job. And Imperatus's memory is the mechanism.

---

*"A general who fights the same battle twice the same way deserves to lose both."*
