# pass_sequence — Team Topology

The fractal engine determines handoff count per mode tier.
Each → is a HITL gate. Human = convergence criterion.

## Tier Mappings

### 2x — Velites (Quick)

```
Imperatus → Censor
```

Skip Legatus. Fast path. Direct command → direct verification.
Trigger: Σ ≤ 12 ∧ Danger ≤ 5

### 3x — Hastati (Analytical)

```
Imperatus → Legatus → Censor
```

Full spine. Plan before execute. Standard path.
Trigger: Σ 13-25 ∨ Danger 6-7

### 4x — Principes (Deliberate)

```
Imperatus → Consilium → Legatus → Censor
```

Expert council assembled before planning. MR.RUG experts engaged.
Trigger: Σ 26-38 ∨ Danger 8

### 8x/nx — Triarii (Maximum)

```
Imperatus → Consilium → Legatus → [Workers] → Censor
                                      ↑
                              [ENRICH → EXECUTE]×n
```

Full cascade. Every module. Recursive until HITL convergence.
Trigger: Σ ≥ 39 ∨ Danger ≥ 9

## Agent Roster

### Layer 1: Doctrine MCP Servers

| Server | Function | Status |
|--------|----------|--------|
| `imperatus` | RKQDE scoring, mode tier, sealed manifest. 10 tags, 5 domains. | Built |
| `legatus` | SkeletrainOT railroad planning. 7 tags, 5 domains, 6 track types. | Built |
| `lotus-wisdom` | General contemplation. Every agent gets this. | Live (npm) |

Censor has NO MCP — ToT+CoD is agent behavior, not a thinking tool.

### Layer 2: Agent Definitions (.claude/agents/)

**Core Officers** (model assignment OPEN):

| Agent | Cognitive Pattern | MCP Tools |
|-------|------------------|-----------|
| `imperatus-commander` | Lotus contemplation (iterative tag flow) | imperatus + lotus-wisdom |
| `legatus-commander` | Lotus contemplation (track-laying) | legatus + lotus-wisdom |
| `censor-officer` | ToT 5-path synthesis + CoD 3-stage curation | lotus-wisdom only |

**Consilium Experts** (permanent trained MR.RUG roles):

| Agent | Domain |
|-------|--------|
| `mr-rug-methodology` | Reasoning strategy selection |
| `mr-rug-user-model` | User intent + context |
| `mr-rug-guardrails` | Constraint enforcement |

**Workers:**

| Agent | Zone |
|-------|------|
| `assembly-worker` | Modules 04-06 |
| `refine-worker` | Modules 12-16 |
| `cep-agent` | Module 16 (context packets) |

## Model Assignment — OPEN

Not locked. The `cross_model` block in the Imperatus manifest supports:
- `planning`: model for strategic/tactical officers
- `execution`: model for workers
- `verification`: model for Censor + guardrails

Current candidates (not assigned):
- Claude Opus — deep reasoning (Imperatus candidate)
- Claude Sonnet — fast workers
- Gemini — flagged for later phases (agentic flows)
- Codex — flagged for verification/review patterns

## Experimental Zones

**Pre-Flight (00-03)** and **Execution (07-10)** supervision:
- Not assigned to agents or MCPs
- Actively experimenting: runtime enforcement vs agentic flow
- Decision deferred by design

## Not In Scope

- EXECUTE phase runtime (07-10 supervision)
- Prompt bombs implementation (CEP vs embedding)
- Forge MCP compiler (superseded by agent definitions)
- Tier overlays / formation templates
