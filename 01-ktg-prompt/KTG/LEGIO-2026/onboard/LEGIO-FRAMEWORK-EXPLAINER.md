# LEGIO — How It Actually Works

**LEGIO** (Legion Engineered Governance of Intelligent Operations) is a recursive quality engine that produces benchmark-tier output from AI models by running multiple focused passes over artifacts, with a human approving at every handoff.

LEGIO does not make AI smarter. It makes AI *iterative*. One draft is a start. Each pass after that attacks the draft from a new angle. The human decides when quality is sufficient.

---

## The Core Insight

AI models produce output that *reads as thorough* but often isn't. Models optimise for what a human rater would score as "helpful" in a 30-second evaluation. That 30 seconds catches confidence, structure, and obvious coverage — but misses second-order effects, softened failure modes, and unsourced confident claims.

LEGIO's answer: don't trust one pass. Run multiple passes with different objectives, and put a human at every boundary to catch what the model won't catch about itself.

---

## Three Sovereign Roles

LEGIO has three roles. Each role is a separate AI instance — a separate model, a separate context window, a separate project. They never share internal instructions. They only share artifacts.

### IMBUED (The Compiler)

IMBUED reads the user's request and produces a **sealed execution manifest** — a structured plan containing the objective, success criteria, expert assignments, constraint levels, and strategic instructions embedded as "bombs" (compressed directives planted at specific points).

IMBUED never generates content. It only plans. Its output is a YAML manifest.

IMBUED runs once at the start. It does not repeat.

### ENRICH (The Analyzer)

ENRICH reads an artifact — either the manifest (before any content exists) or a draft (after EXECUTE has produced content) — and plants **bombs**: targeted attack instructions identifying specific weaknesses.

ENRICH never writes prose. It never rewrites the artifact. It appends a bomb registry — a list of specific problems with specific fix directives — and passes the original artifact through untouched.

ENRICH runs one focused priority per invocation:

| Priority | Lens | What It Attacks |
|----------|------|-----------------|
| 1 | **Gaps** | What's missing? What was skipped? What assumptions went unstated? |
| 2 | **Depth** | What's shallow? Where are claims made without mechanism or evidence? |
| 3 | **Perspective** | What viewpoint is missing? What would a critic say? What's the counter-argument? |
| 4 | **Validation** | What's unfalsifiable? What can't be checked? Where are sources needed? |
| 5 | **Sparkle** | What's generic? Where could a unique insight replace a commodity observation? |
| 6 | **Narrative** | Does the overall arc hold? Does each section earn its place? Does the conclusion follow from the evidence? |

Each priority is a separate ENRICH→EXECUTE cycle. Never grouped. Never compressed. One lens per pass.

### EXECUTE (The Author)

EXECUTE receives the manifest (and any bomb registries from ENRICH) and produces content. It follows the plan. It detonates every bomb it encounters — meaning it addresses every directive ENRICH planted. It produces a complete draft.

EXECUTE never plans. It never restructures the manifest. It never analyses its own output for weaknesses. It writes at maximum depth and ships.

---

## The Engine: How Iterations Work

The three roles pass artifacts between each other through **human gates**. Every handoff requires human approval before the next role begins. The human is the convergence criterion — the only thing that stops the engine.

### One Iteration Cycle

```
ENRICH reads the artifact (manifest or draft)
ENRICH plants bombs targeting weaknesses for ONE priority
ENRICH outputs: original artifact (untouched) + bomb registry (appended)
  >>> HUMAN GATE: Review bomb quality. Are bombs targeted or vague? <<<

EXECUTE reads the artifact + bomb registry
EXECUTE produces a revised draft, detonating every bomb
EXECUTE outputs: new draft
  >>> HUMAN GATE: Review draft quality. Is it good enough? <<<

Human decides: run another cycle with the next priority? Or stop here?
```

### The Full Engine

The complete LEGIO execution looks like this:

```
IMBUED compiles the manifest (once)
  >>> HUMAN GATE: Is the plan correct? <<<

Then the iteration engine:

  ENRICH (Priority 1: Gaps) → HUMAN GATE → EXECUTE → HUMAN GATE
  ENRICH (Priority 2: Depth) → HUMAN GATE → EXECUTE → HUMAN GATE
  ENRICH (Priority 3: Perspective) → HUMAN GATE → EXECUTE → HUMAN GATE
  ENRICH (Priority 4: Validation) → HUMAN GATE → EXECUTE → HUMAN GATE
  ENRICH (Priority 5: Sparkle) → HUMAN GATE → EXECUTE → HUMAN GATE
  ENRICH (Priority 6: Narrative) → HUMAN GATE → EXECUTE → HUMAN GATE
  ... the human can keep going with deeper passes on any priority ...
```

The engine is recursive and unbounded. The human stops it when quality is sufficient.

---

## Formation Presets

Most tasks don't need all six priorities. LEGIO defines preset configurations based on task complexity:

### 2x DUPLEX (Velites — Light Skirmishers)

```
IMBUED → EXECUTE
```

No ENRICH. Simple tasks. The manifest goes straight to execution. Baseline quality.

### 3x TRIPLEX (Hastati — Front Line)

```
IMBUED → ENRICH(Gaps) → EXECUTE
```

One ENRICH cycle attacks the *plan* before EXECUTE runs. ENRICH spots what IMBUED missed. Standard analytical work.

### 4x STANDARD (Principes — Experienced Second Line)

```
IMBUED → EXECUTE → ENRICH(Gaps) → EXECUTE
```

EXECUTE produces a first draft. Then ENRICH attacks the *draft* — identifying observed weaknesses rather than predicted ones. EXECUTE runs again incorporating the bombs. Professional-grade output.

### 7x DELOITTE (Triarii — Veteran Reserves)

```
IMBUED → EXECUTE → ENRICH(Gaps) → EXECUTE → ENRICH(Depth) → EXECUTE → ENRICH(Perspective) → EXECUTE
```

Three full ENRICH→EXECUTE cycles, each with a different priority lens. Gaps, then Depth, then Perspective. This configuration achieved Deloitte-standard benchmark quality in testing with Gemini 2.5 Deep Research.

### nx RECURSIVE (No Limit)

```
IMBUED → [ENRICH(next priority) → EXECUTE]* → human says stop
```

The engine continues through all six priorities and can loop back for deeper passes. There is no architectural ceiling. The human decides when convergence is reached.

---

## Why Iterations, Not One Long Prompt

### Models compact under complexity

Current AI models have a runtime behaviour where effort scales down as complexity scales up. The harder the instruction set, the more the model drifts toward producing the *shape* of a good answer rather than actually executing every instruction. This happens silently — the model cannot detect its own quality degradation.

Multiple short passes avoid this. Each pass is simple enough that the model executes at full depth before the compaction behaviour triggers.

### Fresh attention per pass

Each ENRICH and EXECUTE invocation is a fresh AI instance with a clean context window. No accumulated drift. No lossy middle where earlier instructions fade. Each instance reads the current artifact and the current bomb registry with full attention.

### Artifacts remember, models don't

Models are stateless between passes. The state lives in the artifacts — the manifest, the bomb registries, the drafts. Each artifact accumulates more precision across iterations. The models are disposable processors applied to increasingly rich artifacts.

### Different angles catch different failures

A single pass optimises for one perspective. Running Gaps, then Depth, then Perspective as separate passes means each lens gets full attention. Combining all three in one pass means the model half-executes each.

---

## The Static Stack: Why Roles Never Mix

LEGIO enforces strict role separation — called the **Static Stack Invariant**:

```
IMBUED  = Compiler  (plans — never generates content)
ENRICH  = Analyzer  (identifies weaknesses — never writes prose)
EXECUTE = Author    (writes content — never plans or analyses)
```

Mixing roles within a single pass produces measurable quality degradation:

- **Tone drift**: the model shifts voice when switching between analytical and creative modes
- **Logic breaks**: planning interrupts generation flow, producing disjointed output
- **Hallucination**: the model fills gaps it identified during analysis with confident but unsourced claims

Each role has its own project, its own instructions, its own model instance. They interact only through artifact handoffs at human gates.

---

## Bombs: How ENRICH Communicates With EXECUTE

ENRICH never rewrites. It **appends**. Its output is a bomb registry — structured attack instructions that EXECUTE must follow.

Two types of bombs exist:

**Strategic Bombs** (from IMBUED): Planted during manifest compilation. Broad directives like "at section 3, switch to the financial expert's perspective" or "before concluding, verify all claims against the source data."

**Tactical Bombs** (from ENRICH): Planted after reading the manifest or draft. Specific directives like "Section 3 claims 12% growth but provides no source — add citation or remove claim" or "The competitive analysis covers only direct competitors — add indirect competitors from adjacent markets."

EXECUTE detonates every bomb it encounters. Bombs are operational instructions, not suggestions. Skipping a bomb violates the mandate.

---

## Human Gates: What Gets Reviewed

Every arrow between passes is a human gate. The human reviews different things at each boundary:

| After... | Human Reviews |
|----------|---------------|
| IMBUED | Is the plan correct? Are experts well-assigned? Are success criteria specific enough to test? |
| ENRICH | Are bombs targeted or vague? Did ENRICH find real weaknesses or generic complaints? |
| EXECUTE | Does the draft meet the criteria? Were all bombs detonated? Is quality sufficient to stop, or does it need another ENRICH cycle? |

The human is not a rubber stamp. The human is the convergence criterion — the external quality function that can distinguish between "reads as thorough" and "is thorough." Without the human, the system loops forever.

---

## Quality Calibration

Quality bands were empirically measured during testing with Gemini 2.5 Deep Research (early 2026). These numbers are model-dependent and require recalibration for different models:

| After | Quality Floor (Gemini 2.5 era) |
|-------|-------------------------------|
| EXECUTE alone (no ENRICH) | ~60% |
| + ENRICH(Gaps) → EXECUTE | ~80% |
| + ENRICH(Depth) → EXECUTE | ~92% |
| + ENRICH(Perspective) → EXECUTE | ~99% (Deloitte benchmark) |
| + ENRICH(Validation) → EXECUTE | Beyond benchmark |
| + ENRICH(Sparkle) → EXECUTE | Beyond benchmark |
| + ENRICH(Narrative) → EXECUTE | Beyond benchmark |

Three priorities — Gaps, Depth, Perspective — were sufficient to reach Big Four consulting standard. Priorities 4-6 exist for work that needs to exceed that standard.

Current models (early 2026) may produce different curves due to changes in model training and runtime behaviour. The engine architecture remains constant; the calibration is what changes.

---

## Summary

LEGIO is three sovereign AI roles passing artifacts through human gates in a recursive loop.

- **IMBUED** compiles a plan (once).
- **ENRICH** attacks the plan or draft with one focused priority lens per cycle, planting bombs.
- **EXECUTE** writes or rewrites content, detonating every bomb.
- **The human** decides after each pass whether to continue or stop.
- **Artifacts** carry the state. Models are stateless. Each pass is a fresh instance.
- **Formation presets** (2x through nx) are common configurations, not limits. The engine is unbounded.

The architecture compensates for known AI limitations — compaction under complexity, efficiency-over-effectiveness runtime bias, and the gap between "reads as correct" and "is correct" — by keeping each pass simple, each role isolated, and each boundary human-gated.

---

*LEGIO v31 | Framework Explainer | For NotebookLM*
*"IMBUED compiles. ENRICH attacks. EXECUTE writes. The human decides when it's done."*
