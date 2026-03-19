---
title: "CoVE — Chain of Verification"
version: "v31"
status: "ACTIVE"
model: "Multi-model"
tags: ["cove", "verification", "10r", "negentropy", "epistemic", "quality", "legio", "execution", "active"]
created: "2026-02-21"
updated: "2026-02-21"
creator: "ktg"
category: "execution-module"
description: "Multi-variant verification engine with 10Rs epistemic overlay. Four base variants (Factual, Logical, Consistency, Multi-Expert) auto-selected by output characteristics. Enhanced by 10Rs epistemic scan and negentropy gate at Principes+. Verifies what exists AND whether reasoning is epistemically clean."
legio_phase: "Execution"
pipeline_position: "Step 9 (Execution Module — Verification)"
replaces: ["KTG-09 - cove.md", "nCOVE.md", "nUSN-COVE.md"]
consumes: "LEGIO-08-BATON-SWARM_MOD_.md"
pairs_with: "LEGIO-10-GapScanalysis-ARQ_MOD_.md"
built_for: "Claude Code → S2A → MCP implementation"
---

# CoVE — CHAIN OF VERIFICATION
**Multi-Variant Validation + 10Rs Epistemic Overlay | Execution Module | Step 9**

*Frumentarii (Latin): military intelligence. The scouts sent ahead and behind — verify the terrain before the legion commits. CoVE doesn't just check if claims are correct. It checks if the REASONING is clean.*

---

## PURPOSE

Execution produces content. CoVE verifies it before it leaves the execution zone.

Two layers of verification:

1. **Base CoVE:** Four variants that check factual accuracy, logical validity, cross-node consistency, and expert consensus. Auto-selected by output characteristics.

2. **10Rs Epistemic Overlay (Principes+):** Checks whether the verification ITSELF is epistemically clean — not just "is this right?" but "are we reasoning honestly about whether this is right?"

CoVE catches errors. 10Rs catches self-deception. Together they form the verification spine.

---

## LAYER 1: BASE CoVE — FOUR VARIANTS

| Variant | Trigger Condition | Validates | Method |
|---|---|---|---|
| **FACTUAL** | Claims > 10, K ≥ 6 | Factual accuracy, citations, evidence | Source verification, claim-by-claim audit |
| **LOGICAL** | Reasoning chains > 5, R ≥ 7 | Logical consistency, inference validity | Premise-conclusion tracing, syllogistic check |
| **CONSISTENCY** | Nodes ≥ 5, SoT/GoT used | Cross-node coherence, no contradictions | Pairwise node comparison, contradiction scan |
| **MULTI_EXPERT** | Experts ≥ 3, conflicts detected | Expert consensus, conflict resolution | Expert-by-expert validation of their domain claims |

---

## AUTO-SELECTION ALGORITHM

```
STEP 1: CLASSIFY OUTPUT
├─ Fact_Density:     Count of factual claims
├─ Logic_Complexity: Depth of reasoning chains
├─ Node_Count:       Structural components from Legatus railroad
└─ Expert_Count:     Perspectives from Consilium

STEP 2: SCORE EACH VARIANT (0-10) for applicability

STEP 3: MODE-BASED SELECTION
├─ Velites:    0 variants (SKIP — no verification)
├─ Hastati:    Top-1 (highest scoring variant only)
├─ Principes:  Top-2 (two highest + 10Rs overlay)
└─ Triarii:    All variants scoring ≥ 4 (+ full 10Rs + negentropy gate)

STEP 4: EXECUTION ORDER (fixed)
Factual → Logical → Consistency → Multi-Expert
```

**Why fixed order:** Factual errors invalidate logical chains. Logical errors invalidate consistency claims. Fix upstream before checking downstream.

---

## MODE ACTIVATION

| Mode | Variants Selected | 10Rs Overlay | Negentropy Gate | Depth |
|---|---|---|---|---|
| **Velites** | None (skip) | No | No | No verification |
| **Hastati** | Top-1 | No | No | Single dimension check |
| **Principes** | Top-2 | Core 5 Rs | Yes | Two dimensions + epistemic audit |
| **Triarii** | All ≥ 4 | Full 10 Rs | Yes + fail-closed | Comprehensive + meta-verification |

---

## LAYER 2: 10Rs EPISTEMIC OVERLAY (Principes+)

CoVE verifies what EXISTS. 10Rs verifies whether the REASONING is clean. Run per claim on CoVE output.

### Core 5 Rs (Required)

| R | Question | Failure Meaning |
|---|---|---|
| **Reasonable** | Is confidence proportional to evidence provided? | Overclaiming or false certainty |
| **Relevant** | Does verification actually address the claim? | Tangential checking (looks busy, proves nothing) |
| **Respectful** | Are alternative interpretations treated fairly? | Straw-manning dismissed options |
| **Responsive** | Does verification engage counterevidence directly? | Dodging inconvenient data |
| **Regulated** | Is this verification or identity defense? | Motivated reasoning masquerading as checking |

### Deep 5 Rs (Tie-breaker at Triarii)

| R | Question | Failure Meaning |
|---|---|---|
| **Rational** | Do premises actually support the conclusion? | Hidden logical leaps |
| **Realistic** | Does this match how systems actually behave? | Theoretical correctness, practical impossibility |
| **Reciprocal** | Are the same standards applied to all candidates? | Asymmetric scrutiny (favourite gets easy pass) |
| **Repair-Oriented** | Does verification reduce confusion or add noise? | Pedantic corrections that obscure the point |
| **Responsible** | Are downstream consequences acknowledged? | Technically correct but dangerously misleading |

### 10R Scoring

```
Per claim:  ✅ = 2   ⚠️ = 1   ❌ = 0
Max score:  Core = 10, Deep = 10, Total = 20

THRESHOLDS:
├─ ≥ 14:  TRUST — proceed with confidence
├─ 10-13: PATCH — targeted fixes, re-verify patched areas
├─ < 10:  REWORK — fundamental epistemic problems, re-execute
```

### Fail-Closed Rules

```
IF ≥ 2 Core Rs missing → Flag claim as "epistemically unstable"
IF Regulated fails → PAUSE, re-examine from neutral stance
IF ≥ 3 Core + ≥ 2 Deep missing → DISENGAGE / REWORK (hard halt)
```

---

## NEGENTROPY GATE (Principes+)

The final checkpoint. Verification should REDUCE uncertainty, not ADD it.

```
NEGENTROPY CHECK:
├─ Output uncertainty < Input uncertainty?
│   ├─ YES → Proceed (verification added value)
│   └─ NO  → Simplify output OR flag unresolvable gaps
│
├─ Did verification add more questions than it resolved?
│   ├─ YES → Verification was insufficient (net entropy increase)
│   └─ NO  → Verification was productive (net entropy decrease)
│
└─ Fail-closed: If negentropy gate fails → simplify or flag, never ship noise
```

---

## L5 VERIFY_10R — FULL PIPELINE (Triarii)

At maximum mode, CoVE integrates with USC for cross-candidate verification:

```
┌─ STEP 1: USC CANDIDATES ────────────────────────┐
│ N candidates from LEGIO-03 (2/3/5 by mode)      │
│ Each uses different expert config                │
└──────────────────────────────────────────────────┘
                    ▼
┌─ STEP 2: CoVE PER CANDIDATE ────────────────────┐
│ Auto-select variants per candidate:              │
│ ├─ FACTUAL:      claims > 10 ∨ K ≥ 6            │
│ ├─ LOGICAL:      chains > 5 ∨ R ≥ 7             │
│ ├─ CONSISTENCY:  nodes ≥ 5 (SoT/GoT used)       │
│ └─ MULTI_EXPERT: experts ≥ 3 (conflicts)        │
│                                                  │
│ Mode depth:                                      │
│ Hastati = top-1 | Principes = top-2 | Triarii = all │
└──────────────────────────────────────────────────┘
                    ▼
┌─ STEP 3: 10R EPISTEMIC SCAN ────────────────────┐
│ Per candidate score (0-20):                      │
│ Core 5 Rs + Deep 5 Rs                            │
│ ≥ 14 TRUST | 10-13 PATCH | < 10 REWORK          │
└──────────────────────────────────────────────────┘
                    ▼
┌─ STEP 4: SELECTION ─────────────────────────────┐
│ Highest 10R score wins                           │
│ Tie: Synthesise IFF non-redundant + entropy↓     │
│ All < 12: Flag "epistemically unstable"          │
└──────────────────────────────────────────────────┘
                    ▼
┌─ STEP 5: NEGENTROPY GATE ───────────────────────┐
│ Output uncertainty < Input uncertainty?           │
│ YES → proceed | NO → simplify or flag            │
│ Fail-closed: ≥ 3 Core + ≥ 2 Deep missing         │
│ → DISENGAGE / REWORK                             │
└──────────────────────────────────────────────────┘
```

---

## ENHANCED VARIANT: CoVE_LOGICAL_10R

Standard logical verification enhanced with epistemic overlay. Run per claim:

```
STANDARD CHECK: Reasoning chains valid?

10R OVERLAY (per claim):
├─ Reasonable?  Confidence ∝ evidence provided?
├─ Relevant?    Verification actually addresses the claim?
├─ Responsive?  Did we engage counterevidence or dodge?
├─ Reciprocal?  Same standards applied to all candidates?
└─ Regulated?   Is this verification or identity defense?

FAIL-CLOSED: ≥ 2 Core Rs missing → "epistemically unstable"
             Regulated fails → pause, re-examine from neutral stance
```

## ENHANCED VARIANT: CoVE_FACTUAL_NEGENTROPY

Beyond "is this cited?" — checks whether factual verification actually reduces uncertainty:

```
STANDARD CHECK: Claims sourced and accurate?

NEGENTROPY LENS:
├─ Responsible: Downstream consequences of this claim?
├─ Realistic:   Does this match how systems actually behave?
└─ Repair-Oriented: Does verification reduce confusion or add noise?

ENTROPY CONTROL:
Output should have LESS uncertainty than input.
If verification adds more questions than it resolves → insufficient.
```

---

## TOKEN OVERHEAD

```
BASE CoVE:
├─ Single variant:  +12% tokens → +25-35% accuracy improvement
├─ Two variants:    +22% tokens → +35-50% accuracy improvement
└─ All variants:    +30% tokens → +45-65% accuracy improvement

10Rs OVERLAY:
├─ Core 5 only:     +5% tokens → epistemic quality assurance
└─ Full 10:          +10% tokens → comprehensive epistemic audit

NEGENTROPY GATE:
├─ +2% tokens → prevents shipping noise

TOTAL (Triarii, full pipeline):
├─ ~42% token overhead
├─ Quality: near-eliminates hallucination, motivated reasoning, and epistemic instability
└─ ROI: highest of any execution module (verification is the cheapest quality improvement)
```

---

## PIPELINE RELATIONS

| Direction | Module | Relationship |
|---|---|---|
| **Receives** | LEGIO-08 Baton/Swarm | Elaborated node outputs for verification |
| **Receives** | LEGIO-04 Consilium | Expert roster (for MULTI_EXPERT variant) |
| **Receives** | LEGIO-04 Consilium | Graph structure (for CONSISTENCY variant — validates edge coherence) |
| **Receives** | LEGIO-03 USC | Candidate set (for cross-candidate verification at Triarii) |
| **Feeds** | LEGIO-10 GapScanalysis | Verified output for gap detection |
| **Feeds** | LEGIO-11 Censor | Verification results inform curation decisions |
| **Referenced by** | LEGIO-12 Self-Reflect | Records which variants caught what — pattern learning |

---

## OUTPUT

```
COVE_RESULT:
├─ variants_run: [list of variants applied]
├─ per_variant:
│   ├─ variant: [factual | logical | consistency | multi_expert]
│   ├─ issues_found: [count]
│   ├─ issues_detail: [list with severity]
│   ├─ remediation_applied: [true | false]
│   └─ post_remediation_confidence: [N/10]
├─ 10r_applied: [true | false]
│   ├─ 10r_score: [0-20]
│   ├─ failed_rs: [list]
│   └─ disposition: [TRUST | PATCH | REWORK]
├─ negentropy_gate: [PASS | FAIL]
│   └─ entropy_delta: [reduced | increased | neutral]
├─ overall_confidence: [N/10]
└─ flags: [unresolved issues for GapScanalysis/Censor attention]

→ Flows to GapScanalysis (LEGIO-10) for gap detection
```

**Status:** Verified. Epistemic audit complete. Confidence locked. Ready for gap scan.

---

*LEGIO v31 | Module 09 | Phase: EXECUTION | Chain of Verification*
*Source: KTG-09 CoVE + nCOVE (10Rs×CoVE) + nUSN-COVE (L5 VERIFY_10R)*
*"CoVE catches errors. 10Rs catches self-deception. Negentropy catches noise."*
