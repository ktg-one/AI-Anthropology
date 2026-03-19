---
title: 'LEGIO Init-Ready MCP Fit Spec'
slug: 'legio-init-ready-mcp-fit'
created: '2026-02-21'
status: 'ready-for-development'
stepsCompleted: [1, 2, 3, 4]
tech_stack:
  - 'Markdown specs (LEGIO-00..16)'
  - 'MCP servers (imperatus, legio-forge)'
  - 'AGENTS.md runtime contract'
  - 'Cursor/BMAD workflow-init'
files_to_modify:
  - 'LEGIO-2026/LEGIO-OVERVIEW.md'
  - 'LEGIO-2026/LEGIO-STATUS.md'
  - 'LEGIO-FORGE-SCHEMA_SPEC_.md'
  - 'LEGIO-00-IMPERATUS_CORE_.md'
  - 'LEGIO-05-LEGATUS_CORE_.md'
  - '.cursor/commands/bmad/bmm/workflows/workflow-init.md'
  - '_bmad/core/tasks/workflow.xml'
  - '_bmad/bmm/workflows/workflow-status/init/workflow.yaml'
code_patterns:
  - 'Tag-driven MCP tools with stateful progression'
  - 'HALT/PROCEED gates with explicit statuses'
  - 'Manifest-first planning -> runtime execution'
test_patterns:
  - 'Given/When/Then acceptance checks per phase'
  - 'Contract validation for MCP tool schemas'
  - 'Round-trip template activation checks for AGENTS.md'
---

# Tech-Spec: LEGIO Init-Ready MCP Fit

**Created:** 2026-02-21

## Overview

### Problem Statement

LEGIO has complete module specs and a strong architecture baseline, but `/init`-ready execution is blocked by unresolved integration details: formation template implementation, skill-to-MCP migration boundaries, contract normalization across `imperatus` and `forge`, and a single operational tracking surface that proves coverage and flow parity.

### Solution

Implement a gap-focused architecture fit program: preserve settled LEGIO-2026 decisions, resolve only unclear/conflicting placement areas, and ship a phased `/init` rollout contract with measurable gates for coverage parity, flow parity, and tool contract parity.

### Scope

**In Scope:**
- Compare current LEGIO docs against LEGIO-2026 architecture baseline.
- Build coverage/flow/contract parity matrix for modules 00..16 + forge.
- Recommend target placement only for unresolved areas (framework vs MCP vs skill).
- Define `/init` activation sequence, gating checkpoints, and rollout phases.
- Define acceptance criteria and verification plan to start implementation safely.

**Out of Scope:**
- Coding MCP servers in this step.
- Editing module behavior beyond documented gap resolutions.
- Re-litigating settled architecture choices already explicit in LEGIO-2026.

## Context for Development

### Codebase Patterns

- LEGIO baseline already asserts `MCP is the agent framework`, with `imperatus` as strategic server and `forge` as template-sealing path.
- System spine is fixed (Imperatus -> Legatus -> Censor), while mode tiers adjust strictness and activation depth.
- Contracts are tag-based (`begin/ground/...`, `begin/survey/track/...`) with explicit status outputs and halting semantics.
- Runtime target is `AGENTS.md` execution; planning/assembly belongs to MCP and template-generation layers.

### Files to Reference

| File | Purpose |
| ---- | ------- |
| `LEGIO-2026/LEGIO-OVERVIEW.md` | Canonical architecture, pipeline, and migration intent |
| `LEGIO-2026/LEGIO-STATUS.md` | Completion status and unresolved priorities |
| `ARCHIVE/LEGIO-2026-ARCHITECTURE-v1_pre-combine.md` | Historical ADR context and prior assumptions |
| `LEGIO-FORGE-SCHEMA_SPEC_.md` | Interactive forge model and AGENTS.md schema |
| `LEGIO-00-IMPERATUS_CORE_.md` | Strategic MCP contract and manifest semantics |
| `LEGIO-05-LEGATUS_CORE_.md` | Tactical planning contract and railroad manifest |
| `LEGIO-11-CENSOR_CORE_.md` | Mission-assurance closure and synthesis gates |
| `.cursor/commands/bmad/bmm/workflows/workflow-init.md` | Existing `/init` workflow entry command |

### Technical Decisions

1. **Keep settled architecture**
   - Preserve LEGIO-2026 decision that MCP is framework layer.
   - Preserve AGENTS.md as runtime execution contract.

2. **Placement policy (only unresolved areas)**
   - Use MCP when stateful orchestration, gating, or cross-model portability is required.
   - Use skills for local augmentation patterns that do not require portable tool contracts.
   - Keep framework responsibilities for lifecycle, routing, and orchestration boundary enforcement.

3. **Parity gates**
   - Coverage parity: every required module capability represented in target placement.
   - Flow parity: phase order and halt/proceed semantics preserved.
   - Contract parity: input/output/status behavior stable across MCP interfaces.

## Implementation Plan

### Tasks

1. **Baseline lock and parity map**
   - Build a matrix from LEGIO-2026 baseline for `module -> phase -> required capability`.
   - Mark each capability as `settled` or `gap`.
   - Output artifact: `ArchitectureFitMatrix`.

2. **Gap-focused placement decisions**
   - Resolve only unresolved areas with deterministic target placement.
   - Add rationale linked to coverage/flow/contract parity.
   - Output artifact: `PlacementDecisions`.

3. **`/init` activation contract**
   - Define `/init` inputs, startup checks, phase entry criteria, and fail-fast responses.
   - Include how `workflow-init` invokes baseline loading and gate validation.
   - Output artifact: `InitActivationContract`.

4. **Phased rollout with gates**
   - Define implementation phases P1..P4 with entry/exit criteria.
   - Include measurable quality gates and rollback triggers.
   - Output artifact: `RolloutPlan`.

5. **Tracking and evidence model**
   - Define single status surface (`fit-status`) for module parity and rollout progress.
   - Include evidence fields: `source`, `decision`, `verification`, `date`, `owner`.
   - Output artifact: `TrackingSchema`.

### Gap Matrix (Current -> Target -> Decision)

| Area | Current State | Gap | Target Placement | Decision |
| ---- | ------------- | --- | ---------------- | -------- |
| Formation templates (6 named formations) | Declared but pending specifics | Missing concrete activation matrices | MCP (`legio-forge`) + template library | Forge owns template authoring/sealing; runtime reads AGENTS.md only |
| Skills -> MCP migration (`mr-rug`, `enrichweave`, `context`, `ktg-prompt-forge`) | Migration intent documented | Boundary between skill fallback vs MCP not explicit | MCP-first, skill-fallback only for local non-portable ops | For portability, define MCP contract per migrated skill capability |
| `imperatus` vs `forge` overlap | Both mention planning concerns | Potential duplicated authority in scoring/proposal phases | Framework boundary + MCP delegation map | `imperatus` = strategic command contract; `forge` = interactive template assembly that consumes strategic outputs |
| 17-module vs 18-step references | Both appear in docs | Onboarding ambiguity for `/init` and tracking | Framework-level canonical map file | Canonicalize to 17 module IDs with explicit compatibility mapping for legacy 18-step labels |
| `/init` boot sequence | Command exists but not LEGIO-fit-specific | Missing deterministic LEGIO bootstrap checks | Framework init workflow + MCP health checks | Add preflight checklist: baseline docs, contract schemas, template availability |
| Contract statuses across tools | Status enums differ (`MANIFEST_READY`, `RAILROAD_READY`, `FORMATION_SEALED`) | No unified gate semantics table | Framework-level gate adapter | Create normalized gate states: `READY`, `HALT`, `REVISE`, `SEALED`, mapped from each tool |
| Tracking surface | Status docs are narrative | No operational parity tracker | Framework-level `fit-status` artifact | Add machine-readable progress matrix for modules, contracts, and rollout phases |
| Censor closure in `/init` path | Detailed module spec exists | `/init` does not explicitly require closure readiness check | Framework gate requiring closure criteria presence | `/init` fails if mission-assurance criteria fields are absent |

### Recommended Placement (Only Unresolved Areas)

- **MCP (`imperatus`)**
  - Strategic scoring, mode/formation selection policy, manifest authority, halt/reconsider/adapt semantics.
- **MCP (`legio-forge`)**
  - Interactive clarification/proposal, template authoring, AGENTS.md sealing, formation library operations.
- **Framework (`/init` + orchestration layer)**
  - Startup validation, parity gate execution, canonical step/module mapping, unified status adapter, fit tracking.
- **Skills (fallback/augmentation only)**
  - Local, non-portable enrichments where MCP contract is not yet implemented; must be explicitly marked as temporary.

## `/init` Activation Sequence

1. **Bootstrap**
   - Load canonical baseline docs and canonical map (`17-module with legacy 18-step crosswalk`).
2. **Contract Readiness Check**
   - Validate MCP contract schemas for `imperatus` and `legio-forge`.
3. **Template Readiness Check**
   - Confirm formation templates available or generatable.
4. **Parity Gate**
   - Run coverage/flow/contract parity checks; fail fast on red conditions.
5. **Seal Init State**
   - Emit `fit-status` snapshot with decision/evidence links.

## Acceptance Criteria

1. **Coverage parity**
   - Given baseline module capabilities, when fit mapping runs, then every required capability is either `settled` or assigned a single unresolved gap decision.
2. **Flow parity**
   - Given the SAS spine and phase ordering, when `/init` validates orchestration, then no ordering change bypasses Imperatus->Legatus->Censor responsibilities.
3. **Contract parity**
   - Given `imperatus` and `legio-forge` schemas, when status normalization executes, then each tool status maps to one unified gate state without ambiguity.
4. **Gap-only recommendations**
   - Given settled architecture items, when placement decisions are produced, then no recommendation overrides settled items unless an explicit conflict is detected and documented.
5. **`/init` fail-fast behavior (edge)**
   - Given missing required schema/template/baseline artifact, when `/init` runs, then initialization halts with actionable diagnostics and no partial activation.
6. **Tracking completeness**
   - Given a completed `/init` run, when `fit-status` is generated, then each decision includes source, rationale, verification evidence, and timestamp.
7. **Legacy compatibility (edge)**
   - Given references using 18-step naming, when `/init` reads them, then crosswalk mapping resolves them to canonical 17-module IDs without dropping semantics.
8. **Temporary skill fallback control (edge)**
   - Given a gap requiring skill fallback, when recorded, then fallback is labeled temporary with explicit MCP migration target and exit criteria.

## Additional Context

### Dependencies

- Stable baseline docs in `LEGIO-2026`.
- Existing module specs (`LEGIO-00..16`).
- Forge schema doc and tool contracts.
- Workflow init command path and core workflow engine files.

### Testing Strategy

- **Spec validation pass**
  - Verify all unresolved gaps have one owner and one target placement.
- **Contract simulation pass**
  - Table-test status mappings for `imperatus` and `legio-forge` against unified gate states.
- **`/init` dry-run pass**
  - Simulate missing-schema, missing-template, and malformed-crosswalk cases to confirm fail-fast behavior.
- **Traceability pass**
  - Ensure each placement decision links to at least one baseline source and one acceptance criterion.

### Notes

- This spec is intentionally implementation-ready but code-neutral.
- The plan preserves architecture intent and only resolves unresolved operational seams.
- First coding slice should implement the canonical map + status adapter before template or migration expansion.
