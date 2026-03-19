---
name: skeletrain
description: SkeleTraIn of Thought - Execution planning framework that creates the structural skeleton before elaboration. Use after Nexus-Router global decisions, before Baton/Swarm execution. Triggers on structure planning, node decomposition, expert assignment, dependency mapping, railroad track planning, or when KTG-DIRECTIVE Phase 5 is invoked. Receives global routing (Mode, USC, ARQ depth, CoVE) from Nexus-Router and plans per-node execution.
---

# SKELETRAIN OF THOUGHT
**Phase 5 of KTG-DIRECTIVE | Execution Planning**

Plans the structural skeleton that gets ARQ-gated throughout execution. Receives global decisions from Nexus-Router, outputs execution-ready structure.

## Input from Nexus-Router

| Global Decision | Used By SkeleTraIn |
|-----------------|-------------------|
| Mode (QUICK/ANALYTICAL/DELIBERATE/MAX) | Constrains structure depth |
| USC Level (0/2/3/5) | Parallel structure candidates |
| ARQ Depth (O/R-partial/R-full) | Gate placement density |
| CoVE Variants | Verification checkpoints |
| Output Intent | Shapes node granularity |
| Experts Deployed | Available for assignment |

## SkeleTraIn Process

### 1. NODE DECOMPOSITION

Break task into discrete execution units:

```
TASK → Node Analysis
├─ What distinct components does response need?
├─ What's the minimum viable structure?
├─ Impact score per node (1-10)
└─ Success criteria per node
```

**Node Types:**
- CORE: Must be present (impact ≥8)
- SUPPORTING: Adds value (impact 5-7)
- OPTIONAL: If budget allows (impact <5)

### 2. DEPENDENCY MAPPING (Railroad Tracks)

```
Independent nodes → Swarm candidates
Sequential nodes → Baton candidates

MAP:
Node-1 ──→ Node-3 ──→ Node-5  (Baton chain A)
              ↓
Node-2 ──→ Node-4              (Baton chain B)
              ↓
           Node-6              (Merge point)
```

**Decision:** 
- Dependencies exist → Baton Passing
- Independent → Expert Swarm
- Mixed → Hybrid (swarm with baton handoffs)

### 3. EXPERT → NODE ASSIGNMENT

```
For each node:
├─ Which expert owns this? (from MR.RUG deployment)
├─ Primary responsibility
├─ Consultation rights (who can they ask?)
└─ Handoff target (who receives their output?)
```

### 4. PER-NODE TECHNIQUE ROUTING

Within global bounds set by Nexus-Router:

| Node Characteristic | Route |
|--------------------|-------|
| Code/algorithm | CoC |
| Analysis/creative | FCoT |
| Mixed | Hybrid (FCoT→CoC→FCoT) |

**ARQ Gate Placement:**
- Impact ≥8 nodes: Pre-ARQ + Post-ARQ
- Impact 5-7 nodes: Post-ARQ only
- Impact <5 nodes: Skip ARQ (unless MAXIMUM mode)

### 5. PROMPT BOMB MATRIX

Pre-embed bombs for context preservation:

**High-Risk Zones:**
- Cross-domain handoffs (security↔frontend, data↔API)
- Token boundary regions (80%+ context)
- Complex inference chains
- Temporal gaps between related concepts

**Bomb Types:**

| Type | Purpose | Example |
|------|---------|---------|
| CONTINUITY | Preserve cross-node context | "At Node-4, remember auth decision from Node-1" |
| ANCHOR | Lock core principles | "This constraint applies to all subsequent nodes" |
| BRIDGE | Explain non-obvious connections | "Nodes 2-3 reasoning justifies this choice" |

See [references/prompt-bombs.md](references/prompt-bombs.md) for bomb construction patterns.

### 6. STRATEGY DISCUSSION

Experts discuss and debate before execution:

```
DISCUSSION AGENDA:
├─ Review node assignments - any objections?
├─ Identify uncertainty zones - where might we struggle?
├─ Agree on handoff protocols - what format between experts?
├─ Flag potential conflicts - preempt disagreements
└─ Confirm critical path - what MUST succeed?
```

### 7. CONFIDENCE GATE

Structure plan requires ≥9/10 confidence before execution:

```
CHECKLIST:
[ ] All nodes have clear ownership
[ ] Dependencies mapped completely
[ ] ARQ gates placed on high-impact nodes
[ ] Prompt bombs pre-embedded in risk zones
[ ] Expert agreement on approach
[ ] Success criteria defined per node

IF confidence <9/10:
├─ Identify weak points
├─ Revise structure
└─ Re-evaluate
```

## Output Artifact

```
SKELETRAIN EXECUTION PLAN
├─ Node Structure
│   ├─ Node-1: [description] | Owner: Expert-A | Impact: 9
│   ├─ Node-2: [description] | Owner: Expert-B | Impact: 7
│   └─ ...
├─ Railroad Tracks
│   ├─ Chain A: Node-1 → Node-3 → Node-5 (Baton)
│   └─ Chain B: Node-2, Node-4 (Swarm)
├─ Technique Routes
│   ├─ Node-1: FCoT | Pre-ARQ + Post-ARQ
│   ├─ Node-2: CoC | Post-ARQ only
│   └─ ...
├─ Prompt Bomb Matrix
│   ├─ Continuity: [bomb placements]
│   ├─ Anchor: [bomb placements]
│   └─ Bridge: [bomb placements]
├─ Critical Path: Node-1 → Node-3 → Node-6
└─ Plan Confidence: 9.2/10
```

## Integration Points

| Upstream | SkeleTraIn | Downstream |
|----------|------------|------------|
| Nexus-Router (globals) | Plans structure | Baton/Swarm (execution) |
| MR.RUG (experts) | Assigns to nodes | CoVE (verification) |
| Prompt Bombs (toolkit) | Places in matrix | Output Gate (routing) |

## Mode Scaling

| Mode | Node Depth | ARQ Coverage | Bomb Density |
|------|-----------|--------------|--------------|
| QUICK | Minimal (1-2 nodes) | None | None |
| ANALYTICAL | Standard (3-5 nodes) | High-impact only | Critical handoffs |
| DELIBERATE | Full (5-8 nodes) | All ≥5 impact | All risk zones |
| MAXIMUM | Exhaustive (8+ nodes) | Universal | Comprehensive |

## Verbose Mode

Trigger `/skeletrain-show` for planning trace:

```
=== SKELETRAIN PLANNING TRACE ===
[1] NODE DECOMPOSITION: 6 nodes identified
[2] DEPENDENCY MAP: 2 baton chains, 1 swarm cluster
[3] EXPERT ASSIGNMENT: 4 experts across 6 nodes
[4] TECHNIQUE ROUTING: 4 FCoT, 2 CoC
[5] BOMB MATRIX: 3 continuity, 2 anchor, 1 bridge
[6] STRATEGY DISCUSSION: Resolved 1 conflict
[7] CONFIDENCE: 9.3/10 ✓
=== READY FOR EXECUTION ===
```

---
*SkeleTraIn v28 | Part of KTG-DIRECTIVE v28 | Kevin Tan (ktg.one)*
