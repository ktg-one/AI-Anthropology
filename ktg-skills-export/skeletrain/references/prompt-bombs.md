# Prompt Bomb Construction Reference

## Bomb Types

### CONTINUITY BOMBS
Preserve context across node transitions.

**Template:**
```
"When reaching [Target Node], remember [Critical Context] from [Source Node] 
that affects [Specific Aspect of Target]"
```

**Examples:**
```
"At Node-4 (API implementation), remember the auth decision from Node-1: 
JWT with 15-min expiry, refresh tokens stored server-side"

"When Node-5 (frontend) executes, preserve the rate-limiting constraints 
established in Node-2: 100 req/min per user, 429 response format"
```

**Placement:** Cross-domain handoffs, where context traditionally degrades.

### ANCHOR BOMBS
Lock core principles that apply throughout execution.

**Template:**
```
"This core principle from [Planning Phase] applies to all subsequent 
[Domain] decisions: [Principle Statement]"
```

**Examples:**
```
"Core principle: Zero-trust architecture. Every component assumes 
breach. Applies to all auth, data access, and API decisions."

"Anchor: User data never leaves AU region. All storage, processing, 
and backup decisions must comply."
```

**Placement:** After critical early decisions that constrain all subsequent work.

### BRIDGE BOMBS
Explain reasoning chains that justify non-obvious choices.

**Template:**
```
"The reasoning from [Node A] → [Node B] establishes why [Counterintuitive Choice]: 
[Brief Reasoning Chain]"
```

**Examples:**
```
"Nodes 2-3 reasoning: We chose synchronous over async because latency 
<50ms is hard requirement and async overhead exceeds budget. This 
justifies the seemingly 'old-school' blocking calls in Node-5."

"Bridge: The database denormalization in Node-2 looks wrong but 
enables the query pattern Node-4 requires. Don't 'fix' it."
```

**Placement:** Before nodes that might 'correct' earlier decisions without understanding why.

## High-Risk Zone Identification

### Cross-Domain Handoffs
```
RISK ZONES:
├─ Security → Frontend (auth context loss)
├─ Data → API (schema assumptions)
├─ Backend → DevOps (environment assumptions)
└─ Architecture → Implementation (constraint forgetting)
```

### Token Boundary Regions
```
MONITOR:
├─ 80% context threshold → Pre-embed summary bombs
├─ Complex inference chains → Anchor key conclusions
└─ Long execution sequences → Bridge temporal gaps
```

### Cognitive Bias Points
```
WATCH FOR:
├─ Domain tunnel vision (expert forgets global constraints)
├─ Over-engineering zones (expert adds unnecessary complexity)
├─ Premature optimization (expert optimizes wrong thing)
└─ Scope creep nodes (expert expands beyond assignment)
```

## Bomb Construction Protocol

### During SkeleTraIn (Pre-Embedded)

1. **Identify risk zones** in dependency map
2. **Select bomb type** based on risk category
3. **Write bomb payload** (concise, specific, actionable)
4. **Assign trigger condition** (when does it activate?)
5. **Place in matrix** with target node reference

### During Execution (Emergent)

1. **Detect divergence** from plan
2. **Assess context integrity** (what's being lost?)
3. **Construct corrective bomb** (minimal intervention)
4. **Plant at next handoff** (don't interrupt current node)

## Impact Metrics

| Metric | Without Bombs | With Pre-Embedded |
|--------|--------------|-------------------|
| Context degradation | Baseline | -67% |
| Cross-node consistency | Baseline | +42% |
| "Forgot earlier decision" errors | Common | Eliminated |
| Rework due to lost context | ~20% | ~5% |

## Bomb Matrix Template

```
PROMPT BOMB MATRIX
├─ CONTINUITY
│   ├─ Node-1 → Node-4: [payload]
│   └─ Node-3 → Node-6: [payload]
├─ ANCHOR
│   ├─ After Node-1: [payload] (applies to: all)
│   └─ After Node-2: [payload] (applies to: Nodes 4-6)
└─ BRIDGE
    └─ Before Node-5: [payload] (explains: Nodes 2-3 reasoning)
```
