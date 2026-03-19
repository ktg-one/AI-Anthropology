---
title: "Success Criteria Lock + Intelligent Routing Bypass + Iteration Protocol"
version: "v28.1"
status: "ACTIVE"
model: "Multi-model"
tags: ["routing", "success-criteria", "optimization", "iteration", "stress-reduction", "ktg-directive", "active"]
created: "2025-12-03"
updated: "2025-12-03"
creator: "ktg"
category: "core-technique"
description: "Pre-execution success definition + intelligent phase skipping + structured 3-iteration protocol to reduce model cognitive load"
---

# SUCCESS CRITERIA LOCK + ROUTING BYPASS + ITERATION PROTOCOL
**Phase 1.5 of KTTT v1 | Context: Define done, route intelligently, iterate strategically**

## PURPOSE
1. Lock the definition of "success" BEFORE execution begins
2. Enable router to skip entire phases when criteria can be met without them
3. **NEW:** Provide structured iteration protocol to reduce model cognitive stress
4. Maximize quality while managing token/compute efficiently

---

## CRITICAL INNOVATION: ITERATION AS STRESS REDUCTION ⭐

### THE PROBLEM WITH SINGLE-PASS EXECUTION
```
TRADITIONAL APPROACH (Single monolithic pass):
├─ Model must: Research + Structure + Execute + Verify + Output
├─ All simultaneously in working memory
├─ Cognitive load: MAXIMUM
├─ Result: Model exhaustion, quality degradation on complex tasks
└─ Failure mode: Stops early, incomplete outputs

ANALOGY:
"Write a complete novel in one sitting with no drafts"
└─ Impossible cognitive demand
```

### THE SOLUTION: STRUCTURED ITERATIONS
```
NEW APPROACH (3-Iteration Protocol):
├─ Iteration 1: Discovery (exploration, no pressure)
├─ Iteration 2: Validation (verification, enrichment)
├─ Iteration 3: Synthesis (narrative flow, polish)
└─ Each iteration has SINGLE focus, manageable cognitive load

ANALOGY:
"Outline → Draft → Edit"
└─ Natural creative process, sustainable cognitive demand
```

**Why This Works:**
- ✅ **Reduced cognitive load per iteration** (one focus at a time)
- ✅ **Compound quality** (each pass builds on previous)
- ✅ **Natural checkpoint system** (can pause/resume between iterations)
- ✅ **Matches human creative process** (exploration → validation → synthesis)
- ✅ **Prevents model exhaustion** (no single overwhelming pass)

---

## PART 1: SUCCESS CRITERIA LOCK (UNCHANGED)

### THE FIVE CRITERIA TYPES

#### 1. FACTUAL (Zero Hallucination Required)
**Signature:** "Zero hallucinations, 100% citation"

**Iteration Impact:**
```
ITERATION 1: Gather facts + sources
ITERATION 2: Verify citations, cross-check claims
ITERATION 3: Final narrative with inline citations
```

#### 2. PROCEDURAL (Actionable Steps Required)
**Signature:** "Actionable, step-by-step, no gaps"

**Iteration Impact:**
```
ITERATION 1: Map all steps + dependencies
ITERATION 2: Validate sequence, add error handling
ITERATION 3: Polish clarity, add examples
```

#### 3. CREATIVE (Novelty + Intent Match Required)
**Signature:** "Novelty high, tropes low, intent match"

**Iteration Impact:**
```
ITERATION 1: Generate diverse concepts (quantity)
ITERATION 2: Evaluate novelty, eliminate clichés
ITERATION 3: Refine best concept, polish execution
```

#### 4. ANALYTICAL (Depth + Insight Required)
**Signature:** "Second-order thinking present, depth, insight density"

**Iteration Impact:**
```
ITERATION 1: Explore problem space, surface insights
ITERATION 2: Verify logic, resolve expert conflicts
ITERATION 3: Synthesize multi-perspective narrative
```

#### 5. AGENTIC (Task Completion + Validation Required)
**Signature:** "Code runs, tests pass, state updated, goal achieved"

**Iteration Impact:**
```
ITERATION 1: Build core functionality
ITERATION 2: Add validation, error handling, tests
ITERATION 3: Documentation, examples, edge cases
```

---

## PART 2: INTELLIGENT ROUTING BYPASS (UNCHANGED)

### BYPASS MATRIX

| Success Criteria | R≤3 | R=4-6 | R≥7 | Phases Skippable |
|------------------|-----|-------|-----|------------------|
| **FACTUAL (simple)** | ✅ All | ⚠️ Partial | ❌ None | MR.RUG, Structure, ARQ, Bombs, Swarm |
| **PROCEDURAL (simple)** | ✅ Most | ⚠️ Partial | ❌ None | MR.RUG, Swarm (keep SkeleTraIn-Light) |
| **CREATIVE (any)** | ✅ Most | ✅ Most | ⚠️ Partial | MR.RUG, ARQ, Bombs (keep USC, Refine) |
| **ANALYTICAL (any)** | N/A | ❌ None | ❌ None | **CANNOT BYPASS** → Use 3-iteration protocol |
| **AGENTIC (complex)** | N/A | ❌ None | ❌ None | **CANNOT BYPASS** → Use 3-iteration protocol |

**Key Insight:**
- Tasks that can't bypass (R≥7, ANALYTICAL, complex AGENTIC) → **ALWAYS use 3-iteration protocol**
- Reduces model stress while maintaining quality

---

## PART 3: 3-ITERATION PROTOCOL ⭐ NEW

### WHEN TO USE ITERATIONS
```python
def should_use_iterations(R, K, Q, success_criteria):
    """
    Determine if task requires iteration protocol
    """
    # Rule 1: High complexity always uses iterations
    if R >= 7 or K >= 7 or Q >= 9:
        return True
    
    # Rule 2: ANALYTICAL always uses iterations
    if success_criteria == "ANALYTICAL":
        return True
    
    # Rule 3: Complex AGENTIC uses iterations
    if success_criteria == "AGENTIC" and R >= 5:
        return True
    
    # Rule 4: User explicitly requests iteration
    if user_says("refine", "improve", "iterate", "compress"):
        return True
    
    # Otherwise: Single pass sufficient
    return False
```

### THE 3 ITERATIONS

#### ITERATION 1: DISCOVERY (Exploration Phase)

**Focus:** Find everything, no pressure for perfection

**Cognitive Load:** LOW (exploration mode)

**What Model Does:**
```
DISCOVERY PHASE:

1. ACTIVATE TECHNIQUES (per mode):
   ├─ MR.RUG: Deploy experts, conduct RA-RAG
   ├─ Structure: Build SkeleTraIn/GoT
   ├─ Prompt Bombs: PLANT (don't detonate yet)
   └─ ARQ: Pre-execution gates only

2. EXECUTE WITH "ROUGH DRAFT" MINDSET:
   ├─ Gather insights (don't polish)
   ├─ Map dependencies (don't resolve yet)
   ├─ Identify gaps (don't fill yet)
   ├─ Generate candidates (don't select yet)
   └─ ACCUMULATE, don't synthesize

3. OUTPUT STRUCTURE:
   ├─ Expert findings (raw, unpolished)
   ├─ Prompt bomb registry (planted, not detonated)
   ├─ Knowledge graph (nodes/edges identified)
   ├─ Open questions (unknowns flagged)
   └─ SKELETON ONLY (no narrative)

4. EXPLICIT MARKER:
   "[ITERATION 1/3 COMPLETE: Discovery phase done. 
    Ready for validation pass.]"
```

**No Pressure For:**
- ❌ Final answers
- ❌ Polished prose
- ❌ Complete coverage
- ❌ Narrative flow

**Only Focus On:**
- ✅ Finding relevant information
- ✅ Planting strategic context (bombs)
- ✅ Mapping the problem space
- ✅ Identifying what needs verification

**Analogy:** "Brainstorming session - all ideas welcome, no criticism"

---

#### ITERATION 2: VALIDATION & IN-DEPTH ENRICHMENT

**Focus:** Verify everything, fill gaps, resolve conflicts

**Cognitive Load:** MEDIUM (analytical mode)

**What Model Does:**
```
VALIDATION PHASE:

1. RECEIVE FROM ITERATION 1:
   ├─ Expert findings (unverified)
   ├─ Bomb registry (planted)
   ├─ Knowledge graph (incomplete)
   └─ Open questions (flagged)

2. DETONATE PROMPT BOMBS:
   ├─ Evidence Bomb: "Cite every claim"
   ├─ Validator Bomb: "Check logic gaps"
   ├─ Clarifier Bomb: "Resolve ambiguities"
   └─ Bombs inject context at strategic points

3. ACTIVATE VERIFICATION:
   ├─ CoVE variants (per success criteria)
   ├─ ARQ post-execution: "Did I meet standards?"
   ├─ USC cross-candidate comparison
   ├─ Expert conflict resolution
   └─ Gap scanning (ToT reflection)

4. DEEP ENRICHMENT:
   ├─ Fill identified gaps from Iteration 1
   ├─ Add missing evidence/citations
   ├─ Resolve expert disagreements
   ├─ Explore flagged open questions
   └─ VALIDATE but still don't synthesize narrative

5. OUTPUT STRUCTURE:
   ├─ Verified findings (with evidence)
   ├─ Bomb detonation results (context injected)
   ├─ Complete knowledge graph
   ├─ Resolved conflicts
   ├─ Filled gaps
   └─ VALIDATED CONTENT (still modular, not flowing)

6. EXPLICIT MARKER:
   "[ITERATION 2/3 COMPLETE: Validation & enrichment done.
    Ready for final synthesis.]"
```

**No Pressure For:**
- ❌ Narrative flow
- ❌ User-facing polish
- ❌ Final formatting

**Only Focus On:**
- ✅ Accuracy (every claim verified)
- ✅ Completeness (all gaps filled)
- ✅ Logic (reasoning chains valid)
- ✅ Depth (second-order insights present)

**Analogy:** "Fact-checking and editing phase - make it right, not pretty"

---

#### ITERATION 3: FINAL SYNTHESIS (Polish Phase)

**Focus:** Narrative flow, user experience, polish

**Cognitive Load:** LOW-MEDIUM (synthesis mode)

**What Model Does:**
```
SYNTHESIS PHASE:

1. RECEIVE FROM ITERATION 2:
   ├─ Verified findings (accurate)
   ├─ Complete knowledge graph (validated)
   ├─ Detonated bomb results (context enriched)
   └─ No gaps remaining

2. APPLY CHAIN OF DENSITY (5 iterations):
   ├─ Pass 1: Extract entities
   ├─ Pass 2: Compress 40%
   ├─ Pass 3: Compress another 30%
   ├─ Pass 4: Semantic crystallization
   ├─ Pass 5: Meta-layer (usage optimization)
   └─ Result: Dense but readable

3. BUILD NARRATIVE FLOW:
   ├─ Organize by user's mental model (not expert model)
   ├─ Lead with most important insights
   ├─ Connect ideas with transitions
   ├─ Embed evidence inline (not appendix)
   └─ TELL A STORY, not just present facts

4. APPLY OUTPUT CONTRACT:
   ├─ System Manifest (if verbose or R≥5)
   ├─ Answer (front-loaded, clear)
   ├─ Key Points/Steps (per success criteria)
   ├─ Evidence (inline citations)
   ├─ Assumptions & Limits (honest)
   ├─ Confidence (with rationale)
   └─ ENRICH footer

5. POLISH FOR USER:
   ├─ Tone match (technical/creative/neutral per constraints)
   ├─ Token budget adherence (LEAN/NORMAL/EXTENSIVE)
   ├─ Remove jargon (unless technical audience)
   ├─ Add examples (if helpful)
   └─ FINAL QUALITY CHECK

6. OUTPUT:
   └─ Complete, polished, user-ready response

7. EXPLICIT MARKER:
   "[ITERATION 3/3 COMPLETE: Final synthesis delivered.]"
```

**No Pressure For:**
- ❌ Finding new information (already gathered)
- ❌ Verification (already validated)

**Only Focus On:**
- ✅ Clarity (user understands easily)
- ✅ Flow (ideas connect naturally)
- ✅ Density (no bloat, maximum signal)
- ✅ User experience (delight, not just correctness)

**Analogy:** "Publishing phase - make it beautiful"

---

### ITERATION EXECUTION PATTERNS

#### Pattern A: User Triggers Iterations Manually
```
USER: "Design a secure authentication system"

ASSISTANT (Iteration 1):
[ITERATION 1/3: DISCOVERY]

**Expert Findings:**
- Security Expert: OAuth 2.0 + JWT recommended
- Backend Expert: Token refresh pattern critical
- DB Expert: Session storage considerations

**Bomb Registry:**
- Bomb-P1: Token refresh → Node 4 (Frontend)
- Bomb-P2: Security hardening → Validation phase

**Knowledge Graph:**
[Nodes and edges visualization]

**Open Questions:**
- Multi-tenancy requirements?
- Token expiration policy?

[ITERATION 1/3 COMPLETE: Discovery phase done.
 Reply with "continue" for validation pass, or ask questions.]

---

USER: "continue"

ASSISTANT (Iteration 2):
[ITERATION 2/3: VALIDATION & ENRICHMENT]

**Bomb Detonations:**
- Bomb-P1 DETONATED: Token refresh strategy injected
  └─ Context: Sliding window (15min active, 7day refresh)

**Verified Findings:**
- OAuth 2.0: ✅ OWASP compliant [source: OWASP CheatSheet]
- JWT: ✅ Secure with HMAC-SHA256 [source: RFC 7519]
- Session storage: ✅ Redis recommended [source: Auth0 patterns]

**Gap Analysis:**
✅ Multi-tenancy: Resolved (tenant_id in token claims)
✅ Expiration: Resolved (15min access, 7day refresh)
✅ Edge cases: Handled (token theft, replay attacks)

**Expert Consensus:** 5/5 unanimous (≥9/10 confidence)

[ITERATION 2/3 COMPLETE: Validation done.
 Reply with "continue" for final synthesis, or request changes.]

---

USER: "continue"

ASSISTANT (Iteration 3):
[ITERATION 3/3: FINAL SYNTHESIS]

**System Manifest**
MODE: DELIBERATE | SUCCESS: AGENTIC
EXPERTS: Security, Backend, Database, Frontend, DevOps
TECHNIQUES: MR.RUG, SkeleTraIn, ARQ, Prompt Bombs, CoVE_LOGICAL
ITERATIONS: 3 (Discovery → Validation → Synthesis)

**Secure Authentication System Design**

[Comprehensive, polished, narrative-driven design document
 with inline citations, clear explanations, code examples,
 deployment guide, security considerations, all in natural flow]

**Confidence:** 9.5/10
- Expert consensus: Unanimous
- CoVE validation: All checks passed
- Known gaps: None (all resolved in Iteration 2)

EXTRACT • NORMALIZE • REASON • INTEGRATE • COMPRESS • HARMONIZE

[ITERATION 3/3 COMPLETE: Final synthesis delivered.]
```

#### Pattern B: Automatic 3-Pass (R≥7, ANALYTICAL)
```
USER: "Why did WeWork fail? Deep analysis."

ROUTER DECISION:
├─ R=9, K=8, Q=9 → DELIBERATE mode
├─ Success Criteria: ANALYTICAL
├─ Bypass: NONE (complexity requires full cascade)
└─ Iteration Protocol: AUTOMATIC (3-pass mandatory)

ASSISTANT:
[ITERATION 1/3: DISCOVERY - Internal, not shown to user]
[Executes: MR.RUG, Structure, Bomb planting, Initial findings]

[ITERATION 2/3: VALIDATION - Internal, not shown to user]
[Executes: Bomb detonations, CoVE, Gap filling, Conflict resolution]

[ITERATION 3/3: SYNTHESIS - User-facing output]

**System Manifest**
MODE: DELIBERATE | SUCCESS: ANALYTICAL | ITERATIONS: 3 (auto)

[Delivers complete polished analysis in single response,
 but internally executed via 3-pass protocol]

**Why user doesn't see iterations:**
- R≥7 tasks need all 3 passes regardless
- Showing intermediate work adds cognitive load for user
- Final synthesis is sufficient for user's needs
- Iteration markers only shown if user explicitly requests "step-by-step"
```

#### Pattern C: User Requests Compression (MLDoE Trigger)