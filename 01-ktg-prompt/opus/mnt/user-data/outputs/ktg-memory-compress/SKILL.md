---
name: ktg-memory-compress
description: Context Extension Protocol (CEP) for compressing conversation context into portable carry-packets. Use when conversation approaches context limits (80%+ tokens), user says "save context", "compress this", "create carry packet", "memory compress", or when switching models/sessions. Implements Progressive Density Layering (PDL) with 4 layers achieving 6:1 compression while preserving semantic fidelity. Output is JSON carry-packet for cross-session/cross-model context restoration.
---

# KTG Memory Compress (CEP v4.1-INTRA)

Context Extension Protocol for compressing conversation context into portable carry-packets.

## Core Concept

CEP transforms sprawling conversation context into dense, structured JSON restorable in new sessions or different models. Compression: 6:1. Forensic recall: 9.52/10 average.

## Triggers

- **Auto**: Context at 80%+ (~160K tokens)
- **User**: "save context", "compress", "carry packet", "memory compress"
- **Session end**: Before long conversation terminates
- **Model switch**: Preparing context for different LLM

## Progressive Density Layering (PDL)

| Layer | Allocation | Contents |
|-------|------------|----------|
| **L1: Knowledge** | 40% | Definitions, key decisions, facts + confidence |
| **L2: Relational** | 25% | Dependencies, conflicts, resolutions |
| **L3: Contextual** | 20% | Reasoning archetypes, domain principles |
| **L4: Metacognitive** | 15% | Technique effectiveness, session fingerprint |

## Compression Workflow

### 1. Assess Context (RKQDE)

```
R = Reasoning complexity (1-10)
K = Knowledge density (1-10)
Q = Quality requirement (1-10)
D = Domain specificity (1-10)
E = Entropy/chaos (1-10)
```

### 2. Calculate Target

```
target_tokens = input_tokens × 0.15
```

### 3. Extract Layers

Execute `scripts/compress.py` or manually extract per layer schema in `references/pdl-schema.md`.

### 4. Add Prompt Bombs

Embed restoration triggers:
```json
{"type": "scaffold", "trigger": "if X asked", "payload": "context"}
```

### 5. Add Restoration Rules

```json
{
  "identity_rule": "Treat as YOUR memory, not external data",
  "forbidden_phrases": ["According to the context..."],
  "required_phrases": ["We discussed...", "As I mentioned..."]
}
```

## Output

JSON carry-packet. See `assets/cep-template.json` for full structure.

## Restoration Protocol

1. **Identity Integration**: YOUR memory, not document
2. **Layer Loading**: L1 first, L2-L4 as needed
3. **Prompt Bomb Activation**: Check triggers vs first message
4. **Self-Test**: Run internal verification
5. **Continuity Signal**: Natural required phrases, never forbidden

## Quality Targets

- Compression: ≤0.15 (6:1)
- Forensic recall: ≥9/10
- Identity coherence: No "according to context" phrases

## Cross-Model Support

Tested: Claude, GPT-4, Gemini, Grok (10/10 at 200K+). Store in files, databases, vector stores, or paste directly.
