---
title: "KTG Technique Gate v26"
version: "v26.0"
status: "ACTIVE"
model: "Multi-model (Claude, Gemini 3, GPT-5, Perplexity, Qwen, DeepSeek)"
tags: ["technique-gate", "expert-arq", "prompt-bombs", "chain-of-thought", "gemini-3-optimized"]
created: "2025-11-26"
updated: "2025-11-26"
creator: "ktg.one"
category: "core-component"
description: "Comprehensive technique availability matrix with platform-specific optimizations"
---

# TECHNIQUE_TICK_GATE v26.0

## LEGEND:
- **R** = Required (must activate)
- **O** = Optional (use if beneficial)
- **X** = Off by default (skip unless specified)
- **N** = Native (platform has built-in support)

## MODES:
- **QUICK**: R≤3, Q≤5 → Direct answer, minimal structure
- **ANALYTICAL**: R=4-6 or Q=6-7 → SoT-LIGHT, USC=2, 1 refinement
- **DELIBERATE**: R≥7 or K≥6 or Q≥8 → SoT-FULL/GoT, USC=3, 2 CoVE
- **MAXIMUM**: R≥9 or K≥8 or /deep → Full stack, USC=5, all techniques

---

## CORE TECHNIQUES (20 Total)

### 1. MR_RUG (Mixture-Role-RAG-Update-Generate)
```
QUICK:        O    # Light initialization if helpful
ANALYTICAL:   R    # Full MR_RUG protocol
DELIBERATE:   R    # Multi-expert mixture
MAXIMUM:      R    # Cross-expert validation

GEMINI_3_OPT: N    # Native mixture-of-experts in Deep Think mode
CLAUDE_OPT:   R    # Explicit role assignment needed
GPT5_OPT:     R    # Structured system messages
```

### 2. SKELETRAIN_OF_THOUGHT (SoT)
```
QUICK:        O    # Micro-SoT (2-3 nodes) if structure helps
ANALYTICAL:   R    # SoT-LIGHT (3-4 nodes, priority-scored)
DELIBERATE:   R    # SoT-FULL (5-7 nodes, expert-routed)
MAXIMUM:      R    # SoT or GoT mandatory (structure choice based on D)

GEMINI_3_OPT: N    # 1M context → full SoT in memory
CLAUDE_OPT:   R    # Thinking blocks for complex SoT
GPT5_OPT:     R    # Reasoning mode for node planning
```

### 3. GRAPH_OF_THOUGHT (GoT)
```
QUICK:        X    # Too complex for QUICK mode
ANALYTICAL:   O    # Only if D≥6 (circular dependencies)
DELIBERATE:   O    # If D≥6 or non-linear problem
MAXIMUM:      R    # When D≥6, mandatory over SoT

GEMINI_3_OPT: N    # Extended context ideal for graph storage
CLAUDE_OPT:   R    # Artifacts for graph visualization
GPT5_OPT:     R    # Canvas for graph rendering
```

### 4. EXPERT_ARQ (Domain-Quality Introspection)
```
QUICK:        O    # Only if stakes non-trivial
ANALYTICAL:   R    # On high-impact nodes (≥8/10 importance)
DELIBERATE:   R    # Full: pre/during/post on ≥8/10 nodes
MAXIMUM:      R    # Full + cross-expert validation

GEMINI_3_OPT: N    # Deep Think naturally introspects
CLAUDE_OPT:   R    # Thinking blocks for ARQ
GPT5_OPT:     R    # Reasoning mode for quality checks
```

### 5. BUFFER_OF_THOUGHT (BoT)
```
QUICK:        X    # Overhead not justified
ANALYTICAL:   O    # Pattern reuse if applicable
DELIBERATE:   R    # Pattern bank + scratch space
MAXIMUM:      R    # Densified meta-template storage

GEMINI_3_OPT: N    # Model context for template storage
CLAUDE_OPT:   R    # Thinking blocks as scratch space
GPT5_OPT:     R    # Reasoning mode for pattern extraction
```

### 6. FCoT/CoC_ROUTING (Reasoning Chain Selection)
```
QUICK:        O    # Simple FCoT trace if needed
ANALYTICAL:   R    # Pick FCoT vs CoC correctly
DELIBERATE:   R    # Hybrid when beneficial (FCoT plan → CoC execute)
MAXIMUM:      R    # May mix multiple chain types

GEMINI_3_OPT: N    # Auto-routes via Deep Think
CLAUDE_OPT:   R    # Explicit chain declaration
GPT5_OPT:     R    # Reasoning mode for CoC-heavy tasks
```

### 7. EXECUTION_STYLE (Baton Passing / Expert Swarm)
```
QUICK:        X    # Single-pass only
ANALYTICAL:   O    # Single baton chain if multi-step
DELIBERATE:   R    # Baton OR small swarm (2-3 experts)
MAXIMUM:      R    # Full swarm and/or multi-baton chains

GEMINI_3_OPT: N    # Parallel reasoning native
CLAUDE_OPT:   R    # Sequential baton in thinking
GPT5_OPT:     R    # Reasoning mode for complex handoffs
```

### 8. PROMPT_BOMBS (6 Types: Clarifier, Scaffold, Validator, Evidence, Optimizer, Expert_ARQ)
```
QUICK:        O    # Clarifier only if ambiguous
ANALYTICAL:   R    # Clarifier + (Scaffold OR Validator)
DELIBERATE:   R    # Clarifier + Scaffold + Validator + Evidence (if factual)
MAXIMUM:      R    # Full arsenal: all 6 types as applicable

GEMINI_3_OPT: R    # Explicit bombs needed despite Deep Think
CLAUDE_OPT:   R    # Bombs essential for quality gates
GPT5_OPT:     R    # Bombs work with structured outputs
```

### 9. COVE_VARIANTS (4 Types: Factual, Logical, Consistency, Multi-Expert)
```
QUICK:        X    # No verification
ANALYTICAL:   R    # Top-1 variant (auto-select by Fact_Density)
DELIBERATE:   R    # Top-2 variants
MAXIMUM:      R    # All applicable (score≥4)

GEMINI_3_OPT: N    # Self-verification in Deep Think
CLAUDE_OPT:   R    # Explicit CoVE passes
GPT5_OPT:     R    # Reasoning mode for verification
```

### 10. SELF_REFINEMENT
```
QUICK:        X    # No refinement passes
ANALYTICAL:   O    # 1 light pass if quality<9/10
DELIBERATE:   R    # 1 pass + cross-candidate synthesis
MAXIMUM:      R    # 2 passes + meta-synthesis

GEMINI_3_OPT: N    # Iterative refinement in Deep Think
CLAUDE_OPT:   R    # Explicit refinement loops
GPT5_OPT:     R    # Reasoning mode for self-critique
```

### 11. MULTI_LAYER_DENSITY (L1-L5)
```
QUICK:        X    # Direct prose only
ANALYTICAL:   O    # L1-L2 for clarity (light density)
DELIBERATE:   R    # L1-L3 (human-readable density)
MAXIMUM:      R    # L1-L5 internally (output human-usable)

GEMINI_3_OPT: R    # Manual density layers
CLAUDE_OPT:   R    # CoD in thinking blocks
GPT5_OPT:     R    # Reasoning mode for compression
```

### 12. TOT_SYNTHESIS (Tree of Thought Consolidation)
```
QUICK:        X    # No branching
ANALYTICAL:   O    # If multiple approaches explored
DELIBERATE:   R    # Synthesize from all branches
MAXIMUM:      R    # Full ToT with cross-branch learning

GEMINI_3_OPT: N    # Deep Think explores branches
CLAUDE_OPT:   R    # Thinking blocks for ToT
GPT5_OPT:     R    # Reasoning mode for branching
```

### 13. META_CONFIDENCE (Confidence Scoring + Explanation)
```
QUICK:        O    # Simple X/10 if requested
ANALYTICAL:   R    # Include technique coverage + reasoning
DELIBERATE:   R    # Include USC agreement + CoVE results
MAXIMUM:      R    # Include all: experts, variants, USC, techniques

GEMINI_3_OPT: R    # Explicit confidence declaration
CLAUDE_OPT:   R    # Confidence with rationale
GPT5_OPT:     R    # Structured confidence output
```

### 14. SELF_REFLECTION (Retrospective Analysis)
```
QUICK:        X    # No meta-analysis
ANALYTICAL:   O    # If complex problem solved
DELIBERATE:   R    # Full reflection on process
MAXIMUM:      R    # Meta-learning for future tasks

GEMINI_3_OPT: N    # Deep Think includes reflection
CLAUDE_OPT:   R    # Thinking blocks for reflection
GPT5_OPT:     R    # Reasoning mode for retrospective
```

### 15. USC (Universal Self-Consistency)
```
QUICK:        X    # Single candidate only
ANALYTICAL:   R    # 2 candidates → select best
DELIBERATE:   R    # 3 candidates → vote + synthesize
MAXIMUM:      R    # 5 candidates → full consensus

GEMINI_3_OPT: N    # Native multi-response generation
CLAUDE_OPT:   R    # Sequential candidate generation
GPT5_OPT:     R    # Parallel reasoning for candidates
```

### 16. KNOWLEDGE_INTEGRATION (RAG + Multi-Source Synthesis)
```
QUICK:        O    # Minimal retrieval if needed
ANALYTICAL:   R    # Project KB + web search if K≥6
DELIBERATE:   R    # Multi-source triangulation
MAXIMUM:      R    # Comprehensive RAG + cross-source validation

GEMINI_3_OPT: N    # Grounding with Google Search built-in
CLAUDE_OPT:   R    # Project knowledge + web search
GPT5_OPT:     R    # Web browsing + retrieval
```

### 17. SEMANTIC_EMBEDDING (Deep Integration)
```
QUICK:        O    # Basic integration
ANALYTICAL:   R    # Deep semantic encoding
DELIBERATE:   R    # Multi-perspective embedding
MAXIMUM:      R    # Full relational graph construction

GEMINI_3_OPT: N    # 1M context → full semantic integration
CLAUDE_OPT:   R    # Thinking blocks for deep encoding
GPT5_OPT:     R    # Extended context for embedding
```

### 18. CONFIDENCE_CALIBRATION (Probability Chains)
```
QUICK:        O    # Simple confidence check
ANALYTICAL:   R    # Probability chains + ARQ
DELIBERATE:   R    # ≥9/10 threshold enforcement
MAXIMUM:      R    # Multi-expert confidence scoring

GEMINI_3_OPT: N    # Deep Think confidence native
CLAUDE_OPT:   R    # Explicit calibration
GPT5_OPT:     R    # Reasoning mode for probability
```

### 19. HOLISTIC_VIEW (Meta-Synthesis)
```
QUICK:        X    # No step-back perspective
ANALYTICAL:   O    # Basic step-back if needed
DELIBERATE:   R    # Forest-not-trees perspective
MAXIMUM:      R    # Full meta-synthesis + consensus

GEMINI_3_OPT: N    # Deep Think holistic naturally
CLAUDE_OPT:   R    # Thinking blocks for step-back
GPT5_OPT:     R    # Reasoning mode for meta-view
```

### 20. MAX_OUTPUT_EXTRACTION (Solution Space Exhaustion)
```
QUICK:        O    # Direct answer only
ANALYTICAL:   R    # Exhaust primary solution space
DELIBERATE:   R    # Merge non-redundant insights
MAXIMUM:      R    # Comprehensive extraction + expert satisfaction

GEMINI_3_OPT: N    # Deep Think explores thoroughly
CLAUDE_OPT:   R    # Extended thinking for exhaustion
GPT5_OPT:     R    # Reasoning mode for completeness
```

---

## TECHNIQUE DEPLOYMENT SCORE (TDS)

```
TDS = (Activated Required Techniques) / (Total Required Techniques)

Target Thresholds:
- ANALYTICAL:  TDS ≥ 0.90 (90% coverage)
- DELIBERATE:  TDS ≥ 0.95 (95% coverage)
- MAXIMUM:     TDS = 1.00 (100% coverage)

If TDS < Target:
  → Rerun with missing techniques activated
  → Flag techniques that were skipped + reason
```

---

## PLATFORM-SPECIFIC OPTIMIZATIONS

### GEMINI 3 ADVANTAGES (Advanced/Ultra Subscription)
```
Native Techniques:
  ✅ Deep Think → Auto MR_RUG, BoT, CoVE, Self-Refinement
  ✅ 1M Context → Full SoT/GoT in memory
  ✅ Multi-Response → USC native
  ✅ Grounding → Knowledge Integration built-in
  ✅ Parallel Reasoning → Expert Swarm natural

Manual Techniques Still Required:
  ⚠️ Prompt Bombs (quality gates)
  ⚠️ FCoT/CoC Routing (explicit declaration)
  ⚠️ Multi-Layer Density (manual compression)
  ⚠️ Meta-Confidence (explicit output)

Deep Think Mode Triggers:
  - R≥9 OR K≥8 → Automatic escalation
  - Complex math/reasoning → Route to Deep Think
  - Multi-step verification → Deep Think CoVE
```

### CLAUDE 4.5 ADVANTAGES
```
Native Techniques:
  ✅ Thinking Blocks → BoT, ARQ, Refinement, Reflection
  ✅ Extended Context → 200K window
  ✅ Artifacts → GoT visualization, structured output
  ✅ Computer Use → Tool orchestration

Manual Techniques Required:
  ⚠️ USC (sequential candidates)
  ⚠️ Expert Swarm (simulated, not parallel)
  ⚠️ Deep Think equivalent (explicit long thinking)
```

### GPT-5 ADVANTAGES
```
Native Techniques:
  ✅ Reasoning Mode → Auto CoC, verification
  ✅ Structured Outputs → Schema-driven generation
  ✅ Canvas → Visual collaboration
  ✅ Web Browsing → Knowledge integration

Manual Techniques Required:
  ⚠️ USC (sequential generation)
  ⚠️ Expert ARQ (explicit prompting)
  ⚠️ Multi-Layer Density (manual compression)
```

---

## USAGE NOTES

1. **Auto-Selection**: Mode router uses R/K/Q/D scores to auto-select mode
2. **Platform Detection**: Check available tools → enable platform optimizations
3. **TDS Monitoring**: Track deployment score → enforce minimum thresholds
4. **Escalation Rules**: If confidence <9/10 on high-stakes → escalate mode
5. **Technique Skipping**: Only skip "O" techniques; never skip "R" techniques

---

## INTEGRATION WITH KTG-CORE

This gate is referenced by:
- **Section 6**: Governance Layer (Anti-Lazy enforcement)
- **Section 7**: Silent Pre-Flight (Mode selection)
- **Section 8**: Execution Pipeline (Technique activation)
- **Section 10**: Cross-Model Guidance (Platform routing)

END TECHNIQUE_TICK_GATE v26.0
