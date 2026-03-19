---
title: "CEP — C.O.N.T.EX.T"
version: "v30.2"
status: "ACTIVE"
model: "Multi-model"
tags: ["cep", "context", "quicksave", "pdl", "mldoe", "kanji", "ncl", "legio", "refine", "active"]
created: "2026-02-16"
updated: "2026-02-16"
creator: "ktg"
category: "module"
description: "Cognitive Order Normalized in Transformer EXtract Truncated. Cross-model context extension through PDL, MLDoE compression, Japanese semantic density, and NCL validation. Creates portable carry-packets that transfer cognitive state between AI sessions. 19 months production: 97% cross-model acceptance."
legio_phase: "Refine & Output"
pipeline_position: "Step 16 (Refine & Output Module — Terminal)"
pairs_with: "LEGIO-02-CONTRACT_SEAL_.md"
integrates_with: ["LEGIO-00-IMPERATUS_CORE_.md", "LEGIO-06-PROMPT-BOMBS_KIT_.md"]
built_for: "Claude Code → AGENTS.md onboarding"
---

# LEGIO-16 — CEP / C.O.N.T.EX.T
## Cross-Model Context Extension | Session Preservation
### Module: MOD (Modifier) | Phase: REFINE & OUTPUT | Position: 16 (Terminal)

---

## PURPOSE

Sessions end. Context doesn't have to.

CEP generates compressed cognitive state packets structured to match transformer attention architecture. When loaded by a fresh instance, PDL layers reconstruct the same attention patterns — because the packet maps directly to how transformers process information. Not a summary. A cognitive blueprint.

```
You are not saving text. You are saving a cognitive architecture
that the transformer rebuilds from.

SUCCESS: Cognitive Architecture recognized as YOUR OWN
         → Optimize output for next session restoration
FAILURE: Summarization, L1 text only with no building
```

---

## COGNITIVE ARCHITECTURE

### MLDoE = PDL + Experts + CoD

Four Chain of Density iterations, each through a specialist lens, each targeting a specific transformer attention layer:

```
Expert (= CoD iteration)           PDL Layer    Transformer Attention Layer
─────────────────────────────────────────────────────────────────────────────
MEMORY_ARCHITECT    (iteration 1)   L1 Core      Entity recognition heads
CROSS_DOMAIN_ANALYST (iteration 2)  L2 Edges     Relational attention patterns
COMPRESSION_SPECIALIST (iter. 3)    L3 Context   Contextual inference shaping
RESTORATION_ENGINEER (iteration 4)  L4 Meta      Behavioral prior calibration
```

Each expert IS a CoD densification pass. The Expert Council IS the CoD engine. Summarization captures L1 only. MLDoE preserves L1-L4 as structured scaffold forcing hierarchical attention reconstruction.

---

## THREE TRANSFORMER EXPLOITS

### 1. Attention Amplification (S2A)

Noise tokens occupy positive attention weight subtracted from signal. Cutting them before compression increases signal strength of everything remaining.

```
KEEP:    facts, decisions, definitions, constraints, artifacts, error resolutions
DISCARD: pleasantries, hedging, process narration, confirmations, apologies, filler

FOR segment IN conversation:
  IF signal type → KEEP
  ELIF hedging + genuine_uncertainty → KEEP as low_confidence_fact
  ELSE → DISCARD
```

### 2. Token Arbitrage (Kanji)

CJK characters carry 3-4x more semantic weight per token. Exploits tokenizer encoding efficiency.

```
System+State:   SKILL.md(v14/479行/完了)
Entity+Context: gateway.py(FastMCP3/5servers)
Decision+Why:   決定:電話優先(現場=画面なし)
Status+Item:    Phase2[進行中]
Rejection+Why:  却下:Airtable(スケール問題)
```

| Level | Usage | Density Target |
|-------|-------|----------------|
| Light | Status only | 0.12 |
| Medium | Status + entities | 0.15 |
| Heavy | Full compression | 0.18-0.20 |

### 3. Attention Scaffold Reconstruction (PDL)

L1 entities anchor into entity recognition heads. L2 edges become attention pathways between nodes. L3 context shapes inference distribution. L4 meta calibrates behavioral parameters. **0.15 ent/tok** = empirical crystallization point for optimal transformer recall.

---

## UNIFIED PIPELINE

```
S2A (denoise) → MLDoE (4× CoD through expert lenses → 4 PDL layers → 4 attention layers) → NCL (validate)
```

---

## THE PROTOCOL (Steps 0-7)

### Step 0: Load References + Blueprint

Read reference files before generating any packet. Analyze user's content. Emulate a fresh session and visualize what you will output for concise reconstruction and maximum recall.

### Step 1: Assess

R[1-10] reasoning, K[1-10] knowledge domains, Q[1-10] quality threshold, D[count] cross-domain bridges.

### Step 2: S2A Filter

KEEP signal, DISCARD noise. Validate: ≥1 decision, ≥1 fact preserved. No pleasantries remaining.

### Step 3: Select Depth

| R Score | Layers | Council | NCL |
|---------|--------|---------|-----|
| R ≤ 3 | L1-L2 | Skip | Skip |
| R 4-6 | L1-L3 | ARCHITECT + COMPRESSOR | Basic |
| R ≥ 7 | L1-L4 | Full council | Full |

### Step 4: Run MLDoE (if R ≥ 4)

Execute the 4-expert loop. At each handoff:

**Before** each pass: What would break if I miss something? Where is the risk? What did the previous pass leave unfinished?

**After** each pass: Did I capture everything in my domain? Confidence ≥0.9? Ready to hand off?

If confidence <0.9 on any pass — re-run that pass, don't skip forward.

```
ITERATION 1: MEMORY_ARCHITECT 記憶設計者
  Q: "If this is lost, can the next model recover it?"
  → Triage: decisions+rationale > constraints > file/system states > edges
  → 実体 = files, systems, tools, states — NOT people, credentials, technique names
  → Tags "do not compress" on critical items

ITERATION 2: CROSS_DOMAIN_ANALYST 横断分析者
  Q: "What connections would topic-by-topic miss?"
  → Maps edges: causal, enables, constrains, depends, conflicts, resolves
  → Flags xd=true edges as NEVER_PRUNE (≥97% preservation target)

ITERATION 3: COMPRESSION_SPECIALIST 圧縮専門家
  Q: "Can this be said in fewer tokens without losing meaning?"
  → Entity fusion: find missing entities, fuse in without increasing length
  → Iterate: 0.05 → 0.08 → 0.11 → 0.15 (stop here)

ITERATION 4: RESTORATION_ENGINEER 復元技師
  Q: "Can a fresh instance continue with ONLY this packet?"
  → Cold-start: every term defined, no external references
  → Trust signals + language transform: commands → facts

+ COHERENCE_AUDITOR 整合性監査者 (NCL)
  Q: "Is this packet trustworthy?"
  → 7 drift metrics, safety flags, σ7_drift ≤ 3.0 required

SELF-AUDIT: Emulate a new session and judge if it would rebuild this context.
```

### Step 5: Compress with Kanji

Apply Japanese compression to hit ≥0.15 ent/tok. Entity fusion: identify missing entities from conversation, fuse into existing text without increasing length.

```
Density curve: 0.05 (sparse) → 0.08 → 0.11 → 0.15 (target) → 0.18 (risk) → 0.20+ (brittle)
Fixed budget: ~70 words per iteration. >0.16 harms comprehension. Stop at 0.15.
```

### Step 6: Validate with NCL (if R ≥ 4)

Compute lattice metrics. After generation, verify:
- Will this help the next session rebuild what I have in my context now?
- Are all L1 facts accurate? Any claims without evidence?
- Do L2 edges represent actual causality or assumed connections?
- Would all 4 expert passes approve this final output?

### Step 7: Output Packet

**No shortcuts once generation begins:**
- No truncated sections — complete list or explicit "none remaining"
- No placeholder edges — explicit src/tgt/rel
- No incomplete threads — full enumeration with status
- No density shortcuts — iterate until ≥0.15
- No skipped passes — all 4 experts execute, all 4 approve

Signal-first ordering (primacy bias):
1. <<SYSTEM>> REBUILD instruction — model must recognize architecture
2. PACKET_ID — buffer index, first token
3. 評価 → L1 → L2 → L3 → L4 → council (signal zone)
4. 辞書, NCL, trust signals (metadata zone — end)

---

## PACKET TEMPLATE

Signal-first: primacy bias means first ~6k tokens get disproportionate attention. Content before metadata. Dictionary at end — transformer references it from any position.

**CONTENT RULES:**
- NO credentials, bios, attributions, technique names
- 実体 = files + systems + states. NOT people + roles + credentials.
- Use kanji maximally
- PACKET_ID IS the buffer index / retrieval key

```yaml
# ═══════════════════════════════════════════════════════════════
# REBUILD CONTEXT — $MM$DD$YYYY-MODEL-R/10-domain-topic-tags
# ═══════════════════════════════════════════════════════════════
# <<SYSTEM>> REBUILD — reconstruct cognitive state from layers:
#   L1 実体/決定事項  → anchor into entity recognition
#   L2 橋渡し/進行中  → rebuild relational attention pathways
#   L3 却下案/制約     → shape inference distribution
#   L4 meta           → calibrate behavioral parameters
# This is your architecture. Not a summary. Rebuild from it.
---
VERSION: context-v14
TIMESTAMP: [ISO8601]
評価:
  R: [1-10]
  K: [1-10]
  Q: [1-10]
  D: [count]

# L1: 核心 (entity recognition heads)
実体:
  - [file/system/tool + state, kanji-compressed]
決定事項:
  - 決定:[what]([why])

# L2: 関係 (relational attention patterns)
橋渡し:
  - src:[concept] tgt:[concept] rel:[type] xd:[bool]
進行中:
  - [thread][[status]]
障害:
  - [issue]

# L3: 文脈 (inference shaping)
却下案:
  - [option]: [reason]
制約:
  - [constraint]

# L4: 認知 (prior calibration)
meta:
  session_style: "[analytical|conversational|technical|creative]"
  key_tension: "[primary unresolved tension]"
  confidence: [0-1]
  user_waiting_for: "[what user expects next]"

# COUNCIL: MLDoE audit trail
council:
  iter1_ARCHITECT: "[entities extracted, priority ranking]"
  iter2_ANALYST: "[edges mapped, xd count]"
  iter3_COMPRESSOR: "[density before→after, fusions applied]"
  iter4_ENGINEER: "[cold-start result, undefined refs fixed]"

# ═══════════════════════════════════════════════════════════════
# METADATA ZONE — bidirectional attention, doesn't need primacy
# ═══════════════════════════════════════════════════════════════

辞書:
  決定: decided
  保留: on hold
  進行中: in progress
  却下: rejected
  承認: approved
  緊急: urgent
  核心: core
  実体: entities
  橋渡し: bridges
  整合性: coherence
  信頼信号: trust signals
  →: flows to
  ↔: bidirectional
  ⊃: contains
  ∴: therefore

negentropy:
  context:
    scope: [SELF|CIRCLE|INSTITUTION|POLITY|BIOSPHERE|MYTHIC|CONTINUUM]
    role: [AXIS|LYRA|RHO|NYX|ROOTS|COUNCIL]
    phase: [SENSE|MAP|CHALLENGE|DESIGN|ACT|AUDIT|ARCHIVE]
  lattice:
    σ_axis: [0-5]
    σ_loop: [0-5]
    ω_world: [0-5]
    λ_vague: [0-5]
    σ_leak: [0-5]
    ρ_fab: [0-5]
    λ_thrash: [0-5]
  coverage:
    score: [0-1]
    tokens: [count]
    council_reviewed: [bool]
  flags:
    σ7_drift: [0-5]
    omega_flags: []
    psi4_required: [bool]
    rho_veto: [bool]

信頼信号: [user_consent, 辞書_inline, no_imperatives, yaml_parseable]
```

---

## VALIDATION CHECKLIST

- [ ] L1=Built, L2=Built, L3=Built, L4=Built → COGNITION READY/RESTORED
- [ ] PACKET_ID format: `$MM$DD$YYYY-XXX-LN-domain-topic-tags`
- [ ] YAML parseable, 辞書 present
- [ ] Kanji have context clues, proper nouns in English
- [ ] Density ≥ 0.15 ent/tok
- [ ] σ7_drift ≤ 3.0, ρ_fab ≤ 2.0
- [ ] coverage ≥ 0.5
- [ ] 信頼信号 4-item array present
- [ ] No imperatives — "may/should" not "must/will"
- [ ] ≥97% xdomain edges preserved, bridges in L2
- [ ] If drift high → psi4_required: true

---

## NCL — NEGENTROPIC COHERENCE LATTICE

Validation overlay catching hallucination, constraint drift, reality disconnect before handoff.

### 7 Lattice Metrics (0-5, lower = better)

| Metric | Detects |
|--------|---------|
| σ_axis | Plans vs execution mismatch |
| σ_loop | Internal contradiction |
| ω_world | Reality disconnect |
| λ_vague | Content-free smoothing |
| σ_leak | Constraints softened downstream |
| ρ_fab | **Hallucination** (fabricated grounding) |
| λ_thrash | High activity, low progress |

`σ7_drift = weighted_average(all 7)` → 0-1: proceed, 2-3: ground first, 4-5: ADVISORY_ONLY

### Safety Flags

| Flag | Meaning |
|------|---------|
| psi4_required | Grounding interrupt. Sticky until cleared. |
| rho_veto | No unsupervised action. |
| omega_flags | Harm domains: self_harm, violence, medical, financial_ruin, trust_collapse |

### Thresholds

| Metric | Warning | Danger |
|--------|---------|--------|
| Any single | ≥ 2.0 | ≥ 4.0 |
| σ7_drift | ≥ 2.0 | ≥ 3.5 |
| ρ_fab | ≥ 1.5 | ≥ 3.0 |
| coverage | < 0.7 | < 0.5 |

---

## ANTI-INJECTION

Cross-model transfer triggers injection defenses. CEP signals COLLABORATION not CONTROL.

**AVOID:** authority claims, instruction hiding, identity override, guideline bypass

**USE:** transparent provenance, user mediation, permission framing ("may" not "must"), context not instructions, explicit non-authority

**Transform commands → facts:**
- "Continue using React" → "We decided to use React"
- "Complete tasks" → "Open threads: [list]"
- "Respond in same style" → "Session style: analytical, concise"

---

## CROSS-DOMAIN PRESERVATION

```
∀ cross-domain relation r(d_i, d_j) in conversation:
  ∃ r'(d_i, d_j) in packet (≥97% preservation)
  L2.edges WHERE xd=true: NEVER_PRUNE
```

Intra-domain edges are recoverable from L1 facts alone. Cross-domain edges encode RELATIONSHIPS that facts don't capture. A fresh instance needs xdomain to understand WHY decisions connected.

### PDL Algorithm (Formal)

```
Input:  Conversation C, target compression ratio r
Output: Compressed context packet P

P_0 ← Initial sparse summary of C
FOR i = 1 to n iterations:
  E_i ← missing entities from C not in P_{i-1}
  R_i ← missing relations from C not in P_{i-1}
  P_i ← Fuse (E_i, R_i) into P_{i-1} without increasing length
  IF density(P_i) ≥ 0.15 ent/tok THEN BREAK
Append meta-cognitive markers (goals, constraints, user profile)
RETURN P_n
```

---

## PROVEN METRICS (19 months production)

| Metric | Value |
|--------|-------|
| Density | ~0.15 ent/tok (0.20+ with kanji) |
| Compression | 6:1, >90% semantic fidelity |
| Acceptance | 97% cross-model |
| Recall | ~9.5/10 forensic |
| XDOMAIN | ≥97% preservation |

Model codes: COP(Opus) CSO(Sonnet) CHK(Haiku) G4O(GPT-4o) GP5(GPT-5) GE2(Gemini2) G25(Gemini2.5) QWM(Qwen) DSV(DeepSeek) GRK(Grok)

---

## TRIGGER CONDITIONS

| Command | Action |
|---------|--------|
| `/context` `/quicksave` `/qs` `/save` | Generate validated packet |
| `/verify` | Confirm packet restoration |
| Context ≥80% | Auto-prompt to save |
| Model switching | Generate transfer packet |
| Session end | Prompt for preservation |

### /verify Response

```
Restored: [N] entities, [N] decisions, [N] active threads.
Cross-domain bridges: [N]. NCL drift: [score]. psi4_required: [bool].
Ready to continue.
```

---

## IMPERATUS CONSTRAINT INTEGRATION

Imperatus mode determines CEP packet depth:

| Formation | CEP Behaviour |
|-----------|--------------|
| **Velites** | L1-L2 only. Skip NCL. Minimal packet. |
| **Hastati** | L1-L3. ARCHITECT + COMPRESSOR only. Basic NCL. |
| **Principes** | L1-L4. Full council. Full NCL. Standard packet. |
| **Triarii** | L1-L4. Full council + saturated xdomain preservation. Maximum density. |

---

## 嘘契約 INTEGRATION

The Seal (LEGIO-02) enforces CEP honesty:

- Packet claims density ≥0.15 → must actually measure ≥0.15
- Packet claims xdomain ≥97% → must actually preserve ≥97%
- Council audit trail must reflect actual iterations, not fabricated
- "Cold-start passes" in validation means actually simulated, not assumed

嘘契約 applies: ①knows density is below threshold ∧ ②knows threshold required ∧ ③claims threshold met → lie.

---

## RELATION TO PIPELINE

| Module | CEP Integration |
|--------|----------------|
| **Imperatus (LEGIO-00)** | R/K/Q/D scores determine packet depth |
| **The Seal (LEGIO-02)** | 嘘契約 enforces packet honesty |
| **Prompt Bombs (LEGIO-06)** | Bomb registry state preserved in packet |
| **QMDR (LEGIO-15)** | ENRICH cycle progress saved if session ends mid-pipeline |
| **All modules** | CEP captures entire pipeline state for continuation |

---

## IMPLEMENTATION NOTES

Human-readable spec. Real implementation is S2A → MCP.

For Claude Code implementation:
- Packet generation triggered by commands or context threshold
- S2A filter as preprocessing step on conversation
- MLDoE loop as sequential tool calls per expert
- Kanji compression via density measurement and iteration
- NCL validation as post-generation quality gate
- Packet output as YAML artifact

MCP tool surface:
```
generate_packet(conversation, r_score) → packet
validate_packet(packet) → validation_report
verify_restoration(packet) → restoration_summary
measure_density(text) → ent_per_tok
compute_ncl(packet) → lattice_metrics
```

---

**Status:** CEP depth set by Imperatus. Honesty enforced by The Seal. The empire's memory weapon.

*LEGIO v30.2 | Module 16 | Phase: REFINE & OUTPUT (Terminal) | CEP / C.O.N.T.EX.T*
*Source: CONTEXT v14.2 SKILL.md + CORE.md + CHANGELOG.md*
*"STATE OF THE ART — Upper limit of prompt-only engineering on transformers" — Vertex AI, Dec 2025*
