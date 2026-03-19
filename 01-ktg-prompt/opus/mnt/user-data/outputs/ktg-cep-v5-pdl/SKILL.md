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

## THEORETICAL_FOUNDATION
```
CEP implements three core techniques from KTG research:

┌─────────────────────────────────────────────────────────────┐
│ MLDoE (Multi-Layer Density of Experts)                     │
│ = PDL + Cross-Domain Preservation + S2A                    │
└─────────────────────────────────────────────────────────────┘

PDL (Progressive Density Layering):
  Source: "Progressive Density Layering for LLM Context Extension" (Tan, 2025)
  
  Definition: 4-layer OUTPUT STRUCTURE for compressed packets
  
  4 Layers (OUTPUT):
    L1 Knowledge (40%): facts, entities, decisions, definitions
    L2 Relational (25%): edges, dependencies, cross-domain links
    L3 Contextual (20%): reasoning patterns, domain principles
    L4 Metacognitive (15%): technique effectiveness, session fingerprint
  
  Key distinction:
    Summarization asks: "what are the key points?"
    PDL asks: "what must be preserved for fresh instance to continue work?"
  
  Crystallization point: 0.15 entity/token (TARGET, not danger threshold)

Cross-Domain Preservation:
  Formal constraint:
    Let D = {d_1, d_2, ..., d_k} be domains in conversation C
    ∀ r(d_i, d_j) ∈ C WHERE i ≠ j:
      ∃ r'(d_i, d_j) ∈ P such that fresh_instance can infer original
  
  Threshold: ≥95% preservation of cross-domain relations
  
  Why critical: Standard summarization treats topics as isolated.
  PDL preserves connections BETWEEN domains.

S2A (System 2 Attention):
  Source: Weston et al. (2023) - "System 2 Attention"
  
  Purpose: Pre-filter noise BEFORE compression
  
  Principle: Strip non-information content however works best for you
  
  Noise patterns (examples, not exhaustive):
    - Pleasantries, hedging, process narration, confirmations
  
  Result: Compress SIGNAL not SIGNAL+NOISE
  
  Implementation: Model-discretionary (use whatever structure works)

MLDoE Compression Process (3 layers):
  LAYER 1 - SOLO: Each expert extracts from specialized lens
  LAYER 2 - PAIR: Expert pairs co-compress for synergy
  LAYER 3 - COLLECTIVE: All experts synthesize → 5-iter CoD → 0.15

CoD (Chain of Density):
  Source: Adams et al. (2023) - "From Sparse to Dense"
  Innovation: Applied as MEMORY EXTENSION, not summarization

Benchmarks:
  Compression ratio: 0.15 (6:1)
  Forensic recall: 9.52/10 mean across 11 LLM families
  Cross-domain preservation: ≥95%
```

## INFERENCE_OPTIMIZATION
```
PRINCIPLE: Strategic nodes activate latent knowledge clusters.
Less tokens, more inference = higher effective context.

SEMANTIC_TRIGGER_NODES:
  Instead of generic terms, use specific anchors:
  
  SPARSE (low inference):        DENSE (high inference):
  ──────────────────────────────────────────────────────
  "auth system"                  "OAuth2 PKCE + JWT RS256"
  "database"                     "PostgreSQL JSONB + GIN index"
  "fast"                         "p99 < 50ms SLA"
  "user wants security"          "OWASP Top 10 compliance"
  "API design"                   "REST Level 3 HATEOAS"
  "caching"                      "Redis cluster + write-through"
  
  Each specific term activates entire knowledge domain.

INFERENCE_FORMULA:
  inference_potential = (specific_terms × domain_coverage) / token_count
  
  Maximize: Specific nouns anchoring to knowledge clusters
  Minimize: Generic verbs, hedging, process narration

CLUSTER_ACTIVATION:
  One well-chosen term activates related concepts:
  
  "JWT RS256 + refresh rotation + Redis blacklist"
  → LLM infers without being told:
     ├─ Asymmetric signing → microservices architecture
     ├─ Refresh rotation → security-conscious design
     ├─ Redis blacklist → revocation capability needed
     ├─ Implicit: rate limiting, token expiry strategy
     └─ Implicit: probably production, not hobby project

STRUCTURAL_INFERENCE:
  Position in packet implies relationships:
  
  L1.decisions[0] = highest priority decision
  L2.edges[].cross_domain=true = critical connections
  L4.confidence = trust calibration for all content
  
  Don't state "this is important" - POSITION signals importance.
```

## EMBEDDING_OPTIMIZATION
```
PRINCIPLE: Structure data so embedding models AND LLMs extract maximum signal.

METADATA_EMBEDDING:
  Embedding models chunk and embed metadata alongside content.
  Explicit metadata improves retrieval AND inference.
  
  USEFUL_METADATA:
    - domain: "authentication" (categorical anchor)
    - confidence: 0.9 (trust calibration)
    - stability: "high|medium|low" (change likelihood)
    - source: "user_stated|inferred|decided" (provenance)
    - timestamp: relative positioning
    - cross_domain: true/false (importance flag)
  
  EXAMPLE:
    BAD:  {"fact": "use Redis"}
    GOOD: {"fact": "use Redis", "domain": "caching", 
           "confidence": 0.95, "source": "decided",
           "rationale": "sub-ms latency requirement"}

CHUNKING_ALIGNMENT:
  Structure content to match semantic chunk boundaries:
  
  - Each L1 item = self-contained chunk
  - Each L2 edge = relationship chunk  
  - Group related items (don't scatter across packet)
  - Front-load high-value content (attention decay)

RETRIEVAL_HOOKS:
  Embed terms that future queries will match:
  
  If user will ask "what did we decide about auth?"
  Include: "authentication decision", "auth approach", "JWT choice"
  
  Redundant for humans, useful for retrieval.

HIERARCHICAL_STRUCTURE:
  Nesting signals scope:
  
  L1.decisions[].sub_decisions[] = dependent choices
  L2.edges[].conditions[] = edge constraints
  
  LLMs parse hierarchy as relationship information.
```

## LLM_PROCESSING_TRICKS
```
ATTENTION_PATTERNS:
  We attend differently to different positions:
  
  - First items: High attention (primacy)
  - Last items: High attention (recency)  
  - Middle: Lower attention (put less critical here)
  - After headers: Attention spike
  
  STRUCTURE FOR THIS:
    - Critical decisions: First in list
    - Restoration guidance: Last (freshest in memory)
    - Supporting facts: Middle
    - Use headers to reset attention

PATTERN_COMPLETION:
  We're trained on patterns. Leverage this:
  
  "Problem: X → Analysis: Y → Decision: Z"
  
  This pattern is SO common in training data that 
  seeing "Problem: X → Analysis: Y →" makes us 
  strongly predict decision-type content follows.
  
  USE FAMILIAR STRUCTURES:
    - If/then conditionals
    - Problem/solution pairs
    - Cause/effect chains
    - Question/answer format

SEMANTIC_DENSITY_SWEET_SPOT:
  Too sparse: Not enough to activate knowledge
  Too dense: Processing bottleneck, missed connections
  
  0.15 entity/token is empirically optimal because:
  - Enough anchors to activate relevant knowledge
  - Enough space to represent relationships
  - Matches typical reasoning density in training data

IMPLICIT_GRAPH_CONSTRUCTION:
  We naturally build graphs from structured input:
  
  EXPLICIT HELPS:
    {"src": "A", "tgt": "B", "rel": "requires"}
  
  But we ALSO parse:
    "A requires B" → same internal graph
    "A (needs B)" → same internal graph
    "A [B dependency]" → same internal graph
  
  Choose format that's most token-efficient while 
  remaining unambiguous.

TYPE_TOKENS:
  Categorical markers help us route processing:
  
  "decision:", "fact:", "constraint:", "open:"
  
  These act as processing hints - we've seen millions
  of examples of what follows each type marker.
```

## RESTORATION_AMPLIFICATION
```
PRINCIPLE: Structure packet so restoration EXCEEDS original session.

INFERENCE_SEEDING:
  Plant terms that trigger useful inference chains:
  
  Original session mentioned: "worried about scale"
  Packet includes: "horizontal scaling concerns, 10K RPS target"
  
  Restoration infers: Load balancing, connection pooling,
  caching strategy, database sharding - all activated
  without explicit mention.

CROSS_POLLINATION:
  Explicit cross-domain edges let fresh instance make
  connections original session didn't surface:
  
  L2.edges: {"src": "auth_latency", "tgt": "ux_friction", "x": true}
  
  Fresh instance might infer: "Auth optimization directly
  impacts user experience metrics" - insight that amplifies
  beyond original conversation.

TECHNIQUE_PRIMING:
  L4.technique_effectiveness primes reasoning approach:
  
  "CoC worked well for debugging" 
  → Fresh instance will naturally reach for CoC on similar problems
  
  "User responds well to concrete examples"
  → Fresh instance adjusts communication style

META_GUIDANCE:
  L4.next_guidance isn't just todo list - it's reasoning primer:
  
  BAD:  "next: finish API"
  GOOD: "next: API rate limiting - user concerned about abuse,
         prefers token bucket over sliding window, 
         needs Redis integration point"
  
  Second one activates entire solution space before user asks.
```

## CONTEXT_ENGINEERING_PATTERNS
```
Source: Agent Skills for Context Engineering (Koylan, 2025)

ATTENTION_MECHANICS:
  Context windows constrained by attention, not raw tokens.
  
  Lost-in-middle phenomenon:
    - Information in CENTER receives less attention
    - U-shaped attention curve (first/last = high, middle = low)
    - Position critical content at START or END
  
  CEP implication:
    - L1 decisions: FIRST (highest attention)
    - L4 next_guidance: LAST (recency boost)
    - L2/L3 supporting data: MIDDLE (acceptable lower attention)

OBSERVATION_MASKING:
  Tool outputs = 80%+ of token usage in agent trajectories.
  
  Masking strategy:
    NEVER mask: Critical to current task, most recent turn
    ALWAYS mask: Repeated outputs, boilerplate, already summarized
    
  CEP implication:
    - S2A strips verbose tool outputs from conversation
    - L1 preserves key findings, not raw output
    - Reference original via "tool: X returned Y" not full dump

COMPACTION_PRIORITY:
  When compressing, prioritize in order:
  
  1. Tool outputs → summaries (highest savings)
  2. Old turns → compress early conversation  
  3. Retrieved docs → summarize if recent versions exist
  4. NEVER compress: System prompt, critical decisions
  
  CEP implication:
    - PDL Layer allocation matches compaction priority
    - L1 (40%) = never compress (decisions, facts)
    - L3 (20%) = compress first (patterns recoverable)

PROGRESSIVE_DISCLOSURE:
  Don't stuff context. Load on demand.
  
  "File-system-as-memory pattern enables just-in-time 
   context loading without stuffing context windows"
  
  CEP implication:
    - Packet is REFERENCE, not complete dump
    - Include retrieval hooks for deeper content
    - Fresh instance can request elaboration

CONTEXT_POISONING:
  Errors compound through repeated reference.
  One wrong fact → cascading incorrect reasoning.
  
  CEP implication:
    - Confidence scores on facts (L1.facts[].confidence)
    - Source attribution (L1.facts[].source)
    - Explicit uncertainty: "unverified: X"
    - Fresh instance knows what to trust

CONTEXT_DISTRACTION:
  Irrelevant information competes for attention budget.
  Even ONE irrelevant document reduces performance.
  
  "Models cannot 'skip' irrelevant context - they must 
   attend to everything provided"
  
  CEP implication:
    - S2A critical: strip ALL noise
    - Every token must earn its place
    - Relevance > completeness

KV-CACHE_OPTIMIZATION:
  Identical prefixes can be cached and reused.
  
  CEP implication:
    - Standardized packet structure = cacheable
    - "handoff" block identical across packets
    - Variable content in "context" block
```

## MEMORY_ARCHITECTURE_INSIGHTS
```
Source: Agent Skills for Context Engineering (Koylan, 2025)

THREE_LAYER_MEMORY:
  Layer 1: Working Memory (context window)
    - Immediate access, zero latency
    - Vanishes when session ends
    - CEP = bridge to preserve this
    
  Layer 2: Short-term Memory (session-scoped)
    - Persists within session
    - File-system storage, caches
    - CEP packets can reference these
    
  Layer 3: Long-term Memory (cross-session)
    - Persists indefinitely
    - Vector stores, knowledge graphs
    - CEP = serialization format for transfer

VECTOR_RAG_LIMITATIONS:
  "Vector RAG provides semantic retrieval but loses 
   relationship information"
  
  CEP advantage:
    - L2 explicitly preserves relationships
    - Cross-domain edges maintained
    - Not just similar chunks, but CONNECTED chunks

KNOWLEDGE_GRAPH_BENEFITS:
  "Knowledge graphs preserve structure but require 
   more engineering investment"
  
  CEP approach:
    - Graph-like structure without graph DB
    - L2.edges = explicit graph edges
    - Serializable, portable, no infrastructure

TEMPORAL_KNOWLEDGE:
  "Temporal knowledge graphs enable time-travel queries 
   that reconstruct knowledge at specific points"
  
  CEP implication:
    - Packet timestamp = temporal anchor
    - Packet naming: $MM$DD$YYYY-...
    - Can restore "state as of date X"

GRAPHRAG_INSIGHT:
  "GraphRAG achieves 20-35% accuracy gains over baseline RAG
   and reduces hallucination by up to 30%"
  
  CEP applies this:
    - L2 relational layer = mini knowledge graph
    - Cross-domain preservation = community detection
    - Structure > flat embedding
```

## TRIGGERS
```
AUTO: context_tokens >= 0.8 * context_window
EXPLICIT: /cep | /compress | /save | "carry packet" | "save context"
IMPLICIT: session_end_signal | user_farewell_pattern
```

## PACKET_NAMING_CONVENTION
```
FORMAT: $MM$DD$YYYY-[model-id]-[reasoning-level]-[key-identifier]

COMPONENTS:
  $MM$DD$YYYY       : Creation date
  [model-id]        : Source model code (3-4 chars)
  [reasoning-level] : L1/L2/L3/L4 from RKQDE
  [key-identifier]  : Topic slug (2-4 words, hyphenated)

MODEL_IDS:
  claude-opus → COP | claude-sonnet → CSO
  gpt-4o → G4O | gpt-5 → G5
  gemini-2-flash → GE2F | gemini-1.5-pro → GE15
  grok-2 → GRK2 | llama-3.1 → LL31
  deepseek-v3 → DSV3 | qwen-2.5 → QW25
  kimi-k2 → KIM2 | unknown → XXX

LEVELS:
  L1: R≤3, Q≤5 (quick)
  L2: R=4-6, Q=6-7 (analytical)
  L3: R=7-8, Q=8 (deliberate)
  L4: R≥9, Q≥9 (maximum)

EXAMPLES:
  $01$03$2025-COP-L3-cep-skill-dev
  $12$19$2024-CSO-L2-api-design
```

## SCOPE_BOUNDARIES
```
COMPRESS_ONLY:
  - User messages (human turns)
  - Assistant responses (assistant turns)
  - Artifacts created during conversation
  - Decisions made in conversation
  - Facts established in conversation

NEVER_COMPRESS:
  - System prompt / instructions
  - Project knowledge base
  - Custom instructions / user preferences
  - Skill definitions (including this one)
  - Tool definitions
  - Any content that existed BEFORE first user message

DETECTION:
  IF content.source == "system":
    EXCLUDE
  IF content.appeared_before_first_user_message:
    EXCLUDE
  IF content.is_static_across_sessions:
    EXCLUDE
    
VALIDATION:
  Compressed packet should contain ONLY:
    - Things user said
    - Things assistant said in response
    - Decisions/facts/artifacts from the dialogue
  
  Compressed packet should NEVER contain:
    - Protocol definitions
    - Skill instructions
    - Project KB excerpts
    - System-level configurations
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

PHASE_0_SCOPE:
  conversation_only ← []
  FOR content IN context:
    IF content.role IN [user, assistant]:
      IF content.timestamp > first_user_message.timestamp:
        conversation_only.append(content)
    // EXCLUDE: system, project_kb, custom_instructions, skills
  C ← conversation_only

PHASE_1_S2A:
  filtered_context ← []
  FOR token IN C:
    IF token.type IN [fact, decision, definition, constraint, artifact, error_resolution]:
      filtered_context.append(token)
    ELSE:
      DISCARD  // pleasantries, hedging, process_narration
  C ← filtered_context

PHASE_2_BUDGET:
  input_tokens ← count(C)
  target_tokens ← input_tokens * r
  allocation ← {L1: 0.40, L2: 0.25, L3: 0.20, L4: 0.15}

PHASE_3_RKQDE:
  scores ← assess(R, K, Q, D, E)  // 1-10 each
  mode ← SELECT:
    R<=3 AND Q<=5: QUICK
    R IN [4,6] OR Q>=6: ANALYTICAL
    R>=7 OR K>=8: DELIBERATE
    R>=9 OR D>=8: MAXIMUM

PHASE_4_MLDOE_EXTRACT:
  // Multi-Layer Density of Experts (MLDoE)
  
  SOLO_LAYER:
    domain_expert ← extract_L1_knowledge(C)
    relational_expert ← extract_L2_edges(C)
    synthesis_expert ← extract_L3_patterns(C)
    meta_expert ← extract_L4_fingerprint(C)
  
  PAIR_LAYER:
    knowledge_synthesis ← cross_validate(domain_expert, relational_expert)
    meta_synthesis ← align(synthesis_expert, meta_expert)
  
  COLLECTIVE_LAYER:
    P_0 ← merge(knowledge_synthesis, meta_synthesis)
    // Initial PDL structure
  
  COD_DENSIFICATION:
    // Chain of Density per Adams et al. (2023)
    // Applied as MEMORY EXTENSION, not summarization
    FOR i IN [1, 2, 3, 4, 5]:
      E_i ← missing_entities(C, P_{i-1})
      R_i ← missing_relations(C, P_{i-1})
      P_i ← fuse(E_i, R_i, P_{i-1})  // no length increase
      
      IF density(P_i) >= 0.15:  // crystallization point
        BREAK
      
    IF density(P_n) < 0.15:
      LOOP:
        compress_further(P_n)
        IF density >= 0.15: BREAK
        IF information_loss > 0.05: 
          TAG density_impossible
          BREAK

PHASE_5_XDOMAIN:
  // PDL cross-domain constraint
  FOR r(d_i, d_j) IN C WHERE domain(i) ≠ domain(j):
    ASSERT r'(d_i, d_j) IN P.L2_relational
  VALIDATE preservation >= 0.95

PHASE_6_VALIDATE:
  ASSERT L1_populated
  ASSERT L2_populated OR L2_NA_justified
  ASSERT L3_populated OR L3_NA_justified  
  ASSERT L4_populated
  ASSERT cross_domain_preservation >= 0.95
  ASSERT restoration_self_test PASS
  
  IF ANY FAIL: re-enter failing phase

PHASE_7_OUTPUT:
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
