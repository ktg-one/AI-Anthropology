# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

KTG is an **AI Anthropology methodology and prompt engineering framework** — a research/documentation repository containing structured techniques for optimizing LLM interactions through multi-layered expert systems, reasoning patterns, and context compression. The active development target is **LEGIO** (in `LEGIO-2026/`), which translates these techniques into a model-agnostic agentic framework via MCP.

**Author:** Kevin Tan (ktg.one) | Perth, WA

## Repository Structure

This repo has two layers:

1. **KTG root** — The original methodology files (`KTG-01` through `KTG-14`, `STRAWHATS-*.md`, `MLDoE-*.md`, `cep-v8/`). Pure markdown, no build system. These are the **source research** that LEGIO formalizes.

2. **`LEGIO-2026/`** — The formalized 17-module cascade (v30.2) + MCP server implementation. Has its own `CLAUDE.md` with full architecture details. **This is where active work happens.**

### Quick Reference

| What | Where |
|------|-------|
| LEGIO architecture (single source of truth) | `LEGIO-2026/LEGIO-OVERVIEW.md` |
| Translation progress | `LEGIO-2026/LEGIO-STATUS.md` |
| Module specs (17, read-only) | `LEGIO-2026/specs/` |
| imperatus-mcp (strategic command) | `LEGIO-2026/01-IMPERATUS/` |
| legatus-mcp (tactical planning) | `LEGIO-2026/02-LEGATUS/` |
| Enrichment + execution materials | `LEGIO-2026/03-LEGION-MARCH/` |
| Agent definitions (9) | `LEGIO-2026/.claude/agents/` |
| Onboarding docs (IMBUED/EXECUTE/Doctrine) | `LEGIO-2026/onboard/` |
| Team topology | `LEGIO-2026/docs/architecture/pass-sequence-topology.md` |
| Formation doctrine (IMBUED/ENRICH/EXECUTE) | `LEGIO-2026/onboard/LEGIO-FORMATION-DOCTRINEI.md` |
| One-shot execution entry point | `STRAWHATS-v30-ADAPT.md` |
| Historical versions | `ARCHIVE/` |

## MCP Servers

Three Doctrine MCP servers registered in `.mcp.json`:

| Server | Location | Transport | Function |
|--------|----------|-----------|----------|
| `imperatus` | `LEGIO-2026/01-IMPERATUS/` | stdio | RKQDE scoring, mode tier, sealed manifest |
| `legatus` | `LEGIO-2026/02-LEGATUS/` | stdio | SkeletrainOT railroad planning (7 tags, 6 track types) |
| `lotus-wisdom` | `npx lotus-wisdom-mcp` | stdio | General contemplation (every agent gets this) |

```bash
# imperatus-mcp
cd LEGIO-2026/01-IMPERATUS && npm install && npm run build

# legatus-mcp
cd LEGIO-2026/02-LEGATUS && npm install && npm run build
```

**No test or lint tooling exists.** The root repo is pure markdown (no build system). The Python `pyproject.toml` is a placeholder.

For full MCP details (tools, params, implementation), see `LEGIO-2026/CLAUDE.md`.

## Architecture: Two Pipelines

### KTG Pipeline (root files, 5 phases)

```
QUERY → SYSTEM_COMMAND → PRE-FLIGHT → MR.RUG EXPERTS → SKELETRAIN+BOMBS → EXECUTE+VERIFY → COMPRESS+ENRICH → OUTPUT
```

- **Phase 0:** System Command — RKQDE scoring, mode selection (QUICK/ANALYTICAL/DELIBERATE/MAXIMUM)
- **Phase 1:** Pre-Flight — ARQ gates, Anti-Lazy Contract, USC parallel reasoning
- **Phase 2:** Expert Deployment — MR.RUG (Mixture→Role→Retrieval→Update→Generate), 2-8 specialists
- **Phase 3:** Structure — SkeleTrain pathways + Prompt Bombs (6 types at high-risk zones)
- **Phase 4:** Execution — FCoT/CoC reasoning routing, BATON(sequential)/SWARM(parallel), CoVE verification
- **Phase 5:** Compression — E.N.R.I.C.H (Extract→Normalize→Reason→Integrate→Compress→Harmonize), 3-pass enrichment

### LEGIO Agent Architecture v2 (LEGIO-2026/, 3 MCPs + 9 agents)

```
Layer 1: 3 Doctrine MCP servers (imperatus, legatus, lotus-wisdom)
Layer 2: 9 agent definitions in .claude/agents/ (3 officers, 3 MR.RUG experts, 3 workers)
Layer 3: Model assignment (OPEN — cross_model manifest block)
Layer 4: pass_sequence team topology (tier → handoff chain)
```

**Three-phase spine (SYSTEM-CORE, never skippable):**
1. **Imperatus** (LEGIO-00) — Strategic command. RKQDE scoring → sealed manifest
2. **Legatus** (LEGIO-05) — Tactical command. Manifest → execution skeleton
3. **Censor** (LEGIO-11) — Mission assurance. Output refinement → release gate

**Mode tiers → pass_sequence:**
- 2x Velites (Σ≤12∧Danger≤5): Imperatus → Censor
- 3x Hastati: Imperatus → Legatus → Censor
- 4x Principes: Imperatus → Consilium → Legatus → Censor
- 8x/nx Triarii (Σ≥39∨Danger≥9): Full cascade, recursive

## Naming Conventions

Two rules, no exceptions:
1. **Roman names = command chain roles** (organizational): Imperatus, Armatura, The Seal, Consilium, Legatus, Censor
2. **Original names = techniques** (preserved for model recognition): USC, ARQ, FCoT, CoC, CoVE, PGScan, QMDR, MLDoE, CEP, MR.RUG, SkeletrainOT

Do not rename techniques — models recognise them from training data.

## CEP v8 Knowledge Base (`cep-v8/`)

Expert council for context preservation across sessions. 4 specialists execute in order:

1. MEMORY_ARCHITECT → candidate preservation list
2. CROSS_DOMAIN_ANALYST → edge map + cross-domain links
3. COMPRESSION_SPECIALIST → 5-iter Chain of Density toward ≥0.15 density
4. RESTORATION_ENGINEER → cold-start + self-containment validation
5. Council consensus → final packet approved

**Packet naming convention:** `$MM$DD$YYYY-XXX-LN-keywords` (mandatory per `cep-v8/PROTOCOL.md`)

Additional specialists: MIRAS (audit), CASCADE (error recovery)

## Key Concepts

- **RKQDE**: R=Reasoning depth, K=Knowledge complexity, Q=Quality stakes, D=Decomposition breadth, E=Edge-case density
- **ARQ Gates**: 4 fixed structural checkpoints (during MR.RUG, after Legatus, before execution end, before output)
- **嘘契約 (Anti-Lazy Contract)**: Epistemic honesty binding. Knows non-compliance + knows instruction + pretends done = LIE
- **Confidence Gate**: >9/10 to proceed at each phase boundary
- **S2A Compression**: Full elaboration specs → compressed onboarding docs for model consumption
- **Sealed Railroad**: After Legatus plans, execution follows tracks with zero runtime decisions
- **Armatura Examine Blocks**: 16 constraint dials (BUFFER_VALET through OUTPUT_FORMAT). Dials, not switches — "off" = minimum viable, not absent.
- **Formation Control Laws**: IMBUED (compiler), ENRICH (analyzer), EXECUTE (author) — never mixed within a single pass.

## Versioning

- **STRAWHATS:** v1.0 → v29 → v30-ADAPT (current stable)
- **LEGIO:** v30.2 (17/17 modules complete, cross-cutting 3/5)
- **CEP:** v7.1 (skill format) → v8 (comprehensive KB)

## Working With This Repo

- Files are designed for **LLM context injection** — load relevant `.md` files into context windows
- CEP v8 files are pre-compressed and optimized via MLDoE for minimal token overhead
- The numbered `KTG-01` through `KTG-14` execute as a pipeline in order
- `STRAWHATS-v30-ADAPT.md` is the single-file entry point for one-shot deployment
- For LEGIO work, read `LEGIO-2026/CLAUDE.md` first — it has the full module map and MCP details

## Current Status & Next Priorities

All 17/17 LEGIO module specs complete. Architecture v2 implemented. Stale files archived. See `LEGIO-2026/CLAUDE.md` for full status and priorities.

## Validation

Proven: Replicated Deloitte 6-month/60-person WA SME analysis in 3 AI passes using QMDR Triplexity. Benchmarked against OpenAI Evals, Vertex AI, HuggingFace/BigBench/HELM frameworks.
