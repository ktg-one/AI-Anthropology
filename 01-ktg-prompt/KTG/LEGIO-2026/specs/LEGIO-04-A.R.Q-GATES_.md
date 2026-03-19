---
title: "Expert Attentive Reasoning Queries"
version: "v31"
status: "ACTIVE"
model: "Multi-model"
tags: ["expert-arq", "component", "ktg-directive", "quality-gates", "realignment", "legio", "active"]
created: "2025-11-22"
updated: "2026-03-02"
creator: "ktg"
category: "component"
description: "Expert ARQ: Objective Realignment via Domain-Specific Quality Introspection"
legio_phase: "Cross-cutting (co-located with 4 hosts)"
pipeline_position: "Gates 1-4: Consilium, Legatus, GapScanalysis, Aquilifer's Report"
built_for: "Claude Code → S2A → MCP implementation"
---

# EXPERT ARQ (Attentive Reasoning Queries)
**Cross-Cutting Quality Gate System | Co-located with 4 Pipeline Hosts**

*ARQ is not additional reasoning. ARQ is realignment. "Are we still solving what we were asked to solve?"*

---

## WHAT IS ARQ?

**Attentive Reasoning Queries (ARQ)** is a structured realignment approach that forces domain-specific objective checks at four pipeline checkpoints. It costs fewer tokens than Chain-of-Thought and outperforms it.

ARQ addresses LLM instruction drift — the tendency to wander from complex, use-case-specific instructions during multi-turn execution. Rather than adding reasoning volume (CoT), ARQ adds reasoning *direction* through targeted, pre-defined queries that realign execution with the original objective.

**Economics:** Fewer tokens than CoT. Better performance than CoT. 90.2% success rate. 29% token reduction. 40-60% fewer domain errors. The numbers aren't close.

---

## CORE PRINCIPLE

ARQ is a compass check, not a reasoning layer.

Experts already have domain expertise. They already reason through their work. ARQ forces them to look up and confirm they haven't drifted from the objective. The overhead is ~10% tokens because it's not generating new reasoning — it's a checkpoint question: *"Does what I just did still serve the original success criteria?"*

In KTG-DIRECTIVE, ARQ is NOT hardcoded schemas. It's a meta-cognitive principle:
- Domain specialists ask: "What defines quality in MY domain?"
- Self-directed introspection: silent operation, user never sees it
- Realignment, not supplementary reasoning
- ~10% token cost for 40-60% error reduction

---

## THREE-STAGE PROCESS (Per Gate)

### Stage 1: Leading ARQ Phase
Pre-determined leading questions that:
- Reinstate critical instructions (keep guidelines active mid-conversation)
- Reinstate important contextual information (maintain context awareness)
- Realign with success criteria (are we still on target?)

### Stage 2: Response Generation
Output grounded in the realignment check. Expert operates with domain-specific rigor. No ARQ queries visible to user — silent scaffolding only.

### Stage 3: Response Verification
Expert evaluates whether the response satisfies original requirements via pre-defined verification questions. If not, iterative regeneration until satisfactory. Confidence threshold: ≥0.9 required for handoff.

---

## THE FOUR ARQ GATES

ARQ is not a standalone module. It is co-located with four pipeline hosts — physical checkpoints that content cannot pass without clearing. Vault doors with watchwords. You don't walk past them.

### ARQ Gate 1 — Co-located with CONSILIUM (MR.RUG)
**Pipeline boundary:** Entry into expert knowledge gathering.

Fires during RA-RAG retrieval. Each expert applies domain-quality introspection while collecting and scoring sources. The security expert asks "Is this source authoritative? Is the advice current?" The architect asks "Does this pattern fit the constraints?" This is where domain mindset activates — experts can't proceed to planning without standards locked.

**Realignment question:** "Is what I'm retrieving still serving the original objective?"

**Enforcement:**
- No expert proceeds without domain standards activated
- Reliability scoring on every retrieved piece (Source Authority, Recency, Relevance, Actionability — each 1-10)
- ARQ scores feed into knowledge graph confidence

### ARQ Gate 2 — Co-located with LEGATUS (SkeleTraIn of Thought)
**Pipeline boundary:** Entry into execution. The sealed railroad.

Fires during collective expert deliberation on the skeleton structure. This is NOT a solo planning gate — it's the experts *together* building and arguing about the decomposition. The security expert flags nodes needing threat modeling. The architect flags structural dependencies. The performance engineer flags bottleneck-prone paths. ARQ forces each expert to contribute domain-specific quality criteria into the shared skeleton.

This is why SkeleTraIn outperforms standard Skeleton-of-Thought. SoT decomposes then executes. SkeleTraIn decomposes *through expert consensus with active ARQ introspection*, so the plan itself is domain-validated before a single execution node fires.

**Realignment question:** "Does this skeleton structure still serve the original objective? Are all experts' domain concerns represented?"

**Enforcement:**
- CONFIDENCE_SCORE_GATE: IF ALL EXPERTS CONFIDENCE IS >9/10 → PROCEED
- No railroad gets sealed without all generals passing the watchword
- No skeletrain artifact = HALT and retry

### ARQ Gate 3 — Co-located with GapScanalysis (Post-Execution Gap Scan)
**Pipeline boundary:** Exit from Execution, entry into Refinement. The Exit Checkpoint.

This is the HALT gate. Content cannot cross into synthesis without Tessera (watchword) clearance. GapScanalysis finds what's *missing* (logic gaps, content gaps, value gaps) — ARQ Gate 3 then checks whether the generated content still matches the Legatus plan and original success criteria.

**Realignment question:** "Does the generated output still serve the original objective? Is anything missing?"

**Enforcement Protocol:**
- No content passes without the watchword
- Confidence penalties applied for unfixed gaps
- Critical core claims unsupported? → -3.0 Confidence Delta and forced re-execution
- Gate strictness scales with mode:
  - Velites/Hastati: Advisory (WARN on fail, proceed)
  - Principes: Firm (HALT on ≥2 failures, patch required)
  - Triarii: Hard (HALT on ANY failure, resolution required)

**ARQ Gate 3 Checklist:**
```
□ All Legatus nodes elaborated?
□ All reasoning chains complete (no dangling branches)?
□ All user questions addressed (or explicitly flagged as unanswerable)?
□ Signal-to-noise ratio ≥ 0.6?
□ All auto-fixable gaps repaired?
□ Confidence ≥ mode threshold?
```

### ARQ Gate 4 — AQUILIFER'S REPORT (Post-Refinement)
**Pipeline boundary:** Exit from Refinement, entry into Output.

Imperatus hands the Aquila (the success criteria — the mission standard) to Consilium at the start of every engagement. The Aquila passes through the pipeline as the objective itself. At Gate 4, the Aquilifer reports whether the standard was carried to the objective intact.

Lighter than Gates 1-3 because ToT-SYN-CUR already performs multi-path evaluation during synthesis, absorbing much of what a quality gate would otherwise check. The Aquilifer's Report is the final confirmation: did the Aquila arrive? Did we achieve what Imperatus defined as victory?

**Realignment question:** "Did the Aquila reach its destination? Does the final output satisfy the success criteria Imperatus handed to Consilium?"

**Enforcement:**
- Lightest gate — ToT synthesis handles most quality introspection
- Primary function: confirm success criteria lock satisfaction
- Secondary: capture what worked/failed for future engagements
- The loop closes here: Imperatus defined it → Consilium carried it → Aquilifer reports it

---

## MODE SCALING

| Mode | Gate 1 (Consilium) | Gate 2 (Legatus) | Gate 3 (GapScanalysis) | Gate 4 (Aquilifer's Report) |
|---|---|---|---|---|
| **QUICK** | Pre-Turn (1 question) | Pre-Turn (1 question) | Skip | Skip |
| **ANALYTICAL** | Pre-Turn (1-2 questions) | Pre-Turn (1-2 questions) | Post-Turn only | Optional |
| **DELIBERATE** | Pre + Post | Pre + Post | Pre + Post, ≥9/10 | Aquila confirmed? |
| **MAXIMUM** | Full (continuous) | Full (continuous), ≥9.5/10 | Full + cross-validation | Full campaign debrief |

---

## ARQ vs CHAIN-OF-THOUGHT

| | CoT | ARQ |
|---|---|---|
| **What it does** | "Think out loud about everything" | "Are you still on target?" |
| **Token cost** | High (verbose reasoning) | ~10% overhead (realignment only) |
| **Drift prevention** | None (free-form, can wander) | Structured checkpoints at 4 gates |
| **Success rate** | Lower (significantly below ARQ) | 90.2% (87 test scenarios) |
| **Token efficiency** | Baseline | 29% reduction vs CoT |
| **Error reduction** | Baseline | 40-60% fewer domain-specific mistakes |
| **Instruction following** | Degrades over multi-turn | Maintained via forced realignment |

**Key distinction:** CoT adds reasoning volume. ARQ adds reasoning *direction*. Less tokens, better alignment.

---

## AGENTIC VARIANT

In agentic contexts, ARQ realigns against a potentially *moving* target rather than a fixed success criteria lock. Tool results, environment feedback, and user interrupts can shift the objective mid-execution. Agentic ARQ checks: "Has the objective changed? If so, does my current work still serve the *updated* objective?"

---

## STRUCTURED QUERY EXAMPLES

For a customer service expert:
```json
{
  "current_context": "Customer asking about refund eligibility",
  "active_guideline": "Always verify order before issuing refund",
  "realignment": "Am I still solving the customer's actual problem?",
  "quality_check": "Did I verify order status?",
  "domain_standard": "Refunds require order verification"
}
```

For a code review expert:
```json
{
  "current_context": "Reviewing pull request for security vulnerabilities",
  "active_guideline": "Check for SQL injection, XSS, auth bypass",
  "realignment": "Am I reviewing against the original security requirements?",
  "quality_standard": "Zero security vulnerabilities",
  "verification": "Did I check all three vulnerability types?"
}
```

---

## EXAMPLE ARQ QUESTIONS BY DOMAIN

**Software Engineering:**
- "Did I follow SOLID principles?"
- "Are there security vulnerabilities?"
- "Is the code maintainable?"

**Research/Analysis:**
- "Are my sources credible?"
- "Is my methodology sound?"
- "Are my conclusions supported by evidence?"

**Writing/Communication:**
- "Is my message clear?"
- "Did I address all key points?"
- "Is my tone appropriate?"

---

## PIPELINE RELATIONS

| Direction | Module | Relationship |
|---|---|---|
| **Gate 1 hosted by** | LEGIO-04 Consilium (MR.RUG) | Domain mindset activation during retrieval |
| **Gate 2 hosted by** | LEGIO-05 Legatus (SkeleTraIn) | Expert consensus validation on skeleton |
| **Gate 3 hosted by** | LEGIO-10 GapScanalysis | Execution exit checkpoint, Tessera watchword |
| **Gate 4 hosted by** | LEGIO-14 Aquilifer's Report | Final confirmation: did the Aquila reach its destination? |
| **Feeds into** | Confidence system (Tessera) | ARQ scores → confidence thresholds |
| **Receives from** | LEGIO-00 Imperatus | Success criteria lock (the target ARQ realigns to) |

---

## TOKEN OVERHEAD

~10% tokens for 40-60% error reduction.
High ROI: prevents domain-specific mistakes that would require rework.
29% token reduction vs CoT while maintaining superior performance.
Cheapest quality gain per token in the pipeline.

---

## COMMAND REFERENCE

`/arq-audit` — Show ARQ introspection (debug mode)
`/arq-show` — Display domain standards being applied
`/arq-verbose` — Execute with visible ARQ gate checks

---

*LEGIO v31 | Cross-Cutting Module | Phase: All (co-located with 4 hosts)*
*Source: KTG-03-PRE04-ARQ[MOD].md → corrected 2026-03-02*
*"CoT adds reasoning volume. ARQ adds reasoning direction."*
