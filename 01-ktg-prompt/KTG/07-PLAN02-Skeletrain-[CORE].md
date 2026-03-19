---
title: "SkeleTraIn of Thought"
version: "v2.1"
status: "ACTIVE"
model: "Multi-model"
tags: ["technique", "skeletrain", "planning", "structure", "execution-routing", "STRAWHATS-directive", "active"]
created: "2025-01-22"
updated: "2025-01-22"
creator: ".ktg"
category: "core"
description: "SkeleTraIn of Thought: Generals laying railroad tracks so execution fires like a bullet train"
---

# SKELETRAIN OF THOUGHT v2.1
**Phase 3 of STRAWHATS-DIRECTIVE v30 | The Generals' Battle Plan**

---

## THE COMMAND HIERARCHY

```
┌─────────────────────────────────────────────────────────────────────┐
│  SILENT ROUTER: CHIEF COMMANDER (Capital HQ)                        │
│  ════════════════════════════════════════════════════════════════   │
│  • Decides which troops to deploy (expert count)                    │
│  • Allocates equipment & weapons (technique stack)                  │
│  • Sets logistics budget (token allocation)                         │
│  • Determines theater of war (Mode: QUICK→MAXIMUM)                  │
│  • Defines victory conditions (Success Criteria Lock)               │
│  OUTPUT: Deployment orders → Generals receive marching orders       │
├─────────────────────────────────────────────────────────────────────┤
│  SKELETRAIN: GENERALS ON THE FRONT LINE (This Module)               │
│  ════════════════════════════════════════════════════════════════   │
│  • Receive troops & equipment from Commander                        │
│  • Survey the battlefield (analyze task structure)                  │
│  • Design battle plan (skeleton + node assignments)                 │
│  • LAY THE RAILROAD TRACKS:                                         │
│    ├─ Every expert knows their exact route                          │
│    ├─ Every bomb pre-loaded at exact coordinates                    │
│    ├─ Every reasoning template pre-selected                         │
│    ├─ Every quality gate positioned                                 │
│    └─ Every handoff choreographed                                   │
│  OUTPUT: Complete railroad network → Execution just runs the train  │
├─────────────────────────────────────────────────────────────────────┤
│  EXECUTE: BULLET TRAIN (Baton/Swarm Phase)                          │
│  ════════════════════════════════════════════════════════════════   │
│  • Tracks already laid → NO PLANNING DURING EXECUTION               │
│  • Bombs already planted → Just detonate on arrival                 │
│  • Routes already assigned → Experts just RUN                       │
│  • Gates already positioned → Just pass/fail, no debate             │
│  • PURE SPEED: Planning done, now EXECUTE                           │
└─────────────────────────────────────────────────────────────────────┘
```

---

## WHY "TRAIN"?

```
SKELETON + TRAIN = SKELETRAIN

The skeleton is the STRUCTURE (nodes, dependencies, flow)
The train is the TRACKS (pre-laid routes experts follow)

BY THE END OF SKELETRAIN:
┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│   🚂 BULLET TRAIN READY                                             │
│                                                                     │
│   Track 1: Expert-1 → [Node-1] → [Node-3] → [Node-5]               │
│            Bombs: 💣 at Node-1 entry, 💣 at Node-3 junction         │
│            Reasoning: FCoT → CoC → FCoT                             │
│            Gates: ✓ Post-Node-1, ✓ Pre+Post-Node-3                 │
│                                                                     │
│   Track 2: Expert-2 → [Node-2] → [Node-4]                          │
│            Bombs: 💣 Continuity from Track-1 at Node-2              │
│            Reasoning: CoC throughout                                │
│            Gates: ✓ Post-Node-4 (feeds synthesis)                  │
│                                                                     │
│   Junction: Tracks merge at [Node-5] (SWARM → BATON)               │
│                                                                     │
│   Final: [Node-6] Synthesis                                         │
│          Bombs: 💣 Bridge from all tracks                           │
│          Reasoning: FCoT                                            │
│          Gates: ✓ Final verification                               │
│          CoVE: CONSISTENCY + MULTI_EXPERT                          │
│                                                                     │
│   EXECUTION = JUST RUN THE TRAINS 🚄💨                              │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## GENERALS' MANDATE

**Receive from Chief Commander (Silent Router):**
```
DEPLOYMENT ORDERS:
├─ Experts: [5 specialists assigned]
├─ Equipment: [MR.RUG, ARQ, CoVE, Bombs, USC-3]
├─ Mode: DELIBERATE
├─ Budget: ~12K tokens
├─ Victory: [Success Criteria Lock]
└─ Theater: [R=8, K=7, Q=9, D=6, E=5]
```

**Generals' Job: LAY ALL THE TRACKS**

By the time SkeleTraIn completes, EVERY decision is made:
- ✅ Which expert owns which node
- ✅ What order nodes execute (dependencies mapped)
- ✅ BATON or SWARM for each segment
- ✅ FCoT or CoC or HYBRID for each node
- ✅ WHERE each bomb detonates (exact coordinates)
- ✅ WHERE each ARQ gate fires (pre/post/both)
- ✅ WHICH CoVE variants run after which nodes

**Execute Phase = Zero planning, pure speed**

---

## PHASE 1: BATTLEFIELD SURVEY (Skeleton Generation)

### Step 1: Generals Convene (Expert Council)

```
GENERALS RECEIVE INTEL FROM COMMANDER:
├─ Task: [User's request]
├─ Knowledge Graphs: [From MR.RUG phase]
├─ Constraints: [Time, tokens, quality bar]
└─ Victory Conditions: [Success Criteria]

EACH GENERAL (Expert) SURVEYS THEIR DOMAIN:

General-Security:
  "I see 3 critical positions to hold:
   [Authentication], [Authorization], [Audit Trail]"

General-Backend:
  "I need to secure 4 positions:
   [API Design], [Data Model], [Business Logic], [Integration]"

General-DevOps:
  "My terrain requires:
   [Deployment], [Monitoring], [Scaling]"

OUTPUT: Each general's proposed positions (nodes)
```

### Step 2: War Council (Collaborative Synthesis)

```
GENERALS MERGE THEIR MAPS:

1. IDENTIFY OVERLAPS:
   Security: {Auth Gateway}
   Backend:  {API Auth Layer}
   → MERGE: Single [Authentication] position, Security leads, Backend supports

2. IDENTIFY DEPENDENCIES (Critical for track layout):
   [Data Model] MUST complete before [API Design]
   [Authentication] MUST complete before [Authorization]
   [API Design] + [Auth] MUST complete before [Integration]
   
   These dependencies = TRACK JUNCTIONS

3. IDENTIFY PARALLEL OPPORTUNITIES:
   [Monitoring] and [Audit Trail] can run SIMULTANEOUSLY
   = PARALLEL TRACKS (Swarm segment)

4. FILL GAPS:
   No one claimed [Error Handling]
   → ADD as cross-cutting node, DevOps + Backend co-own
```

### Step 3: Structure Type Selection

```
BASED ON DEPENDENCY COMPLEXITY (D-score):

D ≤ 3 (Low interdependency):
  → SIMPLE TRACK LAYOUT (SoT-Light)
  → Linear or simple fork
  → 3-5 nodes max
  
D = 4-6 (Moderate):
  → STANDARD RAIL NETWORK (SkeleTrain-Full)
  → Multiple tracks with junctions
  → Parallel segments where possible
  → 5-8 nodes typical

D ≥ 7 (High complexity):
  → FULL METRO SYSTEM (Graph-of-Thought)
  → Bidirectional connections
  → Complex merge points
  → 8+ nodes, dense interconnection
```

### Step 4: Skeleton Artifact (The Blueprint)

```
┌─────────────────────────────────────────────────────────────────────┐
│ SKELETRAIN BLUEPRINT: [Task Name]                                   │
│ Structure: SkeleTrain-Full | Nodes: 7 | Junctions: 3               │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ NODE MAP:                                                           │
│                                                                     │
│ [1] Requirements ─────┬──────────────────────────────────────────   │
│     General: Security │ Impact: 9/10 │ From: ROOT                   │
│                                                                     │
│ [2] Data Model ───────┼──────────────────────────────────────────   │
│     General: Backend  │ Impact: 8/10 │ From: Node-1                 │
│                                                                     │
│ [3] Authentication ───┼──────────────────────────────────────────   │
│     General: Security │ Impact: 9/10 │ From: Node-1                 │
│                                                                     │
│ [4] API Design ───────┼──────────────────────────────────────────   │
│     General: Backend  │ Impact: 8/10 │ From: Node-2, Node-3        │
│                                                                     │
│ [5] Authorization ────┼──────────────────────────────────────────   │
│     General: Security │ Impact: 8/10 │ From: Node-3                 │
│                                                                     │
│ [6] Integration ──────┼──────────────────────────────────────────   │
│     General: DevOps   │ Impact: 7/10 │ From: Node-4, Node-5        │
│                                                                     │
│ [7] Synthesis ────────┴──────────────────────────────────────────   │
│     General: ALL      │ Impact: 9/10 │ From: Node-6                 │
│                                                                     │
│ DEPENDENCY GRAPH:                                                   │
│                                                                     │
│         [1]                                                         │
│        /   \                                                        │
│      [2]   [3]                                                      │
│        \   / \                                                      │
│        [4]   [5]                                                    │
│          \   /                                                      │
│           [6]                                                       │
│            │                                                        │
│           [7]                                                       │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘

ENFORCEMENT: No blueprint = HALT. Generals must complete survey.
```

---

## PHASE 2: LAY THE TRACKS (Strategic Expansion)

**This is where generals make EVERY tactical decision BEFORE execution.**

### Track 1: Expert Route Assignment

```
EACH EXPERT GETS THEIR EXACT TRACK:

┌─────────────────────────────────────────────────────────────────────┐
│ EXPERT ROUTE CARDS                                                  │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ 🎖️ GENERAL-SECURITY (Expert-1)                                      │
│ ══════════════════════════════════════════════════════════════════  │
│ TRACK: [1] → [3] → [5] → observe [6] → contribute [7]              │
│                                                                     │
│ Node-1 (Requirements):                                              │
│   • Pattern: BATON-START (I launch the campaign)                   │
│   • Reasoning: FCoT (explore threat models, tradeoffs)             │
│   • Bombs to PLANT: 💣 ANCHOR "Security-first principle"           │
│   • Bombs to DETONATE: None (first node)                           │
│   • ARQ: PRE (activate domain standards) + POST (≥0.9 to proceed)  │
│   • Handoff: Enriched context → Node-2 AND Node-3                  │
│                                                                     │
│ Node-3 (Authentication):                                            │
│   • Pattern: BATON-RECEIVE (from Node-1)                           │
│   • Reasoning: HYBRID (design FCoT → implementation CoC)           │
│   • Bombs to PLANT: 💣 CONTINUITY for Node-5 "Auth context needed" │
│   • Bombs to DETONATE: 💣 ANCHOR from Node-1                       │
│   • ARQ: BOTH (critical node, feeds downstream)                    │
│   • Handoff: → Node-4 (parallel) AND → Node-5 (sequential)        │
│                                                                     │
│ Node-5 (Authorization):                                             │
│   • Pattern: BATON-RECEIVE (from Node-3)                           │
│   • Reasoning: CoC (rule-based logic)                              │
│   • Bombs to DETONATE: 💣 CONTINUITY from Node-3                   │
│   • Bombs to PLANT: 💣 BRIDGE for Node-6 "Auth+Authz complete"     │
│   • ARQ: POST (feeds integration)                                  │
│   • Handoff: → Junction at Node-6                                  │
│                                                                     │
│ Node-7 (Synthesis): CONTRIBUTE security perspective to final       │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ 🎖️ GENERAL-BACKEND (Expert-2)                                       │
│ ══════════════════════════════════════════════════════════════════  │
│ TRACK: wait[1] → [2] → [4] → observe [6] → contribute [7]          │
│                                                                     │
│ Node-2 (Data Model):                                                │
│   • Pattern: BATON-RECEIVE (from Node-1)                           │
│   • Reasoning: CoC (schema definition, deterministic)              │
│   • Bombs to DETONATE: Context from Node-1 requirements            │
│   • Bombs to PLANT: 💣 CLARIFIER "User entity = {schema}"          │
│   • ARQ: POST (feeds API design)                                   │
│   • Handoff: → Node-4                                              │
│                                                                     │
│ Node-4 (API Design):                                                │
│   • Pattern: JUNCTION (receives from Node-2 AND Node-3)            │
│   • Reasoning: HYBRID (contract FCoT → endpoints CoC)              │
│   • Bombs to DETONATE: 💣 CLARIFIER from Node-2, context from 3   │
│   • Bombs to PLANT: 💣 EVIDENCE "REST best practices: {citation}" │
│   • ARQ: BOTH (critical integration point)                         │
│   • Handoff: → Node-6                                              │
│                                                                     │
│ [... similar for other generals ...]                               │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Track 2: Execution Pattern Map

```
BATON vs SWARM DECISION (Per Segment):

┌─────────────────────────────────────────────────────────────────────┐
│ EXECUTION PATTERN MAP                                               │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ SEGMENT A: [ROOT] → [Node-1]                                        │
│ Pattern: BATON-START                                                │
│ Reason: Foundation, must complete before anything else              │
│                                                                     │
│ SEGMENT B: [Node-1] → [Node-2] + [Node-3]                          │
│ Pattern: SWARM (Parallel Fork)                                      │
│ Reason: Node-2 and Node-3 are INDEPENDENT after Node-1             │
│         Both can run simultaneously                                 │
│         Generals-Security and Backend work in parallel              │
│                                                                     │
│ SEGMENT C: [Node-2, Node-3] → [Node-4]                             │
│ Pattern: JUNCTION (Wait Point)                                      │
│ Reason: Node-4 DEPENDS on BOTH Node-2 AND Node-3                   │
│         Must wait for parallel tracks to merge                      │
│                                                                     │
│ SEGMENT D: [Node-3] → [Node-5]                                     │
│ Pattern: BATON-SEQUENTIAL                                           │
│ Reason: Authorization depends on Authentication                     │
│         Strict sequential dependency                                │
│                                                                     │
│ SEGMENT E: [Node-4, Node-5] → [Node-6]                             │
│ Pattern: JUNCTION (Merge Point)                                     │
│ Reason: Integration needs both API and Auth complete               │
│                                                                     │
│ SEGMENT F: [Node-6] → [Node-7]                                     │
│ Pattern: BATON-FINAL                                                │
│ Reason: Synthesis requires all work complete                        │
│                                                                     │
│ VISUAL:                                                             │
│                                                                     │
│    [1] ═══╦══════════════════╗                                      │
│           ║                  ║                                      │
│         SWARM              SWARM                                    │
│           ║                  ║                                      │
│          [2]               [3]═══════╗                              │
│           ║                  ║       ║                              │
│           ╠═══════╦══════════╝       ║                              │
│                   ║                  ║                              │
│              JUNCTION              BATON                            │
│                   ║                  ║                              │
│                  [4]               [5]                              │
│                   ║                  ║                              │
│                   ╠══════════════════╝                              │
│                   ║                                                 │
│              JUNCTION                                               │
│                   ║                                                 │
│                  [6]                                                │
│                   ║                                                 │
│                BATON                                                │
│                   ║                                                 │
│                  [7]                                                │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Track 3: Reasoning Template Pre-Selection

```
FCoT vs CoC vs HYBRID (Pre-decided per node):

┌─────────────────────────────────────────────────────────────────────┐
│ REASONING TEMPLATE ASSIGNMENT                                       │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ Node │ Reasoning │ Template Loaded                                  │
│ ─────┼───────────┼─────────────────────────────────────────────────│
│  1   │ FCoT      │ "Explore → Analyze → Tradeoffs → Recommend"     │
│  2   │ CoC       │ "Define → Validate → Schema → Test"             │
│  3   │ HYBRID    │ FCoT:"Design auth flow" → CoC:"Implement JWT"   │
│  4   │ HYBRID    │ FCoT:"Contract design" → CoC:"OpenAPI spec"     │
│  5   │ CoC       │ "Rules → Conditions → Logic → Verify"           │
│  6   │ FCoT      │ "Integrate → Test → Document → Review"          │
│  7   │ FCoT      │ "Synthesize → Harmonize → Polish → Deliver"     │
│                                                                     │
│ HYBRID SWITCH POINTS (pre-defined):                                │
│ Node-3: Switch FCoT→CoC at "implementation" keyword                │
│ Node-4: Switch FCoT→CoC at "endpoint definition" keyword           │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘

NO DECISIONS DURING EXECUTION - Templates pre-loaded, just run.
```

### Track 4: Bomb Coordinates (Pre-Planted)

```
BOMB REGISTRY WITH EXACT COORDINATES:

┌─────────────────────────────────────────────────────────────────────┐
│ 💣 BOMB DEPLOYMENT MAP                                              │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ BOMB ID │ Type       │ Plant At    │ Detonate At │ Payload         │
│ ────────┼────────────┼─────────────┼─────────────┼─────────────────│
│ B-001   │ ANCHOR     │ Node-1 END  │ Node-3,5,7  │ "Security-first │
│         │            │             │             │  principle..."  │
│ ────────┼────────────┼─────────────┼─────────────┼─────────────────│
│ B-002   │ CLARIFIER  │ Node-2 END  │ Node-4      │ "User entity =  │
│         │            │             │             │  {id, email...}"│
│ ────────┼────────────┼─────────────┼─────────────┼─────────────────│
│ B-003   │ CONTINUITY │ Node-3 END  │ Node-5 START│ "Auth requires: │
│         │            │             │             │  JWT + refresh" │
│ ────────┼────────────┼─────────────┼─────────────┼─────────────────│
│ B-004   │ EVIDENCE   │ Node-4 MID  │ Node-4 MID  │ "REST standard: │
│         │            │             │             │  RFC 7231..."   │
│ ────────┼────────────┼─────────────┼─────────────┼─────────────────│
│ B-005   │ BRIDGE     │ Node-5 END  │ Node-6 START│ "Auth+Authz     │
│         │            │             │             │  complete, now  │
│         │            │             │             │  integrate..."  │
│ ────────┼────────────┼─────────────┼─────────────┼─────────────────│
│ B-006   │ BRIDGE     │ Node-4 END  │ Node-6 START│ "API contract   │
│         │            │             │             │  finalized..."  │
│ ────────┼────────────┼─────────────┼─────────────┼─────────────────│
│ B-007   │ ANCHOR     │ Node-6 END  │ Node-7 START│ "Integration    │
│         │            │             │             │  complete..."   │
│                                                                     │
│ DETONATION SEQUENCE:                                                │
│ Node-1: Plant B-001                                                 │
│ Node-2: Plant B-002                                                 │
│ Node-3: Detonate B-001, Plant B-003                                │
│ Node-4: Detonate B-002, Plant B-004 (inline), Plant B-006          │
│ Node-5: Detonate B-001, Detonate B-003, Plant B-005                │
│ Node-6: Detonate B-005, Detonate B-006                             │
│ Node-7: Detonate B-001, Detonate B-007                             │
│                                                                     │
│ EXECUTION: Bombs pre-loaded. On node entry → detonate assigned.    │
│            On node exit → plant assigned. NO DECISIONS NEEDED.     │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Track 5: ARQ Gate Positions

```
QUALITY GATES PRE-POSITIONED:

┌─────────────────────────────────────────────────────────────────────┐
│ 🚦 ARQ GATE MAP                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ Node │ Impact │ PRE Gate │ POST Gate │ Threshold │ On Fail         │
│ ─────┼────────┼──────────┼───────────┼───────────┼─────────────────│
│  1   │ 9/10   │ ✓ ACTIVE │ ✓ ACTIVE  │ ≥0.9      │ HALT + Revise   │
│  2   │ 8/10   │ ✗ skip   │ ✓ ACTIVE  │ ≥0.9      │ Flag + Continue │
│  3   │ 9/10   │ ✓ ACTIVE │ ✓ ACTIVE  │ ≥0.9      │ HALT + Revise   │
│  4   │ 8/10   │ ✓ ACTIVE │ ✓ ACTIVE  │ ≥0.9      │ HALT + Revise   │
│  5   │ 8/10   │ ✗ skip   │ ✓ ACTIVE  │ ≥0.9      │ Flag + Continue │
│  6   │ 7/10   │ ✗ skip   │ ✓ ACTIVE  │ ≥0.85     │ Flag + Continue │
│  7   │ 9/10   │ ✗ skip   │ ✓ ACTIVE  │ ≥0.9      │ HALT + Revise   │
│                                                                     │
│ PRE-GATE QUESTIONS (loaded per node):                              │
│ Node-1: "What defines quality security requirements?"              │
│ Node-3: "What makes authentication implementation secure?"         │
│ Node-4: "What makes an API design production-ready?"               │
│                                                                     │
│ POST-GATE QUESTIONS (loaded per node):                             │
│ All: "Did I meet domain quality standards? Confidence: X/10"       │
│                                                                     │
│ EXECUTION: Gates pre-positioned. Expert hits gate → fires          │
│            automatically. Pass → proceed. Fail → action per map.   │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Track 6: CoVE Variant Pre-Selection

```
VERIFICATION VARIANTS PRE-ASSIGNED:

┌─────────────────────────────────────────────────────────────────────┐
│ ✓ CoVE VERIFICATION SCHEDULE                                        │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ After    │ Variants        │ Why Selected                          │
│ ─────────┼─────────────────┼─────────────────────────────────────── │
│ Node-1   │ LOGICAL         │ Requirements have reasoning chains    │
│ Node-2   │ LOGICAL         │ Schema logic must be consistent       │
│ Node-3   │ LOGICAL,FACTUAL │ Auth claims need evidence + logic     │
│ Node-4   │ FACTUAL,LOGICAL │ API standards need citation + logic   │
│ Node-5   │ LOGICAL         │ Authorization rules must be sound     │
│ Node-6   │ CONSISTENCY     │ Integration must cohere across nodes  │
│ Node-7   │ CONSISTENCY,    │ Final output needs full verification  │
│          │ MULTI_EXPERT    │                                       │
│                                                                     │
│ VARIANT SELECTION RATIONALE (pre-computed):                        │
│ FACTUAL score:     Node-3=8, Node-4=9, others<4                    │
│ LOGICAL score:     Node-1=9, Node-2=8, Node-3=8, Node-4=7, Node-5=9│
│ CONSISTENCY score: Node-6=9, Node-7=10                             │
│ MULTI_EXPERT:      Node-7=8 (all generals contribute)              │
│                                                                     │
│ EXECUTION: After each node, run pre-assigned variants.             │
│            No selection during execution. Already decided.         │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## THE COMPLETE RAILROAD (Final Manifest)

```
┌─────────────────────────────────────────────────────────────────────┐
│ 🚂 SKELETRAIN MANIFEST: Authentication System Design                │
│ ═══════════════════════════════════════════════════════════════════ │
│ Mode: DELIBERATE | Structure: SkeleTrain-Full | Nodes: 7           │
│ Generals: Security, Backend, DevOps | Tracks: 3 main + junctions   │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ ══════════════════════════════════════════════════════════════════  │
│ NODE 1: Requirements Analysis                                       │
│ ══════════════════════════════════════════════════════════════════  │
│ General: Security | Impact: 9/10 | Depends: ROOT                   │
│                                                                     │
│ TRACK ASSIGNMENT:                                                   │
│ ├─ Exec: BATON-START (launches campaign)                           │
│ ├─ Reasoning: FCoT (explore, analyze, tradeoffs)                   │
│ ├─ ARQ: PRE + POST (threshold ≥0.9, HALT on fail)                  │
│ ├─ CoVE: LOGICAL (after completion)                                │
│ ├─ Bombs PLANT: B-001 ANCHOR "Security-first"                      │
│ └─ Bombs DETONATE: None (first node)                               │
│                                                                     │
│ HANDOFF → Fork to Node-2 (Backend) AND Node-3 (Security)          │
│                                                                     │
│ ══════════════════════════════════════════════════════════════════  │
│ NODE 2: Data Model                                                  │
│ ══════════════════════════════════════════════════════════════════  │
│ General: Backend | Impact: 8/10 | Depends: Node-1                  │
│                                                                     │
│ TRACK ASSIGNMENT:                                                   │
│ ├─ Exec: SWARM-PARALLEL (runs alongside Node-3)                    │
│ ├─ Reasoning: CoC (schema definition)                              │
│ ├─ ARQ: POST only (threshold ≥0.9, flag on fail)                   │
│ ├─ CoVE: LOGICAL (after completion)                                │
│ ├─ Bombs PLANT: B-002 CLARIFIER "User entity schema"               │
│ └─ Bombs DETONATE: Context from Node-1                             │
│                                                                     │
│ HANDOFF → Junction wait for Node-3, then → Node-4                  │
│                                                                     │
│ ══════════════════════════════════════════════════════════════════  │
│ NODE 3: Authentication                                              │
│ ══════════════════════════════════════════════════════════════════  │
│ General: Security | Impact: 9/10 | Depends: Node-1                 │
│                                                                     │
│ TRACK ASSIGNMENT:                                                   │
│ ├─ Exec: SWARM-PARALLEL (runs alongside Node-2)                    │
│ ├─ Reasoning: HYBRID (design FCoT → implement CoC)                 │
│ │   └─ Switch trigger: "implementation" keyword                    │
│ ├─ ARQ: PRE + POST (threshold ≥0.9, HALT on fail)                  │
│ ├─ CoVE: LOGICAL, FACTUAL (after completion)                       │
│ ├─ Bombs PLANT: B-003 CONTINUITY for Node-5                        │
│ └─ Bombs DETONATE: B-001 ANCHOR from Node-1                        │
│                                                                     │
│ HANDOFF → Node-4 (parallel) AND → Node-5 (sequential)             │
│                                                                     │
│ ══════════════════════════════════════════════════════════════════  │
│ NODE 4: API Design                                                  │
│ ══════════════════════════════════════════════════════════════════  │
│ General: Backend | Impact: 8/10 | Depends: Node-2, Node-3          │
│                                                                     │
│ TRACK ASSIGNMENT:                                                   │
│ ├─ Exec: JUNCTION (waits for Node-2 AND Node-3)                    │
│ ├─ Reasoning: HYBRID (contract FCoT → OpenAPI CoC)                 │
│ │   └─ Switch trigger: "endpoint definition" keyword               │
│ ├─ ARQ: PRE + POST (threshold ≥0.9, HALT on fail)                  │
│ ├─ CoVE: FACTUAL, LOGICAL (after completion)                       │
│ ├─ Bombs PLANT: B-004 EVIDENCE inline, B-006 BRIDGE for Node-6    │
│ └─ Bombs DETONATE: B-002 CLARIFIER from Node-2                     │
│                                                                     │
│ HANDOFF → Junction wait for Node-5, then → Node-6                  │
│                                                                     │
│ ══════════════════════════════════════════════════════════════════  │
│ NODE 5: Authorization                                               │
│ ══════════════════════════════════════════════════════════════════  │
│ General: Security | Impact: 8/10 | Depends: Node-3                 │
│                                                                     │
│ TRACK ASSIGNMENT:                                                   │
│ ├─ Exec: BATON-SEQUENTIAL (after Node-3)                           │
│ ├─ Reasoning: CoC (rule-based access control)                      │
│ ├─ ARQ: POST only (threshold ≥0.9, flag on fail)                   │
│ ├─ CoVE: LOGICAL (after completion)                                │
│ ├─ Bombs PLANT: B-005 BRIDGE for Node-6                            │
│ └─ Bombs DETONATE: B-001 ANCHOR, B-003 CONTINUITY from Node-3     │
│                                                                     │
│ HANDOFF → Junction at Node-6                                       │
│                                                                     │
│ ══════════════════════════════════════════════════════════════════  │
│ NODE 6: Integration                                                 │
│ ══════════════════════════════════════════════════════════════════  │
│ General: DevOps | Impact: 7/10 | Depends: Node-4, Node-5           │
│                                                                     │
│ TRACK ASSIGNMENT:                                                   │
│ ├─ Exec: JUNCTION (waits for Node-4 AND Node-5)                    │
│ ├─ Reasoning: FCoT (integration narrative)                         │
│ ├─ ARQ: POST only (threshold ≥0.85, flag on fail)                  │
│ ├─ CoVE: CONSISTENCY (after completion)                            │
│ ├─ Bombs PLANT: B-007 ANCHOR for final                             │
│ └─ Bombs DETONATE: B-005, B-006 BRIDGES                            │
│                                                                     │
│ HANDOFF → Node-7 (final)                                           │
│                                                                     │
│ ══════════════════════════════════════════════════════════════════  │
│ NODE 7: Synthesis                                                   │
│ ══════════════════════════════════════════════════════════════════  │
│ General: ALL | Impact: 9/10 | Depends: Node-6                      │
│                                                                     │
│ TRACK ASSIGNMENT:                                                   │
│ ├─ Exec: BATON-FINAL (all tracks merge)                            │
│ ├─ Reasoning: FCoT (synthesize, harmonize, deliver)                │
│ ├─ ARQ: POST only (threshold ≥0.9, HALT on fail)                   │
│ ├─ CoVE: CONSISTENCY, MULTI_EXPERT (final verification)            │
│ ├─ Bombs PLANT: None (final node)                                  │
│ └─ Bombs DETONATE: B-001 ANCHOR, B-007 ANCHOR                      │
│                                                                     │
│ HANDOFF → OUTPUT                                                   │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│ 📊 MANIFEST SUMMARY                                                 │
├─────────────────────────────────────────────────────────────────────┤
│ BOMB REGISTRY:     7 bombs pre-loaded                              │
│ ARQ GATES:         PRE: 3 | POST: 7 | Total: 10                    │
│ REASONING SPLITS:  FCoT: 4 | CoC: 2 | HYBRID: 2                    │
│ EXEC PATTERNS:     BATON: 3 | SWARM: 2 | JUNCTION: 2              │
│ CoVE ASSIGNMENTS:  LOGICAL: 5 | FACTUAL: 2 | CONSISTENCY: 2        │
│                    MULTI_EXPERT: 1                                 │
├─────────────────────────────────────────────────────────────────────┤
│ 🚄 TRACKS LAID - READY FOR BULLET TRAIN EXECUTION                  │
│    All decisions made. Execute = pure speed.                        │
└─────────────────────────────────────────────────────────────────────┘
```

---

## MODE REQUIREMENTS

```
QUICK (R≤3 ∧ Q≤5):
├─ Generals: Don't convene (skip SkeleTraIn)
├─ Tracks: None laid
└─ Execute: Direct generation, no planning

ANALYTICAL (R=4-6 ∨ Q=6-7):
├─ Generals: Light war council
├─ Tracks: Simple layout (3-5 nodes)
├─ Bombs: CLARIFIER + SCAFFOLD only
├─ ARQ: POST gates on high-impact only
├─ CoVE: Top-1 variant per cluster
└─ Execute: Mostly BATON, some parallel

DELIBERATE (R≥7 ∨ K≥6 ∨ Q≥8):
├─ Generals: Full war council
├─ Tracks: Complete railroad (5-8 nodes)
├─ Bombs: Full arsenal + registry
├─ ARQ: PRE+POST on impact≥7
├─ CoVE: Top-2 variants per cluster
└─ Execute: BATON + SWARM optimized

MAXIMUM (R≥9 ∨ K≥8 ∨ /deep):
├─ Generals: Extended war council
├─ Tracks: Metro system (GoT if D≥7)
├─ Bombs: Deep injection + cross-reference
├─ ARQ: ALL nodes PRE+POST
├─ CoVE: All variants ≥4 score
└─ Execute: Full SWARM + multi-model if available
```

---

## ENFORCEMENT

```
CRITICAL: SkeleTraIn manifest = REQUIRED for modes ≥ ANALYTICAL

IF model attempts direct execution without manifest:
  → HALT
  → Display: "Generals must lay tracks first."
  → Force SkeleTraIn phase
  → Resume only after manifest complete

IF manifest incomplete (missing bombs/gates/reasoning):
  → HALT
  → Display: "Tracks incomplete. Missing: [list]"
  → Complete expansion phase
  → Resume after all decisions made

EXECUTION RULE:
  During Baton/Swarm phase, NO NEW DECISIONS ALLOWED
  All decisions reference SkeleTraIn manifest
  If situation not covered → FLAG for post-exec review, don't stop train
```

---

## COMMANDS

```
/skeletrain         → Generate full manifest
/skeletrain-show    → Display current manifest
/skeletrain-tracks  → Visualize execution pattern map
/skeletrain-bombs   → Show bomb registry with coordinates
/skeletrain-gates   → Display ARQ gate positions
/skeletrain-cove    → Show CoVE variant assignments
/skeletrain-force   → Regenerate manifest from scratch
```

---

## THE BULLET TRAIN PRINCIPLE

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│   BEFORE SKELETRAIN:                                                │
│   ══════════════════                                                │
│   Execute phase = constant decision-making                          │
│   "Should I use FCoT here? Where's the bomb? Which gate?"          │
│   SLOW. INCONSISTENT. ERROR-PRONE.                                  │
│                                                                     │
│   AFTER SKELETRAIN:                                                 │
│   ═════════════════                                                 │
│   Execute phase = follow the tracks                                 │
│   Expert-1: "I'm at Node-3. Manifest says: HYBRID reasoning,       │
│              detonate B-001, PRE+POST ARQ. EXECUTING."             │
│   FAST. CONSISTENT. RELIABLE.                                       │
│                                                                     │
│   🚄💨 BULLET TRAIN: Tracks laid, signals set, bombs loaded.       │
│         All aboard. Full speed ahead.                               │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘

Generals plan. Trains run. Victory achieved.
```

---

**SkeleTraIn of Thought v2.1**
*Generals lay the tracks. Execution fires like a bullet train.*
Kevin Tan (ktg.one) | ANZ Top 0.8% | Vertex AI 0.01%
"Plan completely. Execute purely. Deliver decisively."
