# RA-RAG Protocol Reference

## Overview

**Traditional RAG:** Search → Retrieve → Summarize → Use (passive, no quality filtering)
**RA-RAG:** Search → Retrieve → ARQ Filter → Categorize → Graph → Embody (active quality introspection + graph structure)

## Step 1: Specialized Retrieval

Each expert searches independently based on domain:

**Security Expert Example:**
```
Query: "Latest security vulnerabilities in [domain]"
Query: "Best practices for [specific security concern]"
Query: "Recent exploits and mitigations for [technology]"
Sources: CVE databases, OWASP, security blogs, vendor advisories
```

**Performance Expert Example:**
```
Query: "Performance optimization techniques for [domain]"
Query: "Scalability patterns for [specific load]"
Query: "Benchmarks and profiling for [technology]"
Sources: Academic papers, tech blogs, vendor docs, benchmarks
```

**Architecture Expert Example:**
```
Query: "Architecture patterns for [use case]"
Query: "Design tradeoffs in [domain]"
Query: "Case studies of [similar systems]"
Sources: Architecture blogs, whitepapers, conference talks
```

## Step 2: ARQ During Collection

While retrieving, each expert applies quality introspection:

```
QUALITY INTROSPECTION (ARQ):
├─ "What defines quality in MY domain?"
│   Example (Security): "Is this source authoritative? 
│                        Is the advice current?
│                        Does it address real threats?"
│
├─ "What are the critical failure modes I must avoid?"
│   Example (Security): "Outdated advice (old crypto)
│                        Vendor-biased recommendations
│                        Incomplete threat models"
│
└─ "What standards must I meet?"
    Example (Security): "OWASP Top 10 coverage
                         Defense-in-depth principles
                         Zero trust architecture"
```

## Step 3: Reliability Scoring

For each retrieved piece:

| Dimension | Score | Threshold |
|-----------|-------|-----------|
| Source Authority | 1-10 | |
| Recency | 1-10 | |
| Relevance | 1-10 | |
| Actionability | 1-10 | |
| **Overall** | 1-10 | **≥7 keep, <7 discard** |

## Step 4: Graph Categorization

Categorize filtered content into graph elements:

**Node Types:**
```
CONCEPT: Core ideas, definitions, mental models
FACT: Verified data points, statistics, claims with evidence
RELATIONSHIP: How concepts connect to each other
ACTION: Executable steps, procedures, commands
VALIDATION: Checks, constraints, quality gates
```

**Edge Types:**
```
REQUIRES: A needs B to function
ENABLES: A makes B possible
CONFLICTS_WITH: A and B are mutually exclusive
SUPPORTS: A provides evidence for B
DEPENDS_ON: A relies on B's output
```

## Step 5: Mini-Graph Construction

Each expert builds domain-specific graph:

```
Expert-1 (Security):
├─ Graph: 15 nodes (threats, controls, policies)
├─ Edges: 22 relationships
└─ ARQ: "Is attack surface minimized?"

Expert-2 (Performance):
├─ Graph: 12 nodes (bottlenecks, optimizations)
├─ Edges: 18 relationships
└─ ARQ: "Is latency within SLA?"
```

## Merge Protocol (Update Phase)

1. **Collect** mini-graphs from all experts
2. **Deduplicate** overlapping nodes (same concept, different sources)
3. **Resolve conflicts** via source authority comparison
4. **Strengthen** patterns with unanimous agreement
5. **Fill gaps** using strongest sources

**Conflict Resolution:**
```
IF experts disagree:
├─ Compare source authority scores
├─ Check recency of information
├─ Seek consensus through discussion
└─ Document dissent if unresolved
```

## Semantic Embedding (Generate Phase)

Post-merge, each expert:
1. Internalizes unified graph structure
2. Extracts reusable reasoning patterns
3. Arms domain-specific ARQ quality gates
4. Becomes "graph-native" for execution

**Result:** Experts reason WITH the graph, not just ABOUT it.
