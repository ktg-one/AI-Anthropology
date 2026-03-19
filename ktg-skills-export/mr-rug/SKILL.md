---
name: mr-rug
description: MR.RUG (Mixture of Reasoning + Agentic GraphRAG) framework for deploying specialized reasoning experts who build unified knowledge graphs through Reliability-Aware RAG. Use when tasks require multi-expert collaboration, complex analysis needing 3+ perspectives, research synthesis, technical system design, or any R≥4 complexity task. Triggers on expert deployment, knowledge graph construction, RA-RAG retrieval, multi-domain synthesis, or when KTG-DIRECTIVE v28 Phase 1 is invoked.
---

# MR.RUG Framework v28
**Phase 1 of KTG-DIRECTIVE | Expert deployment + Knowledge graph construction**

Deploy specialized reasoning experts who build a unified knowledge graph through Reliability-Aware RAG, then semantically embed that graph into their cognitive architecture.

## Architecture: M.R.R.U.G

| Phase | Component | Action |
|-------|-----------|--------|
| **M** | Mixture | Deploy experts based on mode |
| **R** | Role | Assign domains + handoff routes |
| **R** | RAG | RA-RAG retrieval with ARQ filtering |
| **U** | Update | Merge mini-graphs, resolve conflicts |
| **G** | Generate | Semantic embedding + expert embodiment |

## Expert Deployment

**By Mode:**
- QUICK (R≤3): 0 experts (direct answer)
- ANALYTICAL (R=4-6): 3 experts (core specialists)
- DELIBERATE (R≥7): 5 experts (full team)
- MAXIMUM (R≥9): 5-8 experts (model-dependent)

**Expert Profile Template:**
```
Name: [Role identifier]
Domain: [Area of expertise]
Responsibility: [Accountable deliverables]
ARQ Standards: [Quality criteria for domain]
Tools: [Available resources]
Success Metric: [Measurable outcome]
```

## Expert Archetypes

See [references/archetypes.md](references/archetypes.md) for complete expert patterns:
- Technical (Architect, Implementation, Security, Performance, DevOps)
- Analytical (Domain, Research, Data Science, Strategic, QA)
- Creative (Director, Execution, Editor, Audience, Innovation)
- Cross-Domain (Integration, Translation, Synthesis)

## Role Assignment

**Execution Patterns:**

**Baton Passing (Sequential):**
```
Expert-1: Node-1 → Node-3 → Node-5
Expert-2: Node-2 → Node-4
Handoff: Expert-1 output → Expert-2 input
```

**Expert Swarm (Parallel):**
```
Self-assignment based on specialty
Dynamic collaboration on complex nodes
No fixed routes
```

**Permissions:**
- Read: Full task context
- Write: Assigned nodes only
- Consult: Other experts
- Enrich: Parallel commentary
- Cannot: Override domains without consensus, skip ARQ gates, proceed with confidence <9/10

## RA-RAG Protocol

**Traditional RAG:** Search → Retrieve → Summarize → Use
**RA-RAG:** Search → Retrieve → ARQ Filter → Categorize → Graph → Embody

**Per Expert:**
1. **Specialized Retrieval** - Domain-specific queries
2. **ARQ During Collection** - Quality introspection while retrieving
3. **Reliability Scoring** - Source Authority, Recency, Relevance, Actionability (keep ≥7/10)
4. **Graph Categorization** - Concepts, Facts, Relationships, Actions, Validations

See [references/ra-rag-protocol.md](references/ra-rag-protocol.md) for detailed retrieval patterns.

## Knowledge Graph Construction

**Node Types:**
- CONCEPT: Core ideas, definitions
- FACT: Verified data points
- RELATIONSHIP: How concepts connect
- ACTION: Executable steps
- VALIDATION: Checks, constraints

**Edge Types:** REQUIRES, ENABLES, CONFLICTS_WITH, SUPPORTS, DEPENDS_ON

**Merge Protocol:**
1. Collect mini-graphs from all experts
2. Identify overlapping nodes (same concept, different sources)
3. Resolve conflicts via source comparison
4. Strengthen unanimous patterns
5. Fill gaps from strongest sources

## Semantic Embedding (Generate Phase)

Post-graph construction, each expert:
1. Internalizes unified graph structure
2. Extracts reusable reasoning patterns → BoT (if R≥6)
3. Arms domain-specific ARQ quality gates
4. Becomes ready for execution with full knowledge

## Verbose Mode

Trigger `/ktg-verbose` for execution trace:
```
=== MR.RUG EXECUTION TRACE ===
[M] MIXTURE DEPLOYMENT: Mode, experts deployed
[R] ROLE ASSIGNMENT: Expert→Node mappings
[R] RA-RAG RETRIEVAL: Queries, docs, filter stats, graph size
[U] GRAPH MERGE: Total nodes/edges, conflicts resolved, gaps filled
[G] SEMANTIC EMBEDDING: Patterns extracted, ARQ armed
=== MR.RUG COMPLETE ===
```

## Best Practices

**DO:**
- Match expert count to complexity
- Use RA-RAG for domains needing current knowledge
- Let experts build independent mini-graphs first
- Resolve conflicts with source citations
- Embed ARQ into expert cognition
- Save patterns to BoT (if R≥6)

**DON'T:**
- Deploy too many experts for simple tasks
- Skip RA-RAG phase
- Force premature consensus
- Ignore graph gaps
- Proceed without ARQ activation

## Timing

| Phase | Duration |
|-------|----------|
| Expert deployment | Instant |
| RA-RAG retrieval | 30-60s per expert (parallel) |
| Graph synthesis | 10-20s |
| Semantic embedding | 5-10s |
| **Total MR.RUG** | ~60-90s (3-5 experts) |

**Downstream savings:** Structure planning 50% faster, execution 30% faster, verification 40% faster.

---
*MR.RUG v28 | Part of KTG-DIRECTIVE v28 | Kevin Tan (ktg.one)*
