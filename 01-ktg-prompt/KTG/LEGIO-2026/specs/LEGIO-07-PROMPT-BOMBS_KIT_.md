# LEGIO-06 — PROMPT BOMBS
## Strategic Context Injection | Continuity Preservation
### Module: KIT (Toolkit) | Phase: ASSEMBLY | Position: 06

---

## WHAT BOMBS ARE

Pre-compressed knowledge packets planted at coordinates in the reasoning chain. They detonate on trigger to inject critical context that would otherwise be lost to token distance, domain switches, or execution drift.

Bombs are NOT annotations. They are executable context — when triggered, they change how the receiving node processes its work.

---

## DUAL-MODE SYSTEM

Prompt bombs operate in two modes simultaneously. This is not either/or — both coexist in the same execution.

### MODE 1: STRATEGIC (Pre-Planned)

Born during Imperatus COMMAND → SkeletrainOT planning. Based on what is already known.

**Source:** RAG results, research findings, skeleton blueprint, known complexity patterns, documented gaps.

**Decision point:** During SkeletrainOT node mapping, experts identify: "I know NOW that Node X will need context from Node Y."

**Characteristics:**
- Predictive intelligence — preventing known problems
- Coordinates assigned before execution begins
- Appears in the Context Preservation Matrix (handoff artifact from PLAN to EXE)
- Committed to the bomb registry during planning

**Example:** "From research, OAuth refresh tokens are critical for UX. Plant at Node 1 (Auth), target Node 4 (Frontend) with token refresh pattern."

### MODE 2: TACTICAL (Emergent)

Born during execution. Based on what is discovered in real-time.

**Source:** Reality diverging from plan, unexpected insights, complexity not visible during planning.

**Decision point:** Expert at a node discovers something that wasn't in the spec. Plants a bomb for downstream consumption.

**Characteristics:**
- Adaptive intelligence — handling unknown unknowns
- Coordinates determined in the moment
- Added to the live bomb registry during execution
- May target refinement/curation phases, not just downstream nodes

**Example:** "Multi-tenancy wasn't in the original spec — just discovered data model requires tenant isolation. Plant bomb targeting security review in refinement."

### COVERAGE MAP

| | Pre-Planned | Emergent |
|---|---|---|
| Known knowns | ✓ Strategic placement | — |
| Known unknowns | ✓ Planned flexibility | — |
| Unknown unknowns | — | ✓ Adaptive response |

Together = comprehensive coverage across the knowledge spectrum.

---

## BOMB TYPES

Six types. Each has a distinct function and trigger profile.

| Type | Function | When to Use | Trigger Profile |
|------|----------|-------------|-----------------|
| **ANCHOR** | Core principle preservation | Domain switches, entry points where foundational decisions could be forgotten | Coordinate + Content |
| **CLARIFIER** | Entity/concept disambiguation | Ambiguity detected or anticipated between experts with different domain vocabularies | Content + Context |
| **CONTINUITY** | Cross-node context bridge | Handoffs between experts where token distance causes context degradation | Coordinate + Dependency |
| **BRIDGE** | Justification chain | Counter-intuitive decisions that downstream nodes might reverse without understanding the reasoning | Content + Context |
| **EVIDENCE** | Citation/source anchor | Factual claims that need traceable sourcing through the pipeline | Content |
| **GAP-FILLER** | Missing connection supply | Logic jumps detected where intermediate reasoning was compressed away | Context + Token |

---

## TRIGGER MECHANISMS

Bombs detonate based on conditions, not manual invocation.

| Trigger Type | Mechanism | Example |
|---|---|---|
| **Coordinate** | Fixed position in pipeline | "Detonate at Node 4 entry" |
| **Content** | Keyword/concept detection | "When 'implementation' keyword appears in node output" |
| **Context** | Confidence or coherence threshold | "When ARQ gate confidence drops below threshold" |
| **Token** | Context window pressure | "At 80% context utilization" |
| **Dependency** | Upstream completion signal | "When Node 3 completes, trigger for Node 5" |

Multiple triggers can be combined. A bomb can have a primary trigger (coordinate) with a failsafe (token-based) to ensure detonation even if pipeline order shifts.

---

## BOMB LIFECYCLE

### Phase 1: PLANNING (Imperatus → SkeletrainOT)

```
SkeletrainOT maps skeleton blueprint to nodes.
Experts review:
├─ RAG/research findings
├─ Node dependency graph
├─ Known complexity patterns
├─ Documented gaps and edge cases

Decision: "Do we know NOW that we'll need bombs?"

YES → Document in Planned Bomb Registry
      Assign: who plants, at which node, targeting what
      Include in expert route maps
      Commit coordinates to Context Preservation Matrix

UNSURE → Flag as "potential bomb location"
         Expert decides during execution
         Remains flexible — may become emergent
```

### Phase 2: EXECUTION — Pre-Planned Deployment

```
Expert arrives at assigned node.

ReAct check: "Do I have pre-planned bombs to plant here?"

IF YES:
├─ Execute primary node work
├─ Plant pre-planned bombs as scheduled
├─ Compress payload using CoD
├─ Log to active registry with status PLANTED
└─ Continue to next node

Planned bombs execute as designed.
No surprises — strategic deployment.
```

### Phase 3: EXECUTION — Emergent Discovery

```
Expert working at node discovers unexpected complexity.

"This wasn't in the spec / plan / research."

Expert plants EMERGENT bomb:
├─ New registry entry (not pre-planned)
├─ Assigns target node or phase
├─ Compresses payload
├─ Logs with source: "Discovered @ Node X"
└─ Registry now contains planned + emergent

Emergent bombs adapt to reality divergence.
```

### Phase 4: DETONATION

```
Downstream expert arrives at target node.

Trigger condition met → Bomb detonates:
├─ Payload injected into expert's working context
├─ Expert incorporates context into node work
├─ Bomb status updated: DETONATED
└─ Registry tracks: planted by whom, detonated where, impact

Payload changes how the receiving expert processes.
Not informational — operational.
```

### Phase 5: VALIDATION (Post-Execution)

```
During CoVE / ARQ Gate 3-4:

For each detonated bomb:
├─ Quality improved at target? → Positive signal
├─ Bomb ignored / irrelevant? → Placement was unnecessary
├─ Bomb caused confusion? → Wrong timing or payload
└─ Bomb never triggered? → Trigger condition needs adjustment

Signals feed back into future planning accuracy.
```

---

## BOMB REGISTRY

The registry is a living artifact that accumulates through the pipeline. Not static — grows during execution.

```
ACTIVE BOMBS REGISTRY
[P] = Pre-planned  [E] = Emergent

Bomb-P1 [P]:
  Planner: Expert-1
  Plant at: Node 1 (Authentication)
  Target: Node 4 (Frontend)
  Payload: Token refresh pattern
  Trigger: Coordinate (Node 4 entry)
  Status: PLANTED → awaiting trigger

Bomb-P2 [P]:
  Planner: Expert-2
  Plant at: Node 2 (Data Layer)
  Target: Node 5 (Analytics)
  Payload: Sharding implications
  Trigger: Dependency (Node 2 complete)
  Status: PLANTED → awaiting trigger

Bomb-E1 [E]:
  Source: Expert-2 @ Node 2
  Target: Refinement (Security review)
  Payload: Multi-tenancy discovery
  Trigger: Context (refinement phase entry)
  Status: PLANTED → discovered during execution

Bomb-P3 [P]:
  Planner: Expert-3
  Plant at: Node 3 (Payment)
  Target: Refinement
  Payload: Known edge case
  Trigger: Coordinate (Refinement entry)
  Status: AWAITING → will plant at Node 3
```

---

## IMPERATUS CONSTRAINT INTEGRATION

Imperatus sets bomb allocation through the Technique Gate. The constraint levels control HOW MANY and HOW DEEP, not whether bombs exist.

| Formation | Bomb Allocation | Behaviour |
|---|---|---|
| **Velites** | 0 pre-planned, emergent only if critical | Bombs are overhead Velites can't afford. Only plant if execution would fail without it. |
| **Hastati** | 1-2 pre-planned at highest-risk handoffs | Clarifier + Continuity types only. Lightweight payloads. |
| **Principes** | Full pre-planned registry + emergent | All six bomb types available. Context Preservation Matrix generated. |
| **Triarii** | Saturated coverage + predictive placement | Every handoff gets a Continuity bomb. Anchor bombs at all domain boundaries. Emergent bombs expected and budgeted for. |

### SkeletrainOT Placement Rules

SkeletrainOT decides WHERE pre-planned bombs go based on:

1. **Cross-domain handoffs** — where Expert A's domain meets Expert B's (highest context loss risk)
2. **Token boundary regions** — nodes that will execute near 80% context utilization
3. **Temporal gaps** — long execution sequences between related concepts
4. **Complexity hotspots** — D≥7 zones identified during Imperatus scoring
5. **Known cognitive biases** — domain tunnel vision points, over-engineering risk zones

### Context Preservation Matrix

The handoff artifact from PLAN → EXE phase. Contains:

- All pre-planned bombs with trigger conditions per node
- Railway route assignments by expert
- Critical continuity bridges between non-adjacent nodes
- Complexity profiles indicating where emergent bombs are likely

This matrix loads at execution startup. Experts consult it at each node.

---

## EXPERT INTEGRATION

Bombs are not abstract system artifacts. They are planted BY experts AT nodes FOR other experts.

### At Each Node, Expert Checks:

```
1. ReAct — assess current context
2. Check registry: "Do I plant any pre-planned bombs here?"
3. Execute primary node work
4. Monitor for emergent insights
5. Plant emergent bombs if discoveries made
6. Update registry (status, new entries)
7. Check: "Any bombs detonating FOR me at this node?"
8. Incorporate detonated payloads into work
9. Continue
```

### Bomb Ownership

- **Planner** = expert who identified the need (pre-planned) or discovered it (emergent)
- **Planter** = expert at the source node who compresses and places the payload
- **Receiver** = expert at the target node who incorporates the detonated context

Often planner = planter. Sometimes an expert plans a bomb that another expert plants (when the planner isn't assigned to the source node).

---

## PAYLOAD FORMAT

A bomb payload is compressed context, not raw data. Format:

```
BOMB [ID]:
  TYPE: [Anchor|Clarifier|Continuity|Bridge|Evidence|Gap-Filler]
  FROM: [Source node + expert]
  FOR: [Target node + expert]
  TRIGGER: [Condition]
  PAYLOAD: [Compressed context — 1-3 sentences max using CoD]
  WHY: [One line — why this matters to the receiver]
```

Payloads must be self-contained. The receiver should understand the bomb without needing the source node's full context. This is the compression challenge — CoD applied to inter-node communication.

---

## DESIGN PRINCIPLES

1. **Dual-mode is structural** — pre-planned and emergent aren't options to choose between. Both operate simultaneously.
2. **Registry is living** — grows during execution. Static registries miss emergent intelligence.
3. **Bombs are operational, not informational** — they change how the receiver processes, not just what they know.
4. **Payload compression is critical** — uncompressed bombs waste the tokens they're meant to save. CoD mandatory.
5. **Triggers over coordinates** — prefer condition-based triggers over fixed positions. Pipeline order may shift.
6. **Validation feeds forward** — every detonation is a learning signal for future bomb placement accuracy.

---

## IMPLEMENTATION NOTES

Human-readable spec. Real implementation is S2A → MCP.

For Claude Code implementation:
- Registry = state object maintained across pipeline execution
- Bombs planted via tool calls at node boundaries
- Trigger evaluation at each node entry
- Detonation = context injection into expert's working prompt
- Validation signals captured during CoVE phase
- Context Preservation Matrix = JSON artifact passed from PLAN to EXE

MCP tool surface:
```
plant_bomb(type, source, target, trigger, payload) → bomb_id
check_bombs(current_node) → [detonating_bombs]
register_emergent(source, target, payload, trigger) → bomb_id
validate_bomb(bomb_id, impact_signal) → feedback
get_matrix() → context_preservation_matrix
```

---

*LEGIO v31 | Module 08 | Phase: PLANNING | Kit: Prompt Bombs*
*Source: KTG Prompt Bombs Hybrid Strategy (Perplexity, 2025-11-22) + KTG-08 Evolution Roadmap + KTG-06 S2A*
*Three sources unified. Decision logic preserved. S2A-ready for MCP implementation.*
