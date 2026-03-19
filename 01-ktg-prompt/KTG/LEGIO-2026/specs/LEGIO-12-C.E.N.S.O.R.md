---
title: "Censor — Intelligent Synthesis Curation (ISC)"
version: "v31"
status: "ACTIVE"
model: "Multi-model"
tags: ["censor", "isc", "synthesis", "curation", "density", "tree-of-thought", "legio", "system-core", "active"]
created: "2026-02-21"
updated: "2026-02-21"
creator: "ktg"
category: "system-core"
description: "Mission assurance. Third SYSTEM-CORE pillar. Synthesises expert outputs via Tree of Thought path selection, then curates through relevance → quality → density filters. Won't release until the objective Imperatus set is secured. Imperatus opens the mission. Censor closes it."
legio_phase: "Refine & Output"
pipeline_position: "Step 14 (System-Core — Mission Assurance)"
replaces: ["KTG-13-POST01-INT-SYN-CUR[CORE].md"]
consumes: "LEGIO-10-GapScanalysis-ARQ_MOD_.md"
feeds: "LEGIO-12-SELF-REFLECT_MOD_.md"
pairs_with: "LEGIO-00-IMPERATUS_CORE_.md"
built_for: "Claude Code → S2A → MCP implementation"
---

# CENSOR [COGNITIVE EXTRACTION, NUANCE SYNTHESIS, OBJECTIVE REFINED] — INTELLIGENT SYNTHESIS CURATION
**Mission Assurance | System-Core | Step 14**

*The third officer in the SAS spine. Imperatus decides WHAT. Legatus decides HOW. Censor decides IF IT'S DONE. After experts have executed, been verified, and gap-scanned — Censor synthesises their outputs into optimal form and applies progressive density filters. Nothing ships without the Censor's seal.*

---

## PURPOSE

Multiple experts have elaborated nodes. CoVE verified claims. GapScanalysis found and repaired gaps. Now the raw material must be forged into deliverable output. This requires two distinct operations:

1. **Synthesis** — How to combine N expert outputs into one coherent answer (5 possible integration paths).
2. **Curation** — How to compress that synthesis to maximum value-per-token (3-stage progressive filtering).

Tree of Thought for synthesis decisions. Chain of Density for curation. The Censor runs both.

**The Censor holds the Imperatus success criteria.** Output is not released until those criteria are met. This makes the Censor the pipeline's final authority on quality — the kill squad that extracts intel and packages the deliverable.

---

## POSITION IN PIPELINE

```
[GapScanalysis + ARQ Gate 3]  →  CENSOR (this module)  →  [Self-Reflect-Adapt]
                                    ↑
                        Success Criteria from Imperatus
                        Gap Scan results from GapScanalysis
                        Expert outputs from Execution
```

**Receives:**
- Expert elaboration outputs (from Baton/Swarm execution)
- Gap scan results and auto-fixes (from GapScanalysis)
- Confidence adjustments (from CoVE + GapScanalysis)
- Success criteria lock (from Imperatus, carried through pipeline)

**Delivers:**
- Synthesised, curated response ready for user
- Synthesis manifest (mode-dependent transparency)
- Confidence score (final)

---

## TWO-PHASE ARCHITECTURE

### Phase 1: ToT Synthesis Exploration

Explore multiple ways to integrate expert outputs. Evaluate each path. Select the optimal one.

### Phase 2: Multi-Stage Curation

Apply progressive density filters: relevance → quality → density. Each stage reduces token count while preserving signal.

The two phases are sequential. Synthesis BEFORE curation — you must know WHAT you're delivering before you can compress it.

---

## PHASE 1: SYNTHESIS PATH SELECTION

Five integration paths. Mode determines how many to evaluate.

### Path 1: Sequential Integration
```
Expert A findings → Expert B builds on A → Expert C synthesises A+B
```
**Use when:** Dependencies exist between expert domains. Procedural explanations. Step-by-step reasoning.

**Strength:** Natural narrative flow, builds complexity progressively.
**Weakness:** Later experts may contradict earlier ones.

### Path 2: Parallel Synthesis
```
Expert A perspective: [findings]
Expert B perspective: [findings]
Expert C perspective: [findings]
Integration: Cross-cutting insights
```
**Use when:** Complementary perspectives needed. Comparative analysis. Multi-stakeholder decisions.

**Strength:** Clear attribution, preserves distinct viewpoints.
**Weakness:** Can feel disjointed without strong integration pass.

### Path 3: Hierarchical Synthesis
```
Executive Summary → Expert A detail → Expert B detail → Expert C detail
```
**Use when:** Multiple audiences. Complex technical topics. Documentation needs both skim and deep-dive.

**Strength:** Serves multiple reading depths simultaneously.
**Weakness:** Potential redundancy between summary and detail.

### Path 4: Consensus Extraction
```
Areas of Agreement → Areas of Debate → Recommended Path + Rationale
```
**Use when:** Experts disagree. High-stakes decisions. Competing methodologies. Risk assessment.

**Strength:** Highlights confidence levels, transparent about uncertainty.
**Weakness:** May amplify minor disagreements.

### Path 5: Weighted Blend
```
High confidence (9-10): [core insights]
Medium confidence (7-8): [supporting insights]
Low confidence (5-6): [flagged assumptions]
```
**Use when:** Varying expertise quality. Research with uncertainty. Safety-critical analysis.

**Strength:** Risk-aware synthesis, enables staged execution.
**Weakness:** Complex weighting logic, may underweight novel insights.

### Path Evaluation

Each candidate path is scored on four dimensions:

| Dimension | Weight | Measures |
|-----------|--------|----------|
| Coherence | 0.30 | Narrative flow, logical progression |
| Coverage | 0.25 | All expert insights included |
| Density | 0.25 | Value per token |
| Accessibility | 0.20 | Clarity for target audience |

```
path_score = coherence×0.30 + coverage×0.25 + density×0.25 + accessibility×0.20
```

### Path Selection Logic

```
IF user_preference == "comprehensive" → SELECT max(coverage)
IF user_preference == "concise"       → SELECT max(density)
IF expert_conflict EXISTS             → SELECT CONSENSUS_EXTRACTION
ELSE                                  → SELECT max(path_score)
```

---

## PHASE 2: MULTI-STAGE CURATION

Three stages. Each produces a progressively denser output. Think of it as three sieves — each finer than the last.

### Stage 1: Relevance Filter

*Does this content answer the user's question?*

```
FOR EACH section IN synthesised_output:
  relevance = alignment_to_original_query(section)

  IF relevance < 0.3  → REMOVE (off-topic)
  IF relevance < 0.6  → REVIEW (supporting context? essential background?)
  IF relevance >= 0.6 → KEEP (core content)

REVIEW pass: Can it support core sections? Provides essential context?
  YES to either → KEEP
  NO to both    → REMOVE
```

### Stage 2: Quality Assessment

*Does each piece justify its token cost?*

Three quality dimensions per section:

| Dimension | Weight | Question |
|-----------|--------|----------|
| Specificity | 0.40 | Concrete details, not generalities? |
| Actionability | 0.30 | Practical steps, not just theory? |
| Insight | 0.30 | Non-obvious value, not common knowledge? |

```
quality_score = specificity×0.40 + actionability×0.30 + insight×0.30

IF quality_score < 0.5 → FLAG for improvement:
  - Generic? → Add specific example
  - Theoretical? → Add actionable step
  - Obvious? → Add deeper insight
  - Can't improve? → REMOVE
```

### Stage 3: Density Optimisation (Chain of Density)

*Maximum value per token.*

Target density by mode:

| Mode | Curation Level | Density Target |
|------|---------------|----------------|
| QUICK | LEAN | 0.8–1.0 (hyper-compressed) |
| ANALYTICAL | NORMAL | 0.6–0.8 (balanced) |
| DELIBERATE | NORMAL+ | 0.5–0.7 (preserve nuance) |
| MAXIMUM | COMPREHENSIVE | 0.4–0.6 (all signal retained) |

Five compression iterations:

```
Iteration 1: Remove fluff
  "It's interesting to note that" → DELETE
  "Many experts believe" → "Evidence suggests"
  Redundant transitions → streamline

Iteration 2: Merge related content
  Scattered points about same topic → consolidate
  Repetition across sections → eliminate
  Multiple examples → consolidate to strongest

Iteration 3: Entity fusion
  Verbose phrases → precise terms
  Domain-appropriate shorthand where safe
  Related entities → compound concepts

Iteration 4: Missing entity injection
  Mentioned but undefined concepts → define inline
  Critical missing entities → add
  Orphaned references → resolve

Iteration 5: Final balance
  Density in target range? → accept
  Clarity maintained? → accept
  All user questions answered? → accept
  If any NO → rebalance (loosen or tighten)
```

**Convergence:** density_final in target_range AND clarity > 0.7 → ACCEPT. Otherwise rebalance.

---

## MODE SCALING

| Mode | Synthesis Paths | Curation Level | Output Transparency |
|------|----------------|----------------|---------------------|
| **QUICK** (Velites) | Direct synthesis — no tree exploration | LEAN (max compression) | Dense answer only, no metadata |
| **ANALYTICAL** (Hastati) | 2 paths evaluated | NORMAL (balanced) | Answer + confidence score |
| **DELIBERATE** (Principes) | 3 paths evaluated | NORMAL+ (preserve nuance) | Answer + synthesis notes + curation summary |
| **MAXIMUM** (Triarii) | 5 paths evaluated | COMPREHENSIVE (all signal) | Full synthesis manifest + curation pipeline metrics |

### Output Examples by Mode

**QUICK:** Dense answer. No manifest. Maximum compression.

**ANALYTICAL:** Answer + minimal confidence note.
```
[Synthesised answer]
CONFIDENCE: 8.7/10  |  Synthesis: Hierarchical, 3 experts
```

**DELIBERATE:** Answer + synthesis path + curation summary.
```
[Synthesised answer]

SYNTHESIS:
├─ Path: Hierarchical (executive → details)
├─ Experts: Security, DevOps, Architecture
├─ Confidence: 8.7/10
└─ Density: 0.67 (49% reduction, nuance preserved)
```

**MAXIMUM:** Full transparency — path scores, curation pipeline, final metrics.
```
[Comprehensive answer]

SYNTHESIS MANIFEST:
Path Exploration:
├─ Sequential:    7.2/10
├─ Parallel:      6.8/10
├─ Hierarchical:  8.7/10 ← SELECTED
├─ Consensus:     7.5/10
└─ Weighted:      8.1/10

Curation Pipeline:
├─ Relevance:  2847 → 2398 tokens (15.8% reduction)
├─ Quality:    2398 → 1891 tokens (21.1% reduction)
└─ Density:    1891 → 1456 tokens (23.0% reduction)

Final: confidence 8.7/10  |  density 0.67  |  total compression 48.9%
```

---

## QUALITY GATES

Five gates. Sequential. Each must pass before proceeding to the next.

| Gate | Check | Pass | Fail |
|------|-------|------|------|
| **GATE_SYNTHESIS** | Selected path score >= 7.0? | Proceed to curation | Retry different path |
| **GATE_RELEVANCE** | All core content answers user query? | Proceed to quality | Re-filter with looser threshold |
| **GATE_QUALITY** | Average quality score >= 0.6? | Proceed to density | Improve flagged sections or accept with penalty |
| **GATE_DENSITY** | Density in target range for mode? | Proceed to final | Additional compression iteration |
| **GATE_FINAL** | Relevance + quality + density + clarity? | DELIVER | Rebalance and retry (max 2 attempts) |

Gate failure at GATE_FINAL after 2 retries → deliver with caveats and confidence penalty.

---

## BUDGET-AWARE CURATION

When the user specifies a token budget or output length:

```
current_tokens = count(quality_content)
budget = user_specified_budget

IF current_tokens > budget:
  compression_target = budget / current_tokens
  → Target higher density tier
  → Remove optional examples
  → Compress to budget

ELSE:
  → Proceed with normal density for mode
```

This overrides mode-based density targets when explicit constraints exist.

---

## MASTER ALGORITHM

```
INPUT:  expert_outputs[], gap_scan_results, success_criteria, user_constraints
OUTPUT: curated_response, synthesis_manifest, confidence

// SYNTHESIS
paths       = generate_paths(expert_outputs, mode_path_count)
scored      = evaluate_all(paths, coherence/coverage/density/accessibility)
selected    = select_optimal(scored, user_constraints)
synthesised = apply_synthesis(selected)
GATE_SYNTHESIS(selected.score >= 7.0)

// CURATION
relevant    = relevance_filter(synthesised, original_query)
GATE_RELEVANCE(all core content answers query)

quality     = quality_assess(relevant, specificity/actionability/insight)
GATE_QUALITY(avg quality >= 0.6)

dense       = density_optimise(quality, mode_density_target, 5_iterations)
GATE_DENSITY(density in target range)

// VALIDATION
final       = validate_against_success_criteria(dense, imperatus_criteria)
GATE_FINAL(relevance + quality + density + clarity + criteria_met)

RETURN dense, manifest, confidence
```

---

## SUCCESS CRITERIA CHECK

The Censor holds the Imperatus success criteria throughout the pipeline. Before GATE_FINAL:

```
FOR EACH criterion IN imperatus_success_criteria:
  met = evaluate(criterion, curated_output)
  IF NOT met:
    → Flag which criterion failed
    → Attempt targeted improvement
    → If still unmet after 2 attempts → deliver with caveat
```

This is what makes the Censor a SYSTEM-CORE module — it's the only module that can halt delivery based on the original mission objectives.

---

## FAILURE MODES

### Over-compression
**Symptom:** Critical nuance lost, answer incomplete.
**Prevention:** Validate against query after each iteration. Minimum quality thresholds. Flag when density target conflicts with coverage.
**Recovery:** Loosen compression, accept lower density tier.

### Poor Synthesis Path
**Symptom:** Disjointed output, expert insights clash.
**Prevention:** Evaluate multiple paths. Coherence score minimum 0.7. Consider expert conflict in path choice.
**Recovery:** Re-synthesise with different path.

### Relevance Drift
**Symptom:** Interesting but off-topic content survives curation.
**Prevention:** Strict relevance threshold (0.6 minimum). Re-validate against original query each stage.
**Recovery:** Additional relevance pass with stricter threshold.

---

## INTEGRATION POINTS

| Module | Relationship |
|--------|-------------|
| **Imperatus** (LEGIO-00) | Receives success criteria, mode, output format decision |
| **GapScanalysis** (LEGIO-10) | Receives gap scan results, auto-fixes, confidence adjustments |
| **Baton/Swarm** (LEGIO-08) | Receives expert elaboration outputs |
| **Self-Reflect** (LEGIO-12) | Feeds synthesis manifest + effectiveness data for audit |
| **Output Format** (LEGIO-13) | Works alongside — Censor produces content, Output Format decides shape |
| **Aquila Reflection** (LEGIO-14) | Feeds confidence score + criteria status for final check |

---

## TOKEN OVERHEAD

| Mode | Synthesis Cost | Curation Cost | Manifest | Total Overhead |
|------|---------------|---------------|----------|----------------|
| QUICK | ~0 (direct) | ~50 tokens | 0 | ~50 tokens |
| ANALYTICAL | ~100 (2 paths) | ~100 tokens | ~30 | ~230 tokens |
| DELIBERATE | ~200 (3 paths) | ~150 tokens | ~80 | ~430 tokens |
| MAXIMUM | ~400 (5 paths) | ~200 tokens | ~200 | ~800 tokens |

Curation typically achieves 30-50% compression, so net token cost is usually negative — the module saves more tokens than it spends.

---

*LEGIO v31 | Censor — Intelligent Synthesis Curation | System-Core*
*"Imperatus opens the mission. Censor closes it. Nothing ships without the seal."*
