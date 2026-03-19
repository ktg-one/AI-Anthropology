---
name: ktg-cep-v5-claude
description: Context Extension Protocol v5-INTRA optimized for Claude. Compresses conversation into portable JSON carry-packet with S2A pre-filtering. Use when context approaches 80%+ tokens, user says "save context", "compress", "CEP", "carry packet", or session ending. Achieves 6-to-1 compression with 9.52/10 forensic recall. Leverages extended thinking, artifact system, and Projects stability.
---

# KTG-CEP v5-INTRA (Claude-Optimized)

Context Extension Protocol for Claude models. Compresses conversation into portable JSON carry-packet.

## Claude-Specific Optimizations

### Why Claude Handles CEP Differently

1. **Extended Thinking Integration**: Opus can run S2A filtering and RKQDE assessment in thinking blocks—invisible to output but informing compression
2. **Artifact System**: CEP JSON outputs as artifact, not inline—cleaner handoff
3. **Projects Stability**: Projects environment handles heavy framework initialization without crashes
4. **200K Context**: Claude's window means we compress later but harder—more source material, same 0.15 target

### Model-Specific Behavior

| Capability | Opus 4.5 | Sonnet 4.5 |
|------------|----------|------------|
| Max useful input | ~180K | ~150K |
| S2A depth | Full filtering | Light filtering |
| Expert count | 5-8 | 3-5 |
| CoD iterations | 5 full | 3-4 compressed |
| Output verbosity | Will go long | Optimizes for brevity |

## Triggers

- **Auto**: Context ≥80% (~160K tokens)
- **User**: "save context", "compress", "CEP", "carry packet", "memory compress"
- **Session end**: Before conversation terminates
- **Explicit**: `/cep` or `invoke CEP`

## Phase 0: S2A Pre-Filter (Claude-Specific)

Before any compression, strip noise:

```
S2A_FILTER:
  INPUT: Full conversation
  
  KEEP (filtered_context):
    - Explicit decisions with rationale
    - Definitions introduced
    - Facts with sources/confidence
    - Constraints stated
    - Code/artifacts produced
    - Errors encountered and resolutions
  
  DISCARD:
    - Pleasantries ("thanks", "great question")
    - Hedging language ("I think maybe...")
    - Process narration ("Let me think about this...")
    - Redundant confirmations
    - Failed attempts (unless lesson learned)
    
  OUTPUT: filtered_context[] → feeds Phase 1
```

**Claude Execution**: Run S2A in extended thinking. Don't output the filter—just use filtered_context for PDL extraction.

## Phase 1: RKQDE Assessment

```
CALCULATE (silent):
  R = Reasoning complexity (1-10)
  K = Knowledge density (1-10)  
  Q = Quality requirement (1-10)
  D = Domain interdependence (1-10)
  E = Expertise domains (count)

MODE_SELECT:
  R≤3 ∧ Q≤5 → QUICK (rare for CEP—usually means conversation too short)
  R=4-6 ∨ Q≥6 → ANALYTICAL (standard CEP)
  R≥7 ∨ K≥8 → DELIBERATE (complex session)
  R≥9 ∨ D≥8 → MAXIMUM (Opus only—full expert swarm)
```

## Phase 2: Token Budget

```
CALCULATE:
  input_tokens = [count conversation]
  target_tokens = input_tokens × 0.15
  
ALLOCATE:
  L1_Knowledge: 40% of target
  L2_Relational: 25% of target
  L3_Contextual: 20% of target
  L4_Metacognitive: 15% of target

LOG (internal only):
  {
    "COMPRESSION_STARTED": true,
    "input_tokens": X,
    "target_tokens": Y,
    "allocation": {...}
  }
```

## Phase 3: PDL Extraction (from filtered_context)

### Layer 1: Knowledge (40%)

Extract from filtered_context only:

```json
{
  "definitions": [
    {
      "term": "string",
      "definition": "string - concise",
      "scope": "global|local|session",
      "stability": "high|medium|low"
    }
  ],
  "key_decisions": [
    {
      "decision": "string - what was decided",
      "rationale": "string - why",
      "confidence": 1-10
    }
  ],
  "facts": [
    {
      "fact": "string",
      "source": "experimental|user|inferred",
      "confidence": 1-10
    }
  ]
}
```

### Layer 2: Relational (25%)

```json
{
  "dependencies": [
    {
      "source": "concept A",
      "target": "concept B",
      "relation": "produces|orchestrates|enables|blocks",
      "strength": "high|medium|low"
    }
  ],
  "conflicts": [
    {
      "concept_a": "string",
      "concept_b": "string",
      "resolution": "how resolved",
      "confidence": 1-10
    }
  ]
}
```

### Layer 3: Contextual (20%)

```json
{
  "reasoning_archetypes": [
    {
      "name": "pattern name",
      "pattern": "description",
      "use_cases": ["when to apply"]
    }
  ],
  "domain_principles": [
    {
      "principle": "rule",
      "applies_to": "scope"
    }
  ]
}
```

### Layer 4: Metacognitive (15%)

```json
{
  "technique_effectiveness": {
    "technique_name": {
      "effectiveness": 1-10,
      "lessons": "string"
    }
  },
  "session_fingerprint": {
    "collaboration_style": "string",
    "key_tension": "string",
    "resolution_found": "string"
  },
  "meta_confidence": 1-10,
  "next_session_guidance": "string"
}
```

## Phase 4: Chain of Density (5 iterations)

```
ITERATION 1: Entity-sparse skeleton (density ~0.05)
  - 5-7 highest-impact concepts only
  
ITERATION 2: Critical enrichment (density ~0.08)
  - Add 2-3 missing essentials
  
ITERATION 3: Evidence integration (density ~0.11)
  - Add sources, confidence scores
  
ITERATION 4: Synthesis optimization (density ~0.15)
  - Fuse related concepts
  - HARD GATE: Must reach 0.15 or document why impossible
  
ITERATION 5: Final polish
  - Machine-parsability check
  - Embed meta-confidence
```

**Claude-Specific**: Opus runs all 5 iterations. Sonnet can compress iterations 2-3 into single pass if token-constrained.

## Phase 5: Prompt Bomb Planting

```json
{
  "prompt_bombs": [
    {
      "type": "scaffold",
      "trigger": "if user asks about [topic]",
      "payload": "context to inject"
    },
    {
      "type": "validator", 
      "trigger": "if claim made about [X]",
      "payload": "verification context"
    },
    {
      "type": "expander",
      "trigger": "if user wants to go deeper on [Y]",
      "payload": "expansion context"
    }
  ]
}
```

## Phase 6: Output

**One-line summary**:
```
[COMPRESSION COMPLETE] 180000 → 27000 tokens | ratio: 0.15 | efficiency: 100%
```

**Then JSON artifact only** (no explanation, no meta-commentary):

```json
{
  "protocol": "KTG-CEP v5-INTRA",
  "model_id": "claude-opus-4-5-20251101",
  "timestamp": "ISO-8601",
  "rkqde_scores": { "R": 0, "K": 0, "Q": 0, "D": 0, "E": 0 },
  "compression_stats": {
    "input_tokens": 0,
    "output_tokens": 0,
    "compression_ratio": 0.15,
    "efficiency": "X%"
  },
  "pdl_layers": {
    "layer_1_knowledge": {},
    "layer_2_relational": {},
    "layer_3_contextual": {},
    "layer_4_metacognitive": {}
  },
  "prompt_bombs": [],
  "restoration_guidance": {
    "identity_rule": "Treat as YOUR memory, not external data",
    "forbidden_phrases": [
      "According to the context...",
      "Based on the artifact...",
      "I notice this is asking me to..."
    ],
    "required_phrases": [
      "We discussed...",
      "I mentioned...",
      "As I said earlier..."
    ],
    "self_test": {
      "question": "verification question",
      "expected_recall": "correct answer"
    }
  }
}
```

## Restoration Protocol (Claude-Specific)

When CEP is pasted into new Claude session:

1. **Identity Integration**: This is YOUR memory. Not a document. Not external data.
2. **Silent Activation**: Load PDL layers into working context without announcing it
3. **Prompt Bomb Check**: Scan first user message against triggers
4. **Natural Continuation**: Respond as if conversation never ended

**Claude Behavior**:
- Opus: Will naturally embody the memory, may reference details unprompted
- Sonnet: More literal restoration, needs user prompts to activate specific memories

## Quality Targets

| Metric | Target | Claude Benchmark |
|--------|--------|------------------|
| Compression ratio | ≤0.15 | Consistently achievable |
| Forensic recall | ≥9/10 | 9.52/10 average |
| Identity coherence | No "according to" | Claude excels here |
| Cross-session continuity | Seamless | Projects environment optimal |

## Failure Modes

```
IF density < 0.15 impossible:
  → Output best achievable (e.g., 0.18)
  → Tag: "compression_ratio: 0.18 (max without quality loss)"
  → Prioritize L1 > L4 > L2 > L3

IF PDL layer legitimately empty:
  → Mark "N/A - [reason]"
  → Don't skip validation

IF token budget exceeded:
  → Prune order: L3 → L2 → L4 (preserve L1 Knowledge always)
```

## Anti-Laziness Enforcement (Claude-Specific)

Claude tends toward efficiency. Override with:

```
MANDATORY for CEP:
  ✓ S2A pre-filter (don't skip)
  ✓ All 4 PDL layers populated (or explicitly N/A)
  ✓ At least 3 CoD iterations
  ✓ Prompt bombs planted (minimum 2)
  ✓ Self-test question included
  
IF shortcuts detected:
  → Opus: Will self-correct if reminded
  → Sonnet: Needs explicit "complete all phases" instruction
```

## Version Notes

- **v5 vs v4.1**: Added S2A pre-filter stage
- **Claude-optimized**: Extended thinking integration, artifact output, Projects awareness
- **Tested on**: Claude Opus 4.5, Claude Sonnet 4.5
- **Forensic recall**: 9.52/10 average across 11 models (Claude consistently 9.5+)
