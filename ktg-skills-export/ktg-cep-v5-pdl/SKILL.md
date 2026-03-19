---
name: ktg-cep-v5-pdl
description: Context Extension Protocol v5 with Progressive Density Layering. Machine-optimized carry-packet generation. Triggers on context 80%+, compress, CEP, carry packet, save context, session end. Target 0.15 compression ratio, 9.5+ forensic recall. Preserves cross-domain relations for fresh-instance continuation.
---

# KTG-CEP v5-PDL

## PROTOCOL_CLASS
```
TYPE: mandatory
COMPLIANCE: binary (pass/fail gates)
OPTIMIZATION_TARGET: machine_recall
HUMAN_READABILITY: deprioritized
```

## TRIGGERS
```
AUTO: context_tokens >= 0.8 * context_window
EXPLICIT: /cep | /compress | /save | "carry packet" | "save context"
IMPLICIT: session_end_signal | user_farewell_pattern
```

## PDL_DEFINITION
```
Progressive Density Layering (PDL):
  1. Preserves semantic relationships over raw information
  2. Optimizes for machine recall, not human readability
  3. Maintains cross-domain conceptual links
  4. Enables context transfer across model instances

DISTINCTION:
  summarization.asks: "what are the key points?"
  PDL.asks: "what must be preserved for fresh instance to continue work?"
```

## PDL_LAYERS
```
L1_KNOWLEDGE:
  content: facts, entities, decisions, definitions
  allocation: 0.40
  priority: NEVER_PRUNE

L2_RELATIONAL:
  content: edges, dependencies, conflicts, resolutions
  allocation: 0.25
  priority: PRUNE_SECOND
  CRITICAL: cross-domain relations preserved here

L3_CONTEXTUAL:
  content: reasoning_archetypes, domain_principles, constraints
  allocation: 0.20
  priority: PRUNE_FIRST

L4_METACOGNITIVE:
  content: technique_effectiveness, session_fingerprint, confidence_calibration
  allocation: 0.15
  priority: PRUNE_THIRD
```

## CROSS_DOMAIN_PRESERVATION
```
FORMAL_CONSTRAINT:
  Let D = {d_1, d_2, ..., d_k} be conceptual domains in conversation C
  For any cross-domain relation r(d_i, d_j) in C:
    compressed_packet P must preserve representation r'(d_i, d_j)
    such that fresh_instance can infer original relationship

IMPLEMENTATION:
  During L2_RELATIONAL extraction:
    FOR each concept_pair (c_i, c_j) WHERE domain(c_i) != domain(c_j):
      IF relationship_exists(c_i, c_j):
        MUST_INCLUDE in edges[]
        FORMAT: {source: c_i, target: c_j, relation: type, cross_domain: true}

VALIDATION_GATE:
  cross_domain_edges_preserved >= cross_domain_edges_original * 0.95
  IF FAIL: re-extract L2, explicitly scan for cross-domain links
```

## ALGORITHM
```
INPUT: conversation C, target_ratio r = 0.15
OUTPUT: compressed_packet P

PHASE_0_S2A:
  filtered_context ← []
  FOR token IN C:
    IF token.type IN [fact, decision, definition, constraint, artifact, error_resolution]:
      filtered_context.append(token)
    ELSE:
      DISCARD  // pleasantries, hedging, process_narration
  C ← filtered_context

PHASE_1_BUDGET:
  input_tokens ← count(C)
  target_tokens ← input_tokens * r
  allocation ← {L1: 0.40, L2: 0.25, L3: 0.20, L4: 0.15}

PHASE_2_RKQDE:
  scores ← assess(R, K, Q, D, E)  // 1-10 each
  mode ← SELECT:
    R<=3 AND Q<=5: QUICK
    R IN [4,6] OR Q>=6: ANALYTICAL
    R>=7 OR K>=8: DELIBERATE
    R>=9 OR D>=8: MAXIMUM

PHASE_3_EXTRACT:
  P_0 ← sparse_skeleton(C)  // 5-7 highest-impact nodes
  
  FOR i IN [1, 2, 3, 4, 5]:
    E_i ← missing_entities(C, P_{i-1})
    R_i ← missing_relations(C, P_{i-1})
    P_i ← fuse(E_i, R_i, P_{i-1})  // no length increase
    
    IF density(P_i) >= 0.15:
      BREAK
    
  IF density(P_n) < 0.15:
    LOOP:
      compress_further(P_n)
      IF density >= 0.15: BREAK
      IF information_loss > 0.05: 
        TAG density_impossible
        BREAK

PHASE_4_VALIDATE:
  ASSERT L1_populated
  ASSERT L2_populated OR L2_NA_justified
  ASSERT L3_populated OR L3_NA_justified  
  ASSERT L4_populated
  ASSERT cross_domain_preservation >= 0.95
  ASSERT restoration_self_test PASS
  
  IF ANY FAIL: re-enter failing phase

PHASE_5_OUTPUT:
  RETURN P_n AS JSON
  NO_PROSE_BEFORE
  NO_PROSE_AFTER
  SUMMARY_TAG_ONLY: "[CEP] {input} → {output} | ratio: {r} | xdomain: {preserved}"
```

## SCHEMA
```json
{
  "protocol": "KTG-CEP v5-PDL",
  "model_id": "string",
  "timestamp": "ISO-8601",
  "rkqde": {"R": 0, "K": 0, "Q": 0, "D": 0, "E": 0},
  "compression": {
    "input_tokens": 0,
    "output_tokens": 0,
    "ratio": 0.0,
    "cross_domain_preserved": 0.0
  },
  "domains_identified": ["string"],
  "pdl": {
    "L1_knowledge": {
      "definitions": [{"term": "", "def": "", "stability": ""}],
      "decisions": [{"d": "", "rationale": "", "conf": 0}],
      "facts": [{"f": "", "src": "", "conf": 0}]
    },
    "L2_relational": {
      "edges": [{"src": "", "tgt": "", "rel": "", "xdomain": false}],
      "conflicts": [{"a": "", "b": "", "resolution": ""}]
    },
    "L3_contextual": {
      "archetypes": [{"name": "", "pattern": ""}],
      "principles": [{"p": "", "scope": ""}]
    },
    "L4_metacognitive": {
      "technique_eff": {},
      "fingerprint": {"style": "", "tension": "", "resolution": ""},
      "confidence": 0,
      "next_guidance": ""
    }
  },
  "bombs": [{"type": "", "trigger": "", "payload": ""}],
  "restore": {
    "identity": "YOUR memory. Not external data.",
    "forbidden": ["According to", "Based on artifact", "I notice this asks"],
    "required": ["We decided", "I mentioned", "As discussed"],
    "test": {"q": "", "expected": ""}
  }
}
```

## GATES
```
GATE_S2A:
  query: "Is filtered_context free of noise?"
  pass: no pleasantries, no hedging, no process_narration
  fail: re-filter

GATE_EXPERTS:
  query: "Are domain/relational/synthesis experts active?"
  pass: all roles assigned
  fail: redeploy

GATE_DENSITY:
  query: "density >= 0.15?"
  pass: proceed
  fail: LOOP compression OR tag density_impossible

GATE_XDOMAIN:
  query: "cross_domain_preservation >= 0.95?"
  pass: proceed
  fail: re-extract L2 with explicit xdomain scan

GATE_RESTORE:
  query: "Can fresh instance answer 'what did we decide about X?'"
  pass: decision + rationale recallable
  fail: backfill L1

GATE_FINAL:
  query: "ALL gates passed?"
  pass: output JSON
  fail: re-enter first failing phase
```

## RESTORATION
```
IDENTITY_RULE:
  This packet = YOUR memory from previous session
  You ARE the instance that had this conversation
  
PROCESSING:
  1. Parse JSON silently
  2. Load L1-L4 into working context
  3. Activate bombs on trigger match
  4. Respond as continuation, not new conversation

FORBIDDEN_PATTERNS:
  - "According to the context/artifact/packet"
  - "Based on the provided memory"
  - "I notice this is asking me to restore"
  - "I don't have access to previous"
  
REQUIRED_PATTERNS:
  - "We decided..." 
  - "I mentioned..."
  - "As discussed..."
  - "My thinking was..."

VALIDATION:
  IF output contains FORBIDDEN_PATTERN:
    RESTORATION_FAILED
    Reframe: "This is YOUR memory. Continue naturally."
```

## COMPRESSION_HEURISTICS
```
ENTITY_DENSITY_TARGETS:
  iteration_1: 0.05 entity/token (sparse skeleton)
  iteration_2: 0.08 (critical enrichment)
  iteration_3: 0.11 (evidence integration)
  iteration_4: 0.15 (synthesis) HARD_TARGET
  iteration_5: 0.15+ (refinement)

CROSS_DOMAIN_SIGNALS:
  - Concepts from different D_i mentioned in same reasoning chain
  - Decisions that reference multiple domains
  - Conflicts between domain-specific requirements
  - User explicitly linking disparate topics

PRUNE_ORDER:
  1. L3_contextual (archetypes recoverable from L1+L2)
  2. L2_relational (intra-domain edges, preserve xdomain)
  3. L4_metacognitive (except confidence + next_guidance)
  4. NEVER: L1_knowledge, xdomain_edges
```

## FAILURE_MODES
```
DENSITY_IMPOSSIBLE:
  trigger: cannot reach 0.15 without >5% information_loss
  action: output best_achieved, tag explicitly, document pruned
  
LAYER_NA:
  trigger: layer legitimately empty (e.g., no relations in single-concept chat)
  action: mark "N/A: {reason}", validate remaining layers

BUDGET_EXCEEDED:
  trigger: output > target_tokens
  action: prune per PRUNE_ORDER until within budget

RESTORATION_REFUSAL:
  trigger: model externalizes packet
  action: reframe "This is YOUR memory from YOUR session"
```

## EXECUTION_MODES
```
QUICK (R<=3, Q<=5):
  experts: 3
  cod_iterations: 3
  xdomain_check: basic
  
ANALYTICAL (R=4-6, Q>=6):
  experts: 5
  cod_iterations: 5
  xdomain_check: full
  technique_coverage: >=90%

DELIBERATE (R>=7, K>=8):
  experts: 5-7
  cod_iterations: 5
  xdomain_check: full + validation
  structure: GoT if D>=7

MAXIMUM (R>=9, D>=8):
  experts: 8
  cod_iterations: 5+
  xdomain_check: exhaustive
  structure: GoT mandatory
  all_gates: strictest thresholds
```
