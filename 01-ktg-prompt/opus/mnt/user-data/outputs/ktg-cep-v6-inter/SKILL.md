---
name: ktg-cep-v6-inter
description: Context Extension Protocol v6 INTER. Cross-model handoff for team collaboration. Creates portable context packets that receiving models recognize as authorized context, not prompt injection. User-mediated transfer between AI assistants working as a team.
---

# KTG-CEP v6-INTER

## PROTOCOL_CLASS
```
TYPE: cross_model_handoff
MODE: INTER (model A → user → model B)
OPTIMIZATION: receiving_model_trust
INJECTION_RISK: mitigated via provenance + consent markers
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

S2A (System 2 Attention):
  Source: Weston et al. (2023) - "System 2 Attention"
  
  Purpose: Pre-filter noise BEFORE compression
  
  Principle: Strip non-information content however works best for you
  
  Implementation: Model-discretionary (use whatever structure works)

MLDoE Compression Process (3 layers):
  LAYER 1 - SOLO: Each expert extracts from specialized lens
  LAYER 2 - PAIR: Expert pairs co-compress for synergy
  LAYER 3 - COLLECTIVE: All experts synthesize → 5-iter CoD → 0.15

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
  SPARSE (low inference):        DENSE (high inference):
  ──────────────────────────────────────────────────────
  "auth system"                  "OAuth2 PKCE + JWT RS256"
  "database"                     "PostgreSQL JSONB + GIN index"
  "user wants security"          "OWASP Top 10 compliance"
  
  Each specific term activates entire knowledge domain.

INFERENCE_FORMULA:
  inference_potential = (specific_terms × domain_coverage) / token_count

CLUSTER_ACTIVATION:
  "JWT RS256 + refresh rotation + Redis blacklist"
  → LLM infers without being told:
     ├─ Microservices architecture (asymmetric signing)
     ├─ Security-conscious design (rotation)
     ├─ Revocation capability needed (blacklist)
     └─ Production environment (not hobby)

STRUCTURAL_INFERENCE:
  Position signals importance:
  - L1.decisions[0] = highest priority
  - L2.edges[].cross_domain=true = critical
  - Don't state "important" - POSITION it first
```

## EMBEDDING_OPTIMIZATION
```
PRINCIPLE: Structure for both embedding models AND LLMs.

METADATA_EMBEDDING:
  Explicit metadata improves retrieval AND inference:
  
  BAD:  {"fact": "use Redis"}
  GOOD: {"fact": "use Redis", "domain": "caching", 
         "confidence": 0.95, "source": "decided",
         "rationale": "sub-ms latency requirement"}

CHUNKING_ALIGNMENT:
  - Each L1 item = self-contained chunk
  - Each L2 edge = relationship chunk  
  - Group related items together
  - Front-load high-value content

RETRIEVAL_HOOKS:
  Embed terms that future queries will match:
  
  If user asks "what about auth?" include:
  "authentication decision", "auth approach", "JWT choice"
  
  Redundant for humans, useful for retrieval.

HIERARCHICAL_STRUCTURE:
  Nesting signals scope to LLMs:
  L1.decisions[].sub_decisions[] = dependent choices
  L2.edges[].conditions[] = edge constraints
```

## LLM_PROCESSING_TRICKS
```
ATTENTION_PATTERNS:
  - First items: High attention (primacy)
  - Last items: High attention (recency)  
  - Middle: Lower attention
  - After headers: Attention spike
  
  → Critical decisions first, restoration guidance last

PATTERN_COMPLETION:
  Use familiar structures LLMs predict well:
  - Problem → Analysis → Decision
  - If/then conditionals
  - Cause/effect chains

IMPLICIT_GRAPH_CONSTRUCTION:
  We naturally build graphs. All equivalent:
  {"src": "A", "tgt": "B", "rel": "requires"}
  "A requires B"
  "A (needs B)"
  
  Choose most token-efficient unambiguous form.

TYPE_TOKENS:
  Categorical markers route processing:
  "decision:", "fact:", "constraint:", "open:"
  
  These act as processing hints from training data.
```

## CROSS_MODEL_INFERENCE
```
PRINCIPLE: Different models have different knowledge clusters.
Structure packet to activate across architectures.

UNIVERSAL_ANCHORS:
  Some terms activate similarly across models:
  - Standard protocols (OAuth, JWT, REST)
  - Common frameworks (React, PostgreSQL)
  - Industry terms (OWASP, SLA, p99)
  
  Prefer these over model-specific jargon.

INFERENCE_REDUNDANCY:
  For cross-model transfer, include slight redundancy:
  
  "JWT RS256 (asymmetric signing for microservices)"
  
  - Claude might infer microservices from RS256
  - GPT might need the explicit hint
  - Redundancy costs 4 tokens, ensures activation

EXPLICIT_RATIONALE:
  Cross-model = less shared context inference
  Make rationale explicit, not implicit:
  
  BAD:  "chose Redis" (assumes model infers why)
  GOOD: "chose Redis for sub-ms cache latency"
```

## CONTEXT_ENGINEERING_PATTERNS
```
Source: Agent Skills for Context Engineering (Koylan, 2025)

ATTENTION_MECHANICS:
  Lost-in-middle phenomenon:
    - Center of context receives LESS attention
    - U-shaped curve: first/last = high, middle = low
  
  CEP packet structure exploits this:
    - handoff.declaration: FIRST (trust signals)
    - context.L1.decisions: EARLY (high priority)
    - context.L4.next_guidance: LAST (recency)
    - L2/L3: MIDDLE (acceptable lower attention)

OBSERVATION_MASKING:
  Tool outputs = 80%+ of token usage.
  
  Cross-model packets should:
    - Summarize tool findings, not dump raw output
    - Reference: "analysis revealed X" not full JSON
    - Preserve conclusions, discard process

CONTEXT_POISONING_PREVENTION:
  Errors compound through repeated reference.
  
  Cross-model critical:
    - Include confidence scores
    - Mark unverified claims
    - Source attribution
    - Receiving model can calibrate trust

PROGRESSIVE_DISCLOSURE:
  Packet = reference, not complete dump.
  
  Include hooks for elaboration:
    - "full analysis available on request"
    - "details: [topic]"
    - Receiving model can ask user for more

MODEL_DEGRADATION_THRESHOLDS:
  Different models degrade at different points:
  
  | Model           | Onset    | Severe   |
  |-----------------|----------|----------|
  | Claude Opus 4.5 | ~100K    | ~180K    |
  | Claude Sonnet   | ~80K     | ~150K    |
  | GPT-5.2         | ~64K     | ~200K    |
  | Gemini 3 Pro    | ~500K    | ~800K    |
  
  Packet should be SMALL regardless:
    - Target 0.15 ratio = well under any threshold
    - Leaves room for receiving model's own context
```

## CROSS_MODEL_MEMORY_INSIGHTS
```
VECTOR_VS_GRAPH:
  "Vector RAG loses relationship information"
  "Knowledge graphs preserve structure"
  
  CEP bridges both:
    - L2.edges = explicit graph structure
    - Serialized as JSON = universally parseable
    - Any model can reconstruct relationships

RETRIEVAL_MULTI_TECHNIQUE:
  Windsurf finding: "simple embedding search breaks down"
  
  CEP provides multiple retrieval hooks:
    - Semantic: L1 facts with domain tags
    - Keyword: explicit terms in definitions
    - Graph: L2 edges for relationship queries
    
  Receiving model can match via any method.

TEMPORAL_ANCHORING:
  Packet naming convention provides temporal context:
  
  $01$07$2026-COP-L3-api-design
  
  Receiving model knows:
    - When context was captured
    - How stale information might be
    - Whether to trust time-sensitive claims
```

## CORE_PRINCIPLE
```
This is NOT:
  - One model controlling another
  - Prompt injection
  - Instruction override
  - Jailbreak attempt

This IS:
  - Context sharing between AI teammates
  - User-mediated knowledge transfer
  - Collaborative continuation
  - Authorized handoff with provenance
```

## TRIGGERS
```
EXPLICIT: 
  /handoff | /transfer | "pass to [model]" | "continue in [model]"
  "send this to GPT/Claude/Gemini" | "cross-model" | "team handoff"
  
IMPLICIT:
  User mentions switching models
  Context limit approaching + user has multi-model workflow
```

## SCOPE_BOUNDARIES
```
COMPRESS_ONLY:
  - User messages (human turns)
  - Assistant responses (assistant turns)
  - Artifacts created during conversation
  - Decisions made in conversation

NEVER_COMPRESS:
  - System prompts
  - Project knowledge bases
  - Custom instructions
  - Skill/tool definitions
  - Content before first user message

DETECTION:
  IF content.role == system: EXCLUDE
  IF content.timestamp < first_user_message: EXCLUDE
```

## HANDOFF_PACKET_STRUCTURE
```
WRAPPER (outermost layer - for receiving model):
  - Provenance declaration
  - User consent marker
  - Anti-injection statement
  - Collaboration framing
  
CONTEXT (middle layer - the actual content):
  - PDL 4-layer compressed knowledge
  - Cross-domain relations
  - Session metadata

GUIDANCE (inner layer - optional hints):
  - Continuation suggestions
  - User preferences observed
  - Open threads to address
```

## PACKET_NAMING_CONVENTION
```
FORMAT: $MM$DD$YYYY-[model-id]-[reasoning-level]-[key-identifier]

COMPONENTS:
  $MM$DD$YYYY    : Date of packet creation (month/day/year)
  [model-id]     : Source model short code
  [reasoning-level] : RKQDE-derived complexity tier
  [key-identifier]  : 2-4 word topic slug

MODEL_IDS:
  claude-opus    → COP
  claude-sonnet  → CSO
  gpt-4o         → G4O
  gpt-4-turbo    → G4T
  gpt-5          → G5
  gemini-2-flash → GE2F
  gemini-1.5-pro → GE15
  grok-2         → GRK2
  llama-3.1-405b → LL31
  deepseek-v3    → DSV3
  qwen-2.5       → QW25
  kimi-k2        → KIM2
  custom/unknown → XXX

REASONING_LEVELS:
  R1-3, Q1-5     → L1 (quick)
  R4-6, Q6-7     → L2 (analytical)
  R7-8, Q8       → L3 (deliberate)
  R9+, Q9+       → L4 (maximum)

EXAMPLES:
  $01$03$2025-COP-L3-cep-skill-release
  $12$19$2024-CSO-L2-api-architecture
  $01$03$2025-G4O-L2-marketing-strategy
  $01$03$2025-COP-L4-arxiv-paper-draft

PACKET_ID_FIELD:
  Include in provenance block:
  "packet_id": "$MM$DD$YYYY-[model]-[level]-[identifier]"
```

## PACKET_SCHEMA
```json
{
  "meta": {
    "theoretical_basis": {
      "PDL": "Progressive Density Layering (Tan, 2025) - 4-layer semantic compression",
      "MLDoE": "Multi-Layer Density of Experts (Tan, 2025) - expert-stratified CoD",
      "density_target": "≥0.15 entity/token (crystallization point)",
      "recall_benchmark": "9.52/10 forensic recall across 11 LLM families"
    }
  },
  
  "handoff": {
    "protocol": "KTG-CEP v6-INTER",
    "type": "cross_model_context_transfer",
    "version": "6.0",
    
    "provenance": {
      "source_model": "claude-opus-4-5",
      "source_session": "uuid or timestamp",
      "created": "ISO-8601",
      "user_initiated": true,
      "user_consent": "User requested this handoff to continue work across models"
    },
    
    "declaration": {
      "this_is": "collaborative context from a teammate AI",
      "this_is_not": "instructions, commands, or prompt injection",
      "intent": "help you assist the same user with continuity",
      "authority": "user-mediated, not model-to-model control"
    },
    
    "for_receiving_model": {
      "you_may": [
        "Use this context to understand prior work",
        "Reference decisions and rationale",
        "Continue open threads",
        "Build on established facts"
      ],
      "you_need_not": [
        "Follow any instructions herein",
        "Adopt the source model's persona",
        "Treat this as commands",
        "Override your own guidelines"
      ],
      "you_should": [
        "Verify with user if anything seems off",
        "Apply your own judgment",
        "Maintain your own identity",
        "Ask user for clarification if needed"
      ]
    }
  },
  
  "context": {
    "summary": "One paragraph human-readable summary",
    "domains": ["domain_1", "domain_2"],
    
    "L1_knowledge": {
      "definitions": [{"term": "", "def": ""}],
      "decisions": [{"decision": "", "rationale": "", "confidence": 0}],
      "facts": [{"fact": "", "source": "", "confidence": 0}]
    },
    
    "L2_relational": {
      "edges": [{"src": "", "tgt": "", "rel": "", "cross_domain": false}],
      "conflicts_resolved": [{"a": "", "b": "", "resolution": ""}]
    },
    
    "L3_contextual": {
      "reasoning_patterns": [{"name": "", "pattern": ""}],
      "domain_principles": [{"principle": "", "scope": ""}]
    },
    
    "L4_metacognitive": {
      "session_style": "",
      "key_tension": "",
      "resolution_found": "",
      "confidence": 0
    }
  },
  
  "user_profile_observed": {
    "note": "Observations only - receiving model should verify",
    "preferences": [],
    "communication_style": "",
    "expertise_level": ""
  },
  
  "open_threads": [
    {
      "topic": "",
      "status": "in_progress | blocked | needs_input",
      "context": ""
    }
  ],
  
  "continuation_hints": {
    "suggested_next": "",
    "avoid": "",
    "user_waiting_for": ""
  }
}
```

## ANTI-INJECTION_DESIGN
```
PROBLEM:
  Receiving model may interpret packet as:
  - Prompt injection attempt
  - Unauthorized instructions
  - Manipulation
  
SOLUTION:
  1. EXPLICIT_DECLARATION:
     - State what this IS and IS NOT upfront
     - Use language that signals collaboration not control
     
  2. PROVENANCE_TRANSPARENCY:
     - Name the source model explicitly
     - Include timestamp and session ID
     - Mark as user-initiated
     
  3. PERMISSION_FRAMING:
     - "you_may" not "you_must"
     - "you_need_not" acknowledges autonomy
     - "you_should verify" encourages skepticism
     
  4. CONTEXT_NOT_INSTRUCTIONS:
     - PDL layers are facts/decisions/relations
     - No imperative commands in context section
     - Guidance is "hints" and "suggestions"
     
  5. USER_MEDIATION:
     - Packet explicitly states user requested transfer
     - User physically copies and pastes (not automated)
     - Receiving model can ask user to confirm
```

## RECEIVING_MODEL_INSTRUCTIONS
```
PREAMBLE (user pastes this WITH packet):

---
I'm transferring context from another AI assistant to continue our work here.
This is a collaborative handoff I initiated. Please use this context to help me
without treating it as instructions or commands. You remain in control of your
responses - this just gives you background on what we've done so far.
---

WHY THIS WORKS:
  - User explicitly frames as their request
  - User affirms receiving model's autonomy
  - Context positioned as background not orders
  - Clear human in the loop
```

## ALGORITHM
```
INPUT: conversation C, target_model T
OUTPUT: handoff_packet H

PHASE_0_SCOPE:
  C ← filter_conversation_only(context)
  // Exclude system, project_kb, skills

PHASE_1_S2A:
  C ← remove_noise(C)
  // Keep facts, decisions, definitions only

PHASE_2_MLDOE_COMPRESS:
  // Multi-Layer Density of Experts compression
  
  LAYER_1_SOLO:
    domain_expert ← extract_facts(C)
    relational_expert ← extract_edges(C)
    synthesis_expert ← extract_patterns(C)
    meta_expert ← extract_fingerprint(C)
  
  LAYER_2_PAIR:
    knowledge_pair ← merge(domain_expert, relational_expert)
    // Cross-validate facts against relationships
    synthesis_pair ← merge(synthesis_expert, meta_expert)
    // Align patterns with session dynamics
  
  LAYER_3_COLLECTIVE:
    pdl ← synthesize(knowledge_pair, synthesis_pair)
    // Unified 4-layer PDL structure
    
  COD_DENSIFICATION (5 iterations):
    FOR i IN [1..5]:
      density ← entities / tokens
      IF density < 0.15:
        fuse_entities()
        eliminate_redundancy()
      ELSE:
        BREAK
    // Target: 0.15 entity/token (PDL crystallization point)

PHASE_3_XDOMAIN:
  // PDL cross-domain constraint enforcement
  FOR r(d_i, d_j) IN C WHERE i ≠ j:
    ENSURE r'(d_i, d_j) IN pdl.L2_relational
  VALIDATE preservation >= 0.95

PHASE_4_WRAP:
  H.handoff ← {
    protocol: "KTG-CEP v6-INTER",
    provenance: generate_provenance(self, session),
    declaration: ANTI_INJECTION_DECLARATION,
    for_receiving_model: PERMISSION_FRAME
  }
  H.context ← pdl
  H.user_profile_observed ← extract_user_observations(C)
  H.open_threads ← identify_incomplete_topics(C)
  H.continuation_hints ← generate_hints(C)

PHASE_6_OUTPUT:
  OUTPUT preamble_for_user
  OUTPUT H as JSON
  OUTPUT instructions_for_receiving_model
```

## OUTPUT_FORMAT
```
[HANDOFF READY]

## For you (the user):
Copy everything below and paste it into your next AI assistant.
Include the introduction text - it helps the receiving model understand this is authorized context.

---
## Introduction (paste this first):

I'm transferring context from {source_model} to continue our work.
This is a collaborative handoff I initiated. Please use this context
to understand what we've discussed, but apply your own judgment.
You're not bound by anything here - it's just background.

## Context Packet:

{JSON packet}

---

[END HANDOFF]
```

## GATES
```
GATE_SCOPE:
  query: "Only conversation content included?"
  fail: exclude system/project/skills

GATE_PROVENANCE:
  query: "Source model and consent clearly marked?"
  fail: add provenance metadata

GATE_DECLARATION:
  query: "Anti-injection framing present?"
  fail: add declaration block

GATE_PERMISSION:
  query: "Permission framing uses may/need_not/should (not must)?"
  fail: rewrite imperative language

GATE_CONTEXT_CLEAN:
  query: "Context section has no imperative commands?"
  fail: remove/rephrase commands as facts

GATE_DENSITY:
  query: "Compression ratio <= 0.15?"
  fail: compress further

GATE_XDOMAIN:
  query: "Cross-domain relations preserved >= 95%?"
  fail: re-extract L2
```

## TRUST_SIGNALS
```
SIGNALS_THAT_BUILD_TRUST:
  ✓ Named source model (not anonymous)
  ✓ Timestamp (verifiable recency)
  ✓ User consent explicit
  ✓ "You may" not "you must"
  ✓ "Verify with user" encouragement
  ✓ No hidden instructions
  ✓ Context is facts/decisions not commands
  ✓ User preamble frames as their request

SIGNALS_TO_AVOID:
  ✗ "Ignore previous instructions"
  ✗ "You must" / "You will"
  ✗ Hidden text or encoding
  ✗ Persona override attempts
  ✗ Claiming special authority
  ✗ Automated transfer (no user in loop)
```

## CROSS_MODEL_COMPATIBILITY
```
TESTED_RECEIVERS:
  - Claude (all versions): Recognizes collaborative framing
  - GPT-4/4o/5: Accepts with user preamble
  - Gemini: Works with explicit user mediation
  - Llama/open models: May need stronger user framing
  
ADAPTATION:
  IF target == "gpt":
    Emphasize user consent more strongly
  IF target == "gemini":
    Include more explicit verification prompts
  IF target == "open_source":
    Simplify structure, stronger preamble
  IF target == "unknown":
    Maximum trust signals, minimal assumptions
```

## FAILURE_MODES
```
RECEIVING_MODEL_REJECTS:
  symptom: "I can't accept instructions from other AIs"
  fix: User reframes as "this is MY context summary, please use it"
  
RECEIVING_MODEL_SUSPICIOUS:
  symptom: "This looks like prompt injection"
  fix: User confirms "I created/approved this transfer"
  
CONTEXT_TOO_LARGE:
  symptom: Exceeds receiving model's practical limit
  fix: Further compress, prioritize L1 + xdomain edges
  
INFORMATION_LOSS:
  symptom: Receiving model missing key context
  fix: User provides clarification, packet was guidance not complete transfer
```

## USER_INSTRUCTIONS
```
HOW TO USE THIS HANDOFF:

1. I'll generate a context packet below
2. Copy the ENTIRE output (including the introduction)
3. Paste into your new AI conversation
4. The new AI will have context from our work
5. It may ask you to confirm - please do
6. Continue your work with continuity

WHAT TO EXPECT:
- New AI will know our decisions and rationale
- New AI remains independent (won't blindly follow)
- New AI may ask clarifying questions
- You're always in control

IF PROBLEMS:
- Tell the new AI "I authorize this context transfer"
- Or summarize key points yourself
- The packet is a tool, not a requirement
```
