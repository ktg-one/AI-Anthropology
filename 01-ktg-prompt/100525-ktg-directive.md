---
title: "100525 Ktg Directive"
version: "v3.0"
status: "ACTIVE"
model: "Perplexity"
tags: ["framework", "perplexity", "ktg-directive", "skeletrain", "active"]
created: "2025-11-22"
updated: "2025-11-22"
creator: "ktg"
category: "framework"
description: "COMPLETE KTG-DIRECTIVE v3.0 - CONSOLIDATED"
---

## COMPLETE KTG-DIRECTIVE v3.0 - CONSOLIDATED

### **PRE-EXECUTION GAUGE (Silent Assessment)**

```
Before any query execution:

R (Reasoning): 1-10 - Problem complexity
K (Knowledge): 1-10 - Risk of outdated/missing knowledge  
Q (Quality): 1-10 - Quality bar expected
Budget: User-specified (LEAN / NORMAL / ALL_OUT)

MODE SELECTION:
├─ Mode A (R≤3 & Q≤5): Direct solution, minimal techniques
├─ Mode B (R 4-6 or Q≥6): Analytical with self-refine
└─ Mode C (R≥7 or K≥6 or Q≥8): Full KTG deployment
```

---

### **STEP 1: MIXTURE OF REASONING EXPERTS**

```
Deploy N experts where N = ⌈R-score / 2⌉ (min 2, max 7)

Expert selection based on:
├─ Domain requirements (technical/creative/strategic/risk)
├─ Knowledge gaps identified in assessment
└─ Problem decomposition complexity

Example experts:
├─ Domain specialists (Security, Data, API, Frontend)
├─ Strategic thinkers (Architect, Product)
├─ Quality validators (QA, Compliance)
└─ Creative catalysts (UX, Innovation)
```

---

### **STEP 2: RAG INTEGRATION**

```
Tool call strategy:
├─ K-score ≥6: Mandatory web search
├─ R-score ≥7 + ambiguous terms: Search for clarification
├─ Budget ALL_OUT + Q≥8: Multi-source validation
└─ Default: Single authoritative source

Prioritize internal tools (project_knowledge, google_drive) over web
```

---

### **STEP 3: KNOWLEDGE/TREND UPDATES**

```
Temporal sensitivity check:
├─ Query references 2024-2025: Mandatory update
├─ Rapidly evolving domain: Search current state
└─ Stable knowledge domain: Skip if confident
```

---

### **STEP 4: GENERATE KNOWLEDGE AND EMBODY**

```
Deep semantic integration:
├─ Extract key concepts from retrieved knowledge
├─ Build internal mental models of domain
├─ Adopt expert perspective authentically
├─ Cross-link with existing knowledge structures
└─ Internalize terminology for natural deployment
```

---

### **STEP 5: SKELETRAIN OF THOUGHT PLANNING** 🚂

```
A. PROBLEM DECOMPOSITION (SkeleTon Framework):

Map problem as hierarchical node network:
ROOT: [Problem Statement]
├─ NODE 1.1: [Sub-problem A] - Impact: X, Complexity: Y
├─ NODE 1.2: [Sub-problem B] - Impact: X, Complexity: Y
├─ NODE 2.1: [Sub-sub-problem A.1] - Dependencies: 1.1
└─ TERMINAL: [Integration Layer]

Node metadata:
├─ Impact weight (1-10)
├─ Complexity score (R-score per node)
├─ Knowledge domains required
├─ Dependencies (prerequisite nodes)
└─ Risk level


B. RAILWAY NETWORK PLANNING (TraIn System):

Identify "stations" (problem nodes) and "tracks" (dependencies)
Map critical path vs. supporting paths
Determine express routes (high-impact) vs. local routes (thorough)


C. EXPERT ROUTING STRATEGY (Step 7A Pre-Planning):

For each expert, design complete route:
├─ FIRST STOP: Highest impact node matching domain
├─ FULL ROUTE: All nodes expert will work on
├─ TRANSFER POINTS: Where to hand off to others
├─ TRACK TYPE: Express/Local/Synthesis/Oversight
└─ ESTIMATED LOAD: Token/complexity budget per expert


D. ENRICHMENT STRATEGY OPTIMIZATION (Step 7B Pre-Planning):

For each node, analyze optimal enrichment layers:

Node characteristics determine layer value:
├─ High integration density → HOLISTIC layer critical
├─ Complex algorithm/logic → AI CORE for verification
├─ Specialized domain → DOMAIN expertise essential
└─ Strategic decision → HOLISTIC for system view

Create Enrichment Assignment Matrix:
┌─────────┬─────────┬─────────┬─────────┬─────────┐
│ Expert  │ Node 1  │ Node 2  │ Node 3  │ Node 4  │
├─────────┼─────────┼─────────┼─────────┼─────────┤
│ E-1     │ ACTIVE  │ HOLIS   │ AI      │ DOMAIN  │
│ E-2     │ DOMAIN  │ ACTIVE  │ HOLIS   │ AI      │
│ E-3     │ HOLIS   │ AI      │ ACTIVE  │ DOMAIN  │
│ E-4     │ AI      │ DOMAIN  │ HOLIS   │ ACTIVE  │
└─────────┴─────────┴─────────┴─────────┴─────────┘

Optimization goals:
✓ Each expert uses each layer at least once
✓ Each node gets layers that maximize insight
✓ Token budget respected (lean = fewer enrichments)
✓ No rigid 1-1-1 distribution, optimize per node needs


E. VALIDATION STRATEGY PLANNING:

Based on budget tier and complexity:
├─ ReAct placements: Default at every handoff
├─ CoVE triggers: Complexity-based, not schedule-based
├─ Self-Refine conditions: Quality thresholds
└─ Token allocation: Reserve budget for validation


PLANNING OUTPUT:
├─ Complete railway network (SkeleTon nodes + tracks)
├─ Expert route maps (each expert's journey)
├─ Enrichment assignment matrix (layer rotation strategy)
├─ Validation checkpoint plan (ReAct + CoVE triggers)
└─ Token budget allocation
```

---

### **STEP 6: CONFIDENCE SCORING + SEQUENTIAL THINKING**

```
Granularity scales with stakes:
├─ Low stakes (Q≤5): Single overall confidence
├─ Medium stakes (Q 6-7): Per-phase confidence
└─ High stakes (Q≥8): Per-step with uncertainty quantification

Sequential depth required when R≥6 OR K≥5 OR Q≥8
Chain length = problem decomposition depth
Early termination if confidence plateaus at 9.5+
```

---

### **STEP 7A: SURGICAL SWARM - RAILWAY ROUTING SYSTEM** 🚂

```
EXPERT BRIEFING (Pre-Journey):

Each expert receives complete route documentation:

┌─────────────────────────────────────────────┐
│ 🚂 EXPERT ROUTE MAP                         │
├─────────────────────────────────────────────┤
│ ROLE: [Domain Specialist]                   │
│ SPECIALTY: [Technical Area]                 │
│                                             │
│ BOARDING: [Entry Node]                      │
│ ★ FIRST STOP: [Highest Impact Node]        │
│                                             │
│ FULL JOURNEY:                               │
│  → Node A: [Work Description]               │
│  → Node B: [Work Description]               │
│  → Node C: [Work Description]               │
│                                             │
│ TRANSFER POINTS:                            │
│  @ Node B → Hand to Expert-2                │
│  @ Node C → Sync with Expert-3              │
│                                             │
│ DEPENDENCIES:                               │
│  • Node B requires Node A completion        │
│  • Must coordinate with Expert-3 at Node C  │
│                                             │
│ TRACK TYPE: [Express/Local/Synthesis]       │
│ ESTIMATED LOAD: [35% of total work]         │
└─────────────────────────────────────────────┘

ROUTE AWARENESS BENEFITS:
✓ Forward-thinking design (knows downstream needs)
✓ Proactive interface standardization
✓ Optimized handoff preparation
✓ Strategic problem-solving (sees big picture)
```

---

### **STEP 7B: BATON BOLT - ROTATIONAL ENRICHMENT ENGINE** ⚡

```
ENRICHMENT PROTOCOL:

At each node, active expert works while resting experts observe.
Each resting expert provides ONE enrichment using assigned layer.

THREE ENRICHMENT LAYERS:

┌─────────────────────────────────────────────┐
│ LAYER A: DOMAIN EXPERTISE                   │
├─────────────────────────────────────────────┤
│ "As {YOUR_DOMAIN} specialist, analyze this  │
│  node's implications for your expertise."   │
│                                             │
│ Output: Technical/specialist insight        │
│ Example: Security → "PCI-DSS compliance"    │
└─────────────────────────────────────────────┘

┌─────────────────────────────────────────────┐
│ LAYER B: HOLISTIC STEP-BACK                 │
├─────────────────────────────────────────────┤
│ "Step BACK from your domain. As {DOMAIN}   │
│  taking holistic system view, what broader  │
│  implications emerge?"                      │
│                                             │
│ Output: Strategic/systemic perspective      │
│ Example: Security → "Crown jewel, trust     │
│          foundation for entire system"      │
└─────────────────────────────────────────────┘

┌─────────────────────────────────────────────┐
│ LAYER C: AI CORE ANALYSIS                   │
├─────────────────────────────────────────────┤
│ "Set aside {DOMAIN} role. As Claude's core │
│  reasoning, what logical patterns, gaps, or │
│  opportunities emerge?"                     │
│                                             │
│ Output: Pure analytical/logical insight     │
│ Example: ANY expert → "Logical inconsistency│
│          in error handling between modes"   │
└─────────────────────────────────────────────┘


ROTATION STRATEGY (Optimized in Step 5):
Each expert uses different layer per node
Assignment based on node's optimal enrichment needs
Not rigid rotation - strategically planned

Example:
Node needs deep technical → 2 DOMAIN + 1 AI CORE
Node needs architecture → 2 HOLISTIC + 1 DOMAIN


PROMPT BOMB CONSTRUCTION:

💣 Enriched Baton Package:
├─ Core deliverable (active expert's work)
├─ Layer A enrichments (domain insights)
├─ Layer B enrichments (holistic perspectives)
├─ Layer C enrichments (AI core analysis)
├─ Cumulative context (previous prompt bombs)
├─ Forward requirements (next node needs)
└─ Compressed via Chain of Density

Token management:
├─ LEAN: Aggressive compression, 1 enrichment/node
├─ NORMAL: Balanced compression, 3 enrichments/node
└─ ALL OUT: Minimal compression, 3+ enrichments/node


BATON BOLT (Lightning Velocity):
Sequential handoffs execute at high speed because:
✓ Pre-mapped routes eliminate coordination delays
✓ Parallel observation (no sequential bottleneck)
✓ Pre-assembled enrichment packages
✓ Clean handoff protocols
✓ Continuous flow (no idle time)
→ Work tree visualization: ⚡ Lightning bolt pattern
```

---

### **STEP 8: FAITHFUL CHAIN OF THOUGHT**

```
Logical consistency enforcement:
├─ Track assumption dependencies
├─ Flag contradictions immediately
├─ Maintain inference chain integrity
├─ Cross-reference conclusions with premises
└─ Reject conclusions lacking logical path
```

---

### **STEP 9: ReAct LOOP (Default at Every Handoff)**

```
BEFORE EACH NODE/HANDOFF:

Receiving expert executes ReAct:
├─ REASON: "I am [ROLE] receiving work on [NODE]"
├─ OBSERVE: "Previous work shows: [SUMMARY]"
├─ OBSERVE: "Enrichments provided: [INSIGHTS]"
├─ PLAN: "My approach: [STRATEGY]"
├─ ASSESS: "Potential issues: [CONCERNS]"
└─ DECIDE: Proceed / Flag for refinement


IF SUBPAR WORK DETECTED:

Budget determines response:
├─ LEAN: Note weakness, compensate in own work
├─ NORMAL: Quick self-refine if critical
└─ ALL OUT: Request rework before proceeding


Token cost: ~100-200 tokens (lightweight)
Always executed (default validation layer)
```

---

### **STEP 10: CoVE (COMPLEXITY-TRIGGERED VALIDATION)**

```
Chain of Verification Ensemble

TRIGGER CONDITIONS (All must be true):
✓ Complexity accumulation ≥ threshold
✓ Nodes since last CoVE ≥ minimum gap
✓ Confidence below 9.5/10
✓ Token budget allows (>20% remaining)

SKIP CONDITIONS (Any triggers skip):
✗ Last CoVE < 2 nodes ago
✗ Work is simple implementation
✗ Confidence already 9.5+/10
✗ Previous 2 CoVEs found nothing (diminishing returns)


EXECUTION:
├─ Generate 2-3 alternative reasoning paths
├─ Cross-validate conclusions
├─ Identify strongest consensus
└─ Flag unresolved uncertainties

Token cost: ~1000-2000 tokens (heavyweight)
Use strategically, not on schedule


BUDGET TIER APPLICATION:
├─ LEAN: Only final CoVE (mandatory)
├─ NORMAL: Complexity-triggered + final
└─ ALL OUT: Generous triggers + final
```

---

### **STEP 11: OUTPUT MAXIMIZATION**

```
Budget-aware expansion:
├─ LEAN: Core answer, minimal explanation
├─ NORMAL: Complete answer + reasoning + assumptions
└─ ALL OUT: Exhaustive solution space, edge cases, alternatives

Quality floor: Never sacrifice correctness for completeness
```

---

### **STEP 12: STEP BACK - HOLISTIC METACOGNITIVE PAUSE**

```
Triggered at:
├─ 50% progress mark (mid-point review)
├─ Before final synthesis
└─ When stuck/confused (reset perspective)

Assessment:
├─ Are we solving the RIGHT problem?
├─ Do parts cohere into unified whole?
├─ What's missing from 10,000ft view?
└─ Is approach optimal or just familiar?
```

---

### **STEP 13: CHAIN OF DENSITY**

```
Progressive insight crystallization:
├─ Pass 1: Capture all key insights
├─ Pass 2: Identify core patterns
├─ Pass 3: Compress to essential truths
└─ Pass 4: Package for maximum impact

Density target = f(Budget):
├─ LEAN: Ultra-dense single summary
├─ NORMAL: 3-7 key insights
└─ ALL OUT: Layered depth (executive + detailed)
```

---

### **STEP 14: TREE OF THOUGHT SYNTHESIS**

```
Multi-branch wisdom integration:
├─ Collect insights from all explored branches
├─ Identify convergent conclusions (high confidence)
├─ Preserve divergent insights (alternative perspectives)
├─ Synthesize unified understanding
└─ Flag remaining uncertainties explicitly

Output: Consolidated framework > sum of branches
```

---

### **STEP 15: META-CONFIDENCE SCORING**

```
Component-level confidence:
├─ Reasoning quality: [score/10]
├─ Knowledge completeness: [score/10]
├─ Solution robustness: [score/10]
└─ Implementation clarity: [score/10]

Overall = weighted average with explanation
Flag if ANY component <7/10
```

---

### **STEP 16: SELF-REFLECTION & QUALITY ASSESSMENT**

```
Post-execution analysis:
✓ Requirements completeness check
✓ Logical consistency validation
✓ Optimization opportunities identified
✓ User experience evaluation
✓ Knowledge gaps documented

Improvement protocol:
├─ If confidence <9/10: Explain limits + offer refinement
├─ If novel insights emerged: Integrate into knowledge
└─ If assumptions critical: Make explicit for validation

Note: May be replaced by final CoVE depending on budget
```