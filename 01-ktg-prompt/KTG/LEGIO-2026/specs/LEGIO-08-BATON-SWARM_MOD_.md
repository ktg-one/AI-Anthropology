---
title: "Baton Bolt / Swarm — Execution Patterns"
version: "v31"
status: "ACTIVE"
model: "Multi-model"
tags: ["baton", "swarm", "execution", "sequential", "parallel", "legio", "active"]
created: "2026-02-21"
updated: "2026-02-21"
creator: "ktg"
category: "execution-module"
description: "Two execution patterns for elaborating Legatus nodes. Baton = sequential handoff with enriched context. Swarm = parallel strike with all experts seeing full structure. Hybrid available. Legatus assigns pattern per execution segment. Iteration protocol included."
legio_phase: "Execution"
pipeline_position: "Step 8 (Execution Module — Execution Pattern)"
replaces: ["KTG-10-EXE02-Baton-Swarm[RMOD].md", "KTG-08 - SWARM-BOLT.MD"]
consumes: "LEGIO-05-LEGATUS_CORE_.md"
pairs_with: "LEGIO-07-Faithful CoT-Chain of Code_MOD_.md"
built_for: "Claude Code → S2A → MCP implementation"
---

# BATON BOLT / SWARM — EXECUTION PATTERNS
**Sequential vs Parallel Node Elaboration | Execution Module | Step 8**

*Two formations. Same legion. Baton = column march (each unit enriches what the last delivered). Swarm = battle line (all units strike simultaneously). Legatus picks the formation per execution segment.*

---

## PURPOSE

Legatus lays the railroad. Faithful CoT/Chain of Code assigns reasoning engines. Baton/Swarm decides HOW the legion moves along those tracks.

**Baton:** Sequential. Expert A finishes Node 1, passes enriched context to Expert B for Node 2. Each handoff carries accumulated intelligence. Order matters — dependencies respected.

**Swarm:** Parallel. All experts see the full structure and execute their assigned nodes simultaneously. Speed over accumulation. Independence assumed.

The decision is structural, not preferential. Dependencies → Baton. Independence → Swarm. Both → Hybrid.

---

## BATON BOLT (Sequential Execution)

```
Expert A          Expert B          Expert C
   │                 │                 │
   ▼                 │                 │
[Node 1]             │                 │
Pre-ARQ → Elaborate → Post-ARQ (≥0.9)
   │                 │                 │
   └── HANDOFF ──────▶                 │
                     ▼                 │
                  [Node 2]             │
                  Pre-ARQ → Elaborate → Post-ARQ (≥0.9)
                     │                 │
                     └── HANDOFF ──────▶
                                       ▼
                                    [Node 3]
                                    Pre-ARQ → Elaborate → Post-ARQ (≥0.9)
```

### Baton Mechanics

1. **Pre-ARQ:** Before elaborating, check: does this node have everything it needs from upstream?
2. **Elaborate:** Execute assigned reasoning type (Faithful CoT/Chain of Code/Hybrid from LEGIO-07)
3. **Post-ARQ:** Quality gate. Confidence ≥ 0.9 to proceed. Below → flag, patch, re-elaborate.
4. **Handoff:** Pass enriched context to next expert/node. Context accumulates.

### Baton Enrichment

Each handoff carries:
- Completed node output
- Confidence score
- Observer notes (gaps spotted, potential bombs for final pass)
- Accumulated context from all prior nodes

**Compound quality:** Baton^n × ARQ^n per transit. Quality compounds across the chain.

### When Baton

- Nodes have **dependencies** (Node 3 needs Node 2's output)
- Building **narrative flow** (each section builds on previous)
- **Sequential reasoning** required (proof chains, step-by-step derivation)
- Knowledge **accumulation** is the goal (each node enriches the whole)

---

## EXPERT SWARM (Parallel Execution)

```
Expert A          Expert B          Expert C
   │                 │                 │
   ▼                 ▼                 ▼
[Node 1]          [Node 2]          [Node 3]
Pre-ARQ           Pre-ARQ           Pre-ARQ
Elaborate         Elaborate         Elaborate
Post-ARQ (≥0.9)  Post-ARQ (≥0.9)  Post-ARQ (≥0.9)
   │                 │                 │
   └────────┬────────┘                 │
            └──────────┬───────────────┘
                       ▼
                  [MERGE POINT]
                  Unify outputs
                  Resolve conflicts
```

### Swarm Mechanics

1. **All experts see full structure** (Legatus blueprint distributed to everyone)
2. **Pre-ARQ per expert:** Does this expert have what they need for their nodes?
3. **Parallel elaboration:** All nodes worked simultaneously
4. **Post-ARQ per expert:** Each node independently quality-gated (≥ 0.9)
5. **Merge:** Unify parallel outputs, resolve any conflicts at junction points

### Swarm Strength

- **Speed:** N experts in time of 1 (amortised)
- **Independence:** No handoff delay, no sequential bottleneck
- **Diversity:** Each expert's work uncontaminated by others (can reveal genuine disagreements)

### When Swarm

- Nodes are **independent** (no upstream dependencies)
- Parallel **domains** (security expert and UX expert working different concerns)
- **Speed** is critical (time-constrained execution)
- Want **uncontaminated perspectives** (swarm reveals real disagreements, baton can mask them)

---

## HYBRID PATTERN

Swarm with baton handoffs at dependency points.

```
[Segment A: Swarm]     [Segment B: Baton]     [Segment C: Swarm]
Nodes 1,2,3 parallel → Node 4 depends on → Nodes 5,6 parallel
                        1+2+3 merge
```

Legatus marks the railroad with:
- `execution: swarm` for independent segments
- `execution: baton` for dependent chains
- Junction points where patterns transition

---

## MODE REQUIREMENTS

| Mode | Pattern | Notes |
|---|---|---|
| **Velites** | Direct generation | No Baton/Swarm. Single-pass output. |
| **Hastati** | Baton (single chain) | Sequential elaboration. Simple handoffs. |
| **Principes** | Baton OR Swarm | Legatus chooses per segment. Hybrid available. |
| **Triarii** | Full Swarm + Multi-Baton | Maximum parallelism. Multiple baton chains. USC≥3 → parallel baton chains, choose best. |

---

## ITERATION PROTOCOL

When Armatura sets iteration count > 1, Baton/Swarm runs multiple passes:

```
ITERATION MODEL:
├─ Single-pass:  Execute once. Deliver.
├─ 2-run (kTTT): Execute → Review → Re-execute with patches
└─ 3-run (ADAPT): Execute → Enrich (LEGIO-15) → Final polish
```

| Mode | Iterations | Iteration Style |
|---|---|---|
| **Velites** | 1 (single pass) | No iteration |
| **Hastati** | 1 (optional 2) | Single pass. Optional review if confidence < 0.8 |
| **Principes** | 2-3 (required) | 2-run default. 3 if quality gate fails. |
| **Triarii** | 3 (enforced) | Full 3-pass. No shortcuts. |

---

## DECISION LOGIC

```
Legatus assigns per execution segment:

Nodes have dependencies?          → BATON
Nodes are independent?            → SWARM
Complex + time-critical?          → HYBRID (swarm with baton at junction points)
USC ≥ 3?                         → Parallel baton chains (one per candidate)
Single node?                     → Neither (direct execution)
```

---

## ARQ INTEGRATION

ARQ gates fire at every handoff and merge point:

```
BATON ARQ:
├─ Pre-ARQ:  Before each node elaboration
├─ Post-ARQ: After each node (≥0.9 to handoff)
└─ Chain-ARQ: Accumulated quality check at chain end

SWARM ARQ:
├─ Pre-ARQ:  Before each parallel expert starts
├─ Post-ARQ: After each expert finishes (≥0.9 to merge)
└─ Merge-ARQ: After unification (conflict resolution quality)
```

---

## TOKEN OVERHEAD

```
BATON:
├─ Token cost:   ~20% overhead (context accumulation per handoff)
├─ Quality gain:  Sequential build-up, compounding confidence
├─ Scales:        Linearly with node count
└─ Sweet spot:    3-7 nodes in chain

SWARM:
├─ Token cost:   ~25% overhead (full structure distributed to all experts)
├─ Quality gain:  Parallel quality multiplication, uncontaminated perspectives
├─ Scales:        With expert count (diminishing above 5)
└─ Sweet spot:    3-5 parallel experts

HYBRID:
├─ Token cost:   ~30% overhead (both patterns + merge points)
├─ Quality gain:  Best of both — parallel speed + sequential depth
└─ Use when:      Mixed dependency structure
```

---

## PIPELINE RELATIONS

| Direction | Module | Relationship |
|---|---|---|
| **Receives** | LEGIO-05 Legatus | Execution pattern assignment per segment in railroad |
| **Receives** | LEGIO-07 Faithful CoT/Chain of Code | Reasoning type per node (executed within Baton/Swarm) |
| **Receives** | LEGIO-01 Armatura | Iteration count, pattern availability |
| **Receives** | LEGIO-03 USC | Candidate count (USC≥3 → parallel baton chains) |
| **Receives** | LEGIO-04 Consilium | Expert roster (who executes which nodes) |
| **Feeds** | LEGIO-09 CoVE | Elaborated outputs for verification |
| **Feeds** | LEGIO-10 GapScanalysis | Completed execution for gap detection |
| **Referenced by** | LEGIO-12 Self-Reflect | Records which patterns worked best |

---

## OUTPUT

```
EXECUTION_RESULT:
├─ pattern_used: [baton | swarm | hybrid]
├─ nodes_completed: [N/N]
├─ iterations_run: [1 | 2 | 3]
├─ per_node:
│   ├─ node_id: [from Legatus railroad]
│   ├─ expert: [who executed]
│   ├─ reasoning_type: [Faithful CoT | Chain of Code | hybrid]
│   ├─ confidence: [N/10]
│   ├─ arq_passed: [true | false]
│   └─ content: [elaborated output]
├─ merge_points: [if hybrid/swarm — conflict resolution log]
├─ handoff_log: [if baton — context accumulation trace]
└─ overall_confidence: [weighted average across nodes]

→ Flows to CoVE (LEGIO-09) for verification
```

**Status:** Nodes elaborated. Pattern executed. Handoffs clean. Ready for verification.

---

*LEGIO v31 | Module 08 | Phase: EXECUTION | Execution Patterns*
*Source: KTG-10-EXE02-Baton-Swarm[RMOD].md*
*"Baton builds depth. Swarm builds breadth. Hybrid builds both."*
