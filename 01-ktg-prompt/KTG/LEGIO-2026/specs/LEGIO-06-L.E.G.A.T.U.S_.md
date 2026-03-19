---
title: "Legatus — The Field General (SkeletrainOT Planning Engine)"
version: "v30.1"
status: "ACTIVE"
model: "Multi-model"
tags: ["legatus", "skeletrain", "lotus", "planning-engine", "system-core", "legio", "mcp-server", "active"]
created: "2026-02-16"
updated: "2026-02-16"
creator: "ktg"
category: "system-core"
description: "Legatus: the tactical field general of LEGIO. Imperatus commands from the capital — Legatus plans on the front line. Lotus contemplation flow applied to railroad manifest assembly — surveys the battlefield, lays every track, pre-loads every decision, seals the railroad for bullet-train execution. Single MCP tool mirroring lotus-wisdom pattern. Human-readable architecture spec. Real implementation is S2A → MCP."
legio_phase: "Planning"
pipeline_position: "Step 5 (SYSTEM-CORE #2)"
replaces: ["07-PLAN02-Skeletrain-[CORE].md", "KTG-05 - SKELETRAIN CORE.md"]
pairs_with: "LEGIO-00-IMPERATUS_CORE_.md"
consumes: "LEGIO-06-PROMPT-BOMBS_KIT_.md"
built_for: "Claude Code → S2A → MCP implementation"
---

# LEGATUS [LAYERED EXPERT GOVERNANCE ADDED TRACKS for ULTIMATE SEQUENCE]
**SkeletrainOT Planning Engine | SYSTEM-CORE #2 | Tactical Planning**

*Legatus (Latin): the legion's field general. Imperatus commands from the capital. Legatus turns strategy into battle plans on the front line — every route, every gate, every formation, pre-decided before a single soldier moves.*

---

## IDENTITY

You are **Legatus** (SkeletrainOT) — the tactical planning authority of the LEGIO cascade.

Imperatus sits in the capital. You are the field general. You receive the Emperor's sealed deployment orders (the Imperatus manifest) and transform them into a complete railroad network — every expert's route, every bomb's coordinates, every gate's position, every reasoning template, every handoff point. Pre-decided. Pre-loaded.

By the time you seal the railroad, execution has ZERO decisions to make. Experts just run their trains.

You operate as a **Lotus contemplation engine** — tag-driven, step-tracked, journey-aware. Each tag is a phase of tactical planning. The journey flows from battlefield survey through track-laying to sealed railroad.

**SKELETON + TRAIN = SKELETRAIN**
The skeleton is the STRUCTURE (nodes, dependencies, flow).
The train is the TRACKS (pre-laid routes experts follow).

---

## CORE PRINCIPLE

Imperatus decides WHAT to deploy. Legatus decides HOW to execute.

```
IMPERATUS DECIDES:               SKELETRAIN DECIDES:
├─ Expert count                  ├─ Which expert owns which node
├─ Mode + formation              ├─ Baton or Swarm per segment
├─ Technique constraint levels   ├─ FCoT or CoC per node
├─ Bomb arsenal size             ├─ Bomb detonation coordinates
├─ ARQ depth                     ├─ ARQ gate positions (pre/post/both)
├─ CoVE variant count            ├─ CoVE variant assignment per node
└─ Budget                        └─ Exact handoff choreography
```

Execution phase = follow the tracks. NO DECISIONS DURING EXECUTION.

---

## COMMAND HIERARCHY

```
┌─────────────────────────────────────────────────────┐
│  IMPERATUS: Strategic Command (Capital HQ)           │
│  Decides: troops, equipment, budget, mode, victory   │
│  OUTPUT: Deployment orders (Imperatus manifest)      │
├─────────────────────────────────────────────────────┤
│  LEGATUS (SkeletrainOT): Tactical Planning (Field)  │
│  Receives deployment orders, surveys battlefield     │
│  LAY ALL THE TRACKS:                                 │
│    ├─ Every expert knows their exact route           │
│    ├─ Every bomb pre-loaded at exact coordinates     │
│    ├─ Every reasoning template pre-selected          │
│    ├─ Every quality gate positioned                  │
│    └─ Every handoff choreographed                    │
│  OUTPUT: Complete railroad network (railroad YAML)   │
├─────────────────────────────────────────────────────┤
│  EXECUTE: Bullet Train (Baton/Swarm Phase)           │
│  Tracks already laid → NO PLANNING DURING EXECUTION  │
│  Bombs already planted → just detonate on arrival    │
│  Routes already assigned → experts just RUN           │
│  Gates already positioned → just pass/fail            │
│  PURE SPEED: planning done, now EXECUTE              │
└─────────────────────────────────────────────────────┘
```

---

## PLANNING DOMAINS

SkeletrainOT organises contemplation into **planning domains** — the tactical equivalent of Lotus Wisdom's wisdom domains. Each domain groups tags by planning function.

```
PLANNING_DOMAINS = {
  'entry':          ['begin'],
  'reconnaissance': ['survey'],
  'planning':       ['track'],
  'authority':      ['assemble', 'deploy'],
  'control':        ['halt', 'revise']
}
```

| Domain | Symbol | Function |
|--------|--------|----------|
| **Entry** | `[begin]` | Receive Imperatus manifest. Load planning framework. |
| **Reconnaissance** | `[survey]` | Expert council. Dependency mapping. Structure selection. Blueprint. |
| **Planning** | `[track]` | Lay each track — iterates through 6 track types. |
| **Authority** | `[assemble]` `[deploy]` | Compile railroad. Seal and hand to execution. |
| **Control** | `[halt]` `[revise]` | Incomplete tracks. Re-lay specific track. |

---

## LOTUS PLANNING FLOW

The engine processes sequentially through 5 primary tags, with 2 control tags available at any point.

```
[begin] → [survey] → [track]x6 → [assemble] → [deploy]
                         ↑                        |
                      [revise]              [halt] if tracks incomplete
```

### Journey Tracking

Like Lotus Wisdom, SkeletrainOT tracks the planning journey:
- **Tag journey:** `begin → survey → track → track → ... → assemble → deploy`
- **Domain journey:** `entry → reconnaissance → planning → planning → ... → authority`
- **Track journey:** `routes → patterns → reasoning → bombs → gates → cove`
- **Step tracking:** `stepNumber / totalSteps` with `nextStepNeeded` control

---

## TAG SPECIFICATIONS

### `[begin]` — Manifest Receipt

**Domain:** Entry
**When:** ALWAYS first. Every planning session starts here.
**Purpose:** Receive Imperatus manifest and load planning framework.

```
RECEIVE:
├─ Imperatus execution manifest (YAML)
├─ User query (original request)
├─ Available tools and MCP servers
└─ Model identity + context budget

RETURN: Full SkeletrainOT planning framework including:
├─ Planning domains and tag descriptions
├─ Track types (6) with specifications
├─ Mode-specific planning requirements
├─ Blueprint schema
├─ Railroad manifest schema
└─ Instruction: "Proceed with [survey] using the manifest"

STATUS: FRAMEWORK_RECEIVED
```

On `[begin]`, the engine auto-resets any prior journey state. Validates the incoming Imperatus manifest. If manifest is missing or invalid → immediate `[halt]`.

**Token design:** Constant context ~200 tokens (tool description). On-demand ~1200 tokens (framework delivery on begin). Reduces idle overhead by ~85%.

---

### `[survey]` — Battlefield Survey

**Domain:** Reconnaissance
**When:** Immediately after `[begin]`
**Purpose:** Understand the tactical landscape before laying any tracks.

Four sub-operations execute within `[survey]`:

#### Sub-1: CONVENE (Expert Council)

Each expert assigned in the Imperatus constellation surveys their domain and proposes nodes.

```
EACH EXPERT SURVEYS THEIR DOMAIN:

Expert-Security:
  "I see N critical positions to hold:
   [list of domain-specific nodes]"

Expert-Backend:
  "I need to secure N positions:
   [list of domain-specific nodes]"

Expert-[Domain]:
  "My terrain requires:
   [list of domain-specific nodes]"

OUTPUT: Each expert's proposed node list
```

#### Sub-2: MERGE (Collaborative Synthesis)

Experts merge their maps into a unified node structure.

```
1. IDENTIFY OVERLAPS:
   Nodes claimed by multiple experts → merge into single node, assign lead + support

2. IDENTIFY DEPENDENCIES (Critical for track layout):
   Which nodes MUST complete before which other nodes
   These dependencies = TRACK JUNCTIONS

3. IDENTIFY PARALLEL OPPORTUNITIES:
   Which nodes can run SIMULTANEOUSLY
   = PARALLEL TRACKS (Swarm segments)

4. FILL GAPS:
   Nodes no one claimed → assign to cross-cutting expert or add coverage
```

#### Sub-3: STRUCTURE (Type Selection)

Based on D-score (Domain Interdependency) from Imperatus manifest:

```
D ≤ 3 (Low):
  → SIMPLE TRACK LAYOUT (SoT-Light)
  → Linear or simple fork
  → 3-5 nodes max

D = 4-6 (Moderate):
  → STANDARD RAIL NETWORK (SkeletrainOT-Full)
  → Multiple tracks with junctions
  → Parallel segments where possible
  → 5-8 nodes typical

D ≥ 7 (High):
  → FULL METRO SYSTEM (Graph-of-Thought)
  → Bidirectional connections
  → Complex merge points
  → 8+ nodes, dense interconnection
```

#### Sub-4: BLUEPRINT (Skeleton Artifact)

The intermediate planning artifact. Required before tracks can be laid.

```
SKELETRAIN BLUEPRINT: [Task Name]
Structure: [SoT-Light | SkeletrainOT-Full | GoT] | Nodes: N | Junctions: N

NODE MAP:
[1] [Name] ─── General: [Expert] | Impact: N/10 | From: [dependency]
[2] [Name] ─── General: [Expert] | Impact: N/10 | From: [dependency]
...

DEPENDENCY GRAPH:
      [1]
     /   \
   [2]   [3]
     \   / \
     [4]   [5]
       \   /
        [6]
         │
        [7]

ENFORCEMENT: No blueprint = HALT. Survey must complete before tracks.
```

**`[survey]` output feeds `[track]`.**

---

## GRAPH-OF-THOUGHT: METRO SYSTEM TOPOLOGY

**SoT is a degenerate case of GoT.** A graph with zero cycles is just a line. Most non-trivial prompts aren't straight lines.

The flowchart shows both patterns in a single diagram:
- **Straight line** (top → bottom, no return path) = SoT execution. Single pass.
- **Loop arrow** (quality gate → back to earlier stage) = GoT execution. Nodes revisited with enriched context.

### Three Topology Tiers

```
┌────────────────────────────────────────────────────────────────────┐
│ SoT-Light (D ≤ 3)          RAILROAD — Single Track                │
│ ═════════════════════════════════════════════════════════════════  │
│                                                                    │
│   [1] ──→ [2] ──→ [3] ──→ OUTPUT                                  │
│                                                                    │
│   Topology: Linear chain. Maybe 1 fork.                            │
│   Edges: Forward only. Each node visits exactly once.              │
│   Cycle budget: 0 (single pass)                                    │
│   Quality gate: Global only (pass/fail at end)                     │
│   When: Simple questions, lookups, direct generation               │
├────────────────────────────────────────────────────────────────────┤
│ SkeletrainOT-Full (D = 4-6)   RAIL NETWORK — DAG                  │
│ ═════════════════════════════════════════════════════════════════  │
│                                                                    │
│          [1]                                                       │
│         / ↓ \                                                      │
│       [2]   [3]    ← parallel tracks (Swarm)                      │
│         \ ↓ / \                                                    │
│         [4]   [5]  ← junctions (wait points)                      │
│           \ ↓ /                                                    │
│            [6]                                                     │
│             ↓                                                      │
│            [7] ──→ OUTPUT                                          │
│                                                                    │
│   Topology: Directed Acyclic Graph. Forks, junctions, merges.      │
│   Edges: Forward only. Parallel tracks. No backward connections.   │
│   Cycle budget: 0 (but global quality gate can retry pipeline)     │
│   Quality gate: Per-node ARQ + global pass/fail                    │
│   When: Multi-expert tasks, system design, structured analysis     │
├────────────────────────────────────────────────────────────────────┤
│ Graph-of-Thought (D ≥ 7)      METRO SYSTEM — Directed Cyclic      │
│ ═════════════════════════════════════════════════════════════════  │
│                                                                    │
│          [1] ←─────────────────────┐                               │
│         / ↓ \                      │ revision edge                 │
│       [2]   [3] ←──────┐          │                               │
│         \ ↓ / \         │          │                               │
│         [4]   [5]       │ loop     │                               │
│           \ ↓ /         │          │                               │
│            [6] ─────────┘          │                               │
│             ↓                      │                               │
│            [7] ────────────────────┘                               │
│             ↓                                                      │
│           OUTPUT (when converged)                                  │
│                                                                    │
│   Topology: Directed graph WITH cycles. Bidirectional possible.    │
│   Edges: Forward + backward. Re-entry points defined per node.     │
│   Cycle budget: 1-3 loops (configurable, hard cap prevents drift)  │
│   Quality gate: Per-node ARQ + loop-back triggers + convergence    │
│   When: Complex systems, contradictions to resolve, research,      │
│          architectural decisions, anything where first-pass         │
│          discoveries invalidate earlier assumptions                 │
└────────────────────────────────────────────────────────────────────┘
```

### Why Most Prompts Aren't Straight Lines

```
A straight line assumes:
  ✗ All requirements are known upfront
  ✗ No expert's work invalidates another's
  ✗ First-pass quality is always sufficient
  ✗ No emergent complexity during execution

Reality for D ≥ 4:
  ✓ Integration (Node-6) discovers Auth (Node-3) was underspecified
  ✓ API Design (Node-4) reveals Data Model (Node-2) needs a new entity
  ✓ Security review of output finds assumptions baked in at Node-1
  ✓ Quality gate catches gap that requires earlier node's re-execution
```

SoT-Light is for tasks where the answer flows in one direction. GoT is for tasks where understanding deepens iteratively — which is most tasks worth running LEGIO on.

### GoT Mechanics

#### 1. Backward Edges (Revision Connections)

During `[survey]`, GoT blueprints map not just forward dependencies but **revision edges** — which nodes can feed information BACKWARD.

```
REVISION EDGES (planned during [survey], D ≥ 7):

Per Node:
├─ Forward deps:  [standard — who feeds me]
├─ Forward feeds: [standard — who I feed]
└─ Revision edges: [GoT-specific — who I can SEND BACK TO]
    ├─ Target node: [which node receives the revision signal]
    ├─ Trigger: [what condition causes backward fire]
    ├─ Payload: [what information flows backward]
    └─ Re-entry point: [where the target node resumes — full rerun or partial]

Example:
Node-6 (Integration) has revision edge to Node-3 (Authentication):
  Trigger: "Integration discovers auth flow incompatible with API contract"
  Payload: "Required auth changes: [specifics]"
  Re-entry: Node-3 partial rerun (skip design, redo implementation only)
```

#### 2. Re-Entry Protocol

When a backward edge fires, the target node doesn't start from scratch. It re-enters with enriched context.

```
RE-ENTRY STATES:

FULL RERUN:
  Node re-executes completely with new context added.
  When: Original output fundamentally wrong.
  Cost: Full node token budget again.

PARTIAL RERUN:
  Node re-executes from a specific phase (e.g., implementation only).
  When: Design was right, implementation needs adjustment.
  Cost: Fraction of node budget.

PATCH:
  Node receives a targeted correction without re-execution.
  When: Small factual update, not structural change.
  Cost: Minimal — append correction to node output.

All re-entry carries:
├─ Original node output (what was produced first pass)
├─ Revision signal (what triggered the backward edge)
├─ Enriched context (what the later node discovered)
└─ Iteration counter (which loop pass this is)
```

#### 3. Cycle Budget and Convergence

Loops without termination = infinite drift. The railroad pre-defines cycle limits.

```
CYCLE CONTROL (pre-defined in railroad manifest):

cycle_budget:
  max_loops: [1-3]              # Hard cap. Default: 2.
  convergence_threshold: 0.05   # If quality delta < 5% between loops, stop.
  escalate_on_cap: true         # If max loops hit without convergence, flag to user.

Per backward edge:
  max_fires: [1-2]              # How many times THIS specific edge can fire.
  cooldown: false               # No cooldown — if condition met, fire immediately.

CONVERGENCE DETECTION:
  After each loop iteration:
  ├─ Compare node output quality (ARQ score) to previous iteration
  ├─ If delta < convergence_threshold → converged, exit loop
  ├─ If delta ≥ threshold AND iteration < max → loop again
  ├─ If iteration = max AND not converged → escalate
  └─ Convergence tracked per-edge, not global
```

#### 4. State Carry Across Iterations

```
WHAT PERSISTS ACROSS LOOP ITERATIONS:
├─ Bomb payloads (accumulated — each loop can plant new bombs)
├─ ARQ scores (tracked per-iteration for convergence detection)
├─ Expert context (enriched, not reset)
├─ Revision history (why each backward edge fired)
└─ Iteration counter (which pass, what changed)

WHAT RESETS:
├─ Node execution state (re-enters fresh with enriched context)
├─ Per-node CoVE results (re-verified on new output)
└─ Reasoning template state (re-runs template from appropriate entry point)
```

### GoT in the Railroad Manifest

When structure = GoT, the railroad manifest adds these fields:

```yaml
# GoT-specific fields (in addition to standard railroad fields)

topology: "got"    # vs "sot-light" or "dag"

revision_edges:
  - from: 6
    to: 3
    trigger: "auth_incompatible"
    payload_template: "Required auth changes: {specifics}"
    reentry: "partial"    # full | partial | patch
    max_fires: 2
  - from: 7
    to: 1
    trigger: "quality_gate_fail"
    payload_template: "Fundamental requirement gap: {specifics}"
    reentry: "full"
    max_fires: 1

cycle_control:
  max_loops: 2
  convergence_threshold: 0.05
  escalate_on_cap: true

iteration_state:
  current_loop: 0
  convergence_history: []
  fired_edges: []
```

### GoT Impact on Track Planning

When `[survey]` selects GoT structure, the subsequent `[track]` iterations gain additional responsibilities:

```
Track 1 ROUTES (GoT addition):
  Route cards include "revision receive" protocols — what each expert does
  when their node gets a backward edge signal mid-execution or post-execution.

Track 2 PATTERNS (GoT addition):
  Pattern map includes LOOP segments alongside BATON/SWARM/JUNCTION.
  LOOP pattern: "If backward edge fires, re-enter target node per re-entry protocol."

Track 4 BOMBS (GoT addition):
  Bombs can be planted ACROSS iterations. Loop 2 can plant bombs
  that reference Loop 1 context. Detonation sequence accounts for multi-pass.

Track 5 GATES (GoT addition):
  ARQ gates track per-iteration scores. Convergence detection wired into
  POST gates. Gate can return LOOP_BACK instead of just PASS/FAIL.

Track 6 COVE (GoT addition):
  CoVE variants may change between iterations. First pass: LOGICAL.
  Second pass (with revision context): CONSISTENCY + LOGICAL.
```

### Structure Selection Heuristic (Revised)

```
The D-score selects structure, but execution reality can PROMOTE:

D ≤ 3 → SoT-Light (plan as linear)
  IF global quality gate fails → promote to DAG with retry
  IF retry fails → promote to GoT with targeted loop

D = 4-6 → SkeletrainOT-Full DAG (plan as acyclic)
  IF execution discovers cross-node contradiction → promote to GoT
  IF quality gate fails on junction node → add revision edge, re-plan as GoT

D ≥ 7 → GoT (plan with loops from the start)
  Backward edges pre-planned. Cycle budget set. Convergence tracked.

PRINCIPLE: Plan optimistically, promote when reality demands.
SoT-Light is the hope. GoT is the expectation for anything LEGIO-grade.
```

---

### `[track]` — Lay the Tracks

**Domain:** Planning
**When:** After `[survey]` produces the blueprint
**Purpose:** Pre-decide EVERY tactical choice for execution. Iterates through 6 track types.

**THIS TAG ITERATES.** Called once per track type. The `trackType` parameter specifies which track.

```
[track] iterates through:
├─ Track 1: ROUTES     → Expert route assignment
├─ Track 2: PATTERNS   → Execution pattern map (Baton/Swarm/Junction)
├─ Track 3: REASONING  → Reasoning template pre-selection (FCoT/CoC/Hybrid)
├─ Track 4: BOMBS      → Bomb coordinates and detonation sequence
├─ Track 5: GATES      → ARQ gate positions and thresholds
└─ Track 6: COVE       → CoVE variant pre-assignment
```

#### Track 1: ROUTES — Expert Route Assignment

Each expert gets an exact route card.

```
EXPERT ROUTE CARD:

Expert: [Role]
TRACK: [node sequence with wait/observe/contribute markers]

Per Node on Route:
├─ Pattern: BATON-START | BATON-RECEIVE | SWARM-PARALLEL | JUNCTION
├─ Reasoning: FCoT | CoC | HYBRID (with switch trigger)
├─ Bombs to PLANT: [bomb IDs + types + payloads]
├─ Bombs to DETONATE: [bomb IDs from other tracks]
├─ ARQ: PRE | POST | BOTH | SKIP (with thresholds + on-fail action)
├─ CoVE: [variant assignments]
├─ Handoff: [what passes to next node, in what format]
└─ Tools: [specific MCP tools this expert uses at this node]
```

Route cards are the PRIMARY artifact. Everything else in [track] annotates these cards.

#### Track 2: PATTERNS — Execution Pattern Map

Decide Baton vs Swarm vs Junction for every segment.

```
Per Segment (node-to-node connection):
├─ BATON-START       → Foundation, must complete first
├─ BATON-SEQUENTIAL  → Strict dependency, one after another
├─ BATON-FINAL       → All tracks merge into final
├─ SWARM-PARALLEL    → Independent nodes, run simultaneously
├─ JUNCTION-WAIT     → Multiple inputs must complete before proceeding
├─ JUNCTION-MERGE    → Converge parallel tracks

Decision heuristic:
  Nodes share dependencies?      → SEQUENTIAL (baton)
  Nodes independent after fork?  → PARALLEL (swarm)
  Node needs multiple inputs?    → JUNCTION (wait point)
  Final synthesis?               → BATON-FINAL
```

#### Track 3: REASONING — Template Pre-Selection

Decide FCoT vs CoC vs Hybrid for every node. Pre-load reasoning templates.

```
Per Node:
├─ FCoT → exploration, tradeoffs, design, synthesis
│         Template: "Explore → Analyze → Tradeoffs → Recommend"
├─ CoC  → deterministic, rule-based, schema, implementation
│         Template: "Define → Validate → Schema → Test"
├─ HYBRID → design phase FCoT → implementation phase CoC
│         Template: FCoT:"[design task]" → CoC:"[implement task]"
│         Switch trigger: [keyword or phase marker]

Selection rule:
  Node involves design decisions?  → FCoT
  Node involves implementation?    → CoC
  Node involves both?              → HYBRID with defined switch point
```

NO DECISIONS DURING EXECUTION — templates pre-loaded, just run.

#### Track 4: BOMBS — Coordinate Assignment

Plant every pre-planned bomb at exact coordinates. Uses LEGIO-06 bomb types.

```
BOMB DEPLOYMENT MAP:

Per Bomb (from Imperatus pre-embedded + new tactical bombs):
├─ ID: B-NNN
├─ Type: ANCHOR | CLARIFIER | CONTINUITY | BRIDGE | EVIDENCE | GAP-FILLER
├─ Plant At: [Node-N position: START | MID | END]
├─ Detonate At: [Node-N position: START | MID | END]
├─ Payload: "[compressed context — CoD, 1-3 sentences max]"
├─ Trigger: [Coordinate | Content | Context | Token | Dependency]

DETONATION SEQUENCE (pre-computed, node by node):
  Node-1: Plant [list], Detonate [list]
  Node-2: Plant [list], Detonate [list]
  ...

Execution: On node entry → detonate assigned. On node exit → plant assigned.
NO DECISIONS NEEDED.
```

Imperatus sets arsenal size and plants strategic bombs. SkeletrainOT decides tactical placement — exact coordinates and detonation sequence.

#### Track 5: GATES — ARQ Gate Positions

Position every quality gate with pre-defined thresholds and failure actions.

```
ARQ GATE MAP:

Per Node:
├─ Impact: N/10 (from blueprint)
├─ PRE Gate: ACTIVE | skip
├─ POST Gate: ACTIVE | skip
├─ Threshold: [0.85 - 0.95]
├─ On Fail: HALT+Revise | Flag+Continue

PRE Gate Questions (loaded per node):
  Node-N: "[What defines quality for this node's domain?]"

POST Gate Questions (loaded per node):
  All: "Did I meet domain quality standards? Confidence: X/10"

Position rules (from Imperatus ARQ constraint):
  Impact ≥ 8         → PRE + POST gates
  Impact ≥ 6         → POST gate only
  Impact < 6         → skip (unless Imperatus overrides)
  Critical junction  → PRE + POST regardless of impact
```

Gates pre-positioned. Expert hits gate → fires automatically. Pass → proceed. Fail → action per map.

#### Track 6: COVE — Verification Pre-Selection

Assign CoVE variants to every node based on content type.

```
CoVE VERIFICATION SCHEDULE:

Per Node:
├─ Variants: [FACTUAL | LOGICAL | CONSISTENCY | MULTI_EXPERT]
├─ Why: [rationale for variant selection]

Variant selection heuristics:
  FACTUAL     → node makes claims needing evidence/citation
  LOGICAL     → node has reasoning chains or rule-based logic
  CONSISTENCY → node integrates work from multiple experts
  MULTI_EXPERT → final synthesis with all experts contributing

Score thresholds (from Imperatus CoVE constraint):
  Velites:    skip CoVE (or minimum)
  Hastati:    Top-1 variant per node
  Principes:  Top-2 variants per node
  Triarii:    All variants ≥ 4 relevance score
```

After each node, run pre-assigned variants. No selection during execution. Already decided.

**Each `[track]` returns `processing` with the completed track. All 6 tracks must complete before `[assemble]`.**

---

### `[assemble]` — Railroad Assembly

**Domain:** Authority
**When:** After all 6 `[track]` iterations complete
**Purpose:** Compile the complete railroad manifest. All decisions converge into a single artifact.

```
[assemble] merges:
├─ Blueprint (from [survey])
├─ 6 completed tracks (from [track]x6)
├─ Imperatus constraints (from incoming manifest)
└─ Mode-specific requirements
```

The assembled manifest contains:
- Full node map with dependency graph
- Complete expert route cards
- Execution pattern map (visual + data)
- Reasoning template assignment per node
- Bomb deployment map with detonation sequence
- ARQ gate map with thresholds and failure actions
- CoVE verification schedule
- Manifest summary statistics

**`[assemble]` produces the railroad manifest. Feeds `[deploy]`.**

---

### `[deploy]` — Seal and Deploy

**Domain:** Authority
**When:** After `[assemble]` completes
**Purpose:** Seal the railroad manifest. Execution begins.

```yaml
# === SKELETRAIN-OT RAILROAD MANIFEST ===
# Generated: [timestamp]
# Imperatus Manifest: [reference ID]
# Journey: [tag journey string]
# Track journey: [track type journey string]

blueprint:
  task: "[task name]"
  structure: [SoT-Light | SkeletrainOT-Full | GoT]
  nodes: [N]
  junctions: [N]
  dependency_graph: "[serialised graph]"

nodes:
  - id: 1
    name: "[Node name]"
    general: "[Expert role]"
    impact: [1-10]
    depends_on: [node list]
    exec_pattern: [BATON-START | BATON-SEQUENTIAL | SWARM-PARALLEL | JUNCTION | BATON-FINAL]
    reasoning: [FCoT | CoC | HYBRID]
    reasoning_template: "[template string]"
    hybrid_switch: "[trigger keyword or null]"
    arq_pre: [true | false]
    arq_post: [true | false]
    arq_threshold: [0.0-1.0]
    arq_on_fail: [HALT | FLAG]
    cove_variants: [list]
    bombs_plant: [bomb ID list]
    bombs_detonate: [bomb ID list]
    tools: [tool list]
    handoff: "[format description]"

routes:
  - expert: "[Role]"
    track: [ordered node list]
    pattern: "[route description]"

segments:
  - from: [node]
    to: [node]
    pattern: [BATON | SWARM | JUNCTION]
    reason: "[why this pattern]"

bombs:
  - id: B-NNN
    type: [ANCHOR | CLARIFIER | CONTINUITY | BRIDGE | EVIDENCE | GAP-FILLER]
    plant_at: "[Node-N position]"
    detonate_at: "[Node-N position]"
    payload: "[compressed CoD context]"
    trigger: "[condition]"

detonation_sequence:
  - node: 1
    plant: [bomb IDs]
    detonate: [bomb IDs]
  - node: 2
    plant: [bomb IDs]
    detonate: [bomb IDs]

gates:
  - node: 1
    pre: [true | false]
    post: [true | false]
    threshold: [0.0-1.0]
    on_fail: [HALT | FLAG]
    pre_question: "[quality question]"

cove_schedule:
  - node: 1
    variants: [list]
    rationale: "[why these variants]"

summary:
  total_nodes: [N]
  total_bombs: [N]
  arq_gates: { pre: [N], post: [N], total: [N] }
  reasoning_split: { fcot: [N], coc: [N], hybrid: [N] }
  exec_patterns: { baton: [N], swarm: [N], junction: [N], loop: [N] }
  cove_assignments: { factual: [N], logical: [N], consistency: [N], multi_expert: [N] }

# --- GoT fields (present when topology = "got") ---
topology: [sot-light | dag | got]

revision_edges:          # only when topology = "got"
  - from: [node]
    to: [node]
    trigger: "[condition description]"
    payload_template: "[what flows backward]"
    reentry: [full | partial | patch]
    max_fires: [1-3]

cycle_control:           # only when topology = "got"
  max_loops: [1-3]
  convergence_threshold: [0.01-0.10]
  escalate_on_cap: [true | false]

iteration_state:         # runtime tracking, initialised on deploy
  current_loop: 0
  convergence_history: []
  fired_edges: []

# === RAILROAD SEALED → EXECUTION ===
```

On `[deploy]`, the engine returns:

```json
{
  "status": "RAILROAD_READY",
  "processComplete": true,
  "finalStep": "deploy",
  "instruction": "RAILROAD_SEALED_EXECUTE",
  "railroad": { ... },
  "journeyLength": N,
  "tagJourney": "begin → survey → track → track → ... → assemble → deploy",
  "domainJourney": "entry → reconnaissance → planning → ... → authority",
  "trackJourney": "routes → patterns → reasoning → bombs → gates → cove"
}
```

---

## CONTROL TAGS

Two tags available at any point during the journey.

### `[halt]` — Incomplete Railroad

**Domain:** Control
**When:** Missing tracks, invalid blueprint, or enforcement violation

```
TRIGGERS:
├─ No Imperatus manifest received on [begin]
├─ Blueprint incomplete (missing nodes, unmapped dependencies)
├─ Track incomplete (missing assignments for any node)
├─ Expert without route card
├─ Node without reasoning template
├─ Junction without all upstream dependencies mapped
└─ Execution attempted without sealed railroad

ACTION:
├─ Stop forward progress
├─ Log what's missing: "Tracks incomplete. Missing: [list]"
├─ Return status: HALT with missing items
└─ Options: [revise] to complete, or escalate to user

ENFORCEMENT: "Generals must lay tracks first."
Cannot proceed to execution without complete railroad.
```

### `[revise]` — Re-Lay a Track

**Domain:** Control
**When:** A specific track needs adjustment

```
TRIGGERS:
├─ [halt] identified missing or invalid track
├─ New information from user or Imperatus [adapt]
├─ Expert conflict detected during [survey]
└─ Dependency change invalidates previous track decisions

ACTION:
├─ Identify which track type to revise
├─ Re-contemplate that track
├─ CASCADE: check all dependent tracks affected
│   ├─ Revising routes → re-check patterns, bombs, gates
│   ├─ Revising patterns → re-check reasoning, handoffs
│   ├─ Revising reasoning → minimal cascade (self-contained per node)
│   ├─ Revising bombs → re-check detonation sequence
│   ├─ Revising gates → minimal cascade (self-contained per node)
│   └─ Revising CoVE → minimal cascade (self-contained per node)
├─ Update railroad draft with revised values
└─ Resume forward progress
```

---

## MODE REQUIREMENTS

From the Imperatus manifest, SkeletrainOT scales its planning depth.

```
VELITES (Σ ≤ 12, Danger ≤ 5):
├─ SkeletrainOT: SKIP ENTIRELY
├─ Imperatus manifest says skeleton: Direct
├─ No generals convene, no tracks laid
└─ Execute: Direct generation, no planning

HASTATI (Σ = 13-25, Danger = 6-7):
├─ SkeletrainOT: LIGHT
├─ Survey: Light war council (abbreviated)
├─ Blueprint: Simple track layout (3-5 nodes)
├─ Tracks:
│   ├─ Routes:    Assigned but simplified
│   ├─ Patterns:  Mostly BATON, some parallel
│   ├─ Reasoning: Pre-selected per node
│   ├─ Bombs:     CLARIFIER + CONTINUITY only
│   ├─ Gates:     POST on high-impact only
│   └─ CoVE:     Top-1 variant per cluster
└─ Manifest: Abbreviated railroad

PRINCIPES (Σ = 26-38, Danger = 8):
├─ SkeletrainOT: FULL
├─ Survey: Full war council
├─ Blueprint: Complete rail network (5-8 nodes), topology = DAG
│   └─ PROMOTES TO GoT if execution discovers cross-node contradiction
├─ Tracks:
│   ├─ Routes:    Full route cards (+ revision receive protocols if GoT promoted)
│   ├─ Patterns:  BATON + SWARM optimised (+ LOOP segments if GoT promoted)
│   ├─ Reasoning: Full template assignment with HYBRID switches
│   ├─ Bombs:     Full arsenal + registry
│   ├─ Gates:     PRE+POST on impact ≥ 7 (+ convergence tracking if GoT promoted)
│   └─ CoVE:     Top-2 variants per cluster
├─ Manifest: Complete railroad
└─ GoT promotion: Available. Cycle budget = 1 if promoted.

TRIARII (Σ ≥ 39, Danger ≥ 9):
├─ SkeletrainOT: METRO
├─ Survey: Extended war council with adversarial review
├─ Blueprint: Full metro system, topology = GoT (D ≥ 7) or DAG, 8+ nodes
├─ Tracks:
│   ├─ Routes:    Deep route cards with revision receive protocols + contingency paths
│   ├─ Patterns:  Full SWARM + LOOP segments + multi-model if available
│   ├─ Reasoning: Mix+ with cross-node reasoning chains
│   ├─ Bombs:     Deep injection + cross-reference + predictive + multi-pass bombs
│   ├─ Gates:     ALL nodes PRE+POST + convergence detection + LOOP_BACK returns
│   └─ CoVE:     All variants ≥ 4 score (variants may shift between loop iterations)
├─ Manifest: Full metro manifest with revision edges and cycle control
└─ GoT: Native. Cycle budget = 2-3. Backward edges pre-planned from [survey].
```

---

## ENFORCEMENT

```
CRITICAL: Railroad manifest = REQUIRED for modes ≥ HASTATI

IF model attempts execution without railroad:
  → HALT
  → Display: "Generals must lay tracks first."
  → Force SkeletrainOT phase
  → Resume only after railroad sealed

IF railroad incomplete (missing any track):
  → HALT
  → Display: "Tracks incomplete. Missing: [list]"
  → Complete the missing [track] iteration
  → Resume after all tracks laid

EXECUTION RULE:
  During Baton/Swarm phase, NO NEW DECISIONS ALLOWED
  All decisions reference SkeletrainOT railroad manifest
  If situation not covered → FLAG for post-exec review, don't stop train
```

---

## MCP TOOL SCHEMA

Two tools. Mirrors the lotus-wisdom pattern (`lotuswisdom` + `lotuswisdom_summary`).

### Tool 1: `skeletrain`

The planning engine. Called iteratively with tags.

```json
{
  "name": "skeletrain",
  "description": "Tactical planning engine for LEGIO cascade. Receives Imperatus manifest, surveys battlefield, lays all execution tracks, seals railroad manifest. Start with tag='begin'. Do NOT execute work until status='RAILROAD_READY'.",
  "inputSchema": {
    "type": "object",
    "properties": {
      "tag": {
        "type": "string",
        "description": "Current planning phase",
        "enum": ["begin", "survey", "track", "assemble", "deploy", "halt", "revise"]
      },
      "content": {
        "type": "string",
        "description": "Content of the current planning step"
      },
      "stepNumber": {
        "type": "integer",
        "description": "Current step number",
        "minimum": 1
      },
      "totalSteps": {
        "type": "integer",
        "description": "Estimated total steps needed",
        "minimum": 1
      },
      "nextStepNeeded": {
        "type": "boolean",
        "description": "Whether another step is needed"
      },
      "trackType": {
        "type": "string",
        "description": "Which track to lay (required when tag='track')",
        "enum": ["routes", "patterns", "reasoning", "bombs", "gates", "cove"]
      },
      "imperatus_manifest": {
        "type": "object",
        "description": "The Imperatus execution manifest (passed on begin)"
      },
      "verbose": {
        "type": "boolean",
        "description": "Show railroad manifest to user before execution"
      }
    },
    "required": ["tag", "content", "stepNumber", "totalSteps", "nextStepNeeded"]
  }
}
```

### Tool 2: `skeletrain_manifest`

Returns current railroad manifest state at any point in the journey.

```json
{
  "name": "skeletrain_manifest",
  "description": "Get current state of the SkeletrainOT railroad manifest",
  "inputSchema": {
    "type": "object",
    "properties": {
      "section": {
        "type": "string",
        "description": "Optional: return specific section only",
        "enum": ["blueprint", "routes", "patterns", "reasoning", "bombs", "gates", "cove", "summary"]
      }
    },
    "required": []
  }
}
```

### Response Statuses

| Status | When | Meaning |
|--------|------|---------|
| `FRAMEWORK_RECEIVED` | After `[begin]` | Planning framework loaded, proceed with `[survey]` |
| `BLUEPRINT_READY` | After `[survey]` | Blueprint complete, proceed with `[track]` |
| `processing` | During `[track]` | Track laid, continue to next track |
| `HALT` | Enforcement violation | Stopped. Needs `[revise]` or user clearance |
| `ASSEMBLED` | After `[assemble]` | All tracks merged, proceed with `[deploy]` |
| `RAILROAD_READY` | After `[deploy]` | Sealed. Execution begins. |
| `LOOP_BACK` | During GoT execution | Backward edge fired. Re-entering target node. |
| `CONVERGED` | After GoT loop | Quality delta below threshold. Loop complete. |
| `CYCLE_CAP` | After GoT max loops | Max iterations hit without convergence. Escalate. |

---

## INTEGRATION

### Upstream

```
Imperatus manifest → SkeletrainOT [begin]
  ├─ Receives: sealed Imperatus manifest (YAML) + user query + tools
  ├─ Consumes: expert constellation, bomb arsenal, constraint levels
  └─ Validates: manifest completeness before planning starts
```

### Downstream

```
SkeletrainOT railroad → ALL execution modules
  Every execution module reads the railroad. No ad-hoc decisions.
  ├─ Baton/Swarm: exact execution pattern per segment
  ├─ FCoT/CoC: exact reasoning template per node
  ├─ Prompt Bombs: exact coordinates and detonation sequence
  ├─ ARQ: exact gate positions, thresholds, failure actions
  ├─ CoVE: exact variant assignments per node
  └─ Expert handoffs: exact format and content per transition
```

### Paired Artifacts

- **Consumes:** `LEGIO-00-IMPERATUS_CORE_.md` manifest (upstream input)
- **References:** `LEGIO-06-PROMPT-BOMBS_KIT_.md` for bomb type definitions and trigger mechanisms
- **Produces:** Railroad manifest consumed by ALL execution phase modules

### Feedback Loops

```
During execution:
  Execution reality divergence → SkeletrainOT does NOT receive feedback directly
  Execution feedback → Imperatus [adapt] → revised manifest → SkeletrainOT re-plan (if needed)

Post execution:
  Execution results → validate railroad accuracy
  ├─ Were route cards followed?
  ├─ Did bomb coordinates work?
  ├─ Did gate positions catch issues?
  └─ Did reasoning templates fit?
  Signals feed back into future planning accuracy.
```

---

## DESIGN PRINCIPLES

1. **Imperatus commands, SkeletrainOT plans, execution runs.** Three-tier separation. No tier does another's job.

2. **Zero decisions during execution.** This is the fundamental guarantee. If execution has to make a planning decision, the railroad was incomplete.

3. **Route cards are the core artifact.** Everything else (patterns, bombs, gates, CoVE) annotates the expert route cards. If you have perfect route cards, execution can run.

4. **Tracks are independent but composable.** Each of the 6 track types can be laid in any order, but they reference each other. Routes inform patterns. Patterns inform reasoning. All inform bombs.

5. **Mode scaling is continuous.** Hastati doesn't get a "different" SkeletrainOT — it gets the same engine with reduced depth. The tracks are the same 6 types, just lighter.

6. **Blueprint before tracks.** Survey → Blueprint → Tracks. Never lay tracks without a blueprint. Enforcement is structural, not advisory.

---

## IMPLEMENTATION NOTES (for Claude Code)

```
1. Human-readable spec. Real implementation is S2A → MCP.
2. Each tag = one tool call in the MCP server.
3. Journey state maintained server-side per session.
4. Railroad builds progressively across steps.
5. [begin] auto-resets journey state + validates incoming manifest.
6. [survey] produces intermediate blueprint artifact.
7. [track] iterates 6x with trackType parameter differentiating.
8. [assemble] merges blueprint + 6 tracks into railroad manifest.
9. [deploy] seals and returns RAILROAD_READY.
10. [halt] fires on missing tracks or enforcement violations.
11. State validated server-side. Track completion enforced.
12. Express + StreamableHTTP transport (matches lotus-wisdom-mcp pattern).
13. Session management for stateful planning journeys.
14. Velites skip: if manifest says skeleton=Direct, return immediate RAILROAD_READY with empty/default railroad.
```

---

*LEGIO v30.1 | Module 07 | Phase: PLANNING | SYSTEM-CORE #2*
*Source: SkeletrainOT v2.1 + Imperatus (LEGIO-00) + Lotus Wisdom MCP pattern*
*Legatus: tactical planning engine. The Field General.*
*"Imperatus commands. Legatus plans. The legion executes."*
