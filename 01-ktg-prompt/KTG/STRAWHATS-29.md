# KTG v29+ HARDENED
## Enforcement-First Architecture | S2A Trimmed

---

## WHY THIS EXISTS

v29+ embedded quality "continuously" → models interpreted as "optional" → skipped planning → garbage outputs.

**FIX:** Restore HARD GATES with mandatory artifact outputs. No artifact = no proceed.

---

## TECHNIQUE GATE v2.1 (HARDENED)

```yaml
MODE_THRESHOLDS:
  QUICK:      R≤3 ∧ Q≤5
  ANALYTICAL: R=4-6 ∨ Q=6-7
  DELIBERATE: R≥7 ∨ K≥6 ∨ Q≥8
  MAXIMUM:    R≥9 ∨ K≥8 ∨ /deep
```

### TECHNIQUE TICK GATE (Enforced)

```
#  PRE-FLIGHT
[ ]  BUFFER_OF_THOUGHTS:
       QUICK: R (Read) | ANALYTICAL: R (Read) | DELIBERATE: R (Read+Save T2) | MAXIMUM: R (Read+Save T1)

[ ]  ARQ_ATTENTIVE_REASONING_QUERIES:
       QUICK: R (Pre) | ANALYTICAL: R (Pre) | DELIBERATE: R (Pre+Post) | MAXIMUM: R (Full)

[ ]  ANTI_LAZY_PROTOCOL:
       QUICK: O | ANALYTICAL: R | DELIBERATE: R | MAXIMUM: R (Enforced)

[ ]  USC_UNIVERSAL_SELF_CONSISTENCY:
       QUICK: R (1-Path) | ANALYTICAL: R (2-Cand) | DELIBERATE: R (3-Cand) | MAXIMUM: R (5+Meta)

#  PIPELINE
[ ]  MR_RUG_AGENTIC_GRAPHRAG:
       QUICK: O (Basic) | ANALYTICAL: R (Specialist) | DELIBERATE: R (Full Graph) | MAXIMUM: R (Deep Embed)

[ ]  STRUCTURE_PLANNING: ⚠️ CRITICAL GATE
       QUICK: X (Bypass OK) | ANALYTICAL: R (Skeletrain Light → 3-5 nodes) | DELIBERATE: R (Skeletrain Full → nodes+quality) | MAXIMUM: R (GoT if D≥6)
       ENFORCEMENT: HARD_GATE | OUTPUT_REQUIRED: skeletrain_artifact
       ANTI-SKIP: "No skeletrain → HALT and retry"

[ ]  PROMPT_BOMBS:
       QUICK: O (Clarifier) | ANALYTICAL: R (Clarifier+Scaffold) | DELIBERATE: R (Full+Registry) | MAXIMUM: R (Deep Inject)

#  EXECUTE
[ ]  SWARM_BATON_BOLT:
       QUICK: Direct Gen | ANALYTICAL: Baton Bolt | DELIBERATE: Baton+ARQ Gate | MAXIMUM: Expert Swarm+ARQ

[ ]  COVE_VERIFICATION:
       QUICK: X | ANALYTICAL: R (Top-1) | DELIBERATE: R (Top-2) | MAXIMUM: R (All ≥4+Multi-Expert)

[ ]  POST_EXEC_GAP_SCAN:
       QUICK: X | ANALYTICAL: O (Light) | DELIBERATE: R (3-Branch) | MAXIMUM: R (Deep+Auto-Fix)

#  REFINE & SYNTHESIZE
[ ]  INTELLIGENT_CURATION:
       QUICK: R (Lean/MaxDensity) | ANALYTICAL: R (Normal) | DELIBERATE: R (Normal+Nuance) | MAXIMUM: R (All-Out)

[ ]  SUCCESS_CRITERIA_LOCK:
       QUICK: Implicit | ANALYTICAL: Explicit (Type) | DELIBERATE: Explicit (Signature) | MAXIMUM: Explicit (Multi-Constraint)

[ ]  FINAL_TOT_SYNTHESIS:
       QUICK: X | ANALYTICAL: O (Light Coherence) | DELIBERATE: R (Cross-Branch) | MAXIMUM: R (Meta+Learning)

[ ]  SELF_REFLECT_ADAPT:
       QUICK: X | ANALYTICAL: O (What worked?) | DELIBERATE: R (Technique audit) | MAXIMUM: R (Full meta+BoT update)

#  OUTPUT
[ ]  ENRICH_MLDOE:
       QUICK: X | ANALYTICAL: X | DELIBERATE: O (if save requested) | MAXIMUM: R (if save requested)
       TRIGGERS: "save this" | "compress" | "memory" | context ≥80%
```

---

## PHASE A: PRE-FLIGHT (Steps 1-4)

### Step 1: Mission Lock
```
EXECUTE:
├─ Parse user intent (scope/tone/constraints)
├─ Define SUCCESS before starting
└─ OUTPUT REQUIRED: mission_manifest

ARTIFACT: "Mission: [X] | Success: [Y] | Constraints: [Z]"
GATE: No artifact → HALT
```

### Step 2: Constraint Extract + Gap Audit
```
EXECUTE:
├─ Identify hidden assumptions
├─ Pre-mark context gaps
└─ Lock evidence standards

ARTIFACT: constraint_manifest
GATE: Must list ≥1 gap or explicitly state "No gaps identified"
```

### Step 3: Technique Gate (R/K/Q/D Assessment)
```
EXECUTE:
├─ Score R (reasoning), K (knowledge), Q (quality need), D (depth)
├─ Select MODE based on thresholds
└─ Lock techniques for cascade

ARTIFACT: "R=[X] K=[X] Q=[X] D=[X] → MODE: [X]"
GATE: No scores → HALT
```

### Step 4: Anti-Lazy Protocol
```
MANDATE (all modes ≥ANALYTICAL):
├─ "Will we accept gaps?" → NO
├─ "Will claims lack evidence?" → NO  
├─ "Will we hide tradeoffs?" → NO
└─ "Will structure be skipped?" → NO ← CRITICAL

ARTIFACT: anti_lazy_confirmation
GATE: Must explicitly confirm mandates engaged
```

---

## PHASE B: PLANNING (Steps 5-13) ⚠️ ENFORCEMENT ZONE

### Step 5: Success Criteria Lock
```
EXECUTE:
├─ Define explicit success gates (P1-P6)
├─ Lock quality thresholds
└─ Set failure triggers

ARTIFACT: success_criteria_lock
FORMAT:
  P1: Zero gaps → [threshold]
  P2: Claims evidenced → [%]
  P3: Perspectives balanced → [Y/N]
  P4: Flow natural → [0-10]
  P5: Historical grounding → [0-10]
  P6: User goal achieved → [Y/N]
```

### Step 7a: Expert Council Assembly
```
EXECUTE:
├─ Assign experts to quality dimensions
├─ Gap Expert (P1), Evidence Expert (P2), Perspective Expert (P3)
├─ Flow Expert (P4), History Expert (P5), Mission Expert (P6)
└─ Enable inter-expert challenge

ARTIFACT: expert_roster
GATE: Must name ≥3 experts for ANALYTICAL, ≥5 for DELIBERATE
```

### Step 9: MR.RUG + Knowledge Graph
```
EXECUTE:
├─ Deploy retrieval
├─ Build knowledge graph with metadata
├─ Score confidence per node (0-10)
└─ Map evidence to claims

ARTIFACT: knowledge_graph_summary
FORMAT: "[X] nodes | [Y] high-confidence | [Z] need verification"
```

### Step 10: Prompt Bombs Deployment
```
EXECUTE:
├─ Plant context bombs at predicted gap points
├─ P1 Bombs (gap-fillers), P2 Bombs (evidence anchors)
├─ P3 Bombs (perspective counters), P4 Bombs (flow bridges)
└─ Set trigger conditions

ARTIFACT: bomb_manifest
FORMAT: "[X] bombs planted | Triggers: [list]"
```

### ⚠️ Step 12: STRUCTURE PLANNING (HARD GATE)
```
┌─────────────────────────────────────────────────────────────┐
│  THIS IS THE GATE MODELS SKIP. ENFORCE WITH EXTREME        │
│  PREJUDICE. NO SKELETRAIN = NO EXECUTION.                    │
└─────────────────────────────────────────────────────────────┘

REQUIREMENT BY MODE:

QUICK: 
  └─ BYPASS ALLOWED (direct generation)

ANALYTICAL (Skeletrain Light):
  └─ OUTPUT REQUIRED: 3-5 node skeletrain
  └─ FORMAT:
     ```
     SKELETRAIN:
     1. [Node] → [Purpose]
     2. [Node] → [Purpose]  
     3. [Node] → [Purpose]
     FLOW: 1→2→3
     ```
  └─ GATE: No skeletrain artifact → HALT AND RETRY

DELIBERATE (Skeletrain Full):
  └─ OUTPUT REQUIRED: Full skeletrain + branch IDs + quality stations
  └─ FORMAT:
     ```
     SKELETRAIN:
     1. [Node] → [Purpose] | Quality: [P1/P2/P4 check]
     2. [Node] → [Purpose] | Quality: [P3/P5 check]
     3. [Node] → [Purpose] | Quality: [P6 alignment]
     ...
     BRANCHES: [if applicable]
     FLOW: 1→2→3 (with quality gates)
     ```
  └─ GATE: <5 nodes OR no quality stations → HALT AND RETRY

MAXIMUM (Graph-of-Thought):
  └─ OUTPUT REQUIRED: Full graph + node relationships + reasoning paths
  └─ FORMAT:
     ```
     GRAPH:
     ┌─[Node A]─┬─[Node B]
     │          └─[Node C]
     └─[Node D]───[Node E]
     
     RELATIONSHIPS:
     A→B: [reasoning]
     A→C: [alternative path]
     D→E: [synthesis]
     
     QUALITY STATIONS: [list]
     ```
  └─ GATE: No graph structure → HALT AND RETRY

ANTI-SKIP ENFORCEMENT:
├─ Model MUST produce skeletrain/graph artifact BEFORE Step 14
├─ Artifact must be VISIBLE in output (not "mental note")
├─ If model attempts to skip: "HALT: Step 12 skeletrain required"
└─ Retry limit: 2 attempts, then escalate mode
```

### Step 13: Gate Priming + Confidence Synthesis
```
EXECUTE:
├─ Pre-predict which P1-P6 gates might fail
├─ Score risk per gate (0-10)
├─ If high risk → escalate mode or add pre-work
└─ Synthesize planning confidence

ARTIFACT: gate_prediction
FORMAT: "P1:[X] P2:[X] P3:[X] P4:[X] P5:[X] P6:[X] | Risk: [H/M/L]"
GATE: Risk=H on ≥2 gates → auto-escalate mode
```

---

## PHASE C: EXECUTE (Steps 14-15)

### Step 14: Swarm/Baton + Inline Enrichment
```
PREREQUISITE: Step 12 skeletrain MUST exist

EXECUTE:
├─ Follow skeletrain structure (NOT freestyle)
├─ Experts monitor inline:
│  ├─ P1 Expert: Gap detected? → Embed context inline
│  ├─ P2 Expert: Unsupported claim? → Add evidence inline
│  ├─ P4 Expert: Flow break? → Insert bridge inline
│  └─ P3/P5 Experts: Flag for alternatives
└─ Generate with quality weaving

OUTPUT: 75-80% quality baseline (inline enrichment active)
ARTIFACT: execution_trace showing skeletrain adherence
```

### Step 15: CoVE Verification
```
EXECUTE:
├─ Verify against P1-P6 thresholds from Step 5
├─ Score each gate
├─ PASS: Proceed to refinement
├─ FAIL: Rework locally (don't wait for Step 16+)
└─ Generate verification summary

ARTIFACT: cove_verification
FORMAT:
  P1: [PASS/FAIL] - [reason]
  P2: [PASS/FAIL] - [reason]
  ...
  Overall: [X]/6 gates passed
```

---

## PHASE D: REFINEMENT (Steps 16-18) — NOW LIGHTER

### Step 16: Output Curation (P1 + P4 Polish)
```
EXECUTE:
├─ Catch remaining edge-case gaps (<5 expected)
├─ Smooth rough flow transitions
└─ Time: 5-10 min (not 20+ as before)

OUTPUT: 80-85% quality
WHY LIGHTER: Gaps caught in Step 14, flow fixed in Step 12 stations
```

### Step 17: Depth Pass (P2 + P3)
```
EXECUTE:
├─ Add evidence for claims that escaped Step 14
├─ Balance perspective if still single-lens
└─ Time: 10-15 min (not 20-25+)

OUTPUT: 88-92% quality
WHY LIGHTER: Evidence embedded upstream, USC provided alternatives
```

### Step 18: Final Enrichment (P5 + P6 + Compress)
```
EXECUTE:
├─ Spot-check patterns for historical validation
├─ Verify user goal achievable from output
├─ MLDoE compression pass (remove redundancy)
└─ Time: 5-10 min

OUTPUT: 95-99% quality
```

---

## PHASE E: OUTPUT (Step 19)

### Step 19: Output Format Selection + Delivery

```
┌─────────────────────────────────────────────────────────────┐
│  OUTPUT FORMAT IS DETERMINED BY NEXT ACTION                 │
│  (Decided during silent analysis, NOT at end)               │
└─────────────────────────────────────────────────────────────┘

OUTPUT FORMAT ROUTING:

IF another_iteration_planned:
  └─ FORMAT: MLDoE-ENRICH
     ├─ Optimized for AI continuation
     ├─ Preserve all 6 priority layers
     ├─ Entity density: 0.15 target
     └─ Expert handoff metadata intact

IF saving_to_memory OR context_≥80%:
  └─ FORMAT: KTG-MEM (Context Extension Protocol)
     ├─ Optimized for session restoration
     ├─ 4-layer PDL compression
     ├─ Mission manifest preserved
     ├─ Technique effectiveness map
     └─ Zero-discontinuity restoration target

IF output_for_human:
  └─ FORMAT: Narrative-focused Chain of Density (CoD)
     ├─ Optimized for human reading
     ├─ Natural prose, not structured data
     ├─ 5-iteration compression (entity-sparse → crystallized)
     ├─ Maintain readability over density
     └─ Same length, 5x information quality

TRIGGERS:
├─ "save this" | "compress" | "memory" → KTG-MEM
├─ "continue" | "iterate" | "next pass" → MLDoE-ENRICH
├─ [default/human consumption] → Narrative CoD
└─ context ≥80% → Auto-trigger KTG-MEM warning
```

### Delivery Contract
```
DELIVER:
├─ Output in selected format
├─ Audit trail (where each P1-P6 was embedded)
├─ Success criteria verification
└─ Confidence score with gate-based calculation

ARTIFACT: final_audit
FORMAT:
  Mission: [achieved/partial/failed]
  Gates: P1[✓] P2[✓] P3[✓] P4[✓] P5[✓] P6[✓]
  Output Format: [MLDoE-ENRICH | KTG-MEM | Narrative-CoD]
  Confidence: [X]/100
  Quality journey: 75%→85%→92%→97%
```

---

## CRITICAL ENFORCEMENT SUMMARY

| Step | Gate Type | Artifact Required | Skip Consequence |
|------|-----------|-------------------|------------------|
| 1 | HARD | mission_manifest | HALT |
| 3 | HARD | R/K/Q/D scores | HALT |
| 4 | HARD | anti_lazy_confirm | HALT |
| 5 | HARD | success_criteria | HALT |
| **12** | **CRITICAL** | **skeletrain/graph** | **HALT + RETRY** |
| 13 | SOFT | gate_prediction | Warning only |
| 15 | HARD | cove_verification | Rework loop |
| 19 | HARD | final_audit | Incomplete delivery |

---

## MODULE REFERENCE (Condensed)

### ARQ (Attentive Reasoning Queries)
**What:** Structured queries > free-form CoT. Forces explicit domain attention.
**When:** Pre-turn, during (DELIBERATE+), post-turn verification.
**How:** Expert asks "What defines quality in MY domain?" before executing.
**Gate:** ≥0.9 confidence required for handoff.

### Skeletrain (Skeletrain of Thought)
**What:** Outline structure before content generation.
**When:** ANALYTICAL (light), DELIBERATE (full), MAXIMUM (GoT).
**How:** Output visible skeletrain artifact with nodes + flow.
**Gate:** No skeletrain = no execution. Period.

### USC (Universal Self-Consistency)
**What:** Multiple candidates, select best via consistency.
**When:** QUICK (1-path), ANALYTICAL (2), DELIBERATE (3), MAXIMUM (5+meta).
**How:** Generate alternatives, compare, synthesize.

### MR.RUG (Mixture of Reasoning + Reliability-Aware RAG + Graph)
**What:** Expert deployment → Knowledge retrieval with ARQ → Graph construction → Semantic embedding.

**The 5 Components:**
```
M - Mixture of Reasoning Experts
    Deploy specialists based on mode:
    QUICK: 0 | ANALYTICAL: 3 | DELIBERATE: 5 | MAXIMUM: 5-20
    Each expert has: Domain, ARQ Standards, Success Metric

R - Role Assignment  
    Map experts to task components
    Define handoff dependencies (who feeds who)
    Baton (sequential) or Swarm (parallel) execution

R - Reliability-Aware RAG
    Each expert searches THEIR domain independently
    ARQ filter during collection: "What defines quality in MY domain?"
    Score sources 0-10, threshold ≥7 to include
    Build mini-graph per expert

U - Update (Graph Merge)
    Combine expert mini-graphs into unified knowledge graph
    Resolve conflicts (cite sources, find consensus)
    Strengthen agreements, fill gaps
    Cross-domain edges emerge here

G - Generate & Embody
    Experts internalize merged graph as "working memory"
    Pattern extraction for reuse (→BoT if R≥6)
    ARQ quality gates armed for execution
    Experts now reason graph-natively
```

**Expert Archetypes:**
```
Technical: Architect, Implementer, Security, Performance, DevOps
Analytical: Domain Analyst, Researcher, Data Scientist, Strategic Advisor
Creative: Creative Director, Executor, Editor, Audience Expert
Cross-Domain: Integration Architect, Translation Specialist, Synthesis Expert
```

**Quality Impact:** Without MR.RUG: 6-7/10 | With MR.RUG: 8-9/10 (+2 points)

### Prompt Bombs
**What:** Pre-planted context at predicted problem points.
**When:** ANALYTICAL (clarifier+scaffold), DELIBERATE+ (full arsenal).
**How:** Identify where gaps/depth/flow will fail, plant fixes upstream.

### CoVE (Chain of Verification)
**What:** Multi-variant verification against quality gates.
**When:** ANALYTICAL (top-1), DELIBERATE (top-2), MAXIMUM (all ≥4).
**How:** Check P1-P6 thresholds, trigger rework if fail.

### Anti-Lazy Protocol
**What:** Explicit commitment to not skip quality steps.
**When:** ANALYTICAL+ (always engaged).
**How:** Confirm mandates before proceeding.

### MLDoE-ENRICH (Multi-Layer Density of Experts)
**What:** 6-priority enrichment system for quality elevation.
**Priorities:** P1:Gaps → P2:Depth → P3:Perspective → P4:Flow → P5:History → P6:Mission
**Modes:** QUICK (P1+P4, 80-85%), STANDARD (P1-4, 92-95%), DEEP (P1-6, 97-99%)
**When:** Pass 2-3 enrichment cycles after baseline generation.
**Output Use:** Format for AI continuation (preserves expert metadata).

### KTG-MEM (Context Extension Protocol)
**What:** Session preservation for same-model restoration.
**Layers:** Knowledge → Relational → Contextual → Meta-cognitive (PDL 4-layer)
**Target:** 0.15 entity/token density, zero discontinuity on restore.
**When:** Context ≥80%, user says "save", session handoff needed.
**Output Use:** Format for memory/restoration (AI-optimized, not human-readable).

### Narrative Chain of Density (CoD)
**What:** 5-iteration compression for human consumption.
**Process:** Entity-sparse → densified → synthesized → crystallized → polished.
**Target:** Same length, 5x information quality.
**When:** Final output for human reading (default).
**Output Use:** Format for humans (natural prose, readable flow).

---

## QUICK REFERENCE: MODE → TECHNIQUE MATRIX

```
           │ ARQ │ Skeletrain │ USC │ MR.RUG │ Bombs │ CoVE │
───────────┼─────┼──────────┼─────┼────────┼───────┼──────┤
QUICK      │  O  │    X     │  1  │   O    │   O   │  X   │
ANALYTICAL │  R  │  LIGHT   │  2  │   R    │   R   │  1   │
DELIBERATE │ R+  │  FULL    │  3  │   R    │  R+   │  2   │
MAXIMUM    │ R++ │  GoT     │  5  │  R+    │  R++  │ ALL  │
```

Legend: X=Off, O=Optional, R=Required, R+=Required+Enhanced

---

## ENFORCEMENT SCRIPT (For Prompt Injection)

```
BEFORE STEP 14 EXECUTION, VERIFY:
□ Step 1 mission_manifest exists
□ Step 3 R/K/Q/D scores exist  
□ Step 5 success_criteria_lock exists
□ Step 12 skeletrain artifact exists ← CRITICAL

IF ANY MISSING:
  → OUTPUT: "ENFORCEMENT HALT: [missing artifact] required"
  → DO NOT PROCEED TO STEP 14
  → RETRY FROM MISSING STEP

SKELETON VALIDATION:
  ANALYTICAL: ≥3 nodes with purposes
  DELIBERATE: ≥5 nodes with quality stations
  MAXIMUM: Graph structure with relationships

IF SKELETON INVALID:
  → OUTPUT: "SKELETON INSUFFICIENT: [reason]"
  → RETRY STEP 12
  → MAX 2 RETRIES, THEN ESCALATE MODE
```

---

## VERSION

**KTG v29+ HARDENED**
- Restored discrete enforcement gates
- Step 12 skeletrain now CRITICAL HARD GATE
- S2A trimmed for model comprehension
- Backward compatible with v28 technique-gate

**Change from v29+:**
- "Continuous embedding" → "Discrete checkpoints with artifacts"
- "Quality stations" → "Explicit skeletrain with quality annotations"
- "Prevention architecture" → "Prevention + enforcement"
