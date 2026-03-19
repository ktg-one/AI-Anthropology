# Variant: Armatura Bidirectional Standards

**Status:** IDEA — awaiting experiment
**Origin:** Session 5, 2026-03-01
**Tags:** armatura, imperatus, legatus, consilium, censor, quality-gates, HITL

---

## Concept

Armatura constraints flow through the entire chain. Each role consumes them differently AND can reject upstream output through HITL if standards aren't met.

```
IMPERATUS (sets dials) → manifest
    ↓ HITL
LEGATUS (plans against dials) → can reject manifest
    ↓ HITL
CONSILIUM + LEGION (executes to standard) → can reject manifest OR plan
    ↓ HITL
CENSOR (validates output) → can reject manifest OR plan OR execution
```

## Three Projects

| Project | Defines | Rejects |
|---------|---------|---------|
| P1 | What Legatus needs to plan | Incomplete/incoherent manifest |
| P2 | What Consilium needs to execute | Bad manifest OR bad plan |
| P3 | What Censor needs to release | Bad manifest OR bad plan OR bad execution |

Each phase accumulates rejection rights of all previous phases plus its own.

## Current Server Gap

`handleExamine` in imperatus-mcp is a dumb recorder. Has RKQDE scores but doesn't use them to guide calibration. The spec defines per-tier levels for all 16 blocks but the server doesn't surface them.

## Four Enhancement Phases (within each project)

1. **Tier default tables** — HASTATI/PRINCIPES/TRIARII_DEFAULTS (like existing VELITES_DEFAULTS)
2. **Guided examine responses** — Server tells calling model what each block means + recommended level
3. **Zone confidence gates** — 3 checkpoints (Pre-Flight, Pipeline, Execution) not just generic
4. **Validation layer** — Warn if set level is below tier recommendation

## Key Principles

- Imperatus always outputs manifest. Doesn't care what happens downstream.
- Each downstream role defines its own acceptance criteria for what it receives.
- Human is the routing decision at every rejection — sends back to right phase.
- Standards are per-consumer, not per-boundary.
- Cores don't need to know project details — just that standards exist.

## Experiment Plan

TBD — test variants to find best approach for each project.
