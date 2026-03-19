---
title: "Self-Reflect-Adapt — Technique Effectiveness Audit"
version: "v31"
status: "ACTIVE"
model: "Multi-model"
tags: ["self-reflect", "meta-learning", "bot", "technique-audit", "pattern-capture", "legio", "refine", "active"]
created: "2026-02-21"
updated: "2026-02-21"
creator: "ktg"
category: "refine-module"
description: "Post-delivery meta-learning. Audits which techniques fired, how effective each was, what synergies or anti-patterns emerged. Extracts reusable patterns for BoT (session-local) and CEP (cross-session). The cascade gets smarter with every execution."
legio_phase: "Refine & Output"
pipeline_position: "Step 15 (Refine Module — Technique Audit)"
replaces: ["KTG-14-POST02-Self-Ref-Adapt[MOD].md"]
consumes: "LEGIO-11-CENSOR_CORE_.md"
feeds: "LEGIO-13-OUTPUT-FORMAT_MOD_.md"
pairs_with: "LEGIO-16-CEP_MOD_.md"
built_for: "Claude Code → S2A → MCP implementation"
---

# SELF-REFLECT-ADAPT — TECHNIQUE EFFECTIVENESS AUDIT
**Meta-Learning | Refine Module | Step 15**

*Every execution teaches the cascade something. After delivering output, Self-Reflect audits what happened — which techniques fired, which performed, which synergised or conflicted. Novel patterns get saved to BoT (session memory). Cross-session insights feed CEP (persistent memory). The loop closes: future executions retrieve proven stacks for similar problems.*

---

## PURPOSE

The pipeline up to this point is forward-looking — score, plan, execute, verify, synthesise, deliver. Self-Reflect looks backward. It asks: what just happened, and what can we learn from it?

This is the cascade's learning mechanism. Without it, every execution starts from scratch. With it, proven technique combinations accumulate, anti-patterns get flagged, and the system adapts to the user's problem landscape over time.

**Key distinction:** Self-Reflect does NOT modify the output already delivered. It runs AFTER delivery. Its value is in the patterns it captures for future use.

---

## POSITION IN PIPELINE

```
[Censor delivers output]  →  SELF-REFLECT (this module)  →  [Output Format / CEP]
                                       ↑
                          Full execution trace available
                          Technique stack with parameters
                          Confidence scores at each gate
                          User feedback (if any)
```

**Receives:**
- Complete execution trace (every technique that fired, with parameters)
- Synthesis manifest from Censor (path chosen, density achieved)
- Gate results from all ARQ checkpoints
- Final confidence score
- User feedback (explicit if available, implicit from follow-ups)

**Produces:**
- Technique effectiveness scores
- Extracted patterns (success, failure, discovery, efficiency)
- BoT entries for session-local retrieval
- CEP R-label metadata for cross-session transfer

---

## FOUR-PHASE AUDIT

### Phase 1: Technique Inventory

Scan the execution trace. Catalog every technique that activated.

```
FOR EACH technique IN [
  ARQ, USC, MR.RUG, SkeletrainOT, GoT, Prompt Bombs,
  Faithful CoT, Chain of Code, Baton, Swarm, CoVE, GapScanalysis, Censor/ISC, MLDoE
]:
  IF technique activated:
    RECORD:
      name, mode_level, parameters_used, trigger_reason
```

Outputs: `technique_stack[]` and `stack_complexity` (count of activated techniques).

### Phase 2: Effectiveness Measurement

For each technique in the stack, evaluate four dimensions:

| Dimension | Weight | Questions |
|-----------|--------|-----------|
| **Contribution** | 0.40 | Did it improve final output? By how much? Was it worth the token cost? |
| **Efficiency** | 0.25 | Token overhead vs value added. Execution time impact. Complexity introduced. |
| **Quality Impact** | 0.25 | Confidence delta attributable to this technique. Gaps reduced. |
| **Synergies** | 0.10 | Which techniques amplified it? Which conflicted? Optimal ordering? |

```
effectiveness = contribution×0.40 + efficiency×0.25 + quality_impact×0.25 + synergies×0.10
```

### Phase 3: Pattern Extraction

Four pattern categories:

**Success Patterns** — What worked exceptionally well?
- Technique combinations with high collective effectiveness
- Parameter settings that produced best results
- Problem characteristics that favored specific techniques
- Expert configurations that were optimal

**Failure Patterns** — What underperformed?
- Techniques that didn't justify their token cost
- Combinations that created conflicts (e.g., Swarm on high-dependency problems)
- Parameter settings that caused issues

**Discovery Patterns** — What was novel?
- Unexpected technique applications
- New synergies not previously documented
- Creative edge-case solutions

**Efficiency Patterns** — What shortcuts maintained quality?
- Techniques safely skippable for certain problem types
- Optimal ordering discoveries
- Resource allocation strategies

### Phase 4: Contextual Metadata

Capture the full execution context to make patterns retrievable:

```
problem_signature:
  R_score, K_score, Q_score, D_score, E_score
  domain, user_style, constraints

outcome_quality:
  final_confidence, user_feedback, unfixed_gaps
  synthesis_path, density_achieved

lessons_learned:
  what_worked, what_failed, innovations, optimisations
```

---

## BoT UPDATE PROTOCOL

Buffer of Thought (BoT) — session-local pattern storage. Enables retrieval of proven technique stacks for similar problems within the same session.

### Save Criteria

A pattern is saved to BoT when ANY of these criteria are met:

| Criterion | Threshold | Rationale |
|-----------|-----------|-----------|
| Reasoning complexity | R >= 6 | Problem complex enough to learn from |
| Exceptional performance | effectiveness >= 0.85 | Technique stack performed well above average |
| Novel pattern | novelty = true | Discovery worth preserving |

### BoT Entry Structure

```
pattern:
  id: [UUID]
  tier: 2 or 3    # Tier 2 = R6-8 (hard), Tier 3 = R8+ (difficult)
  R_range: [6, 8]
  domains: [domain1, domain2]

  problem_signature:
    [from Phase 4 contextual metadata]

  technique_stack:
    - technique: MR.RUG
      effectiveness: 0.87
      parameters: {expert_count: 5}
      notes: "5 experts optimal for this domain combination"

  execution_template:
    recommended_mode: DELIBERATE
    expert_configuration: [...]
    technique_ordering: [...]
    key_decisions: [...]

  lessons:
    critical_success_factor: "Early ARQ gate prevented scope creep"
    avoid: "Swarm execution when D >= 7"
    synergy: "SkeletrainOT + Baton exceptional for this structure"

  retrieval_tags: [multi_domain_synthesis, high_interdependency, 5_expert_optimal]
```

### BoT Tier Assignment

| Tier | R Range | Problem Class |
|------|---------|---------------|
| Skip | R < 6 | Too simple to warrant pattern storage |
| Tier 2 | R 6–8 | Hard problems — proven technique stacks |
| Tier 3 | R 8+ | Difficult problems — deep execution schemas |

---

## CEP INTEGRATION

When CEP handoff occurs (session end, context limit, model switch), Self-Reflect contributes R-label metadata to the CEP packet.

### R-Label Mapping

| R Score | Q Score | CEP Reasoning Level |
|---------|---------|---------------------|
| 1–3 | 1–5 | L1 (quick) |
| 4–6 | 6–7 | L2 (analytical) |
| 7–8 | 8 | L3 (deliberate) |
| 9+ | 9+ | L4 (maximum) |

### CEP Contribution Data

```
cep_metadata:
  reasoning_level: L3
  source_model: [model_id]
  technique_stack_used: [from Phase 1]
  effectiveness_summary: [from Phase 2]
  pattern_insights: [from Phase 3]
```

This data accumulates in the CEP thought buffer over time, enabling queries like:
- "Similar L3 problems used these technique stacks..."
- "For R8 + K7, this configuration works best..."
- "Cross-domain synthesis? These patterns excel..."

---

## MODE SCALING

| Mode | Reflection Depth | BoT Save | CEP Contribution | Output |
|------|-----------------|----------|------------------|--------|
| **QUICK** (Velites) | SKIP — no reflection overhead | No | No | None |
| **ANALYTICAL** (Hastati) | Light — simple effectiveness check | If R >= 6 and pattern novel | No | Silent (internal only) |
| **DELIBERATE** (Principes) | Full technique audit | Yes — pattern extraction + save | If handoff triggered | Compact reflection summary |
| **MAXIMUM** (Triarii) | Deep meta-analysis + cross-technique synergy | Yes — full audit + save | Yes — full R-label contribution | Detailed meta-analysis |

### Output by Mode

**ANALYTICAL** (internal, or on explicit "what did you learn?" request):
```
LEARNINGS:
├─ Stack: ARQ → MR.RUG → SkeletrainOT → CoVE
├─ Top: ARQ (0.89), SkeletrainOT (0.87)
└─ Saved to BoT Tier 2 (R=6 domain synthesis)
```

**DELIBERATE:**
```
REFLECTION:
Techniques: 8 used
├─ Highest impact: ARQ (prevented scope drift)
├─ Best synergy: SkeletrainOT + Baton (structure + execution)
└─ Underperformed: Swarm (dependencies too tight for parallel)

Pattern: "Multi-domain technical synthesis"
└─ Saved to BoT Tier 2 for R=6-7 problems

Optimisation: Skip Swarm when D >= 7
```

**MAXIMUM:**
```
META-ANALYSIS:

TECHNIQUE AUDIT:
├─ ARQ (Pre-Turn): 0.89
│  └─ Prevented 3 scope creep instances
├─ MR.RUG (5 experts): 0.82
│  └─ 5 optimal (4 too few, 6 redundant)
├─ SkeletrainOT: 0.87
│  └─ 7 nodes, dependencies well-mapped
├─ Baton: 0.84
│  └─ Sequential build-up crucial
├─ CoVE (2 variants): 0.79
│  └─ FACTUAL + LOGICAL sufficient, CONSISTENCY overkill
├─ GapScanalysis: 0.91
│  └─ Caught 2 gaps CoVE missed
├─ Censor (Hierarchical): 0.88
│  └─ Best path for multi-audience output
└─ Density (Normal+): 0.76
   └─ 51% compression, nuance preserved

SYNERGIES: SkeletrainOT→Baton, ARQ→GapScanalysis, MR.RUG→Censor
ANTI-PATTERNS: Swarm at D=7 (reverted to Baton)

PATTERN: "Multi-Domain Technical Synthesis, High Dependencies"
R=7, K=6, Q=8, D=7, E=5
Template: ARQ → MR.RUG(5) → SkeletrainOT → Baton → CoVE(2) → GapScanalysis → Censor
Saved: BoT Tier 2  |  Tags: [multi_domain, high_dependency, technical_synthesis]

CEP: L3 contribution  |  Indexed: "L3 multi-domain synthesis"
```

---

## LONG-TERM LEARNING ACCUMULATION

Self-Reflect generates compounding value over time.

### After ~100 executions:
- ~23 proven patterns in BoT
- ~8 technique optimisations discovered
- ~5 model-specific adaptations learned
- ~67% faster routing from pattern recognition

### After ~1000 executions:
- L1-L4 reasoning levels well-indexed in thought buffer
- Cross-domain patterns established
- Model performance profiles refined
- Automatic technique selection improves ~43%
- Cascade adapts to user style automatically

### Model-Specific Learnings (accumulated over time)

```
model_learnings[claude]:
  strengths: [ARQ, SkeletrainOT, GapScanalysis]
  optimal_expert_count: 5-8
  density_sweet_spot: 0.6-0.7

model_learnings[gpt]:
  strengths: [Faithful CoT, Synthesis, Creative]
  optimal_expert_count: 3-5
  density_sweet_spot: 0.5-0.6
```

---

## QUALITY GATES

| Gate | Check | Pass | Fail |
|------|-------|------|------|
| **GATE_WORTH_SAVING** | R >= 6 OR effectiveness >= 0.85 OR novelty? | Save to BoT | Skip — pattern too simple/common |
| **GATE_PATTERN_QUALITY** | Problem signature clear? Stack replicable? Lessons concrete? Tags meaningful? | Save | Refine pattern or flag incomplete |
| **GATE_CEP_READY** | R-label assigned? Effectiveness measured? Patterns extracted? | Contribute to thought buffer | Skip CEP contribution |

---

## FAILURE MODES

### Over-saving to BoT
**Symptom:** BoT cluttered with trivial patterns.
**Prevention:** Strict R >= 6 threshold. Novelty detection (skip if pattern exists). Effectiveness minimum 0.85.
**Recovery:** Prune low-retrieval patterns after 3 months.

### Incorrect Effectiveness Attribution
**Symptom:** Technique credited or blamed for outcomes it didn't drive.
**Prevention:** Multi-metric evaluation. Synergy detection (don't credit solo). Baseline comparison.
**Recovery:** Manual review of outlier scores.

### Pattern Over-generalisation
**Symptom:** Pattern applied to wrong problem types.
**Prevention:** Detailed problem signature. Clear domain tags. Context preservation.
**Recovery:** Narrow retrieval tags, refine applicability.

---

## INTEGRATION POINTS

| Module | Relationship |
|--------|-------------|
| **Censor** (LEGIO-11) | Receives synthesis manifest, effectiveness data, final confidence |
| **Imperatus** (LEGIO-00) | Receives original RKQDE scores for problem signature |
| **Armatura** (LEGIO-01) | Receives technique constraint levels for audit baseline |
| **CEP** (LEGIO-16) | Feeds R-label metadata + technique insights for cross-session transfer |
| **Output Format** (LEGIO-13) | Self-Reflect output appended based on mode |
| **ARQ** (all gates) | Receives gate pass/fail results for quality tracking |

---

## TOKEN OVERHEAD

| Mode | Audit Cost | BoT Write | CEP Write | Total |
|------|-----------|-----------|-----------|-------|
| QUICK | 0 (skipped) | 0 | 0 | 0 |
| ANALYTICAL | ~30 tokens (internal) | ~50 if saved | 0 | ~80 |
| DELIBERATE | ~100 tokens | ~100 | ~50 if handoff | ~250 |
| MAXIMUM | ~250 tokens | ~150 | ~100 | ~500 |

Self-Reflect is a low-cost module. The patterns it captures pay forward across future executions.

---

*LEGIO v31 | Self-Reflect-Adapt — Technique Effectiveness Audit | Refine Module*
*"The cascade gets smarter with every use. Every execution teaches something."*
