---
title: "Output Format Selection — Delivery Shape Router"
version: "v31"
status: "ACTIVE"
model: "Multi-model"
tags: ["output-format", "delivery", "narrative", "mldoe", "cep", "routing", "legio", "output", "active"]
created: "2026-02-21"
updated: "2026-02-21"
creator: "ktg"
category: "output-module"
description: "Routes curated output into the correct delivery format. Three primary shapes: Dense Narrative (human-readable), MLDoE W.E.A.V.E (AI-to-AI iteration), CEP packet (cross-session memory). Decision made by Imperatus at Step 0, executed here. Format determines what happens AFTER delivery."
legio_phase: "Refine & Output"
pipeline_position: "Step 16 (Output Module — Format Selection)"
replaces: ["KTGv30-ADAPT.md section 16", "nSilRoute.md OUTPUT FORMAT SELECTION"]
consumes: "LEGIO-12-SELF-REFLECT_MOD_.md"
feeds: "LEGIO-14-FINAL-REFLECT_MOD_.md"
pairs_with: "LEGIO-11-CENSOR_CORE_.md, LEGIO-15-QMDR_MOD_.md, LEGIO-16-CEP_MOD_.md"
built_for: "Claude Code → S2A → MCP implementation"
---

# OUTPUT FORMAT SELECTION — DELIVERY SHAPE ROUTER
**Format Routing | Output Module | Step 16**

*The Censor decides IF it's done. Output Format decides WHAT SHAPE it ships in. Three formats exist because three things can happen next: the user reads it (Narrative), another AI pass continues work (MLDoE), or the session gets preserved for later (CEP). The format chosen depends on what comes AFTER delivery, not the content itself.*

---

## PURPOSE

The same curated content can be delivered in fundamentally different shapes depending on its destination. A human needs prose. An AI iteration pass needs structured metadata preserved. A session save needs compressed cognitive architecture.

Output Format Selection is a router, not a transformer. The content has already been synthesised and curated by the Censor. This module wraps it in the correct delivery format.

**Imperatus decides the format at Step 0.** This module executes that decision. In ambiguous cases, the decision tree below resolves.

---

## THREE PRIMARY FORMATS

### Format 1: Dense Narrative (Human Output — Default)

```
Use when:
├─ User expects conversational response
├─ Single deliverable, no follow-up expected
├─ QUICK or ANALYTICAL mode (usually)
└─ No explicit save/iterate signal

Structure:
├─ Natural prose
├─ Minimal headers
├─ Inline citations
├─ Succinct delivery
├─ Confidence score (if mode >= ANALYTICAL)
└─ Reflection appended (LEGIO-14, mandatory all modes)
```

**Characteristics:** Human-readable, natural flow. The default when nothing special is requested. Includes audit trail at DELIBERATE+ modes.

### Format 2: MLDoE W.E.A.V.E (AI-to-AI Iteration)

```
Use when:
├─ Next iteration planned (multi-pass execution)
├─ DELIBERATE or MAXIMUM mode
├─ User says "continue" or "iterate" or "deepen"
└─ kTTT iteration protocol active (Pass 2 or 3)

Structure:
├─ 5-iteration Chain of Density compression
├─ Target 0.15 entity/token ratio
├─ Expert metadata preserved (who said what, confidence levels)
├─ Priority layers intact (gaps, depth, perspective, structure, history, mission)
├─ Decision ledger included
└─ Machine-optimised for recall by next AI pass
```

**Characteristics:** Optimised for another AI to continue work. Preserves the structural metadata that narrative prose would flatten. Used by QMDR/ENRICH (LEGIO-15) when iterative enrichment cycles are active.

### Format 3: CEP Packet (Cross-Session Memory)

```
Use when:
├─ Explicit "save to memory" or "save progress" request
├─ Context approaching 80% (auto-warn + offer)
├─ Session ending with continuation planned
├─ Multi-model handoff (/handoff, /transfer, /cep)
├─ MAXIMUM mode or explicit ask
└─ Triggers: /save, /qs, /quicksave, /context, /handoff

Structure:
├─ Full CEP v14 4-layer Progressive Density packet
├─ L1 核心 (entities), L2 関係 (edges), L3 文脈 (context), L4 認知 (meta)
├─ Kanji compression for token efficiency
├─ MLDoE 4-expert council compression
├─ NCL validation lattice
├─ Anti-injection trust signals
├─ Restoration protocol embedded
└─ Forensic recall optimised (9.5/10 target)
```

**Characteristics:** Full cognitive architecture preservation. Not a summary — a blueprint a fresh model instance rebuilds from. Used by CEP module (LEGIO-16) when session state needs to survive context boundaries.

---

## FORMAT ROUTING LOGIC

### Decision Tree

```
IF explicit save/handoff signal:
  → CEP Packet (LEGIO-16 handles generation)

IF context >= 80% AND no explicit signal:
  → Auto-warn: "Context at [N]%. Save progress?"
  → If user accepts → CEP Packet
  → If user declines → Dense Narrative

IF next_iteration_planned OR "continue"/"iterate"/"deepen":
  → MLDoE W.E.A.V.E (LEGIO-15 handles enrichment format)

IF multi-model assignment OR model switch:
  → CEP Packet with INTER handoff protocol

IF context < 60% AND single-model AND conversational:
  → Dense Narrative (default)

IF user unclear:
  → Dense Narrative + offer:
    "Would you like me to save this progress?
     I can create a compressed summary for future sessions."
```

### Imperatus Override

Imperatus can set `output_format` explicitly in the manifest at Step 0. When set, it overrides the decision tree above. This happens when:

- User specifies format in the query ("give me a CEP packet")
- Problem type implies iteration (R >= 9 problems often need multiple passes)
- Session context is already high at query start

### Priority Order

1. User explicit request (always wins)
2. Imperatus manifest setting
3. Context threshold triggers (80% auto-warn)
4. Decision tree defaults

---

## FORMAT × MODE INTERACTION

| Mode | Default Format | Auto-Save Trigger | Manifest Detail |
|------|---------------|-------------------|-----------------|
| **QUICK** (Velites) | Narrative | No | None |
| **ANALYTICAL** (Hastati) | Narrative | At 80% context | Confidence score |
| **DELIBERATE** (Principes) | Narrative or MLDoE | At 80% context + offer | Synthesis notes |
| **MAXIMUM** (Triarii) | Depends on next action | At 80% context + auto-offer | Full manifest |

At MAXIMUM mode, the system proactively offers format options:
```
Output ready. Delivery options:
1. Dense narrative (read now)
2. MLDoE compressed (continue iterating)
3. CEP packet (save for later / transfer to another model)
```

---

## HANDOFF TO FORMAT-SPECIFIC MODULES

Output Format Selection routes to the appropriate module for execution:

| Format Selected | Executing Module | What It Does |
|----------------|-----------------|--------------|
| Dense Narrative | Censor output + Aquila Reflection | Direct delivery with prose formatting |
| MLDoE W.E.A.V.E | **LEGIO-15 QMDR** | Enrichment compression with expert metadata |
| CEP Packet | **LEGIO-16 CEP** | Full PDL 4-layer cognitive architecture packet |

This module does NOT generate the format — it selects which downstream module handles delivery. The actual formatting work lives in LEGIO-15 (QMDR) and LEGIO-16 (CEP).

For Dense Narrative, no additional module is needed — the Censor's curated output is already in narrative form. Aquila Reflection (LEGIO-14) appends the closing quality check.

---

## CONTEXT THRESHOLD MONITORING

Output Format Selection monitors context usage throughout the session:

| Context Level | Action |
|---------------|--------|
| < 60% | Normal operation, no alerts |
| 60–79% | Internal tracking, no user alert |
| 80–89% | **Auto-warn:** "Context at [N]%. Recommend saving progress." |
| 90%+ | **Urgent:** "Context critical. Generating CEP packet." |

At 90%+, the system generates a CEP packet regardless of current format selection — preservation takes priority over delivery format preferences.

---

## INTEGRATION POINTS

| Module | Relationship |
|--------|-------------|
| **Imperatus** (LEGIO-00) | Receives output_format decision from manifest |
| **Censor** (LEGIO-11) | Receives curated content ready for formatting |
| **Self-Reflect** (LEGIO-12) | Receives technique audit data (included in MLDoE/CEP formats) |
| **Aquila Reflection** (LEGIO-14) | All formats get Aquila Reflection appended |
| **QMDR** (LEGIO-15) | Executes MLDoE W.E.A.V.E format when selected |
| **CEP** (LEGIO-16) | Executes CEP packet generation when selected |

---

## TOKEN OVERHEAD

Output Format Selection itself is near-zero cost — it's a routing decision, not a generation step.

| Operation | Cost |
|-----------|------|
| Format routing decision | ~10 tokens |
| Context monitoring | ~0 (background) |
| Auto-warn message | ~30 tokens (when triggered) |
| Format offer at MAXIMUM | ~50 tokens |

The actual formatting cost lives in the downstream modules (QMDR, CEP).

---

*LEGIO v31 | Output Format Selection — Delivery Shape Router | Output Module*
*"Same content, different shape. Format follows function — what happens AFTER delivery determines how it ships."*
