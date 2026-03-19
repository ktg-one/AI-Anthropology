# LEGIO TRANSLATION STATUS
**Last updated: 2026-03-01 | v31 (Architecture v2)**

---

## COMPLETED SPECS (15 modules) — ALL MODULES DONE

| # | File | Name | Zone | Status |
|---|------|------|------|--------|
| 00 | `specs/LEGIO-00-I.M.P.E.R.A.T.U.S.md` | Imperatus | SYSTEM-CORE | DONE |
| 01 | `specs/LEGIO-01-A.R.M.A.T.U.R.A.md` | Armatura (The Arsenal) | SYSTEM-CORE | DONE |
| 02 | `specs/LEGIO-02-CONTRACT_SEAL_.md` | The Seal + 嘘契約 | PRE-FLIGHT | DONE |
| 03 | `specs/LEGIO-03-USC_MOD_.md` | USC | PRE-FLIGHT | DONE |
| 04 | `specs/LEGIO-04-CONSILIUM_MOD_.md` | Consilium (MR.RUG + GSIF) | ASSEMBLY | DONE |
| 05 | `specs/LEGIO-05-L.E.G.A.T.U.S_.md` | Legatus (SkeletrainOT) + GoT | SYSTEM-CORE | DONE |
| 06 | `specs/LEGIO-06-PROMPT-BOMBS_KIT_.md` | Prompt Bombs | ASSEMBLY | DONE |
| 07 | `specs/LEGIO-07-FCOT-COC_MOD_.md` | FCoT / CoC Reasoning Router | EXECUTION | DONE |
| 08 | `specs/LEGIO-08-BATON-SWARM_MOD_.md` | Baton Bolt / Swarm | EXECUTION | DONE |
| 09 | `specs/LEGIO-09-COVE_MOD_.md` | CoVE + 10Rs + Negentropy | EXECUTION | DONE |
| 10 | `specs/LEGIO-10-PGSCAN-ARQ_MOD_.md` | PGScan + ARQ Gate 3 | EXECUTION | DONE |
| 11 | `specs/LEGIO-11-C.E.N.S.O.R.md` | Censor (ISC) | SYSTEM-CORE | DONE |
| 12 | `specs/LEGIO-12-SELF-REFLECT_MOD_.md` | Self-Reflect-Adapt | REFINE & OUTPUT | DONE |
| 13 | `specs/LEGIO-13-OUTPUT-FORMAT_MOD_.md` | Output Format Selection | REFINE & OUTPUT | DONE |
| 14 | `specs/LEGIO-14-FINAL-REFLECT_MOD_.md` | Final Reflection + 嘘契約 | REFINE & OUTPUT | DONE |

## OUTPUT TEMPLATES (`templates/`)

Separated from specs — these are output format templates, not cascade steps.

| File | Purpose | Status |
|------|---------|--------|
| `LEGIO-OUTPUT-ENRICH-WEAVE.md` | Enrichment/compression output (was module 15) | DONE |
| `LEGIO-OUTPUT-CEP.md` | Context packet generation (was module 16) | DONE |
| `LEGIO-OUTPUT-NARRATIVE.md` | Narrative output format | NEW |

---

## INFRASTRUCTURE

### MCP Servers (3 Doctrine MCPs)

| Server | Location | Status | Tools |
|--------|----------|--------|-------|
| `imperatus` | `01-IMPERATUS/` | Built, registered | `imperatus`, `imperatus_manifest` |
| `legatus` | `02-LEGATUS/` | Built, registered | `skeletrain`, `skeletrain_manifest` |
| `lotus-wisdom` | `npx lotus-wisdom-mcp` | Live (npm) | `lotuswisdom`, `lotuswisdom_summary` |

Censor has NO MCP — ToT+CoD is agent behavior, not a thinking tool.

### Agent Definitions (9, in `.claude/agents/`)

| Agent | Role | MCP Access | Status |
|-------|------|------------|--------|
| `imperatus-commander` | Strategic command | imperatus + lotus-wisdom | Created |
| `legatus-commander` | Tactical planning | legatus + lotus-wisdom | Created |
| `censor-officer` | Mission assurance | lotus-wisdom only | Created |
| `mr-rug-methodology` | Consilium: reasoning strategy | lotus-wisdom | Created |
| `mr-rug-user-model` | Consilium: user intent | lotus-wisdom | Created |
| `mr-rug-guardrails` | Consilium: constraints | lotus-wisdom | Created |
| `assembly-worker` | Assembly zone (04-06) | lotus-wisdom | Created |
| `refine-worker` | Refine zone (12-16) | lotus-wisdom | Created |
| `cep-agent` | Context packets (16) | lotus-wisdom | Created |

### Onboarding Docs (`onboard/`)

| File | Purpose | Version |
|------|---------|---------|
| `LEGIO-DUPLEX-IMBUED-MODULE-MAP.md` | IMBUED model instructions (Pass 1 compiler) | v31 |
| `LEGIO-DUPLEX-EXECUTE-INSTRUCT.md` | EXECUTE model prompt (Pass 2 runtime) | v31 |
| `LEGIO-FORMATION-DOCTRINEI.md` | Formation routing doctrine | v31 |
| `LEGIO-FRAMEWORK-EXPLAINER.md` | Framework explainer for onboarding | v31 |
| `LEGIO-FORGE-SCHEMA_SPEC_.md` | Forge architecture + AGENTS.md schema | v30.2 |

---

## ARCHITECTURE DECISIONS

### Decided (locked)

| Decision | Date | Detail |
|----------|------|--------|
| 3 Doctrine MCPs (not 7) | 2026-02-28 | imperatus + legatus + lotus-wisdom. Censor is agent-only. |
| 9 agent definitions | 2026-02-28 | 3 officers + 3 MR.RUG experts + 3 workers |
| pass_sequence topology | 2026-02-28 | Velites(2x) → Hastati(3x) → Principes(4x) → Triarii(8x/nx) |
| Formation Doctrine | 2026-02-28 | IMBUED/ENRICH/EXECUTE control laws. 4 formations (DUPLEX→DELOITTE). |
| MCPs = thinking tools, Models = roles | 2026-02-28 | MCPs are calculators, models are craftsmen. Each model uses its MCP as contemplation aid. |
| LEGIO = framework, not prompt cascade | 2026-02-26 | Forge offline → AGENTS.md templates. 5 permanent experts replace dynamic MR.RUG. |
| Prompt Bombs eliminated | 2026-02-26 | Embeddings + skeleton imprint replace runtime bombs (module 06). |
| Repository restructure | 2026-03-01 | Flat 40+ files → specs/, onboard/, templates/, 01-IMPERATUS/, 02-LEGATUS/, 03-LEGION-MARCH/, 04-CENSOR/, archive/ |
| Modules 15+16 → templates | 2026-03-01 | ENRICH-WEAVE + CEP are output templates, not cascade steps. Moved to templates/ with NARRATIVE. |

### Experimental (testing)

| Area | Status | Notes |
|------|--------|-------|
| Pre-Flight supervision (00-03) | UNDECIDED | Runtime enforcement vs agentic flow |
| Execution supervision (07-10) | UNDECIDED | Runtime enforcement vs agentic flow |
| Model assignment | TESTING | Opus/Imperatus, ChatGPT/Legatus, ClaudeCode/Consilium+Execution, Gemini/Censor |

---

## CROSS-CUTTING

| Item | Status | Notes |
|------|--------|-------|
| Tier system (Velites/Hastati/Principes/Triarii) | DEFERRED | Constraint overlays AFTER smoke test |
| ARQ (Quality Gates) | DEFINED | Co-located with 4 hosts: Consilium, Legatus, PGScan, Self-Reflect |
| GoT elaboration | DONE | In Legatus (LEGIO-05). Three topologies. Cycle budget. |
| Formation Doctrine | DONE | `onboard/LEGIO-FORMATION-DOCTRINEI.md` |
| pass_sequence topology | DONE | `docs/architecture/pass-sequence-topology.md` |

---

## OVERALL PROGRESS

```
SPECS (15/15):       ████████████ DONE
TEMPLATES (3/3):     ████████████ DONE
MCP SERVERS (3/3):   ████████████ DONE
AGENT DEFS (9/9):    ████████████ DONE
ONBOARD DOCS (5/5):  ████████████ DONE
CROSS-CUTTING:       ████████░░░░ 3/5
SMOKE TEST:          ░░░░░░░░░░░░ NOT STARTED
```

---

## NEXT PRIORITIES

1. **Smoke test** — Verify imperatus + legatus + agent definitions work end-to-end
2. **Variants folder** — Move TRIPLEX-IMPERATUS + DUPLEX specs out of MCP folders into proper location
3. **Experimental zones** — Decide Pre-Flight/Execution supervision approach
4. **Tier overlays** — Velites→Triarii constraint tables for each module
5. **Formation templates** — 6 use-case configs (Testudo, Triplex Acies, Cuneus, Orbis, Coding, Creative)
6. **Skills → MCP migration** — mr-rug, enrichweave, context, ktg-prompt-forge → universal MCP tools

---

## ARCHIVED (2026-03-01)

Moved to `archive/`:
- `LEGIO-08-PROMPT-BOMBS_KIT_.md` — Misnamed duplicate of LEGIO-06
- `LEGIO-15-QMDR_MOD_.md` — Superseded by ENRICH-WEAVE
- `01-LEGIO-Imperatus.md` — Superseded by LEGIO-00
- `AGENTS.md` — ktg.one web audit, not LEGIO agents
- `GEMINI.md` — Auto-generated summary
- `new 3.json` — Stray file
