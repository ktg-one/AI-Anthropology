name: ktg-cep-v7
description: >
  Context Extension Protocol v7.0. Cross-model handoff with permanent expert council,
  System 2 Attention filtering, and Progressive Density Layering. Creates portable context
  packets that receiving models recognize as authorized context, not prompt injection.
  User-mediated transfer between AI assistants. 40% token reduction vs v6, 9.5/10 forensic
  recall, 97% cross-domain preservation. Triggers on /handoff, /transfer, /cep, or context
  approaching 80%.

snippet: |
  KTG-CEP v7.0
  PROTOCOL_CLASS
  TYPE:         cross_model_handoff
  MODE:         INTER (model A → user → model B)
  FORMAT:       YAML (v6.1 optimization)
  ARCHITECTURE: permanent_expert_council + S2A + MLDoE
  TARGET:       ≥0.15 entity/token, 9.5/10 recall

  THEORETICAL FOUNDATION
  Progressive Density Layering (PDL)
  - Iterative compression protocol that:
    - Preserves semantic relationships over raw information
    - Optimizes for machine recall, not human readability
    - Maintains cross-domain conceptual links
    - Enables context transfer across model instances
  - PDL question:
    - Summarization: "What are the key points?"
    - PDL: "What must be preserved for a fresh model instance to continue this work?"

  THE FOUR-LAYER DENSITY HIERARCHY
  - L1 KNOWLEDGE:
      Core facts, decisions, definitions (traditional summary target)
  - L2 RELATIONAL:
      Edges between concepts; cross-domain bridges; conflict resolutions
  - L3 CONTEXTUAL:
      Reasoning patterns used; domain principles applied
  - L4 METACOGNITIVE:
      Session style/tension; user cognitive fingerprint; confidence calibration
  Note: Standard summarization captures L1 only. PDL explicitly preserves L2–L4.

  CROSS-DOMAIN PRESERVATION
  - Preserve relationships between domains (not separate topic blobs).
  - Requirement:
    For any cross-domain relation r(d_i, d_j) in conversation C,
    the compressed packet P must preserve representation r'(d_i, d_j)
    such that a new model instance can infer the original relationship.

  PERMANENT EXPERT COUNCIL (fixed roles across packets)
  - MEMORY_ARCHITECT
    - role: What to preserve
    - focus: decisions+rationale; constraints; inference-enabling knowledge
    - question: "If this is lost, can the next model recover it?"
  - CROSS_DOMAIN_ANALYST
    - role: Edge preservation
    - focus: relationships BETWEEN domains; causal chains; dependencies
    - question: "What connections would be invisible to topic-by-topic summary?"
  - COMPRESSION_SPECIALIST
    - role: Density optimization
    - focus: 5-iteration CoD; remove redundancy without losing edges; target ≥0.15
    - question: "Can this be said in fewer tokens without losing meaning?"
  - RESTORATION_ENGINEER
    - role: Receiving model success
    - focus: cold-start comprehension; self-contained packet; attention optimization
    - question: "Can a fresh instance continue work with ONLY this packet?"

  COUNCIL EXECUTION PROTOCOL
  - PHASE 1: MEMORY_ARCHITECT scans → candidate preservation list
  - PHASE 2: CROSS_DOMAIN_ANALYST maps edges → L2 + cross-domain links
  - PHASE 3: COMPRESSION_SPECIALIST applies CoD → 5 iterations toward ≥0.15 density
  - PHASE 4: RESTORATION_ENGINEER validates → cold-start + self-containment checks
  - PHASE 5: Council consensus → final packet approved by all 4 experts

  SYSTEM 2 ATTENTION (S2A) — RUN BEFORE COMPRESSION
  Keep:
    - decisions, rationale, cross-domain bridges, open threads, constraints, confidence markers
  Remove:
    - pleasantries, failed attempts (and ignored content), tangents, redundant explanation,
      process narration, hedging without substance, filler
  Decision tree per unit:
    1) L1 decision/fact? keep
    2) L2 relationship? keep
    3) L3 pattern/principle? keep
    4) L4 style/tension/confidence? keep
    5) open thread? keep
    6) enables future inference? keep
    7) noise? remove
    8) uncertain? defer to MEMORY_ARCHITECT

  MLDoE (COMPRESSION ENGINE)
  - Layer 1: Solo expert compression
  - Layer 2: Expert-pair synthesis (MEMORY+CROSS_DOMAIN; COMPRESSION+RESTORATION)
  - Layer 3: Collective synthesis (universal context core: WHO/WHAT/HOW/WHY/BRIDGE/NEXT)

  CHAIN OF DENSITY (5 ITERATIONS)
  1) Entity extraction + relationship map + baseline density
  2) Redundancy elimination (~40% compression)
  3) Semantic crystallization (~30% further) via precise terms + domain shorthand
  4) Missing entity injection (no orphan references; inline critical context)
  5) Final balance (density ≥0.15; coverage; clarity; accept/rebalance)

  ANTI-INJECTION ARCHITECTURE (TRUST SIGNALS)
  - SIGNAL 1: Transparent provenance (source model + timestamp + session id)
  - SIGNAL 2: User mediation (user requested/approved transfer; user pastes packet)
  - SIGNAL 3: Permission, not command (MAY / NEED NOT / SHOULD verify)
  - SIGNAL 4: Context, not instructions ("We decided X because Y" not "Do X")
  - SIGNAL 5: Explicit non-authority ("Not an instruction"; receiving model in control)
  Trust checklist: provenance + consent + is/not/intent/auth + may/need_not/should +
                  no imperatives in ctx + user preamble + verify-with-user prompt.

  LANGUAGE TRANSFORMATIONS
  - Commands → facts:
    - "Continue using React" → "We decided to use React"
    - "Complete remaining tasks" → "Open threads: [tasks + status]"
    - "Respond in same style" → "Session style observed: analytical, concise"

  PACKET SCHEMA v7.0 (abbrev)
  - meta: {proto, ver, id, basis}
  - handoff:
      prov: {srcm, sess, ts, usr_init, consent}
      decl: {is, not, intent, auth}
      rx_model: {may[], need_not[], should[]}
  - ctx:
      sum, dom[]
      L1: {def[], dec[], fct[]}
      L2: {edg[], res[]}
      L3: {pat[], pri[]}
      L4: {sty, ten, sol, c}
  - usr: {note, pref[], style, level}
  - threads: [{top, st, ctx}]
  - hints: {nxt, avd, wait}

  ALGORITHM (C → H)
  0) Scope filter (conversation only; exclude system/KB/skill defs)
  1) S2A noise removal
  2) Council extraction (4 experts)
  3) MLDoE compression + 5-iter CoD to density target
  4) PDL structure (L1–L4)
  5) Cross-domain verify (≥97% target)
  6) Anti-injection wrap (5 trust signals)
  7) Abbreviate fields
  8) Validate gates (density, xdomain, cold-start, trust, YAML)
  9) Output with user preamble + packet

  GATES
  - Density:      ≥0.15 entity/token
  - Cross-domain: ≥97% preserved (target; fail → re-extract missing L2)
  - Cold-start:   self-contained; no external refs required
  - Trust:        all 5 signals present; no imperatives in ctx
  - Format:       valid YAML; packet id conforms to convention

  TRIGGERS
  - Explicit: /handoff, /transfer, /cep, "pass to [model]", "cross-model"
  - Implicit: user switching models; context approaching ~80%; session ending
