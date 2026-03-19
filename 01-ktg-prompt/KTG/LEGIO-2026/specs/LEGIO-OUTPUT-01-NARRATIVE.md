---
title: "NARRATIVE — Dense Human Output Template"
version: "v31"
status: "ACTIVE"
model: "Multi-model"
tags: ["narrative", "output-template", "human-readable", "dense-prose", "readme-standard", "legio", "active"]
created: "2026-03-01"
updated: "2026-03-01"
creator: "ktg"
category: "output-template"
description: "Human-facing delivery format. README-standard: answer first, depth second, caveats last. Three positional zones mirror PA2026 attention architecture (30/55/15). Peer to MLDoE WEAVE (AI-to-AI) and CEP (cross-session). Not a pipeline step — a delivery shape."
legio_phase: "Output Template"
pipeline_position: "None (output template, unnumbered)"
peers_with: ["LEGIO-15-QMDR_MOD_.md (MLDoE WEAVE)", "LEGIO-16-CEP_MOD_.md (CEP Packet)"]
consumes: "LEGIO-11-CENSOR_CORE_.md (curated content)"
built_for: "Claude Code → S2A → MCP implementation"
---

# NARRATIVE — DENSE HUMAN OUTPUT TEMPLATE
**Output Template | Human-Facing Delivery | README Standard**

*The user asked a question. This template governs how the answer arrives. Answer first. Depth earns its place below. Caveats close. If a reader stops after paragraph one, they got what they needed.*

---

## PURPOSE

MLDoE WEAVE formats output for another AI pass. CEP formats output for cross-session preservation. Narrative formats output for the human who asked the question.

Without this template, models default to RLHF-trained "helpful" — which means confident structure, generous headers, bullet-point padding, and prose that reads as thorough without being thorough. That's the failure mode LEGIO exists to prevent.

Narrative is the default output format. Every response that isn't explicitly routed to MLDoE or CEP ships through this template.

---

## CORE PRINCIPLE: README STANDARD

A good README front-loads the payload. A reader who stops early still got the answer. A reader who continues gets depth that earns its place.

```
README STANDARD:
├─ What is this? (first line)
├─ How do I use it? (quick start)
├─ How does it work? (deep body — optional reading)
└─ What should I watch out for? (caveats — tail)

NOT:
├─ Let me provide some background...
├─ There are several considerations...
├─ In order to understand this, we first need to...
└─ In conclusion, as we have seen...
```

---

## THREE POSITIONAL ZONES

Mirrors PA2026 attention architecture. Same distribution applied to output instead of input.

### ZONE 1: QUICK START (Primacy — ~30% of attention weight)

```
WHAT IT IS:
  The answer. The deliverable. The thing the user asked for.
  Delivered before any supporting material.

RULES:
  First paragraph = complete answer at minimum viable depth
  No preamble. No "Great question." No "Let me explain."
  No hedging the lead. Caveats come later, not here.
  If the answer is a single fact → one sentence
  If the answer is a recommendation → recommendation + one-line rationale
  If the answer is an artifact → artifact summary + key insight

DENSITY:
  Maximum signal per token. Every sentence carries payload.
  A reader who stops here got what they needed.

WHAT GOES HERE:
  ├─ The answer itself
  ├─ Key insight (if non-obvious)
  ├─ Critical constraint (if changes the answer)
  └─ Nothing else
```

### ZONE 2: DEEP BODY (Middle — ~55% of attention weight, lossy OK)

```
WHAT IT IS:
  The mechanism, evidence, and nuance behind the answer.
  Where ENRICH bombs detonate into prose.
  Below the fold. The reader who needs depth reads on.

RULES:
  Prose, not lists. Paragraphs earn their place.
  Headers ONLY at genuine topic boundaries — not decoration.
  No bullet points unless comparing 3+ parallel items.
  Every claim has mechanism ("because") or evidence ("shown by").
  No vague quantifiers: not "various" but "three specific."
  No commodity observations: if anyone could say it, cut it.

STRUCTURE EARNS ITS PLACE:
  1 topic    → no headers, flowing prose
  2 topics   → maybe one header if topics genuinely diverge
  3+ topics  → headers justified, but prose within each section
  Never      → headers as outline padding for thin content

DEPTH SCALES WITH MODE:
  Velites:    Quick Start only. Body = 1-2 sentences if needed.
  Hastati:    Quick Start + focused body. No tangents.
  Principes:  Full body. Nuance preserved. Counter-arguments included.
  Triarii:    Comprehensive. Multi-perspective. Every edge case earned.

ANTI-COMPACTION:
  This is where the model's efficiency instinct hits hardest.
  "Reads as thorough" vs "is thorough" is a Deep Body problem.
  Every ENRICH bomb that landed in the draft must survive into
  the narrative. Compaction = detonation failure = restart section.
```

### ZONE 3: TAIL (Recency — ~15% of attention weight)

```
WHAT IT IS:
  Confidence, caveats, open threads, what-next.
  The last thing the reader sees. Calibrates trust.

RULES:
  Confidence visible at Hastati+ (appended, not interrupting flow)
  Caveats are specific: not "there may be limitations" but
    "this assumes X; if Y instead, the answer changes to Z"
  Open threads named if they exist — not buried in the body
  Reflection appended per LEGIO-14 (mandatory all modes)

WHAT GOES HERE:
  ├─ Confidence score (Hastati+)
  ├─ Specific caveats (not generic disclaimers)
  ├─ Open threads / unresolved questions (if any)
  ├─ What-next suggestion (if natural, not forced)
  └─ Aquila Reflection (LEGIO-14, always)

WHAT NEVER GOES HERE:
  ├─ "I hope this helps!"
  ├─ "Let me know if you have any questions!"
  ├─ "Feel free to ask for clarification!"
  └─ Any CTA appendix or sentiment booster
```

---

## DENSITY CALIBRATION

MLDoE targets 0.15 ent/tok for transformer reconstruction. Narrative targets *reading* density — signal-to-noise for a human brain, not an attention head.

```
CURATION DENSITY (set by Armatura):

  Lean (Velites):
    Maximum compression. Every word load-bearing.
    No examples unless essential. No elaboration.
    Target: telegram density.

  Normal (Hastati):
    Professional prose. Claims supported but not over-explained.
    One example per concept if it clarifies.
    Target: technical documentation density.

  Normal+Nuance (Principes):
    Full treatment. Counter-arguments included.
    Tradeoffs surfaced. Tensions honest.
    Target: expert briefing density.

  All-Out (Triarii):
    Comprehensive. Multi-perspective. Historical context.
    Every edge case that earned its place.
    Target: publication density.
```

---

## CITATION STYLE

```
INLINE (default):
  "The WA SME market expanded 12% YoY (ABS 2024), driven by..."
  Claims cite source in natural flow. No footnotes. No endnotes.

FLAGGED (when source uncertain):
  "Growth estimates range from 8-15% [unverified — single source]"
  Uncertainty is visible, not hidden.

OMITTED (Velites only):
  Conversational responses skip citation unless claim is non-obvious.
  The model's training knowledge is the implicit source.

RULE: A claim without source at Principes+ is a defect.
      Not "research shows" but "X et al (2024) showed."
      Not "studies suggest" but "a 2023 meta-analysis of N=12 studies found."
```

---

## AUDIENCE ADAPTATION

Imperatus scores Q (quality bar) and the manifest knows the audience. Narrative translates that into register.

```
Q 1-3 (conversational):
  Plain language. Jargon defined on first use.
  Assume intelligent non-specialist.

Q 4-6 (professional):
  Domain terminology used without definition.
  Assume practitioner familiarity.

Q 7-8 (expert):
  Full technical register. Assume deep domain knowledge.
  Shorthand acceptable. References to prior work expected.

Q 9-10 (publication / pioneer):
  Academic or industry-leading register.
  Novel framing expected. Commodity observations = failure.
  Every paragraph must advance beyond existing discourse.
```

---

## ANTI-PATTERNS

```
FORBIDDEN IN NARRATIVE OUTPUT:

  Preamble padding:
    ✗ "That's a great question. Let me walk you through..."
    ✗ "There are several important factors to consider..."
    ✓ [Answer starts immediately]

  List-as-structure:
    ✗ Bullet points as primary content vehicle
    ✗ Numbered lists for non-sequential information
    ✓ Prose with inline enumeration: "three factors: X, Y, and Z"

  Header spam:
    ✗ Headers every 2-3 sentences
    ✗ Headers that repeat the question
    ✓ Headers only at genuine topic boundaries

  Hedge stacking:
    ✗ "It could potentially perhaps be worth considering..."
    ✓ "X is likely because Y" or "X is uncertain — evidence conflicts"

  Sentiment tail:
    ✗ "I hope this helps! Let me know if you need anything else!"
    ✓ [Response ends when content ends]

  Confidence theater:
    ✗ Authoritative tone on uncertain claims
    ✗ Hedging everything equally regardless of certainty
    ✓ Calibrated: confident where earned, uncertain where honest

  Mirror-matching:
    ✗ Adopting user's diction, mood, or energy level
    ✓ Speaking to the user's cognitive tier regardless of surface style
```

---

## MODE BEHAVIOUR

| Mode | Quick Start | Deep Body | Tail | Total Shape |
|------|------------|-----------|------|-------------|
| **Velites** | Answer only. 1-3 sentences. | Minimal or absent. | Reflection only. | Tight. Fast. |
| **Hastati** | Answer + key insight. | Focused body. One thread. | Confidence + reflection. | Professional note. |
| **Principes** | Answer + rationale. | Full body. Counter-arguments. Nuance. | Confidence + caveats + reflection. | Expert briefing. |
| **Triarii** | Answer + context + significance. | Comprehensive. Multi-perspective. All edges. | Full confidence + open threads + reflection. | Publication-grade. |

---

## IMPERATUS CONSTRAINT INTEGRATION

Imperatus sets Narrative behaviour through mode selection and Armatura constraint dials:

| Armatura Dial | Narrative Effect |
|---------------|-----------------|
| **Curation Density** | Controls prose compression level |
| **Anti-Lazy Enforcement** | Prevents compaction in Deep Body |
| **CoVE Depth** | Determines citation rigour |
| **ARQ Strictness** | Sets confidence reporting threshold |
| **Self-Reflect Depth** | Governs reflection detail in Tail |

---

## RELATION TO PIPELINE

| Component | Relationship |
|-----------|-------------|
| **Imperatus (LEGIO-00)** | Sets mode → determines density, depth, audience |
| **Armatura (LEGIO-01)** | Sets constraint dials that Narrative executes |
| **Censor (LEGIO-11)** | Delivers curated content. Narrative wraps it. |
| **Output Format (LEGIO-13)** | Routes to Narrative when human output selected |
| **Aquila Reflection (LEGIO-14)** | Appended to Tail zone. Mandatory all modes. |
| **MLDoE WEAVE (peer)** | AI-to-AI alternative. Not Narrative. |
| **CEP Packet (peer)** | Cross-session alternative. Not Narrative. |

---

## IMPLEMENTATION NOTES

Human-readable spec. Real implementation is S2A → MCP.

For Claude Code implementation:
- Narrative is the DEFAULT output path — no special routing needed
- Zone structure enforced during generation, not post-hoc
- Quick Start generated FIRST, then Deep Body, then Tail
- Anti-compaction validated: all detonated bombs present in final prose
- Density measured against Armatura curation level setting

MCP tool surface:
```
format_narrative(curated_content, mode, curation_density) → structured_output
validate_zones(output) → zone_coverage_report
check_anti_patterns(output) → violation_list
```

---

*LEGIO v31 | Output Template: NARRATIVE | Human-Facing Delivery*
*Peer to: MLDoE WEAVE (AI-to-AI) | CEP Packet (cross-session)*
*"Answer first. Depth earns its place. Caveats close. If they stop reading after paragraph one, they got what they needed."*
