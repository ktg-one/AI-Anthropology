---
title: "LEGIO — Complete System Overview"
version: "v30.2"
status: "ACTIVE"
created: "2026-02-16"
updated: "2026-02-16"
creator: "ktg"
category: "overview"
description: "Bird's-eye view of the LEGIO cascade. 17-module pipeline (LEGIO-00 through LEGIO-16), command chain, naming rules, mode tiers, architecture, and module index."
---

# LEGIO — THE LEGION
**17-Module Prompt Cascade → Agentic Framework**

*LEGIO (Latin): the legion — Rome's self-contained fighting force. Same units, different formations per campaign. One system, infinite configurations.*

---

## WHAT LEGIO IS

LEGIO is a 17-module prompt engineering cascade that transforms any query into a structured, multi-expert, quality-gated execution pipeline. Built as KTG-DIRECTIVE v30 (STRAWHATS ADAPTIVE-BATTALION), now being translated into modular specs compiled into executable agent configurations.

```
LEGIO-*.md (specs) → Forge MCP (compiler) → AGENTS.md (S2A compressed) → Claude Code (runtime)
```

Specs = blueprints. Forge compiles them into onboarding docs. Models read the onboarding and execute.

---

## NAMING RULES

Two rules. No exceptions.

**Rule 1 — Roman names = command chain roles.** Organisational hierarchy. WHO does what.

**Rule 2 — Original names = techniques.** Methods models already recognise from training data. Renaming loses signal.

```
ROMAN (6 command roles):     ORIGINAL (11 techniques):
├─ Imperatus                 ├─ USC
├─ Armatura                  ├─ ARQ
├─ The Seal                  ├─ Prompt Bombs
├─ Consilium                 ├─ FCoT / CoC
├─ Legatus                   ├─ Baton Bolt / Swarm
└─ Censor                    ├─ CoVE
                             ├─ PGScan
                             ├─ Self-Reflect-Adapt
                             ├─ QMDR / MLDoE
                             └─ CEP
```

---

## COMMAND CHAIN

Six officers. Fixed order. Each has one job.

```
┌───────────────────────────────────────────────────────────┐
│  IMPERATUS — Supreme Commander              [LEGIO-00]    │
│  Scores query (RKQDE). Selects mode. Sets all dials.      │
│  OUTPUT → Sealed execution manifest                       │
├───────────────────────────────────────────────────────────┤
│  ARMATURA — The Arsenal                     [LEGIO-01]    │
│  Sets CONSTRAINT LEVELS for every technique.               │
│  Dials, not switches. Even "off" = minimum viable.         │
│  OUTPUT → Constraint levels embedded in manifest           │
├───────────────────────────────────────────────────────────┤
│  THE SEAL — Anti-Lazy Contract (嘘契約)       [LEGIO-02]    │
│  Epistemic honesty binding. Shortcut = restart verbose.    │
│  No manifest executes without contract signature.          │
│  OUTPUT → Signed commitment, execution authorised          │
├───────────────────────────────────────────────────────────┤
│  CONSILIUM — War Council (MR.RUG)           [LEGIO-04]    │
│  Assembles N domain experts. Each surveys terrain.         │
│  Expert count from Imperatus. Formation from Armatura.     │
│  OUTPUT → Expert constellation ready for deployment        │
├───────────────────────────────────────────────────────────┤
│  LEGATUS — Field General (SkeletrainOT)     [LEGIO-05]    │
│  Takes manifest + experts. Lays all tracks: routes,        │
│  patterns, reasoning, bombs, gates, verification.          │
│  OUTPUT → Sealed railroad. Zero decisions during execution │
├───────────────────────────────────────────────────────────┤
│  ═══════════ EXECUTION: The Legion Marches ═══════════    │
│  Tracks laid. Bombs planted. Gates set. Pure speed.        │
│  Experts follow route cards. No planning — just run.       │
├───────────────────────────────────────────────────────────┤
│  CENSOR — Mission Assurance (ISC)           [LEGIO-11]    │
│  Refines output against Imperatus success criteria.        │
│  Won't release until objective is secured.                 │
│  Imperatus opens the mission. Censor closes it.            │
├───────────────────────────────────────────────────────────┤
│  ═══════════ REFINE & OUTPUT: Post-Battle ════════════    │
│  Reflect. Format. Verify. Compress. Deliver.               │
│  Quality loops close. Memory updates. Output ships.        │
└───────────────────────────────────────────────────────────┘
```

---

## MODE TIERS

Four tiers. Named for Roman military ranks. Tiers set CONSTRAINT LEVELS across all techniques simultaneously.

| Tier | Name | Role | Trigger | USC | Experts | Skeleton |
|------|------|------|---------|-----|---------|----------|
| QUICK | **Velites** | Light skirmishers | R≤3 ∧ Q≤5 | 0 | 0 | Direct |
| ANALYTICAL | **Hastati** | Front line | R=4-6 ∨ Q=6-7 | 2 | 3 | Light |
| DELIBERATE | **Principes** | Second line | R≥7 ∨ K≥6 ∨ Q≥8 | 3 | 5 | Full/DAG |
| MAXIMUM | **Triarii** | Veterans | R≥9 ∨ K≥8 ∨ /deep | 5 | 5-8 | GoT |

> *"It has come to the Triarii"* — Roman saying for when the situation demands everything you have.

**RKQDE scoring:** R=Reasoning depth, K=Knowledge complexity, Q=Quality stakes, D=Decomposition breadth, E=Edge-case density.

---

## THE PIPELINE

17 modules across 4 zones. Sequential numbering, no gaps.

### PRE-FLIGHT (LEGIO-00 → 03) — Before the legion moves

| # | File | Name | Function |
|---|------|------|----------|
| 00 | `LEGIO-00-IMPERATUS_CORE_.md` | **Imperatus** | Scores query (RKQDE). Selects mode tier. Sets success criteria. Issues sealed manifest. |
| 01 | `LEGIO-01-ARMATURA_CORE_.md` | **Armatura** | Sets constraint LEVELS for every technique. Pipeline is fixed — dials, not switches. |
| 02 | `LEGIO-02-CONTRACT_SEAL_.md` | **The Seal** | Anti-lazy contract. 嘘契約 epistemic binding. Shortcut = restart. Signs before execution. |
| 03 | `LEGIO-03-USC_MOD_.md` | **USC** | Universal Self-Consistency. Generates N candidates (0/2/3/5 by mode). Selects or synthesises. |

### ASSEMBLY (LEGIO-04 → 06) — Assembling the force

| # | File | Name | Function |
|---|------|------|----------|
| 04 | `LEGIO-04-CONSILIUM_MOD_.md` | **Consilium** (MR.RUG) | War council. Assembles domain experts. Each expert surveys terrain, proposes nodes. |
| 05 | `LEGIO-05-LEGATUS_CORE_.md` | **Legatus** (SkeletrainOT) | Field general. Builds execution skeleton. Lays all 6 track types. Seals railroad. |
| 06 | `LEGIO-06-PROMPT-BOMBS_KIT_.md` | **Prompt Bombs** | Pre-compressed context packets. Planted at coordinates. Detonate on trigger. |

### EXECUTION (LEGIO-07 → 10) — The legion marches

| # | File | Name | Function |
|---|------|------|----------|
| 07 | `LEGIO-07-FCOT-COC_MOD_.md` | **FCoT / CoC** | Reasoning style per node. FCoT = exploration. CoC = deterministic. Hybrid available. |
| 08 | `LEGIO-08-BATON-SWARM_MOD_.md` | **Baton Bolt / Swarm** | Execution patterns. Baton = sequential handoff. Swarm = parallel strike. + Iteration. |
| 09 | `LEGIO-09-COVE_MOD_.md` | **CoVE** | Chain of Verification. Factual / Logical / Consistency / Multi-Expert variants. |
| 10 | `LEGIO-10-PGSCAN-ARQ_MOD_.md` | **PGScan + ARQ** | Post-execution gap scan. Cross-candidate synthesis. ARQ quality gates. |

### REFINE & OUTPUT (LEGIO-11 → 16) — After the battle

| # | File | Name | Function |
|---|------|------|----------|
| 11 | `LEGIO-11-CENSOR_CORE_.md` | **Censor** (ISC) | Mission assurance. Refines against success criteria. Won't release until objective secured. SYSTEM-CORE. |
| 12 | `LEGIO-12-SELF-REFLECT_MOD_.md` | **Self-Reflect-Adapt** | Technique effectiveness audit. Pattern capture. Meta-analysis at Triarii. |
| 13 | `LEGIO-13-OUTPUT-FORMAT_MOD_.md` | **Output Format** | Format selection: Narrative / MLDoE / CEP — based on what comes AFTER. |
| 14 | `LEGIO-14-FINAL-REFLECT_MOD_.md` | **Final Reflection** | Last quality pass. Success criteria check. Confidence gate. |
| 15 | `LEGIO-15-QMDR_MOD_.md` | **QMDR / MLDoE** | Multi-Layer Density of Experts enrichment. Cross-candidate learning synthesis. |
| 16 | `LEGIO-16-CEP_MOD_.md` | **CEP** | Context Engineering Protocol. Memory compression. 嘘契約 final check. |

---

## ARCHITECTURE

```
              HUMAN LAYER                      MACHINE LAYER
        ┌──────────────────┐            ┌──────────────────────┐
        │  LEGIO-*.md      │            │  AGENTS.md           │
        │  (17 spec files) │──→ FORGE ──│  (S2A compressed     │
        │  Human-readable  │   (MCP)    │   onboarding doc)    │
        │  Full elaboration│            │  Model reads this    │
        └──────────────────┘            └──────────┬───────────┘
                                                    │
                                                    ▼
                                         ┌──────────────────────┐
                                         │  Claude Code         │
                                         │  (Runtime execution) │
                                         │  Follows the railroad│
                                         └──────────────────────┘
```

- **Specs** (LEGIO-*.md) = human-readable blueprints
- **Forge** = offline MCP compiler. Reads specs, applies S2A compression, outputs AGENTS.md
- **AGENTS.md** = onboarding document a model reads before executing
- **Runtime** = Claude Code (or any agent) executing the pipeline. No decisions — follow the railroad

---

## CROSS-CUTTING SYSTEMS

| System | Status | How It Works |
|--------|--------|-------------|
| **Tier System** (Velites → Triarii) | DEFERRED | Constraint overlays applied AFTER full path documented |
| **ARQ** (Quality Gates) | DEFINED | Co-located with 4 hosts: Consilium, Legatus, PGScan, Self-Reflect |
| **GoT** (Graph-of-Thought) | DONE | In Legatus. Three topologies: Railroad (SoT), Rail Network (DAG), Metro (GoT) |
| **嘘契約** (Epistemic Contract) | DONE | In The Seal. ①knows non-compliance ∧ ②knows instruction ∧ ③pretends done = LIE |

**Absorbed into other modules (no standalone spec needed):**
- Success Criteria Lock → inside Imperatus `[ground]` tag
- Buffer Valet → FUTURE (commented out in v30)
- ARQ pre-flight → co-located with host modules

---

## BUILD PROGRESS

```
PRE-FLIGHT (00-03):  ████████████ DONE  (Imperatus + Armatura + Seal + USC)
ASSEMBLY (04-06):    ████████░░░░ 2/3   (Consilium TODO)
EXECUTION (07-10):   ░░░░░░░░░░░░ 0/4
REFINE (11-16):      ░░░░░░░░░░░░ 0/6
CROSS-CUTTING:       ████████░░░░ 3/5

TOTAL: 6 written + 4 meta / 17 modules needed
```

---

## MODULE INDEX

| # | File | Name | Zone | Status |
|---|------|------|------|--------|
| 00 | `LEGIO-00-IMPERATUS_CORE_.md` | Imperatus | SYSTEM-CORE | DONE |
| 01 | `LEGIO-01-ARMATURA_CORE_.md` | Armatura | SYSTEM-CORE | DONE |
| 02 | `LEGIO-02-CONTRACT_SEAL_.md` | The Seal + 嘘契約 | PRE-FLIGHT | DONE |
| 03 | `LEGIO-03-USC_MOD_.md` | USC | PRE-FLIGHT | DONE |
| 04 | `LEGIO-04-CONSILIUM_MOD_.md` | Consilium (MR.RUG) | ASSEMBLY | TODO |
| 05 | `LEGIO-05-LEGATUS_CORE_.md` | Legatus (SkeletrainOT) + GoT | SYSTEM-CORE | DONE |
| 06 | `LEGIO-06-PROMPT-BOMBS_KIT_.md` | Prompt Bombs | ASSEMBLY | DONE |
| 07 | `LEGIO-07-FCOT-COC_MOD_.md` | FCoT / CoC | EXECUTION | TODO |
| 08 | `LEGIO-08-BATON-SWARM_MOD_.md` | Baton Bolt / Swarm | EXECUTION | TODO |
| 09 | `LEGIO-09-COVE_MOD_.md` | CoVE | EXECUTION | TODO |
| 10 | `LEGIO-10-PGSCAN-ARQ_MOD_.md` | PGScan + ARQ | EXECUTION | TODO |
| 11 | `LEGIO-11-CENSOR_CORE_.md` | **Censor** (ISC) | SYSTEM-CORE | TODO |
| 12 | `LEGIO-12-SELF-REFLECT_MOD_.md` | Self-Reflect-Adapt | REFINE | TODO |
| 13 | `LEGIO-13-OUTPUT-FORMAT_MOD_.md` | Output Format | OUTPUT | TODO |
| 14 | `LEGIO-14-FINAL-REFLECT_MOD_.md` | Final Reflection | OUTPUT | TODO |
| 15 | `LEGIO-15-QMDR_MOD_.md` | QMDR / MLDoE | OUTPUT | TODO |
| 16 | `LEGIO-16-CEP_MOD_.md` | CEP + 嘘契約 final | OUTPUT | TODO |
| — | `LEGIO-ARCHITECTURE-v1.md` | Architecture Decision Record | META | DONE |
| — | `LEGIO-FORGE-SCHEMA_SPEC_.md` | Forge Schema | META | DONE |
| — | `LEGIO-STATUS.md` | Translation Status | META | DONE |
| — | `LEGIO-OVERVIEW.md` | This document | META | DONE |

---

*LEGIO v30.2 | System Overview | 2026-02-16*
*"Imperatus commands. Consilium advises. Legatus plans. The legion executes. Censor secures."*
