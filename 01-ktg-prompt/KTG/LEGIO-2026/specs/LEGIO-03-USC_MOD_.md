---
title: "USC — Universal Self-Consistency"
version: "v30.1"
status: "ACTIVE"
model: "Multi-model"
tags: ["usc", "self-consistency", "multi-candidate", "legio", "pre-flight", "active"]
created: "2026-02-16"
updated: "2026-02-16"
creator: "ktg"
category: "module"
description: "Multi-candidate generation and selection. USC sets the parallelism dial — how many independent solution paths run before synthesis. Mode-locked levels. Integration across the full pipeline."
legio_phase: "Pre-flight"
pipeline_position: "Step 3 (Pre-flight Technique)"
replaces: ["KTG-05-PRE06-USC[MOD].md"]
pairs_with: "LEGIO-00-IMPERATUS_CORE_.md"
built_for: "Claude Code → AGENTS.md onboarding"
---

# USC — UNIVERSAL SELF-CONSISTENCY
**Multi-Candidate Generation & Selection | Pre-flight Technique | Step 3**

---

## PURPOSE

One shield is a gamble. Two shields are a comparison. Three shields are a wall.

USC generates N independent candidate solutions using different expert configurations, then selects or synthesises the most consistent result. It's the pipeline's built-in second opinion — and third, and fifth.

USC is set by Imperatus during mode selection. It's a dial, not a switch. Even USC=0 is a conscious decision (single candidate, accepted risk).

---

## USC LEVELS BY MODE

| Mode | USC Level | Candidates | Strategy |
|------|-----------|------------|----------|
| **Velites** | 0 | 1 | Single pass. No comparison. Accepted risk. |
| **Hastati** | 2 | 2 | Generate 2 candidates. Compare. Select best. |
| **Principes** | 3 | 3 | Generate 3 candidates. Cross-synthesise non-redundant insights. |
| **Triarii** | 5 | 5 | Generate 5 candidates. Meta-synthesis. Full disagreement analysis. |

**Override:** `/usc-boost` forces USC=5 regardless of mode. User explicit request = override.

---

## EXECUTION FLOW

```
1. GENERATE N candidates (N = USC level)
   └─ Each candidate uses a DIFFERENT expert configuration
      (different MR.RUG expert mix, different emphasis weights)

2. COMPARE candidates for consistency
   └─ Agreement matrix: which conclusions do ≥2 candidates share?
   └─ Disagreement analysis: where do candidates diverge? Why?

3. SELECT or SYNTHESISE
   └─ USC=2: Select the stronger candidate. Note divergence.
   └─ USC≥3: Synthesise non-redundant insights from all candidates.
              Keep agreements. Resolve disagreements. Flag irreconcilables.

4. REPORT
   └─ Candidate agreement score (0-1)
   └─ Selection rationale OR synthesis method
   └─ Flagged disagreements that couldn't be resolved
```

---

## INTEGRATION ACROSS PIPELINE

USC isn't a single phase — it multiplies work across multiple pipeline steps.

| Module | USC Impact |
|--------|------------|
| **Consilium / MR.RUG (LEGIO-04)** | Different expert configs per candidate |
| **Legatus / SkeletrainOT (LEGIO-05)** | Multiple candidate structures if USC≥2 |
| **FCoT/CoC (LEGIO-07)** | Parallel reasoning chains per candidate |
| **Baton/Swarm (LEGIO-08)** | Parallel baton chains if USC≥3 |
| **CoVE (LEGIO-09)** | Cross-candidate verification |
| **PGScan (LEGIO-10)** | Cross-candidate synthesis if USC≥3 |
| **Censor / ISC (LEGIO-11)** | Merge non-redundant insights if USC≥3 |
| **Self-Reflect (LEGIO-12)** | Meta-synthesis if USC≥3 |
| **QMDR (LEGIO-15)** | Synthesise learning across all candidates |

---

## TOKEN OVERHEAD

USC is expensive. That's the point — quality costs tokens.

| Level | Token Overhead | Quality Gain | When Worth It |
|-------|---------------|-------------|---------------|
| USC=0 | Baseline | Baseline | Trivial tasks. Time-critical. Known domain. |
| USC=2 | +80% | +41% | **Sweet spot.** Most Hastati+ tasks. |
| USC=3 | +120% | +45% | High-stakes. Principes default. |
| USC=5 | +200% | +50% | Maximum stakes. Triarii. Research. |

Diminishing returns above USC=3. The jump from 2→3 is +4% quality for +40% tokens. The jump from 3→5 is +5% quality for +80% tokens. Imperatus makes this tradeoff during scoring.

---

## CANDIDATE DIFFERENTIATION

Candidates must actually differ. Generating 5 copies of the same reasoning is USC=0 pretending to be USC=5. Contract violation.

**Differentiation methods:**
- Different MR.RUG expert mix (e.g., Candidate A: Security+UX, Candidate B: Architecture+Performance)
- Different emphasis weights (e.g., Candidate A: risk-first, Candidate B: opportunity-first)
- Different structure type (e.g., Candidate A: SoT approach, Candidate B: GoT approach)
- Different retrieval focus (e.g., Candidate A: recent sources, Candidate B: foundational sources)

**Minimum differentiation:** Each candidate must differ in at least ONE expert config or emphasis weight from every other candidate.

---

## OUTPUT

USC produces a single consolidated output regardless of candidate count:

```
USC_RESULT:
├─ candidates_generated: [N]
├─ agreement_score: [0.0-1.0]
├─ selection_method: [best_pick | synthesis | meta_synthesis]
├─ divergence_flags: [list of unresolved disagreements]
├─ confidence_boost: [quality gain from USC vs single candidate]
└─ consolidated_output: [the actual answer]

→ Continues pipeline as single stream
```

---

## RELATION TO CONTRACT

The Seal (LEGIO-02) enforces USC deployment:
- Mode sets minimum USC level → Contract binds it
- Running Principes with USC=0 is a contract violation
- Generating identical candidates is a contract violation (嘘契約 applies: ①knows they're identical ∧ ②knows differentiation required ∧ ③pretends USC=N → lie)

---

**Status:** USC level set by Imperatus. Enforced by The Seal. Non-negotiable per mode.
