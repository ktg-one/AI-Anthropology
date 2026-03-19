# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## SESSION START — CHECK EXTERNAL MEMORY FIRST

Before doing ANY work, check these memory stores for cross-session context:
1. `mcp__mem0__search-memories` — search "LEGIO", "imperatus", "session" (userId: "ktg-kevin")
2. `in-memoria` MCP — check conversation persistence if available
3. Read auto-memory: `~/.claude/projects/.../memory/MEMORY.md`
4. Do NOT skip this. Context loss across compactions/sessions is the #1 problem.

## What This Is

LEGIO (Legion Engineered Governance of Intelligent Operations) — a 17-module prompt engineering cascade (KTG-DIRECTIVE v30.2) formalized as an agentic framework via 3 Doctrine MCP servers + 9 Claude Code agent definitions. All 17 module specs are complete. Architecture v2 (2026-02-28) supersedes the earlier 7-server plan.

**Parent repo:** `../` contains the original KTG methodology files that LEGIO formalizes. The parent has its own `CLAUDE.md` with root-level context.

## Repository Structure

```
LEGIO-2026/
├── CLAUDE.md                        # This file
├── LEGIO-OVERVIEW.md                # Single source of truth (architecture, command chain)
├── LEGIO-STATUS.md                  # Translation progress tracker
│
├── .claude/agents/                  # 9 agent definitions (Claude Code auto-discovers)
│
├── specs/                           # 15 module specs, 00-14 (read-only reference)
│   └── LEGIO-{00..14}-*.md
│
├── templates/                       # Output format templates
│   ├── LEGIO-OUTPUT-ENRICH-WEAVE.md         # Enrichment/compression output
│   ├── LEGIO-OUTPUT-CEP.md                  # Context packet output
│   └── LEGIO-OUTPUT-NARRATIVE.md            # Narrative output
│
├── onboard/                         # Agent onboarding + operational docs
│   ├── LEGIO-DUPLEX-IMBUED-MODULE-MAP.md    # IMBUED model instructions
│   ├── LEGIO-DUPLEX-EXECUTE-INSTRUCT.md     # EXECUTE model prompt
│   ├── LEGIO-FORMATION-DOCTRINEI.md         # Formation routing doctrine
│   ├── LEGIO-FRAMEWORK-EXPLAINER.md         # Framework explainer
│   └── LEGIO-FORGE-SCHEMA_SPEC_.md          # Forge architecture
│
├── 01-IMPERATUS/                    # Strategic command MCP
│   ├── index.ts, http-server.ts, cli.js, package.json, tsconfig.json
│   ├── dist/                        # Build artifacts
│   └── LEGIO-TRIPLEX-IMPERATUS.MD   # Triplex formation variant
│
├── 02-LEGATUS/                      # Tactical planning MCP
│   ├── index.ts, cli.js, package.json, tsconfig.json
│   └── dist/                        # Build artifacts
│
├── 03-LEGION-MARCH/                 # Execution + enrichment materials
│   ├── LEGIO-ENRICH-WEAVE_MOD__2.md
│   ├── QMDR-ENRICH-WEAVE-10000.md
│   └── Unified Architecture...md
│
├── 04-CENSOR/                       # Mission assurance + output (placeholder)
│
├── docs/
│   ├── architecture/
│   │   └── pass-sequence-topology.md
│   ├── plans/
│   │   ├── 2026-02-26-legio-framework-mcp.md    # Superseded
│   │   └── 2026-02-28-legio-agent-architecture-v2.md
│   └── assets/
│       ├── The_LEGIO_Doctrine-1x.png
│       ├── LEGIO_Sovereign_Command.pdf
│       ├── LEGIO_Tactical_Execution.pdf
│       └── DUPLEX-ARCHITECTURE.mermaid
│
└── archive/                         # Stale/superseded files
    ├── LEGIO-08-PROMPT-BOMBS_KIT_.md    # Misnamed duplicate of LEGIO-06
    ├── LEGIO-15-QMDR_MOD_.md            # Superseded by ENRICH-WEAVE
    ├── 01-LEGIO-Imperatus.md            # Superseded by LEGIO-00
    ├── AGENTS.md                        # ktg.one audit, not LEGIO agents
    ├── GEMINI.md                        # Gemini-generated summary
    └── new 3.json                       # Stray file
```

## Build & Run Commands

### imperatus-mcp (01-IMPERATUS/)
```bash
cd 01-IMPERATUS
npm install
npm run build          # tsc + esbuild → dist/bundle.js (589KB) + dist/http-bundle.js (2.3MB)
npm run start:stdio    # tsc + node dist/index.js (stdio transport)
npm run start:http     # tsc + node dist/http-server.js (Express/StreamableHTTP, port 3000)
npm run dev            # tsc + node dist/index.js
```

### legatus-mcp (02-LEGATUS/)
```bash
cd 02-LEGATUS
npm install
npm run build          # tsc → dist/index.js
npm run start          # node dist/index.js (stdio transport)
npm run dev            # tsc + node dist/index.js
```

**Debug mode (imperatus only):** `IMPERATUS_DEBUG=true node 01-IMPERATUS/dist/bundle.js`

**No test or lint tooling exists.** Verification is `npm run build` (must succeed) + manual MCP smoke tests.

**Three MCP servers coexist (by design):**
- `imperatus` — local config (`.mcp.json`), stdio, `node 01-IMPERATUS/dist/bundle.js`
- `legatus` — local config (`.mcp.json`), stdio, `node 02-LEGATUS/dist/index.js`
- `lotus-wisdom` — user config, stdio, `npx lotus-wisdom-mcp` (general contemplation, every agent gets this)

## Architecture

### Agent Architecture v2 (2026-02-28)

Supersedes the 7-server plan (`docs/plans/2026-02-26-legio-framework-mcp.md`). Implementation plan: `docs/plans/2026-02-28-legio-agent-architecture-v2.md`.

**Layer 1: Doctrine MCP Servers** — thinking engines, commanders invoke them:

| Server | Location | Function | Status |
|--------|----------|----------|--------|
| `imperatus` | `01-IMPERATUS/` | RKQDE scoring, mode tier, sealed manifest. 10 tags, 5 domains. | Built |
| `legatus` | `02-LEGATUS/` | SkeletrainOT railroad planning. 7 tags, 5 domains, 6 track types. | Built |
| `lotus-wisdom` | `npx` | General contemplation. Every agent gets this. | Live (npm) |

Censor has NO MCP — ToT+CoD is agent behavior, not a thinking tool.

**Layer 2: Agent Definitions** (`.claude/agents/`):

| Agent | Role | MCP Tools |
|-------|------|-----------|
| `imperatus-commander` | Strategic command (Lotus contemplation, tag flow) | imperatus + lotus-wisdom |
| `legatus-commander` | Tactical planning (Lotus contemplation, track-laying) | legatus + lotus-wisdom |
| `censor-officer` | Mission assurance (ToT 5-path + CoD 3-stage) | lotus-wisdom only |
| `mr-rug-methodology` | Consilium: reasoning strategy selection | lotus-wisdom |
| `mr-rug-user-model` | Consilium: user intent + context | lotus-wisdom |
| `mr-rug-guardrails` | Consilium: constraint enforcement | lotus-wisdom |
| `assembly-worker` | Assembly zone (modules 04-06) | lotus-wisdom |
| `refine-worker` | Refine zone (modules 12-16) | lotus-wisdom |
| `cep-agent` | Context packet generation (module 16) | lotus-wisdom |

**Layer 3: Model Assignment** — OPEN. `cross_model` manifest block supports planning/execution/verification slots.

**Layer 4: pass_sequence Team Topology** (`docs/architecture/pass-sequence-topology.md`):
- 2x Velites: Imperatus → Censor
- 3x Hastati: Imperatus → Legatus → Censor
- 4x Principes: Imperatus → Consilium → Legatus → Censor
- 8x/nx Triarii: Full cascade, every → = HITL gate

**Experimental zones:** Pre-Flight (00-03) and Execution (07-10) supervision not yet assigned — actively testing runtime vs agentic flow.

### Three-Phase Spine (SYSTEM-CORE, never skippable)

1. **Imperatus** (LEGIO-00) — Strategic command. Scores query via RKQDE, selects mode tier, issues sealed manifest.
2. **Legatus** (LEGIO-05) — Tactical command. Takes manifest, builds execution skeleton, lays tracks.
3. **Censor** (LEGIO-11) — Mission assurance. Refines output against success criteria. Won't release until secured.

### Four Zones, 17 Modules

- Pre-Flight (00-03): Imperatus → Armatura → The Seal → USC
- Assembly (04-06): Consilium (MR.RUG) → Legatus (SkeletrainOT) → Prompt Bombs
- Execution (07-10): FCoT/CoC → Baton/Swarm → CoVE → PGScan+ARQ
- Refine & Output (11-16): Censor (ISC) → Self-Reflect → Output Format → Final Reflection → QMDR → CEP

**Mode tiers:** Velites (Quick, Σ≤12∧Danger≤5) → Hastati (Analytical) → Principes (Deliberate) → Triarii (Maximum, Σ≥39∨Danger≥9)

### Formation Doctrine (onboard/LEGIO-FORMATION-DOCTRINEI.md)

Three control laws — never mixed within a pass:
- **IMBUED** = Compiler (scores, routes, compiles manifest — never generates content)
- **ENRICH** = Analyzer (reads, spots gaps, weaves improvements — never writes prose)
- **EXECUTE** = Author (writes content, detonates bombs — never plans or restructures)

Four formations route passes between these roles:
- 2x DUPLEX (Velites): IMBUED → EXECUTE
- 3x TRIPLEX (Hastati): IMBUED → ENRICH → EXECUTE
- 4x STANDARD (Principes): IMBUED → EXECUTE → ENRICH → EXECUTE
- 8x DELOITTE (Triarii): IMBUED → ENRICH → EXECUTE → [ENRICH → EXECUTE]×3

## MCP Server — `imperatus-mcp`

Located in `01-IMPERATUS/`. TypeScript, ESM, `@modelcontextprotocol/sdk ^1.23`, Node ≥18.

### Source Files
- `index.ts` — `ImperatusServer` class (exported) + stdio bootstrap. 5 command domains, 10 tags, phase ordering enforced, 16 Armatura examine blocks.
- `http-server.ts` — Express + `StreamableHTTPServerTransport`. Imports from `index.ts`. Per-session state. Endpoints: `POST/GET/DELETE /mcp`, `GET /health`.
- `cli.js` — CLI entry point (`imperatus` binary), imports `dist/bundle.js`
- `tsconfig.json` — ES2022 target, NodeNext module resolution, strict mode

### MCP Tools (2)

**`imperatus`** — iterative command engine. Tag flow: `begin → ground → examine... → route → marshal → issue`. Required params: `tag`, `content`, `stepNumber`, `totalSteps`, `nextStepNeeded`. Optional: `query`, `modeOverride`, `examineBlock`, `confidenceScore`, `verbose`.

**`imperatus_manifest`** — read-only manifest + journey summary. No params.

### Key Implementation Details
- `begin` tag auto-resets all state (journey, manifest, tags visited, halt status)
- Phase ordering enforced: each tag has prerequisites (e.g., `ground` requires `begin`, `route` requires `ground`)
- Confidence gate: `confidenceScore < 9` triggers HALT at any `examine` step
- `adapt` tag only available post-`issue` (post-manifest), escalation only (never de-escalate)
- Velites fast path: skips `examine` loop, applies `VELITES_DEFAULTS` automatically
- RKQDE parsed from LLM content via regex (best-effort extraction)
- Mode selection: RKQDE Σ + Danger thresholds, or `modeOverride`
- Formation auto-selected: Orbis (D≥7), Testudo (K≥8), Cuneus (R≤3∧Q≤5), Triplex (default)
- stdio mode: single `ImperatusServer` instance per process
- HTTP mode: per-session `ImperatusServer` via `createMCPServer()` factory

### Known Bug (Fixed 2026-02-26)
The stdio bootstrap guard at the end of `index.ts` checked `includes('index')` but the bundled entry is `dist/bundle.js`. Fixed to `match(/index|bundle/)`. If the server is silently dead, check this guard first.

## MCP Server — `legatus-mcp`

Located in `02-LEGATUS/`. TypeScript, ESM, `@modelcontextprotocol/sdk ^1.23`, Node ≥18. Mirrors imperatus pattern.

### Source Files
- `index.ts` — `LegatusServer` class (exported) + stdio bootstrap. 5 planning domains, 7 tags, 6 track types, phase ordering enforced.

### MCP Tools (2)

**`skeletrain`** — tactical planning engine. Tag flow: `begin → survey → track×6 → assemble → deploy`. Required params: `tag`, `content`, `stepNumber`, `totalSteps`, `nextStepNeeded`. Optional: `trackType` (required for `track` tag), `imperatus_manifest`, `verbose`.

**`skeletrain_manifest`** — read-only railroad manifest state. Optional param: `section`.

### Key Implementation Details
- `begin` tag auto-resets state and loads planning framework
- Phase ordering enforced: `survey` requires `begin`, `track` requires `survey`, etc.
- 6 track types iterate in order: routes → patterns → reasoning → bombs → gates → cove
- All 6 tracks must be laid before `assemble` (enforced — missing tracks = HALT)
- Topology auto-selected from D-score: SoT-Light (D≤3), DAG (D 4-6), GoT (D≥7)
- `deploy` seals railroad with status `RAILROAD_READY` — execution has zero decisions
- `halt`/`revise` for control flow (same pattern as imperatus halt/reconsider)

## Naming Conventions

**Two rules, no exceptions:**
1. **Roman names = command chain roles** (organizational): Imperatus, Armatura, The Seal, Consilium, Legatus, Censor
2. **Original names = techniques** (preserved for model recognition): USC, ARQ, FCoT, CoC, CoVE, PGScan, QMDR, MLDoE, CEP, MR.RUG, SkeletrainOT

Do not rename techniques — models recognise them from training data.

## File Map

### Module Specs (`specs/`, 15 modules, read-only — all complete)
| Range | Files | Zone |
|-------|-------|------|
| 00-03 | `specs/LEGIO-00-I.M.P.E.R.A.T.U.S.md` through `specs/LEGIO-03-USC_MOD_.md` | Pre-Flight |
| 04-06 | `specs/LEGIO-04-CONSILIUM_MOD_.md` through `specs/LEGIO-06-PROMPT-BOMBS_KIT_.md` | Assembly |
| 07-10 | `specs/LEGIO-07-FCOT-COC_MOD_.md` through `specs/LEGIO-10-PGSCAN-ARQ_MOD_.md` | Execution |
| 11-14 | `specs/LEGIO-11-C.E.N.S.O.R.md` through `specs/LEGIO-14-FINAL-REFLECT_MOD_.md` | Refine & Output |

### Output Templates (`templates/`)
- `LEGIO-OUTPUT-ENRICH-WEAVE.md` — Enrichment/compression output (was module 15)
- `LEGIO-OUTPUT-CEP.md` — Context packet generation (was module 16)
- `LEGIO-OUTPUT-NARRATIVE.md` — Narrative output format

### Agent Definitions (`.claude/agents/`)
- 3 core officers: `imperatus-commander.md`, `legatus-commander.md`, `censor-officer.md`
- 3 MR.RUG experts: `mr-rug-methodology.md`, `mr-rug-user-model.md`, `mr-rug-guardrails.md`
- 3 workers: `assembly-worker.md`, `refine-worker.md`, `cep-agent.md`

### Onboarding Docs (`onboard/`)
- `LEGIO-DUPLEX-IMBUED-MODULE-MAP.md` — Pass 1 compiler spec (IMBUED model instructions)
- `LEGIO-DUPLEX-EXECUTE-INSTRUCT.md` — Pass 2 runtime spec (EXECUTE model prompt)
- `LEGIO-FORMATION-DOCTRINEI.md` — Formation routing doctrine (IMBUED/ENRICH/EXECUTE control laws)
- `LEGIO-FRAMEWORK-EXPLAINER.md` — Framework explainer for new users/models
- `LEGIO-FORGE-SCHEMA_SPEC_.md` — Forge architecture, AGENTS.md output schema, interactive flow

### Imperatus Variants
- `specs/LEGIO-00-I.M.P.E.R.A.T.U.S.md` — Canonical module spec (module 00)
- `01-IMPERATUS/LEGIO-TRIPLEX-IMPERATUS.MD` — Triplex formation variant

### Enrichment Variants (`03-LEGION-MARCH/`)
- `templates/LEGIO-OUTPUT-ENRICH-WEAVE.md` — Canonical enrichment template
- `03-LEGION-MARCH/LEGIO-ENRICH-WEAVE_MOD__2.md` — Extended ENRICH-WEAVE v2
- `03-LEGION-MARCH/QMDR-ENRICH-WEAVE-10000.md` — Extended QMDR enrichment spec (36KB)

### Documentation (`docs/`)
- `docs/plans/2026-02-28-legio-agent-architecture-v2.md` — Current: 3 MCPs + 9 agents (13 tasks)
- `docs/plans/2026-02-26-legio-framework-mcp.md` — Superseded: 7-server plan
- `docs/architecture/pass-sequence-topology.md` — Team topology reference
- `docs/assets/The_LEGIO_Doctrine-1x.png` — Visual architecture diagram
- `docs/assets/DUPLEX-ARCHITECTURE.mermaid` — Mermaid diagram

### Archive (`archive/`)
Superseded or misplaced files. See `archive/` for contents.

## CLI Agent Orchestration (Tested 2026-02-26)

Multiple CLIs map to LEGIO roles for parallel execution:

| CLI Agent | LEGIO Role | Modules | Pattern |
|-----------|-----------|---------|---------|
| Claude (Opus) | Imperatus+Legatus+Censor | 00, 02, 05, 11, 13 | Sequential spine |
| gemini-cli | Consilium+Frumentarii | 03, 04, 09, 12, 15 | Analytical/parallel |
| codex-cli | Primus Pilus (Executor) | 06, 07, 08, 10 | Mechanical/sequential |
| jules-cli | Optio (Logistics) | 01, 14, 16 | Async background queue |

## Current Status & Next Priorities

All 17/17 module specs complete. Architecture v2 implemented: 3 MCPs (imperatus built, legatus built, lotus-wisdom live) + 9 agent definitions in `.claude/agents/`. pass_sequence topology documented. Formation doctrine formalized (IMBUED/ENRICH/EXECUTE control laws with 4 formation types).

**Decided:** 3 Doctrine MCPs, 3 core officers, 3 MR.RUG experts, 3 workers, pass_sequence team topology, formation routing doctrine.

**Experimental:** Pre-Flight (00-03) and Execution (07-10) supervision — testing runtime enforcement vs agentic flow.

1. **Smoke test** — Verify legatus-mcp + agent definitions work end-to-end
2. **Experimental zones** — Decide Pre-Flight/Execution supervision approach
3. **Tier overlays** — Velites→Triarii constraint tables for each module
4. **Formation templates** — 6 use-case configs (Testudo, Triplex Acies, Cuneus, Orbis, Coding, Creative)
5. **Skills → MCP** — Migrate mr-rug, enrichweave, context, ktg-prompt-forge to universal MCP tools

## Key Concepts

- **RKQDE**: R=Reasoning depth, K=Knowledge complexity, Q=Quality stakes, D=Decomposition breadth, E=Edge-case density. Σ=sum(max 50), Danger=max(R,K,Q)
- **ARQ Gates**: 4 fixed structural checkpoints (during MR.RUG, after Legatus, before execution end, before output). Imperatus controls strictness, not count.
- **嘘契約 (Anti-Lazy Contract)**: Epistemic honesty binding. ①knows non-compliance ∧ ②knows instruction ∧ ③pretends done = LIE. Enforced project-wide.
- **Confidence Gate**: >9/10 to proceed at each phase boundary
- **S2A Compression**: Full elaboration specs → compressed onboarding docs for model consumption
- **Sealed Railroad**: After Legatus plans, execution follows tracks with zero runtime decisions
- **Armatura Examine Blocks**: 16 constraint dials (BUFFER_VALET through OUTPUT_FORMAT). Dials, not switches — "off" = minimum viable, not absent.
- **Formation Control Laws**: IMBUED (compiler), ENRICH (analyzer), EXECUTE (author) — never mixed within a single pass.
