---
title: "Armatura — The Arsenal (Technique Gate)"
version: "v31"
status: "ACTIVE"
model: "Multi-model"
tags: ["armatura", "technique-gate", "lotus", "imperatus", "system-core", "legio", "active"]
created: "2026-02-15"
updated: "2026-02-15"
creator: "ktg"
category: "system-core"
description: "Technique gate v5 converted from flat checklist into contemplative constraint-setting process. Imperatus does NOT pick techniques — the pipeline is fixed. Imperatus sets CONSTRAINT LEVELS for each technique based on mode and query. Human-readable architecture spec. Real implementation is S2A."
legio_phase: "Planning"
pipeline_position: "Step 1 (Imperatus Phase 4 content)"
replaces: "TECHNIQUE_TICK_GATE_V5.0"
pairs_with: "LEGIO-00-IMPERATUS_CORE_.md"
built_for: "Claude Code → S2A implementation"
---

# ARMATURA [Agentic Recursive Mode: Analyze Techniques Useful for Routing Architecture] — THE ARSENAL
**Technique Gate as Lotus Thought Process | Constraint Setting, Not Technique Selection**

*Armatura (Latin): weapons drill, equipment assignment. The armoury that arms each tier before deployment.*

---

## CORE PRINCIPLE

The pipeline is FIXED. Every technique exists in every execution.
Imperatus doesn't choose techniques. Imperatus sets the DIALS.

```
WRONG:  "Should ARQ activate?" → yes/no
RIGHT:  "What strictness level does ARQ need?" → light/standard/hard/HALT
```

Even at Velites, techniques run — they just run at minimum constraint.
"Off" means "minimum viable" not "absent."

---

## RELATIONSHIP TO IMPERATUS LOTUS

Imperatus (LEGIO-00) = the engine (tags, phases, flow).
This document = the content Imperatus contemplates during Phase 4.

Each entry below is a constraint-setting contemplation, not a selection decision.

---

## MODE THRESHOLDS (set during Phase 3 [route])

```
Velites:    R≤3 ∧ Q≤5
Hastati:    R=4-6 ∨ Q=6-7
Principes:  R≥7 ∨ K≥6 ∨ Q≥8
Triarii:    R≥9 ∨ K≥8 ∨ /deep
```

---

## PRE-FLIGHT CONSTRAINTS

### [examine] BUFFER_VALET

```
CONTEMPLATE: What memory depth does this query need?

CONSTRAINT LEVELS:
  Velites:    Read
  Hastati:    Read
  Principes:  Read + Save Tier 2
  Triarii:    Read + Save Tier 1

SET: Memory depth = [Read / Read+Save-2 / Read+Save-1]
```

### [examine] SUCCESS_CRITERIA_LOCK

```
CONTEMPLATE: How rigid do victory conditions need to be?

CONSTRAINT LEVELS:
  Velites:    Implicit (1-2 conditions, obvious)
  Hastati:    Explicit Type Check (2-3 stated)
  Principes:  Signature Lock (3-5, immutable)
  Triarii:    Multi-Constraint Lock (5+, cross-dimensional)

SET: Lock rigidity = [Implicit / Type / Signature / Multi]
     Criteria count = [N]
```

### [examine] ARQ_GATES

```
CONTEMPLATE: How strict do quality gates need to be?
             Where are the failure points?

CONSTRAINT LEVELS:
  Velites:    Pre-Turn | light
  Hastati:    Pre-Turn | standard
  Principes:  Pre+Post | hard
  Triarii:    Full (Pre+During+Post) | HALT-on-fail

SET: Coverage = [Pre / Pre+Post / Full]
     Strictness = [light / standard / hard / HALT]
     Domain checks = [2-3 quality questions]
```

### [examine] ANTI_LAZY

```
CONTEMPLATE: How likely is the model to shortcut this output?

CONSTRAINT LEVELS:
  Velites:    Advisory (flag but don't block)
  Hastati:    Required (no placeholders)
  Principes:  Required (complete output mandatory)
  Triarii:    Enforced (any truncation = restart section)

SET: Enforcement = [Advisory / Required / Enforced]
```

### [examine] USC_CANDIDATES

```
CONTEMPLATE: How many valid approaches exist in the solution space?

CONSTRAINT LEVELS:
  Velites:    1-path sanity check
  Hastati:    2 candidates
  Principes:  3 candidates
  Triarii:    5 candidates + meta-synthesis

SET: Candidate count = [1 / 2 / 3 / 5+meta]
```

### ── CONFIDENCE GATE: Pre-flight coherent? >9/10 → proceed ──

---

## PIPELINE CONSTRAINTS

### [examine] MR_RUG_EXPERTS

```
CONTEMPLATE: How many domains need specialist coverage?
             What formation fits the domain shape?

CONSTRAINT LEVELS:
  Velites:    0 experts (basic retrieval only)
  Hastati:    3 specialists
  Principes:  5 specialists
  Triarii:    5-8 specialists + deep semantic embedding

SET: Expert count = [0 / 3 / 5 / 5-8]
     Formation = [Testudo / Triplex / Cuneus / Orbis]
     Graph depth = [retrieval / specialist / full / deep-embed]
```

### [examine] SKELETRAIN_SCALE

```
CONTEMPLATE: How many execution nodes does the task need?
             Linear or branching?

NOTE: Imperatus sets SCALE. SkeletrainOT makes all tactical decisions.

CONSTRAINT LEVELS:
  Velites:    Direct path (no skeleton)
  Hastati:    Light (3-5 nodes)
  Principes:  Full (5-10 nodes)
  Triarii:    GoT if D≥6, else Deep (10+ nodes)

SET: Scale = [Direct / Light / Full / GoT]
     Estimated nodes = [N]
```

### ── CONFIDENCE GATE: Pipeline matches complexity? >9/10 → proceed ──

### [examine] PROMPT_BOMBS

```
CONTEMPLATE: How many confusion points will execution hit?

NOTE: Imperatus sets ARSENAL SIZE. SkeletrainOT places them.

CONSTRAINT LEVELS:
  Velites:    Clarifier only (0-1 bombs)
  Hastati:    Clarifier + Scaffold (2-3 bombs)
  Principes:  Full Arsenal + Registry (4-6 bombs)
  Triarii:    Deep Injection (6+ bombs, continuous)

SET: Arsenal = [Clarifier / Scaffold / Full / Deep]
     Count = [N bombs allocated]
```

---

## EXECUTION CONSTRAINTS

### [examine] REASONING_STYLES

```
NOTE: Imperatus makes styles AVAILABLE. SkeletrainOT assigns per node.

CONSTRAINT LEVELS:
  Velites:    Chain of Code available
  Hastati:    Faithful CoT available
  Principes:  Faithful CoT + ARQ gating available
  Triarii:    Mix + ARQ gating available

SET: Available = [Chain of Code / Faithful CoT / Faithful CoT+ARQ / Mix+ARQ]
```

### [examine] ITERATION_COUNT

```
CONTEMPLATE: Does quality require multiple passes?
             Does R + Q justify the token cost?

CONSTRAINT LEVELS:
  Velites:    1-shot
  Hastati:    1-shot (2-run if R≥5 ∧ Q≥6)
  Principes:  3-run kTTT
  Triarii:    3-run kTTT enforced

SET: Iterations = [1 / 2 / 3]
     Protocol = [single / ADAPT / kTTT]
```

### [examine] EXECUTION_PATTERN

```
NOTE: Imperatus makes patterns AVAILABLE. SkeletrainOT assigns per segment.

CONSTRAINT LEVELS:
  Velites:    Direct generation
  Hastati:    Baton Bolt
  Principes:  Baton + ARQ gating
  Triarii:    Swarm + ARQ gating

SET: Available = [Direct / Baton / Baton+ARQ / Swarm+ARQ]
```

### [examine] CoVE_DEPTH

```
CONTEMPLATE: How critical is correctness? What's the cost of error?

CONSTRAINT LEVELS:
  Velites:    Minimum (existence check only)
  Hastati:    Top-1 variant
  Principes:  Top-2 variants
  Triarii:    All variants ≥4 + multi-expert cross-check

SET: Depth = [Minimum / Top-1 / Top-2 / All+Multi]
```

### [examine] GAP_SCAN_DEPTH

```
CONTEMPLATE: How complex was execution? How many gaps are likely?

CONSTRAINT LEVELS:
  Velites:    Minimum (visual inspection sufficient)
  Hastati:    Light logic check
  Principes:  3-branch holistic
  Triarii:    Deep scan + auto-fix

SET: Depth = [Minimum / Light / 3-Branch / Deep+AutoFix]
```

---

## REFINE & OUTPUT CONSTRAINTS

### [examine] CURATION_DENSITY

```
CONTEMPLATE: What signal-to-noise ratio does the audience need?

Always active. Intelligent Curation is SYSTEM-CORE. Non-negotiable.

CONSTRAINT LEVELS:
  Velites:    Lean / max density
  Hastati:    Normal budget
  Principes:  Normal + nuance preserved
  Triarii:    All-out / comprehensive

SET: Density = [Lean / Normal / Normal+Nuance / All-Out]
```

### ── CONFIDENCE GATE: Output ready? Criteria met? >9/10 → proceed ──

### [examine] SELF_REFLECT_DEPTH

```
CONTEMPLATE: Did this execution produce patterns worth capturing?

CONSTRAINT LEVELS:
  Velites:    Minimum (nothing to learn)
  Hastati:    Note if notable
  Principes:  Technique effectiveness audit
  Triarii:    Full meta-analysis + BoT update

SET: Depth = [Minimum / Note / Audit / Full+BoT]
```

### [examine] OUTPUT_FORMAT

```
CONTEMPLATE: What comes AFTER this output?

FORMAT LOGIC:
  next_iteration_planned    → MLDoE compressed
  save/compress/context≥80% → CEP packet
  default                   → Narrative

SET: Format = [Narrative / MLDoE / CEP]
```

---

## VELITES FAST PATH

When mode = Velites, skip the [examine] loop. Apply minimum constraints:

```
VELITES DEFAULTS:
  Memory:       Read
  Criteria:     Implicit
  ARQ:          Pre-Turn | light
  Anti-Lazy:    Advisory
  USC:          1-path
  Experts:      0
  Skeleton:     Direct
  Bombs:        Clarifier if needed
  Reasoning:    Chain of Code
  Iteration:    1-shot
  Execution:    Direct
  CoVE:         Minimum
  Gap Scan:     Minimum
  Curation:     Lean
  Self-Reflect: Minimum
  Format:       Narrative
```

No contemplation overhead. [marshal] uses defaults → [issue].

---

## EXECUTION MANIFEST

After all constraints set, [marshal] assembles:

```
=== EXECUTION MANIFEST ===
Mode: [Velites/Hastati/Principes/Triarii]
R=[N] K=[N] Q=[N] D=[N] E=[N]

CRITERIA:
  ✓ [1] ... ✓ [N]

CONSTRAINTS:
  Memory:       [level]
  Criteria:     [rigidity]
  ARQ:          [coverage] | [strictness]
  Anti-Lazy:    [enforcement]
  USC:          [candidates]
  Experts:      [count] | Formation: [template]
  Skeleton:     [scale] | Nodes: [N]
  Bombs:        [arsenal] | Count: [N]
  Reasoning:    [available styles]
  Iteration:    [count] | Protocol: [type]
  Execution:    [available patterns]
  CoVE:         [depth]
  Gap Scan:     [depth]
  Curation:     [density]
  Self-Reflect: [depth]
  Format:       [type]

Confidence: [X/10]
=== SEALED → SKELETRAIN ===
```

---

## IMPLEMENTATION NOTES (for Claude Code)

```
1. Human-readable spec. Real implementation is S2A.
2. Each [examine] = one constraint-setting step in the MCP.
3. Manifest builds progressively across steps.
4. [marshal] = final assembly. [issue] = lock and send.
5. [halt] fires on confidence gate failure.
6. [reconsider] revises a previous constraint with cascade.
7. Velites fast path = single call, returns defaults manifest.
8. State validated server-side. Phase order enforced.
```
