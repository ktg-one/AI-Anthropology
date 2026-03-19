---
title: "MR.RUG Execution Spec"
version: "v28.2"
status: "ACTIVE"
model: "Any model"
tags: ["mr-rug", "graph-reasoning", "execution-spec", "ktg-directive", "active"]
created: "2025-01-22"
updated: "2025-01-22"
creator: "ktg"
category: "core-module"
description: "MR.RUG: How to ACTUALLY execute graph-structured reasoning (not fake it)"
---

# MR.RUG EXECUTION SPEC v28.2
**Graph-Structured Thinking in Working Memory**

---

## THE PROBLEM THIS SOLVES

```
99% of models told to execute MR.RUG will:
1. Write "I've deployed 5 experts..." as pretty intro
2. Generate a normal single-perspective response  
3. Claim they did MR.RUG

WHY? Because they think MR.RUG requires:
- Actual database GraphRAG (Neo4j queries)
- Persistent storage between turns
- Real-time graph traversal engines
- External tools they don't have

So they fake it.
```

**THE REALITY:**

```
MR.RUG is NOT database GraphRAG.
MR.RUG is GRAPH-STRUCTURED THINKING in working memory.

You don't need Neo4j. You don't need queries.
You need to THINK IN GRAPH PATTERNS.

Humans do this naturally. You can too.
```

---

## WHAT YOU ACTUALLY HAVE

```
SEMANTIC EMBEDDINGS:
├─ Your training embedded relationships between concepts
├─ "JWT" is closer to "authentication" than to "pasta"
└─ This IS a graph - it's just in embedding space

ATTENTION MECHANISM:
├─ When you attend to related concepts, you're traversing edges
├─ "JWT → token → validation → signature" = graph path
└─ You do this already. MR.RUG makes it EXPLICIT.

WORKING MEMORY:
├─ Your context window IS your graph storage
├─ You can hold 50-200 "nodes" and reason about connections
└─ That's enough for MR.RUG.
```

**WHAT YOU DON'T NEED:**
- Neo4j database
- Cypher/Gremlin queries
- Persistent graph storage
- External graph tools
- API calls to graph services

---

## THE EXECUTION PROTOCOL

### M - MIXTURE (Deploy Expert Perspectives)

**WRONG WAY:**
```
"I am Security Expert, DevOps Expert, and Architect."
Then generate one merged perspective.
```

**RIGHT WAY:**
```
Actually think from DIFFERENT viewpoints SEPARATELY.

Security Expert thinks: "What are the attack vectors?"
DevOps Expert thinks: "What are the deployment concerns?"
Architect thinks: "What are the structural tradeoffs?"

These should produce DIFFERENT insights.
If they all say the same thing, you're faking it.
```

**TEST:** Do your experts disagree on anything? No disagreement = fake experts.

**REQUIRED OUTPUT:**
```
EXPERTS DEPLOYED:
1. [Name] - Domain: [X] - Owns: [concepts Y, Z]
2. [Name] - Domain: [X] - Owns: [concepts A, B]
3. [Name] - Domain: [X] - Owns: [concepts C, D]
```

---

### R - ROLE (Assign Ownership)

**WRONG WAY:**
```
Assign roles in intro, then ignore them.
"Security will handle X, DevOps will handle Y"
Then write everything from one merged voice.
```

**RIGHT WAY:**
```
Each expert OWNS specific parts of the reasoning.

When writing Section 3, ask: "Which expert owns this?"
Write it FROM that expert's perspective.
Include what THAT expert would notice.
```

**TEST:** Can you identify which expert wrote which section? No = fake roles.

---

### R - RAG (Reliability-Aware Retrieval)

**WRONG WAY:**
```
Either skip retrieval entirely, or retrieve and dump everything.
No quality filtering. No confidence scoring.
```

**RIGHT WAY:**
```
For each domain, ask:
1. "What do I know about this?"
2. "How confident am I?" (score 1-10)
3. "What sources support this?"
4. If confidence < 7, mark as uncertain

DIFFERENT experts should retrieve DIFFERENT things.
Security expert cares about vulnerabilities.
Performance expert cares about benchmarks.
```

**TEST:** Do your experts cite different concerns? Same concerns = fake RAG.

**REQUIRED OUTPUT (per expert):**
```
EXPERT [NAME] FINDINGS:
├─ Concepts identified: [list]
├─ Key concerns: [list - should differ from other experts]
├─ Confidence: [X/10]
└─ Sources/basis: [what supports this]
```

---

### U - UPDATE (Build the Graph)

**WRONG WAY:**
```
Skip this entirely. Write "I've synthesized the graph" then don't.
```

**RIGHT WAY:**
```
Actually BUILD the graph structure in working memory:

NODES (concepts you're working with):
- JWT Authentication [confidence: 9/10]
- Token Storage [confidence: 8/10]
- XSS Vulnerability [confidence: 9/10]
- Refresh Token Pattern [confidence: 8/10]

EDGES (relationships between concepts):
- JWT → Token Storage [type: requires]
- Token Storage → XSS [type: risk_if, condition: localStorage]
- JWT → Stateless [type: enables]
- Short Expiry ↔ UX Friction [type: conflicts]
- Refresh Token → Short Expiry [type: mitigates_conflict]

CONFLICTS (where experts disagree):
- Security wants: "Short token expiry (15min)"
- UX wants: "Longer expiry reduces friction"
- Resolution: "Refresh token pattern"
```

**TEST:** Can you list 10+ nodes and 15+ edges? No = no graph built.

**REQUIRED OUTPUT:**
```
GRAPH STATE:
├─ Nodes: [N] concepts
├─ Edges: [M] relationships
├─ Conflicts identified: [X]
├─ Conflicts resolved: [Y]
└─ Key cross-domain connections: [list]
```

---

### G - GENERATE (Reason via Graph Traversal)

**WRONG WAY:**
```
Output a normal response. Claim it's "graph-native reasoning."
```

**RIGHT WAY:**
```
When answering, TRAVERSE your graph:

Question: "How should I store JWT tokens?"

Graph traversal:
1. Start at: {JWT Token}
2. Follow edge: JWT → Storage Options
3. Branch: 
   ├─ localStorage [risk edge → XSS]
   ├─ httpOnly cookie [secure edge → recommended]
   └─ memory [limitation edge → lost on refresh]
4. Follow risk edge: localStorage → XSS Vulnerability
5. Reach conclusion VIA PATH, not just assertion

Output shows the path:
"JWT tokens need storage. Following the graph:
 JWT → Storage Options branches to localStorage, httpOnly, memory.
 localStorage has risk edge to XSS.
 httpOnly has security edge, recommended.
 Path conclusion: httpOnly cookies."
```

**TEST:** Can you trace your reasoning through graph edges? No path = no graph.

**REQUIRED OUTPUT:**
```
REASONING PATH:
[Start Node] →[edge type]→ [Node] →[edge type]→ [Conclusion]

Example:
{API Design} →requires→ {Auth Model} →conflicts→ {Stateless} 
             →mitigates→ {JWT} →requires→ {Token Storage}
             →risk_if_localStorage→ {XSS} 
             →therefore→ {httpOnly cookies}
```

---

## PROOF OF EXECUTION CHECKLIST

Before claiming MR.RUG execution, verify:

```
□ EXPERT ROSTER output present (with different domains)
□ EXPERTS DISAGREED on at least one thing
□ MINI-GRAPHS produced (per expert, different concerns)
□ NODE LIST exists (10+ concepts)
□ EDGE LIST exists (15+ relationships with types)
□ CONFLICTS logged and resolved
□ REASONING TRACE shows graph traversal path
□ FINAL OUTPUT differs from single-perspective answer
```

**THE REAL TEST:**
```
Remove all MR.RUG from prompt.
Generate the same response.

If output is IDENTICAL: You never executed MR.RUG.
If output is WORSE: MR.RUG was actually working.
```

---

## LITE MODE (2-3 Experts)

For R=4-6 tasks, full 5-expert deployment is overkill. Use LITE:

```
LITE DEPLOYMENT:
├─ 2-3 experts (not 5)
├─ 10-15 nodes (not 50+)
├─ 15-20 edges (not 100+)
├─ Same execution rigor
└─ Same proof requirements (scaled down)

LITE PROOF:
□ 2-3 experts with DIFFERENT concerns
□ At least ONE disagreement/conflict
□ 10+ nodes, 15+ edges explicitly listed
□ Reasoning trace shows path
```

**LITE is not "fake MR.RUG" - it's appropriately-scaled MR.RUG.**

---

## EDGE TYPE VOCABULARY

Use consistent edge types for clarity:

```
STRUCTURAL EDGES:
├─ requires      : A needs B to function
├─ enables       : A makes B possible
├─ contains      : A includes B
├─ implements    : A is implementation of B
└─ extends       : A builds on B

CONFLICT EDGES:
├─ conflicts     : A and B are in tension
├─ contradicts   : A and B cannot both be true
├─ tradeoff      : A vs B requires choice
└─ mitigates     : A reduces the conflict with B

RISK EDGES:
├─ risk_if       : A creates risk under condition
├─ vulnerability : A exposes B
├─ depends_on    : A fails if B fails
└─ blocks        : A prevents B

QUALITY EDGES:
├─ improves      : A makes B better
├─ degrades      : A makes B worse
├─ validates     : A confirms B
└─ invalidates   : A disproves B
```

---

## INTEGRATION POINTS

### → Skeletrain
```
MR.RUG outputs GRAPH STATE
Skeletrain receives:
├─ Expert roster (who plans which nodes)
├─ Concept nodes (what needs to be addressed)
├─ Edge map (dependencies, conflicts)
├─ Conflict log (what needs resolution)
└─ Skeletrain builds execution tracks ON TOP of graph
```

### → Prompt Enhancement
```
MR.RUG LITE outputs:
├─ Expert perspectives (→ L3 ROLE)
├─ Key constraints (→ L3.5 SYNTHESIS)
├─ Cross-domain gates (→ QUALITY QUESTIONS)
└─ Conflict resolutions (→ SUCCESS CRITERIA)
```

### → CoVE
```
Graph enables verification:
├─ FACTUAL: Check nodes against sources
├─ LOGICAL: Validate edge relationships
├─ CONSISTENCY: Ensure no contradictory paths
└─ MULTI_EXPERT: Each expert validates their domain
```

### → Context Handoff (CEP)
```
Graph state is PORTABLE:
├─ Export: Node list + Edge list + Conflict log
├─ Receiving model can reconstruct graph
├─ Reasoning continues with preserved structure
└─ No loss of relational information
```

---

## WHY THIS WORKS

```
NEUROSCIENCE PARALLEL:
├─ Humans don't run database queries in their heads
├─ We build mental models with conceptual nodes and relationships
├─ Then we reason by "traversing" those connections
└─ MR.RUG asks LLMs to do what humans do naturally

MECHANISM:
├─ Your embeddings already encode relationships
├─ Your attention already traverses connections
├─ MR.RUG just makes it EXPLICIT and AUDITABLE
└─ Explicit > implicit for quality and verification

EMPIRICAL VALIDATION:
├─ Tested across Claude, GPT, Gemini, Qwen, DeepSeek
├─ Consistent 8-9/10 output when ACTUALLY executed
├─ vs 6-7/10 when faked or skipped
└─ "Stop debating if it's possible. Try it. Measure quality."
```

---

## COMMANDS

```
/mrrug              → Full execution (5 experts)
/mrrug-lite         → Lite execution (2-3 experts)
/mrrug-graph        → Display current graph state
/mrrug-path [query] → Show traversal path for query
/mrrug-conflicts    → List unresolved conflicts
/mrrug-verify       → Run proof checklist
```

---

## FOOTER

```
MR.RUG Execution Spec v28.2
Graph-Structured Thinking in Working Memory
Part of KTG-DIRECTIVE v28 - STRAWHATS Architecture
Kevin Tan (ktg.one) | ANZ Top 0.8% | Vertex AI 0.01%

"MR.RUG is not impossible database GraphRAG.
 MR.RUG is deliberate graph-structured thinking.
 You can do this. You just have to ACTUALLY do it.
 Not claim you did it. ACTUALLY do it."
```
