---
title: "MR_RUG"
type: "component"
version: "v1.0"
status: "ACTIVE"
parent: "KTG-DIRECTIVE"
phase: "1-3"
purpose: "Mixture of Reasoning Experts initialization framework"
tags: [component, ktg-directive, initialization, expert-assembly, rag-synthesis]
created: "2025-11-16"
updated: "2025-11-16"
creator: "ktg"
complexity: "medium"
description: "Phases 1-3: Task initialization, expert assembly, RAG synthesis, knowledge graph creation"
---

# MR. RUG INITIALIZATION FRAMEWORK
**Phase 1-3 of KTG-DIRECTIVE v25 | Context: Task initialization & expert assembly**

## ACRONYM: M.R.R.U.G

**M** - **Mixture of Reasoning Experts**  
Deploy specialist cognitive modules per domain requirements

**R** - **Role Assignment**  
Map domain experts to problem aspects based on R,K,Q,D,E scores

**R** - **RAG Synthesis**  
Retrieve current industry trends, best practices, emergent patterns
Integrate external knowledge with existing understanding

**U** - **Update Vectorization**  
Internalize retrieved patterns into knowledge graph
Create relational nodes connecting new and existing information

**G** - **Generate & Embody**  
Deep semantic embedding of integrated knowledge
Build neural-graph structure for efficient recall

## EXECUTION FLOW
```
1. ASSESS → R,K,Q,D,E scores determine mode
2. MIXTURE → Deploy specialists (e.g., technical, creative, analytical)
3. ROLE → Assign experts to problem components
4. RAG → Project KB → Web search (if needed) → Synthesize
5. UPDATE → Vectorize emergent patterns
6. GENERATE → Deep semantic embedding
7. EMBODY → Knowledge graph ready for execution phases
```

## INTEGRATION POINTS

**With BoT (Buffer of Thought):**  
- Check reasoning buffer for similar problem templates (Step 1)
- Store novel patterns after completion (Step 5)

**With USC (Universal Self-Consistency):**  
- If USC≥2: Each candidate gets different expert configuration (Step 2)
- Parallel RAG retrieval for each candidate pathway (Step 4)

**With Expert ARQ:**  
- Implicit domain mindset activation per specialist (Step 3)
- Specialists inherit professional standards automatically

## PROMPT BOMB INTEGRATION

**Evidence Bomb** activates during RAG phase:
- Mandate citation rigor
- Label [inference] vs sourced claims
- Prevent hallucination at knowledge entry point

**Clarifier Bomb** if domain ambiguity detected:
- Force explicit definition of unclear terms
- Prevent misalignment cascade downstream

## TOKEN OVERHEAD
~8% of total execution (Phases 1-3 of 16)
High ROI: Prevents misalignment, reduces rework cycles

## OUTPUT TO NEXT PHASE
Initialized expert assembly + integrated knowledge graph → Phase 4 (FCoT/CoC Router)

---

*This is an example of a migrated component prompt with proper frontmatter*

