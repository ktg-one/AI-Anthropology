---
title: "FCoT / CoC — Reasoning Router"
version: "v31"
status: "ACTIVE"
model: "Multi-model"
tags: ["fcot", "coc", "reasoning", "routing", "hybrid", "legio", "execution", "active"]
created: "2026-02-21"
updated: "2026-02-21"
creator: "ktg"
category: "execution-module"
description: "Reasoning style selection per execution node. FCoT (Faithful Chain of Thought) for exploration and ambiguity. CoC (Chain of Code) for deterministic verification. Hybrid for complex problems. Decision is per-node, not per-task — Legatus assigns reasoning type in the railroad."
legio_phase: "Execution"
pipeline_position: "Step 7 (Execution Module — Reasoning Style)"
replaces: ["KTG-07 - FCOT-COC.MD"]
consumes: "LEGIO-05-LEGATUS_CORE_.md"
pairs_with: "LEGIO-08-BATON-SWARM_MOD_.md"
built_for: "Claude Code → S2A → MCP implementation"
---

# FCoT / CoC — REASONING ROUTER
**Reasoning Style Selection Per Node | Execution Module | Step 7**

*Two engines in the same machine. FCoT explores. CoC verifies. Legatus decides which engine runs at which node. This module defines the engines — Legatus assigns them.*

---

## PURPOSE

Not all thinking is the same shape. Analytical reasoning, creative synthesis, and code generation require fundamentally different cognitive approaches. Forcing one style everywhere degrades quality.

FCoT/CoC is the engine selector. Each node in the Legatus railroad gets assigned a reasoning type BEFORE execution begins. During execution, no decisions — just run the assigned engine.

**Legatus decides which engine per node. This module defines what each engine does.**

---

## THE TWO ENGINES

### FCoT — Faithful Chain of Thought (Exploration Engine)

Explores possibility space. Handles ambiguity, nuance, multi-perspective reasoning. Keeps intermediate reasoning visible and auditable.

**Strengths:** Ambiguity tolerance, creative synthesis, dialectic reasoning, context maintenance across long chains.

**Weaknesses:** Can wander. Slower to converge. Risk of over-exploration.

### CoC — Chain of Code (Verification Engine)

Deterministic execution. Treats reasoning as executable steps with verifiable outputs. State machine clarity.

**Strengths:** Precision, executable verification, formal proof support, deterministic outcomes.

**Weaknesses:** Brittle on ambiguous inputs. Cannot handle genuine uncertainty. Fails on nuance.

---

## ROUTING MATRIX

| Problem Type | Route | Why |
|---|---|---|
| Code generation / debugging | **CoC** | Executable verification, precision |
| Binary / boolean logic | **CoC** | Deterministic outcomes |
| Mathematical proofs | **CoC** | Formal verification |
| Algorithm design | **CoC** | State machine clarity |
| Natural language analysis | **FCoT** | Handles ambiguity |
| Creative synthesis | **FCoT** | Explores possibilities |
| Nuanced judgment | **FCoT** | Maintains context |
| Multi-perspective reasoning | **FCoT** | Dialectic reasoning |
| Ethical / philosophical | **FCoT** | Ambiguity tolerance |
| Complex multi-domain | **Hybrid** | Explore → Verify → Synthesise |

**Default:** FCoT (safer for uncertainty).

---

## HYBRID MODE

For complex problems requiring both exploration and verification. Pattern: **FCoT → CoC → FCoT**.

```
Phase 1 — FCoT: Explore requirements, map terrain, identify constraints
Phase 2 — CoC:  Implement precise logic, validate formally, execute deterministically
Phase 3 — FCoT: Synthesise into coherent narrative, integrate findings, resolve tensions
```

**Example:** "Design auth system"
1. **FCoT:** Explore requirements, threat models, tradeoffs, user flows
2. **CoC:** Implement JWT logic, validation chains, encryption selection
3. **FCoT:** Synthesise into architectural narrative, weigh tradeoffs, recommend

**When Hybrid:** Node involves both creative/analytical AND deterministic components. Legatus marks these as `reasoning: hybrid` in the railroad.

---

## DECISION TREE

```
Legatus assigns per node. If manual override needed:

Problem has executable tests?     → YES → CoC
Needs formal proof?               → YES → CoC
Involves code generation?         → YES → CoC (or Hybrid if architecture-level)
Has genuine ambiguity/nuance?     → YES → FCoT
Needs creative exploration?       → YES → FCoT
Multiple valid interpretations?   → YES → FCoT
Mixed creative + deterministic?   → YES → Hybrid
DEFAULT                           → FCoT
```

---

## MODEL PROFILES

Different models have different native reasoning styles. Router accounts for this.

| Model | Native Bias | Adjustment |
|---|---|---|
| **Claude (Sonnet/Opus)** | FCoT native | Use CoC for deterministic domains. Naturally strong at exploration. |
| **GPT-4o/5** | FCoT native | Similar to Claude. CoC for code-specific tasks. |
| **Gemini** | CoC bias | Force FCoT for multi-perspective tasks. Default CoC is fine for structured work. |
| **Qwen / DeepSeek** | FCoT | Simple CoC only for straightforward algorithms. Complex CoC may degrade. |

**Cross-model rule:** When model has native CoC bias, FCoT assignments need explicit "explore before concluding" instruction. When model has FCoT bias, CoC assignments need explicit "converge, don't wander" instruction.

---

## MODE ACTIVATION

| Mode | Reasoning Assignment | Hybrid Available |
|---|---|---|
| **Velites** | Single reasoning type (usually CoC for simple, FCoT for ambiguous) | No |
| **Hastati** | Per-node assignment from Legatus | Yes, for complex nodes |
| **Principes** | Per-node assignment + ARQ between reasoning phases | Yes, with ARQ gates between phases |
| **Triarii** | Per-node assignment + ARQ + cross-candidate reasoning comparison | Yes, with full verification overlay |

---

## INTEGRATION

### With Legatus (LEGIO-05)
```
Legatus railroad includes per-node:
├─ node_id: "N3"
├─ reasoning: "fcot" | "coc" | "hybrid"
├─ reasoning_rationale: "Multi-perspective analysis required"
└─ If hybrid: phase boundaries specified
```

### With USC (LEGIO-03)
Generate candidates using BOTH reasoning styles. Compare consistency. If FCoT and CoC candidates agree → high confidence. If they diverge → investigate the disagreement (it's usually informative).

### With CoVE (LEGIO-09)
- CoC output → verify via test execution / formal checks
- FCoT output → verify via logical consistency / multi-expert review
- Hybrid output → verify both phases independently

### With Consilium (LEGIO-04)
Expert roles map to reasoning styles:
- Software Engineer → CoC
- Domain Analyst → FCoT
- Architect → Hybrid
- Researcher → FCoT

---

## TOKEN OVERHEAD

```
ROUTING DECISION: ~2% tokens (negligible — single classification)
QUALITY ROI:      15-30% accuracy improvement by matching reasoning style to problem

COST BY TYPE:
├─ Pure FCoT:  Baseline
├─ Pure CoC:   -10% tokens (shorter, more structured)
├─ Hybrid:     +15% tokens (three phases vs one)
└─ Wrong match: -20% quality (FCoT on deterministic = wandering; CoC on ambiguous = brittle)
```

---

## PIPELINE RELATIONS

| Direction | Module | Relationship |
|---|---|---|
| **Receives** | LEGIO-05 Legatus | Per-node reasoning assignment in the railroad |
| **Receives** | LEGIO-01 Armatura | Constraint level (affects hybrid availability) |
| **Parallel** | LEGIO-08 Baton/Swarm | Reasoning style operates WITHIN execution pattern |
| **Feeds** | LEGIO-09 CoVE | Verification variant matched to reasoning type used |
| **Referenced by** | LEGIO-12 Self-Reflect | Records which reasoning styles worked best for pattern capture |

---

## OUTPUT

```
PER NODE:
├─ reasoning_type: [fcot | coc | hybrid]
├─ reasoning_output: [the actual content]
├─ confidence: [N/10]
├─ if hybrid:
│   ├─ phase_1_output: [FCoT exploration]
│   ├─ phase_2_output: [CoC verification]
│   └─ phase_3_output: [FCoT synthesis]
└─ reasoning_trace: [auditable chain showing how conclusion was reached]

→ Content flows to Baton/Swarm execution pattern (LEGIO-08)
```

**Status:** Reasoning engine assigned. Thinking style locked per node. Execute.

---

*LEGIO v31 | Module 07 | Phase: EXECUTION | Reasoning Router*
*Source: KTG-07 FCOT-COC.MD*
*"FCoT explores. CoC verifies. Hybrid does both. Legatus decides which."*
