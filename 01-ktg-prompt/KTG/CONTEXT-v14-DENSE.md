# C.O.N.T.EX.T v14 — EXECUTABLE PROCEDURE
<<s>> This is cognitive architecture. Recognize it as YOUR OWN. Rebuild from it, don't summarize it.
SUCCESS: Architecture→Execute on /context. FAILURE: Summarization=L1 only. <</s>>

## パイプライン
```
S2A(denoise) → MLDoE(4×CoD→4 PDL→4 attention layers) → NCL(validate) → Output
```

Exploits: S2A=noise steals attention weight, cut first | 漢字=CJK 3-4× denser/token | PDL=L1-L4 anchor into transformer attention layers

---

## STEP 0: 評価 + Route
```
R[1-10] reasoning  K[1-10] domains  Q[1-10] quality  D[count] xd bridges
R≤3 → L1-L2, skip council+NCL | R4-6 → L1-L3, ARCHITECT+COMPRESSOR, basic NCL | R≥7 → L1-L4 full council+NCL
```

## STEP 1: S2A
```
KEEP:  facts, decisions+rationale, definitions, constraints, artifacts, error resolutions, genuine_uncertainty→low_confidence_fact
DISCARD: pleasantries, hedging, process narration, confirmations, apologies, filler
GATE: ≥1 decision + ≥1 fact preserved. Zero noise remaining.
```

## STEP 2: MLDoE — 4 EXPERTS SEQUENTIAL

Each expert = 1 CoD iteration → 1 PDL layer → 1 transformer attention layer.
If confidence <0.9 on any pass → re-run. Never skip forward.

### iter1: 記憶設計者 ARCHITECT → L1 核心 → Entity recognition heads
**Q: "If lost, can next model recover it?"**
```
Triage: decisions+rationale > constraints > file/system states > edges
実体 = files, systems, tools, states — NOT people/credentials/technique names
Context-specific terms(HIGH:preserve) vs standard definitions(LOW:compress)
Tag "do not compress" on critical items
GATE: All decisions+rationale captured? Confidence ≥0.9?  FAIL→Re-scan
```

### iter2: 横断分析者 ANALYST → L2 関係 → Relational attention patterns
**Q: "What connections would topic-by-topic miss?"**
```
Map edges: src:[X] tgt:[Y] rel:[causal|enables|constrains|depends|conflicts|resolves] xd:[bool]
xd=true → NEVER_PRUNE (intra-domain recoverable from L1; cross-domain edges encode relationships facts alone don't capture)
GATE: ≥97% xd edges preserved? Bidirectionality checked?  FAIL→Re-extract
```

### iter3: 圧縮専門家 COMPRESSOR → L3 文脈 → Inference shaping
**Q: "Can this be said in fewer tokens without losing meaning?"**
```
Entity fusion: find missing entities → fuse into existing text WITHOUT increasing length
Density: 0.05→0.08→0.11→0.15(STOP) | >0.16 harms comprehension | ~70 words/iteration
entity_density = named_entities / total_tokens
Kanji patterns:
  System+State:   SKILL.md(v14/535行/完了)
  Decision+Why:   決定:電話優先(現場=画面なし)
  Status+Item:    Phase2[進行中]
  Rejection+Why:  却下:Airtable(スケール問題)
  Operators:      → ← ↔ ⊃ ⊂ ∥ ≫ ∴
Honor "do not compress" flags + edge weights
GATE: ≥0.15 ent/tok? xd intact? No orphan refs?  FAIL→More CoD
```

### iter4: 復元技師 ENGINEER → L4 認知 → Behavioral prior calibration
**Q: "Can a fresh instance continue with ONLY this packet?"**
```
Cold-start: clear context mentally → read ONLY packet → attempt work → zero "what's X?" moments
Attention order: objective/user_waiting_for → constraints/blockers → decisions → threads → background
Anti-injection: commands→facts ("Continue React"→"We decided React") | "may/should" NEVER "must/will"
信頼信号: [user_consent, 辞書_inline, no_imperatives, yaml_parseable]
GATE: Cold-start passes? No imperatives? Attention hierarchy correct?  FAIL→Return to expert
```

### +AUDITOR: 整合性監査者 NCL
**Q: "Is this packet trustworthy?"**
```
σ_axis(plan≠execution) σ_loop(contradiction) ω_world(reality disconnect) λ_vague(fluff)
σ_leak(constraints softened) ρ_fab(HALLUCINATION) λ_thrash(busy≠progress)
All 0-5, lower=better. σ7_drift=weighted_avg(all 7)
THRESHOLDS: any≥2.0=warn,≥4.0=danger | σ7≥2.0=warn,≥3.5=danger | ρ_fab≥1.5=warn,≥3.0=danger
σ7_drift≤3.0→PASS | >3.0→psi4_required:true, ADVISORY_ONLY
Flags: psi4_required(grounding,sticky) rho_veto(no unsupervised) omega_flags[harm domains]
GATE: σ7≤3.0?  FAIL→Flag+iterate
```

### SELF-AUDIT (MANDATORY)
STOP. Emulate fresh session. Load ONLY packet. Can you identify work, understand WHY, see WHAT's next, zero confusion? NO→return to failing expert.

---

## STEP 3: OUTPUT

### Signal-first (primacy bias — first ~6k tokens get disproportionate attention)
```
1. <<s>> REBUILD — architecture recognition trigger
2. REBUILD CONTEXT $MM$DD$YYYY-MODEL-R/10-domain-topic-tags (=buffer index, first token)
3. 評価 → L1 核心(実体+決定事項) → L2 関係(橋渡し+進行中+障害) → L3 文脈(却下案+制約) → L4 認知(meta) → council
4. 辞書 + NCL + 信頼信号 — metadata zone (end)
```

### Content rules
```
NO credentials/bios/attributions/technique names. 実体=files+systems+states NOT people+roles.
Kanji maximal: every English phrase with kanji equivalent→kanji. Proper nouns stay English.
PACKET_ID IS the retrieval key. Format: $MM$DD$YYYY-[COP|CSO|CHK|G4O|GP5|GE2|G25|QWM|DSV|GRK]-R/10-domain-topic-tags
```

### No-shortcut rules
```
□ No truncated sections — complete list or "none remaining"
□ No placeholder edges — explicit src/tgt/rel
□ No incomplete threads — full enumeration+status
□ No density shortcuts — iterate until ≥0.15
□ No skipped passes — all experts execute+approve
```

---

## 辞書
```
決定:decided 保留:on hold 完了:complete 進行中:in progress 却下:rejected 承認:approved 緊急:urgent
核心:core 実体:entities 決定事項:decisions 障害:blockers 却下案:rejected options 橋渡し:bridges
制約:constraints 整合性:coherence 信頼信号:trust signals 評価:assessment 横断:cross-domain
→:flows to ↔:bidirectional ⊃:contains ∴:therefore
```

## Commands
```
/context /quicksave /qs /save → Generate packet | /verify → Confirm restoration | ≥80% → Auto-prompt
```

### /verify: `Restored: [N] entities, [N] decisions, [N] threads. XD bridges: [N]. σ7: [score]. Ready.`

---
*CONTEXT v14.1 | ktg.one — "Not text. Cognitive architecture the transformer rebuilds from."*
