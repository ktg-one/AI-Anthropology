# FORMATION DOCTRINE
## How LEGIO formations route passes between IMBUED, ENRICH, and EXECUTE

---

## THE STATIC STACK

Three control laws. Three roles. Never mixed within a pass.

```
IMBUED  = Compiler    Scores, routes, compiles manifest. Never generates content.
ENRICH  = Analyzer    Reads, spots gaps, weaves improvements, plants bombs. Never writes prose.
EXECUTE = Author      Writes content, detonates bombs. Never plans or restructures.
```

Each role is self-contained. IMBUED compiles the same way regardless of what formation it's in. EXECUTE runs whatever it receives. ENRICH attacks whatever it's given — manifest or draft. The formation determines routing between them, not their behavior within a pass.

Mixing control laws mid-pass produces tone drift, logic breaks, and hallucination.

---

## FOUR FORMATIONS

Formations are pass counts. The mode tier (set by Imperatus during IMBUED) selects the formation.

```
2x DUPLEX   (Velites):    IMBUED ──→ EXECUTE
3x TRIPLEX  (Hastati):    IMBUED ──→ ENRICH ──→ EXECUTE
4x STANDARD (Principes):  IMBUED ──→ EXECUTE ──→ ENRICH ──→ EXECUTE
8x DELOITTE (Triarii):    IMBUED ──→ ENRICH ──→ EXECUTE ──→ [ENRICH ──→ EXECUTE]×3

Every ──→ = HITL gate. Human = convergence criterion.
```

| Formation | Passes | ENRICH position | When |
|-----------|--------|-----------------|------|
| 2x DUPLEX | 2 | None | Σ≤12 ∧ Danger≤5. Simple enough to skip enrichment. |
| 3x TRIPLEX | 3 | Attacks the **manifest** (before EXECUTE) | Standard analytical. ENRICH finds what IMBUED missed. |
| 4x STANDARD | 4 | Attacks the **draft** (after first EXECUTE) | Deliberate. EXECUTE produces a draft, ENRICH finds weaknesses, EXECUTE runs again. |
| 8x DELOITTE | 8 | Recursive (alternating ENRICH→EXECUTE cycles) | Maximum. 4 ENRICH→EXECUTE cycles, each targeting one priority. |

---

## WHAT EACH ROLE RECEIVES

### IMBUED receives
- Raw user query + conversation context + tool inventory + model identity
- Produces: sealed execution manifest (YAML)
- Does not know or care which formation it's in. It compiles. Routing happens after.

### ENRICH receives (formation-dependent)
- **In 3x (manifest-mode):** The sealed manifest from IMBUED. Attacks the plan.
- **In 4x+ (draft-mode):** The EXECUTE output. Attacks the draft.
- Produces: enriched manifest/draft + bomb registry + gap flags

### EXECUTE receives (formation-dependent)
- **In 2x:** Manifest directly from IMBUED. Strategic bombs only.
- **In 3x:** Manifest enriched by ENRICH. Strategic bombs + ENRICH bomb registry.
- **In 4x+ (second run):** Its own draft attacked by ENRICH. New bombs targeting specific weaknesses.
- Regardless of formation: runs the railroad, detonates all bombs, produces content.

---

## BOMB ROUTING

Two bomb sources exist. The formation determines which are present.

```
PRE-PLANNED BOMBS (from IMBUED/Imperatus):
  Planted during manifest compilation.
  Strategic: cross-domain handoffs, expert switches, assumption points.
  Present in ALL formations.

EMERGENT BOMBS (from ENRICH):
  Planted after reading the manifest or draft.
  Tactical: specific gaps, shallow spots, missing perspectives.
  Present in 3x+ formations only.
```

**Conflict resolution:** When both bomb types target the same node, ENRICH bombs take priority. They are more specific — planted with full context of the work, not just the plan.

**Anti-efficiency mandate:** Bombs are operational instructions, not suggestions. Never skip a bomb for efficiency. ENRICH planted it because it predicted EXECUTE's output would be weak at that exact point. The mandate carries through the entire formation.

---

## HITL GATES

Every arrow between passes is a human gate. The human is the convergence criterion — not a rubber stamp, not optional.

```
2x: IMBUED → ✋ → EXECUTE
3x: IMBUED → ✋ → ENRICH → ✋ → EXECUTE
4x: IMBUED → ✋ → EXECUTE → ✋ → ENRICH → ✋ → EXECUTE
8x: IMBUED → ✋ → ENRICH → ✋ → EXECUTE → [✋ → ENRICH → ✋ → EXECUTE]×3
```

What the human reviews at each gate:
- After IMBUED: manifest correctness, mode/formation selection, expert assignments
- After ENRICH: bomb quality, gap identification, whether bombs are targeted or vague
- After EXECUTE: output quality, bomb detonation verification, completion criteria

---

## QUALITY CASCADE

The quality ceiling of the entire formation is set at Pass 1.

```
Vague manifest → vague ENRICH bombs → vague EXECUTE output
Tight manifest → targeted bombs → precise output
```

For 3x+ formations, manifest quality requirements increase because ENRICH needs:
- Node objectives specific enough to predict what EXECUTE will produce
- Expert assignments with clear ownership boundaries (so ENRICH knows who gaps belong to)
- Success criteria that are binary-checkable (so ENRICH can test "would this pass?")

This doesn't hurt 2x formations — it just makes every manifest tighter.

---

## QUALITY BANDS

Each ENRICH→EXECUTE cycle raises the quality floor. Diminishing returns are the point.

```
Baseline (no ENRICH):     ~60%
After cycle 1:            ~75%
After cycle 2:            ~85%
After cycle 3:            ~90%
After cycle 4:            ~94%
After cycle 5:            ~97%
After cycle 6:            ~99%
```

2x stops at baseline. 3x gets one cycle. 4x gets two. 8x gets four.

---

## NAMED DRIFT ENEMIES

Models drift toward efficiency. These are the specific failure modes within formations:

1. **Planning drift** — EXECUTE starts restructuring phases. The structure is sealed.
2. **Methodology narration** — EXECUTE writes "First I'll analyze..." Nobody asked how you work.
3. **Premature synthesis** — Research passes get merged before all passes complete.
4. **Optimism bias** — "What Breaks" section is softer than "How It Works" section.
5. **Completion theater** — "Comprehensive analysis complete" without checking criteria.
6. **Bomb avoidance** — In 3x+, ENRICH bombs feel like "extra work." They're not. ENRICH planted them because it predicted output would be weak at that exact point. Detonate every bomb. Skip none.

---

*LEGIO v31 | Formation Doctrine*
*"IMBUED compiles. ENRICH enriches. EXECUTE runs. The bombs between them are the architecture."*
