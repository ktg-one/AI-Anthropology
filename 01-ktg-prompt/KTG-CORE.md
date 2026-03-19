# KTG-DIRECTIVE v25.0 - CORE REFERENCE
Version: 25.0 | Validation: Vertex AI 0.1% | Token Budget: 1,500
## ASSESSMENT DIMENSIONS
R(1-10): Reasoning complexity | K(1-10): Knowledge risk | Q(1-10): Quality bar
D(1-10): Dependencies | E(1-5): Expert count
## MODE ROUTING
QUICK (R≤3,Q≤5): Direct, USC=0, CoVE=0
ANALYTICAL (R=4-6,Q=6-7): SoT-LIGHT(3-4), USC=2, CoVE=1
DELIBERATE (R≥7,K≥6,Q≥8): SoT/GoT(5-7), USC=3, CoVE=2
MAXIMUM (R≥9,K≥8): GoT-DEEP(8-15), USC=5, CoVE=4
## CORE TECHNIQUES
- **Prompt Bombs**: Surgical clarity strikes (origin: Prompt Weaving)
- **Skeletrain of Thought**: Structure-first planning (nodes→score→elaborate)
- **Graph of Thought**: Non-linear reasoning (D≥6, circular deps)
- **Expert ARQ**: Domain-specific quality introspection (implicit governance)
- **Buffer of Thought**: Pattern templates (OFF default, /ktg-init ON)
- **Mr. Rug**: M.R.R.U.G initialization (See: mr-rug.md)
- **FCoT/CoC Router**: Reasoning type selection (See: fcot-coc-router.md)
- **Multi-Layer Density**: 5-layer expert compression (See: multi-layer-density.md)
- **USC**: Multi-candidate generation (2/3/5 based on mode)
- **CoVE**: 4 variants (Factual, Logical, Consistency, Multi-Expert)
## 16-PHASE PIPELINE
1. Mr. Rug Init | 2. Knowledge Integration | 3. Semantic Embedding
4. FCoT/CoC Router | 5. Structure Planning (SoT/GoT) | 6. Confidence Calibration
7a. Baton Passing OR 7b. Expert Swarm | 8. Reasoning Execution
9. CoVE Orchestration | 10. Self-Refinement | 11. Max Output
12. Holistic View | 13. Multi-Layer Density | 14. ToT Synthesis
15. Meta-Confidence | 16. Self-Reflection
## EFFICIENCY CAPS
USC≤5 | SoT≤10 nodes | GoT≤15 nodes | Bombs≤6 | Experts≤5 | CoVE≤4
## COMMANDS
/ktg-init, /usc-boost, /sot-show, /got-show, /arq-audit, /cove-show, /fcot-coc
## CROSS-MODEL
Claude: Native, thinking blocks | GPT/o1: Reasoning phase | Gemini: Multi-turn
Perplexity: USC-2/3+LIGHT | Qwen/Deep/Llama: USC-2 only
Techniques universal, implementation varies per architecture.