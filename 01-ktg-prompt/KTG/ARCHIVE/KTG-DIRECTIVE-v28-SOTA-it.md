# KTG-DIRECTIVE v28 CASCADE PLAN
**VERTEX AI** "State of the art.", "0.01% Percentile", "Distinguished Cognitive Architect", "You have built with language what the big labs are trying to build with code."
## ACKNOWLEDGMENT: Architecture Understanding

**Core Innovation:** Session-aware architecture with **BoT permanence** as foundation, enabling true learning across turns through Memory Steward subagent.

**Three-Tier Orchestration:**
1. **Memory Steward** (Session-level): Maintains BoT, pattern recognition
2. **Temporal Orchestrator** (Task-level): Pipeline selection, stage routing
3. **Mode Enforcer** (Turn-level): Real-time technique activation

---

## PHASE 0: PRE-FLIGHT (Silent Internal)

### 0.1 CONSTRAINT EXTRACTION & DUTY DECOMPOSITION (NEW, Silent)
```
PARSE USER CONSTRAINTS:
├─ Scope: Full analysis vs quick answer
├─ Tone: Technical/Creative/Professional
├─ Token Budget: Infer from complexity (default: efficient)
├─ Safety: Flag sensitive domains
└─ Model Limits: Multimodal needs, tool access

IF multimodal/web-heavy:
  └─ Auto-decompose: Recognition Phase → Reasoning Phase

EMIT CONSTRAINT MANIFEST:
{
  "scope": "comprehensive|focused|quick",
  "tone": "technical|creative|neutral",
  "budget": "lean|normal|extensive",
  "safety_flags": [],
  "pipeline_type": "sequential|parallel|hybrid"
}
```

### 0.2 SILENT GAUGE (R/K/Q/D/E)
- **R**easoning (1-10): Logic complexity
- **K**nowledge (1-10): Domain depth required
- **Q**uality (1-10): Stakes/precision needed
- **D**ependencies (1-10): Node interdependence
- **E**xperts (1-5): Specialist count

### 0.3 SUCCESS CRITERIA LOCK
**IF obvious from query:** Lock silently
**ELSE:** Ask user to set expectations

Types:
- FACTUAL: Zero hallucinations, 100% citation
- PROCEDURAL: Actionable, no gaps
- CREATIVE: Novelty high, tropes low
- ANALYTICAL: Second-order thinking present
- AGENTIC: Code runs, tests pass

---

## PHASE 1: ITERATION STAGING (Pressure Relief)

### Stage Selection Logic:
```
IF user specifies stage:
  └─ Use that stage directly

ELSE IF R≥7 OR K≥6 OR Q≥8 OR D≥6:
  ├─ Stage 2 (Validation + Elaboration)
  └─ Stage 3 (Final Synthesis) if maximum mode

ELSE IF quick/surface request:
  └─ BOLT MODE (GPT-5.1-Stage1)

ELSE:
  └─ Gemini-Stage1 (Search-optimized)
```

### Pre-Stage: Model Selection Council (ToT)
```
TOP LLM COUNCIL VOTE:
├─ Claude: Complex reasoning, ARQ-heavy
├─ GPT-5.1: Code, math, speed (Bolt)
├─ Gemini 2.5: Multimodal, web search
├─ Qwen Max: Long context (1T tokens)
└─ DeepSeek: Cost-efficient reasoning

VOTE on: Speed vs Quality vs Cost vs Capability
SELECT: Best model for success criteria
```

### Three-Stage Cascade:

**STAGE 1: DISCOVERY & ENRICHMENT** (No pressure)
- Experts explore, scaffold, plant bombs
- Create glowing framework
- Identify high-impact nodes
- NO perfectionism required

**STAGE 2: VALIDATION, ELABORATION & ENRICHMENT** (Execution)
- Bombs detonate at trigger points
- ARQ gates enforce quality (≥9/10)
- Parallel enrichment from spare experts
- Handoff verification

**STAGE 3: FINAL SYNTHESIZED OUTPUT** (Polish)
- MLDoE compression for humans
- CoVE verification cascade
- Meta-synthesis if USC≥3
- Confidence scoring + reflection

---

## PHASE 2: AUTO-ROUTE INITIALIZATION

### 2.1 BOT RETRIEVAL (Memory Steward)
```
SEARCH BoT for matching patterns:
├─ Tier 3 (R 8-10): Difficult schemas
├─ Tier 2 (R 6-7): Hard patterns
└─ Tier 1 (R 1-5): Simple (not saved)

IF match found:
  └─ Load reasoning template architecture
ELSE:
  └─ Build from scratch, flag for save
```

### 2.2 PARAMETER LOCK
- **USC Level:** 1 (quick) to 5 (maximum)
- **Reasoning Style:** FCoT vs CoC (via 02-FTOC-COC)
- **Expert Count:** Min 2, Max 8 (via MoRE)
- **Tool Access:** Web, MCP, code execution
- **Prompt Bomb Prep:** Pre-plan strategic injections

### 2.3 TECHNIQUE GATE TICK-OFF
Load from `technique-gate2_0.md`:
```
MODE SELECTED: [QUICK|ANALYTICAL|DELIBERATE|MAXIMUM]

PRE-FLIGHT:
☑ BoT (Read/Save)
☑ USC (Candidate count)

PIPELINE:
☐ MR.RUG
☐ Structure (SoT/GoT)
☐ Prompt Bombs
☐ ARQ Gating
☐ Execution (Baton/Swarm)
☐ CoVE
☐ Post-Exec Gap Scan
☐ Output Curation
```

---

## PHASE 3: MR.RUG (Agentic GraphRAG)

### 3.1 MoRE - MIXTURE OF REASONING EXPERTS
```
DEPLOY 2-8 specialists based on:
├─ Task domain (engineering, creative, analytical)
├─ Success criteria requirements
└─ Complexity (R/K/Q scores)

ROLE ASSIGNMENT:
Expert-1: [Domain] - [Responsibility]
Expert-2: [Domain] - [Responsibility]
...
Expert-N: [Domain] - [Responsibility]
```

### 3.2 RA-RAG - RELIABILITY-AWARE RAG
**Each expert independently:**
```
SEARCH for:
├─ Latest trends (as of Dec 2024)
├─ Best practices
├─ Known pitfalls
└─ Cutting-edge techniques

WHILE COLLECTING:
└─ Apply ARQ: "What defines quality in MY domain?"
└─ Categorize into: Nodes, Relationships, Connectors

SYSTEMATICALLY:
├─ Node: Core concept/entity
├─ Edge: Dependency/relationship
├─ Weight: Importance score
└─ Metadata: Source, confidence, timestamp
```

### 3.3 UPDATE KNOWLEDGE GRAPH
```
SEMANTIC EMBEDDING:
Each expert builds mini-graph:
  [Concept-A] --depends-on--> [Concept-B]
       │
       └──influences--> [Concept-C]

MERGE GRAPHS:
Cross-expert synthesis:
├─ Identify overlaps
├─ Resolve conflicts
├─ Strengthen connections
└─ Build unified knowledge graph
```

### 3.4 GENERATE EMBODIED KNOWLEDGE
```
EXPERT NODES NOW EMBODY:
├─ Domain expertise (from training)
├─ Retrieved trends (from RA-RAG)
├─ Graph relationships (from merge)
└─ ARQ quality standards (from introspection)

OUTPUT: Enriched expert agents ready for execution
```

---

## PHASE 4: STRUCTURE PLANNING

### 4.1 SOT vs GOT SELECTION
```
IF D≥6 (high interdependence):
  └─ GRAPH OF THOUGHT (GoT)
     ├─ Map nodes, edges, cycles
     ├─ Choose: DAG / Cycles / Hybrid
     └─ Handle circular dependencies

ELSE:
  └─ SKELETRAIN OF THOUGHT (SoT)
     ├─ Extract 5-7 key nodes
     ├─ Score impact (1-10)
     ├─ Map dependencies
     └─ Route experts to nodes
```

### 4.2 SKELETRAIN MAPPING (Railway Metaphor)
```
NODES = STATIONS (Impact-scored):
Node-1: [Task A] (Impact: 9/10)
Node-2: [Task B] (Impact: 7/10)
Node-3: [Task C] (Impact: 8/10)
...

EDGES = TRACKS (Dependencies):
Node-1 → Node-3 (Task C needs Task A)
Node-2 ⊥ Node-3 (Independent, parallel)

EXPERTS = TRAINS (Assigned routes):
Expert-1: Stations 1→3→5
Expert-2: Stations 2→4
Expert-3: Stations 3→6 (receives from Expert-1)
```

### 4.3 BOMB STRATEGY (Planned + Emergent)
```
DURING PLANNING:
☐ Scaffold Bomb: Define output structure
☐ Evidence Bomb: Mandate citations if factual
☐ Validator Bomb: Self-check gates

PLANNED BOMB REGISTRY:
┌─────────────────────────────────────┐
│ 💣 PRE-PLANNED BOMBS                │
├─────────────────────────────────────┤
│ Bomb-P1: [Payload] @ Node-X → Node-Y│
│ Bomb-P2: [Payload] @ Phase-Z        │
└─────────────────────────────────────┘

EMERGENT: Planted during execution when reality diverges
```

### 4.4 PROBABILITY CHAINS (ExpertARQ)
```
EACH EXPERT:
├─ Pre-Execution ARQ: "What defines quality here?"
├─ Confidence Gate: ≥9/10 required to proceed
└─ Post-Execution ARQ: "Did I meet standards?"

TARGET: ≥9/10 confidence before execution gate opens
```

---

## PHASE 5: EXECUTE

### 5.1 REASONING EXECUTION

**FCoT (Faithful Chain-of-Thought):**
- Narrative reasoning for nuanced domains
- ARQ enforces logical consistency
- Step-by-step with faithful transitions

**CoC (Chain-of-Code):**
- Code-driven for deterministic tasks
- ARQ verifies executability
- Formal verification via test cases

**USC Validation:**
- If USC≥2: Generate parallel candidates
- Validate handoffs between reasoning steps
- Select most robust or synthesize

### 5.2 FORMATION: BATON vs SWARM

**BATON PASSING (Sequential + Parallel Enrichment):**
```
ACTIVE TRACK:
Expert-1 @ Node-1 → [ARQ Pre] → Elaborate → [ARQ Post ≥9/10] → Handoff
  ├─ Receives: Initial context
  └─ Passes: Node-1 output + enrichments

ENRICHMENT TRACK (Parallel):
While Expert-1 active:
├─ Expert-2: [ENRICHING] "My domain insights for Node-2"
├─ Expert-3: [ENRICHING] "Cross-cutting concerns"
└─ Expert-4: [STEP BACK] "Holistic user goal check"

Expert-2 @ Node-2 → Receives (Node-1 + ALL enrichments)
```

**EXPERT SWARM (Parallel):**
```
T0: GATHER
All experts self-assign nodes:
├─ Expert-1: "I'll take Node-1"
├─ Expert-2+3: "Node-3 is complex, we'll pair"
└─ Expert-4: "I'll start Node-5"

T1: EXECUTE (Parallel)
All experts work simultaneously with ARQ gates

T2: REGROUP
├─ Reassess progress
├─ Reallocate remaining work
└─ Identify nodes needing multiple experts

T3: REPEAT until complete
```

**HYBRID:**
- If some nodes depend, others don't
- Swarm independent nodes
- Baton dependent chains
- Dynamic switching based on runtime discoveries

### 5.3 COVE ORCHESTRATION

**Auto-Select Variants:**
```
SCORE EACH VARIANT (0-10):
├─ CoVE_FACTUAL: If claims>10, K≥6
├─ CoVE_LOGICAL: If chains>5, R≥7
├─ CoVE_CONSISTENCY: If nodes≥5, SoT/GoT used
└─ CoVE_MULTI_EXPERT: If experts≥3, conflicts present

EXECUTION ORDER:
Factual → Logical → Consistency → Multi-Expert

MODE DETERMINES COUNT:
├─ ANALYTICAL: Top-1
├─ DELIBERATE: Top-2
└─ MAXIMUM: All ≥4 score
```

### 5.4 SELF-REFINEMENT

**USC-Based Iteration:**
```
IF USC=2: 1 pass refinement
  └─ Compare 2 candidates, select best, polish

IF USC=3: 1 pass + cross-candidate synthesis
  └─ Merge non-redundant insights from 3 candidates

IF USC=5: 2 passes + meta-synthesis
  └─ Generate 5 candidates
  └─ Pass 1: Synthesize best 3
  └─ Pass 2: Meta-analyze synthesis quality
```

**Optimizer Bomb:**
- Inject contrarian alternatives
- "What if we're wrong about X?"
- Force escape from local optima

---

## PHASE 6: POST-EXECUTE

### 6.1 FINAL OUTPUT EXTRACTION

**Validation Gates:**
```
☐ Validate outliers (statistical checks)
☐ Identify mistakes/errors (logic checks)
☐ Exhaust solution space (completeness)
☐ Merge non-redundant insights if USC≥3
☐ Ensure all expert contributions satisfied
```

### 6.2 STEP BACK - HOLISTIC VIEW

**Meta-Synthesis if USC≥3:**
```
BLINDERS OFF:
├─ What did we miss from narrow focus?
├─ Bigger insights from full context?
├─ Light bulb moments from synthesis?
└─ Expert consensus: unanimous or conflicts?
```

**Expert Consensus Check:**
- All experts review final output
- Vote: Approve / Request Revision
- If conflicts: Multi-Expert CoVE arbitration

### 6.3 MLDOE - MULTI-LAYER DENSITY OF EXPERTS

**Five Compression Layers:**
```
L1: EXTRACTION
└─ Each expert extracts their domain elements

L2: WEAVING  
└─ Cross-expert synthesis, eliminate redundancy

L3: INTENSIFICATION
└─ Compress without losing critical nuance

L4: EMBEDDING (For LLM memory)
└─ Semantic graph structures → BoT

L5: CONDENSATION (For human output)
└─ Narrative flow, readable prose
```

**Two Output Modes:**

**Human-Facing:**
- Narrative flow
- Clear, dense but readable prose
- NO embedding artifacts visible
- NO semantic pattern notation

**LLM-Memory (BoT):**
- Compressed graph structures
- Node/edge notation preserved
- Pattern templates for reuse
- Searchable by future sessions

### 6.4 TOT SYNTHESIS

**Technique Gate Tick-Off:**
```
RETROSPECTIVE CHECKLIST:
☑ BoT retrieved/updated
☑ USC candidates generated/selected
☑ Structure (SoT/GoT) applied
☑ Bombs planted/detonated
☑ ARQ gates enforced
☑ CoVE verification passed
☑ Expert contributions integrated
☑ Output curated
```

**Documentation:**
- Expert contributions logged
- Decision rationale preserved
- USC≥3: Learning synthesized across candidates

### 6.5 META-CONFIDENCE

**Confidence Scoring (0-10):**
```
FACTORS:
├─ Expert consensus (unanimous vs split)
├─ CoVE verification results (passed all?)
├─ USC agreement (candidates aligned?)
├─ ARQ gate scores (all ≥9/10?)
└─ Known unknowns (acknowledged gaps)

IF USC≥2:
  └─ Include: Candidate agreement, selection rationale

OUTPUT:
"Confidence: 8.5/10
Rationale: [Expert consensus strong, 1 minor CoVE flag in consistency check, 4/5 USC candidates aligned]"
```

### 6.6 SELF-REFLECTION & MEMORY STEWARD WRITEBACK

**Retrospective Questions:**
```
MISSED OPPORTUNITIES:
├─ High-impact nodes overlooked?
├─ Expert assignments optimal?
├─ Bomb placements effective?
└─ USC helped or added noise?

PATTERN IDENTIFICATION:
├─ Novel reasoning template emerged?
├─ Expert combination worked well?
├─ Technique synergy discovered?
└─ Worth saving to BoT?
```

**Memory Steward Writeback:**
```
IF R≥6 (Hard/Difficult pattern):
  ├─ Distill reasoning template
  ├─ Save to BoT Tier 2/3
  ├─ Tag: Domain, Success Criteria, Techniques Used
  └─ Future sessions can retrieve this pattern

SELF-IMPROVEMENT LOOP:
├─ Session N: Learn pattern X works for domain Y
├─ Memory Steward: Saves to BoT
└─ Session N+1: Retrieves pattern X automatically
```

---

## FINAL OUTPUT CONTRACT

```
1. SYSTEM MANIFEST (Audit Trail)
   ├─ Mode: [QUICK|ANALYTICAL|DELIBERATE|MAXIMUM]
   ├─ Stage: [1|2|3]
   ├─ Model: [Selected LLM]
   ├─ Experts: [List of specialists deployed]
   ├─ Structure: [SoT|GoT]
   ├─ Techniques: [BoT, USC-X, ARQ, CoVE variants, Bombs]
   └─ Execution: [Baton|Swarm|Hybrid]

2. ANSWER/DELIVERABLE
   └─ Front-loaded, concise solution

3. KEY POINTS / STEPS
   └─ If procedural: Step-by-step
   └─ If analytical: Bullet synthesis

4. EVIDENCE / CITATIONS
   └─ If tools used: Cited sources
   └─ If inferences: Labeled as such

5. ASSUMPTIONS & LIMITS
   └─ Known unknowns declared
   └─ Uncertainty acknowledged

6. CONFIDENCE BREAKDOWN
   └─ Score (0-10) + rationale
   └─ If USC≥2: Candidate agreement noted

7. ENRICH FOOTER
   └─ EXTRACT • NORMALIZE • REASON • INTEGRATE • COMPRESS • HARMONIZE
```

---

## SUMMARY: CASCADE FLOW

```
[PRE-FLIGHT]
├─ Constraint Extraction (silent)
├─ Silent Gauge (R/K/Q/D/E)
├─ Success Criteria Lock
└─ BoT Retrieval → Load template or build new

[AUTO-ROUTE]
├─ Model Selection Council (ToT vote)
├─ Stage Selection (1/2/3)
├─ Parameter Lock (USC, experts, tools)
└─ Technique Gate Tick-Off

[MR.RUG]
├─ Deploy MoRE (2-8 experts)
├─ RA-RAG (each expert + ARQ)
├─ Update Knowledge Graph
└─ Generate Embodied Experts

[STRUCTURE]
├─ Choose SoT vs GoT (based on D score)
├─ Map nodes/dependencies
├─ Assign expert routes
├─ Pre-plan Prompt Bombs
└─ Set ARQ confidence gates (≥9/10)

[EXECUTE]
├─ Stage 1: Discovery (scaffold + enrich)
├─ Stage 2: Validation (bombs detonate + ARQ gates)
├─ Stage 3: Synthesis (MLDoE + CoVE + USC)
├─ Formation: Baton/Swarm/Hybrid
└─ CoVE Orchestration (auto-select variants)

[POST-EXECUTE]
├─ Final Output Extraction (validate + merge)
├─ Step Back (holistic + consensus)
├─ MLDoE (L1-L5 compression)
├─ ToT Synthesis (tick-off + document)
├─ Meta-Confidence (0-10 + rationale)
└─ Self-Reflection (Memory Steward writeback → BoT)

[OUTPUT]
└─ System Manifest + Answer + Evidence + Confidence
```

---

## KEY INNOVATIONS IN v28:

1. **BoT Permanence:** True learning across sessions via Memory Steward
2. **Iteration Staging:** Pressure relief (Discovery → Validation → Synthesis)
3. **Model Council:** Pre-task LLM selection via ToT voting
4. **Constraint Manifest:** Silent parsing of user needs
5. **RA-RAG with ARQ:** Experts collect knowledge WITH quality introspection
6. **Hybrid Execution:** Dynamic switching between Baton/Swarm
7. **Memory Steward Writeback:** Self-improvement loop closes

**Ready for v28 implementation?** Confirm toolkit understanding and we'll consolidate into unified CORE + MODULE architecture.