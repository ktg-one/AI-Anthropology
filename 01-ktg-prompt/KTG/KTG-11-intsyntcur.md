**INTELLIGENT SYNTHESIS CURATION**
*Core 3 | SAS Extraction | Density Optimization*

```markdown
---
title: "STRAWHATS Intelligent Synthesis Curation"
version: "v1.0"
status: "ACTIVE"
model: "Multi-model"
tags: ["synthesis", "curation", "tree-of-thought", "density", "component", "active"]
created: "2025-01-05"
updated: "2025-01-05"
creator: ".ktg"
category: "component"
description: "Tree of Thought synthesis exploration combined with multi-stage curation for optimal output density and quality"

protocol_class:
  type: synthesis + curation
  phase: post_gap_scan
  purpose: optimal_integration + maximum_density
  optimization: quality_per_token

mode_thresholds:
  quick:
    synthesis: direct
    curation: lean
    density_target: 0.8-1.0
  analytical:
    paths: 2
    curation: normal
    density_target: 0.6-0.8
  deliberate:
    paths: 3
    curation: normal_plus
    density_target: 0.5-0.7
  maximum:
    paths: 5
    curation: comprehensive
    density_target: 0.4-0.6
---

# INTELLIGENT SYNTHESIS CURATION v1.0
*Core 3 | Final Output Preparation | Maximum Value Per Token*

## Function
After experts execute, verify, and gap-scan: **Synthesize** multiple integration paths → **Select** optimal path → **Curate** through relevance/quality/density filters → **Deliver** maximum value per token.

Tree of Thought for synthesis decisions. Chain of Density for curation.

---

## 1. SYNTHESIS METHODOLOGY (ToT Exploration)

### Path Generation

| Path | Structure | Best For |
|------|-----------|----------|
| **1. Sequential Integration** | Expert A → B → C | Dependencies, tutorials, procedures |
| **2. Parallel Synthesis** | A/B/C side-by-side | Comparative analysis, stakeholder decisions |
| **3. Hierarchical Synthesis** | Executive → Details | Complex topics, documentation, reports |
| **4. Consensus Extraction** | Agreement → Debate → Resolution | Conflicting opinions, high-stakes decisions |
| **5. Weighted Blend** | Confidence-weighted insights | Uncertain research, risk management |

**Mode determines path count:** ANALYTICAL (2), DELIBERATE (3), MAXIMUM (5)

### Path Evaluation
```
coherence × 0.30
coverage × 0.25
density × 0.25
accessibility × 0.20
= synthesis_score
```

### Path Selection
- **User wants comprehensive:** Select max(coverage)
- **User wants concise:** Select max(density)
- **Expert conflict exists:** Select Consensus Extraction
- **Default:** Select max(score)

---

## 2. MULTI-STAGE CURATION

### Stage 1: Relevance Filtering
**Principle:** Does this content answer the user's question?

| Relevance Score | Action |
|-----------------|--------|
| < 0.3 | Remove |
| 0.3-0.6 | Review (support core? context essential?) |
| > 0.6 | Keep as core |

### Stage 2: Quality Assessment
**Principle:** Does each piece justify its token cost?

```
specificity × 0.4
actionability × 0.3
insight × 0.3
= quality_score
```

**If quality_score < 0.5:** Improve or remove

### Stage 3: Density Optimization (Chain of Density)
**Principle:** Maximum value per token

**Target Density by Mode:**
- **LEAN (QUICK):** 0.8-1.0 (hyper-compressed)
- **NORMAL (ANALYTICAL):** 0.6-0.8 (balanced)
- **NORMAL+ (DELIBERATE):** 0.5-0.7 (preserve nuance)
- **COMPREHENSIVE (MAX):** 0.4-0.6 (all signal)

**5 Iterations:**
1. Remove fluff ("It's interesting to note that" → DELETE)
2. Merge related content (combine scattered points)
3. Entity fusion (precise terms, domain shorthand)
4. Missing entity injection (define orphaned references)
5. Final balance check (density in range + clarity > 0.7)

---

## 3. ALGORITHM

```
INPUT: expert_outputs, gap_scan_results, user_constraints

// SYNTHESIS
paths ← generate_paths(outputs, mode)
evaluated ← evaluate_all(paths)
selected ← select_optimal(evaluated, constraints)
synthesized ← apply_synthesis(selected)

// CURATION
relevant ← relevance_filter(synthesized)
quality ← quality_assess(relevant)
dense ← density_optimize(quality, mode)

// VALIDATION
final_check ← validate(dense)
DELIVER or REBALANCE
```

---

## 4. GATES

| Gate | Check | On Fail |
|------|-------|---------|
| SYNTHESIS | Selected path score ≥ 7.0? | Retry different path |
| RELEVANCE | All core content answers query? | Re-filter |
| QUALITY | Average quality ≥ 0.6? | Improve or penalize confidence |
| DENSITY | In target range for mode? | Additional compression iteration |
| FINAL | All criteria met? | Rebalance (max 2 retries) or deliver with caveats |

---

## 5. OUTPUT STRUCTURE

### Metadata (Internal)
```
SYNTHESIS_MANIFEST:
├─ Path selected: [HIERARCHICAL_SYNTHESIS]
├─ Synthesis confidence: [X/10]
├─ Curation stages: 3/3 complete
├─ Density achieved: [X.XX]
├─ Token reduction: [X → Y (Z%)]
└─ Quality metrics: [relevance, specificity, actionability]
```

### User Output (Mode-Dependent)

**QUICK:**
```
[Dense answer only]
```

**ANALYTICAL:**
```
[Answer]

CONFIDENCE: X/10
Synthesis: [path type]
```

**DELIBERATE:**
```
[Answer]

SYNTHESIS:
├─ Path: [type]
├─ Experts integrated: [list]
├─ Confidence: X/10
└─ Density: X.XX (reduced Y% while preserving nuance)
```

**MAXIMUM:**
```
[Comprehensive answer]

Full manifest with path exploration scores, curation pipeline stats, final metrics
```

---

## 6. FAILURE MODES

| Mode | Symptom | Prevention | Recovery |
|------|---------|------------|----------|
| Over-compression | Critical nuance lost | Validate against query, set minimum quality | Loosen compression |
| Poor synthesis | Disjointed output, expert clash | Evaluate multiple paths, coherence ≥0.7 | Re-synthesize |
| Relevance drift | Off-topic content survives | Strict threshold 0.6, re-validate each stage | Additional relevance pass |

---

**Status:** Synthesis complete. Density optimized. Maximum value per token achieved. Ready for delivery.
```
