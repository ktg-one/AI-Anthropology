---
title: "LEGIO Forge — AGENTS.md Schema & Interactive Protocol"
version: "v1.0"
status: "DRAFT"
model: "Multi-model"
tags: ["legio", "forge", "agents-md", "schema", "interactive", "mcp-server", "spec"]
created: "2026-02-16"
updated: "2026-02-16"
creator: "ktg"
category: "spec"
description: "The LEGIO Forge is an interactive MCP server that produces reusable AGENTS.md formation templates. Pre-flight modules become config sections. Claude Code reads AGENTS.md natively and executes. This spec defines: the AGENTS.md output format, the interactive forge session flow, and the template library system."
architectural_pivot: "18-step runtime pipeline → interactive forge (offline) + Claude Code native execution"
depends_on: ["LEGIO-00-IMPERATUS-LOTUS_CORE_.md", "LEGIO-07-SKELETRAIN-OT_CORE_.md", "LEGIO-08-PROMPT-BOMBS_KIT_.md"]
built_for: "Claude Code → S2A → MCP implementation"
---

# LEGIO FORGE — AGENTS.md SCHEMA & INTERACTIVE PROTOCOL
**The Forge That Shapes Legions**

---

## ARCHITECTURAL PIVOT

The original design: 18 MCP tools running a linear pipeline.
The evolved design: **1 interactive forge** that produces reusable formation templates.

```
OLD MODEL:
  User query → 18-step MCP pipeline → Output
  (every query runs the full cascade)

NEW MODEL:
  Phase 1 — THE FORGE (offline, interactive, once per use case)
    User + Forge ←→ back and forth
    → produces AGENTS.md formation template
    → saved to template library

  Phase 2 — THE LEGION (runtime, per task)
    Claude Code reads AGENTS.md natively
    → executes with full formation loaded
    → no custom execution infrastructure
```

### Why This Works

1. **Claude Code already reads AGENTS.md** — it's a native convention for agent configuration
2. **Pre-flight is planning, not execution** — it makes decisions that don't change per task within a use case
3. **Templates are reusable** — once you forge "nextjs-website," every Next.js task uses that formation
4. **Interactive is better** — back-and-forth catches gaps that one-shot scoring misses
5. **1 MCP server not 18** — the forge IS the product; execution is Claude Code doing what it already does

---

## TWO SYSTEMS

### THE FORGE (`legio-forge` MCP Server)

**What it is:** An interactive planning MCP server that runs Imperatus + SkeletrainOT as a conversational session with the user.

**What it produces:** A sealed `AGENTS.md` file — the complete formation template.

**When it runs:** Once per use case type. Not per task. Not per session. Once.

**MCP surface:** Single tool (`forge`) with tag-driven flow, mirroring Lotus pattern.

### THE LEGION (Claude Code Native)

**What it is:** Claude Code reading the forged AGENTS.md and executing.

**What it produces:** Whatever the user asked for — code, content, analysis.

**When it runs:** Every task. Reads AGENTS.md from project root or template library.

**MCP surface:** None needed. Claude Code's existing agent infrastructure.

---

## AGENTS.MD OUTPUT SCHEMA

The forge produces a markdown file with YAML frontmatter + structured sections. Every section maps to a pre-flight module or planning decision from the LEGIO cascade.

### Full Template Structure

```markdown
---
# FORMATION METADATA
formation: "triplex-acies"
tier: "Principes"
use_case: "nextjs-website"
forged: "2026-02-16T14:30:00+08:00"
forged_by: "legio-forge v1.0"
imperatus_version: "v30.1"
rkqde:
  reasoning: 7
  knowledge_risk: 5
  quality_bar: 8
  domain_interdependency: 6
  expert_perspectives: 5
mode: "DELIBERATE"
iterations: 3
---

# AGENTS.md — [USE CASE NAME]
## Formation: [ROMAN NAME] | Tier: [TIER] | Mode: [MODE]

---

## SUCCESS CRITERIA

[Binary checkboxes. The forge extracted these interactively.]

- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] [Criterion 3]
- [ ] [Criterion N]

---

## CONSTRAINTS

### Buffer Valet
mode: [read_only | read_save | full]
context_budget: [token estimate]
save_triggers: [list of conditions]

### ARQ Gates
depth: [pre | pre_post | full]
strictness: [advisory | standard | hard | halt]
positions:
  - gate_1: "During expert summoning — does this expert belong?"
  - gate_2: "After planning — plan validates against success criteria"
  - gate_3: "Before execution finishes — content matches plan"
  - gate_4: "Before output — final success criteria verification"

### Anti-Lazy Protocol
mode: [optional | required | enforced]
enforcement: "[specific instruction for this use case]"

### USC (Universal Self-Consistency)
candidates: [1 | 2 | 3 | 5]
selection: [best_of | consensus | meta_analysis]

### Confidence Gate
threshold: [7 | 8 | 9 | 10] out of 10
halt_on_fail: [true | false]
applies_at: [list of phase boundaries]

---

## EXPERT CONSTELLATION

[MR.RUG-sourced specialists. Each expert owns specific domains.]

### Expert 1: [Role Name]
- **domain:** [what they own]
- **reasoning:** [FCoT | CoC | HYBRID]
- **tools:** [context7, filesystem, web, etc.]
- **owns_nodes:** [list of railroad node IDs]

### Expert 2: [Role Name]
- **domain:** [what they own]
- **reasoning:** [FCoT | CoC | HYBRID]
- **tools:** [list]
- **owns_nodes:** [list]

[... up to N experts based on tier]

---

## PROMPT BOMBS

[Pre-planned context injections. Coordinates from SkeletrainOT.]

### B-001 [TYPE]
- **from:** [source expert/node]
- **target:** [destination expert/node]
- **trigger:** [coordinate | content | context | token | dependency]
- **payload:** "[compressed context — 1-3 sentences]"
- **why:** "[one line — why receiver needs this]"

### B-002 [TYPE]
[...]

---

## RAILROAD

[The complete execution plan from SkeletrainOT. Every decision pre-made.]

### Execution Pattern
pattern: [baton | swarm | hybrid]
segments:
  - nodes: [1-3]
    pattern: baton
    reason: "[why sequential]"
  - nodes: [4-5]
    pattern: swarm
    reason: "[why parallel]"

### Node Map

#### Node 1: [Name]
- **expert:** [Expert N]
- **reasoning:** [FCoT | CoC]
- **input:** [what it receives]
- **output:** [what it produces]
- **bombs_plant:** [list of bomb IDs to plant here]
- **bombs_receive:** [list of bomb IDs that detonate here]
- **cove:** [skip | top-1 | top-2 | full]
- **arq_gate:** [none | pre | post | both]
- **handoff_to:** [next node(s)]

#### Node 2: [Name]
[...]

### Quality Stations
- **CoVE checkpoints:** [after which nodes]
- **PGScan:** [skip | light | 3-branch | deep]
- **Curation mode:** [lean | normal | nuance | all-out]

---

## OUTPUT FORMAT

format: [narrative | mldoe | cep | structured]
density: [standard | compressed | maximum]
epistemic: true
reflection: true

---

## FORGE SESSION LOG

[The interactive decisions that shaped this formation.
NOT the execution history. The PLANNING history.]

### Intent
"[Original user description of what they want to build]"

### Clarifications
1. Q: "[Forge asked]" → A: "[User answered]"
2. Q: "[Forge asked]" → A: "[User answered]"
[...]

### Scoring Rationale
"[Why RKQDE scores landed where they did, informed by Q&A]"

### Formation Choice
"[Why this formation, not another]"

### User Overrides
[Any places where user disagreed with forge recommendation]
- "[Override 1]"
- "[Override 2]"
```

---

## SECTION-TO-MODULE MAPPING

Every AGENTS.md section traces back to a LEGIO pipeline module:

| AGENTS.md Section | Pipeline Module | Step | Phase |
|-------------------|----------------|------|-------|
| Frontmatter (RKQDE, mode, tier) | Imperatus scoring | 0 | Pre-flight |
| Success Criteria | Success Criteria Lock | 1 | Pre-flight |
| Constraints → Buffer | Buffer Valet | 2 | Pre-flight |
| Constraints → ARQ | ARQ Gates | 3 | Pre-flight |
| Constraints → Anti-Lazy | Anti-Lazy Protocol | 4 | Pre-flight |
| Constraints → USC | USC | 5 | Pre-flight |
| Constraints → Confidence | Confidence Gate | 0 (Imperatus) | Pre-flight |
| Expert Constellation | MR.RUG | 6 | Pipeline |
| Railroad | SkeletrainOT | 7 | Pipeline |
| Prompt Bombs | Prompt Bombs Kit | 8 | Pipeline |
| Output Format | Output Selection | 16 | Output |
| Forge Session Log | (new — interactive audit trail) | — | Meta |

Steps 9-15 (Execute + Refine) are NOT in AGENTS.md — they happen at runtime via Claude Code following the railroad.

---

## INTERACTIVE FORGE FLOW

The forge is conversational. Not one-shot. Back and forth.

### Session Architecture

```
USER                          FORGE
  |                              |
  |-- "I want to build X" ----→ |
  |                              |-- [begin] load framework
  |                              |-- [decompose] break apart intent
  |                              |
  | ←-- clarifying question 1 --|
  |-- answer 1 ---------------→ |
  |                              |
  | ←-- clarifying question 2 --|
  |-- answer 2 ---------------→ |
  |                              |
  |                              |-- [score] RKQDE with full context
  |                              |-- [propose] formation + tier
  |                              |
  | ←-- "Here's what I'd forge" |
  | ←-- formation preview ------ |
  |                              |
  |-- "looks good" or "change X" |
  |                              |
  |                              |-- [track] lay railroad
  |                              |-- [arm] place bombs
  |                              |
  | ←-- "Railroad preview" ----- |
  |                              |
  |-- "approved" or "adjust" --- |
  |                              |
  |                              |-- [seal] write AGENTS.md
  |                              |
  | ←-- "Formation sealed." ---- |
  | ←-- AGENTS.md path --------- |
```

### Clarification Categories

The forge asks about things it CANNOT infer from the intent alone:

| Category | Example Questions |
|----------|-------------------|
| **Scope** | "Does this include auth? Payments? Admin panel?" |
| **Quality** | "Is this a prototype or production? What's the audience?" |
| **Constraints** | "Any existing codebase? Framework preferences? Time pressure?" |
| **Risk** | "What breaks if this is wrong? Compliance requirements?" |
| **Domain** | "Which APIs/services does this integrate with?" |
| **Output** | "Documentation level? Test coverage expectations?" |

The forge does NOT ask about:
- Things it can score from the intent (RKQDE dimensions)
- Things that are always the same (ARQ gate count = 4)
- Things that have safe defaults (Anti-Lazy = required)

### Minimum Viable Forge Session

Even the shortest session has structure:

```
1. User states intent
2. Forge asks 1-3 clarifying questions
3. User answers
4. Forge proposes formation (preview)
5. User approves
6. Forge seals AGENTS.md
```

Velites = ~2 minutes. Triarii = could be a 15-minute conversation.

---

## FORGE MCP TOOL

Single tool. Tag-driven. Lotus pattern.

### Tool: `forge`

```json
{
  "name": "forge",
  "description": "LEGIO formation forge — interactive planning engine that produces AGENTS.md templates. Start with tag='begin'.",
  "inputSchema": {
    "type": "object",
    "properties": {
      "tag": {
        "type": "string",
        "enum": ["begin", "clarify", "score", "propose", "track", "arm", "seal", "load", "list"],
        "description": "Current forge phase"
      },
      "content": {
        "type": "string",
        "description": "Phase content — intent, answer, rationale, or adjustment"
      },
      "stepNumber": {
        "type": "integer",
        "description": "Current step in forge session"
      },
      "totalSteps": {
        "type": "integer",
        "description": "Estimated total steps"
      },
      "nextStepNeeded": {
        "type": "boolean",
        "description": "Whether another step is needed"
      },
      "clarification": {
        "type": "object",
        "properties": {
          "question": { "type": "string" },
          "answer": { "type": "string" },
          "category": {
            "type": "string",
            "enum": ["scope", "quality", "constraints", "risk", "domain", "output"]
          }
        },
        "description": "For [clarify] tag — the Q&A pair"
      },
      "override": {
        "type": "object",
        "properties": {
          "section": { "type": "string" },
          "from": { "type": "string" },
          "to": { "type": "string" },
          "reason": { "type": "string" }
        },
        "description": "User override of forge recommendation"
      },
      "template_name": {
        "type": "string",
        "description": "For [load] and [seal] — template identifier"
      }
    },
    "required": ["tag", "content", "stepNumber", "totalSteps", "nextStepNeeded"]
  }
}
```

### Tag Specifications

| Tag | Domain | Function | Returns |
|-----|--------|----------|---------|
| `[begin]` | entry | Load forge framework. Receive user intent. | Framework + decomposition prompts |
| `[clarify]` | reconnaissance | Ask or answer a clarifying question | Question or acknowledgment |
| `[score]` | strategy | RKQDE scoring with full clarified context | Scores + tier + mode |
| `[propose]` | strategy | Propose formation — experts, constraints, structure | Formation preview (not yet sealed) |
| `[track]` | planning | Lay railroad — nodes, routes, handoffs | Railroad preview |
| `[arm]` | planning | Place prompt bombs at coordinates | Bomb registry preview |
| `[seal]` | authority | Write AGENTS.md to filesystem | File path + confirmation |
| `[load]` | library | Load existing template for reuse or modification | Template contents |
| `[list]` | library | List available templates | Template index |

### Response Statuses

| Status | Meaning |
|--------|---------|
| `FRAMEWORK_RECEIVED` | Forge loaded, ready for intent |
| `CLARIFICATION_NEEDED` | Forge asks user a question |
| `CLARIFICATION_RECEIVED` | User's answer processed |
| `SCORED` | RKQDE complete, tier selected |
| `PROPOSED` | Formation preview ready for review |
| `TRACKED` | Railroad laid, ready for review |
| `ARMED` | Bombs placed, ready for review |
| `FORMATION_SEALED` | AGENTS.md written. Done. |
| `TEMPLATE_LOADED` | Existing template loaded for modification |
| `TEMPLATE_LIST` | Available templates returned |

---

## TEMPLATE LIBRARY

### Storage Structure

```
project_root/
├── AGENTS.md                     ← active formation (Claude Code reads this)
└── .legio/
    └── formations/
        ├── nextjs-website.agents.md
        ├── api-backend.agents.md
        ├── research-paper.agents.md
        ├── data-pipeline.agents.md
        ├── mobile-app.agents.md
        └── custom-[name].agents.md
```

### Template Lifecycle

```
1. FORGE — Create new template
   forge[seal] → .legio/formations/nextjs-website.agents.md

2. ACTIVATE — Copy to project root
   forge[load] → cp .legio/formations/X.agents.md → ./AGENTS.md

3. EXECUTE — Claude Code reads AGENTS.md
   Claude Code → reads ./AGENTS.md → executes with formation

4. EVOLVE — Modify existing template
   forge[load] → modify → forge[seal] → updated template

5. SHARE — Templates are portable
   Copy .legio/formations/ between projects
   Publish formations as community resources
```

### Template Naming Convention

```
[use-case]-[variant].agents.md

Examples:
  nextjs-website.agents.md          — standard Next.js site
  nextjs-website-ecommerce.agents.md — with payment integration
  api-backend-rest.agents.md         — REST API
  api-backend-graphql.agents.md      — GraphQL API
  research-paper-arxiv.agents.md     — academic paper
  voice-agent-twilio.agents.md       — voice agent
```

### Built-in Formation Templates

Six standard formations from the architecture doc, pre-forged:

| Formation | Roman | Use Case | Default Tier |
|-----------|-------|----------|-------------|
| `standard-analytical` | Triplex Acies | General analytical work | Hastati |
| `high-stakes-research` | Testudo | Research requiring maximum protection | Principes |
| `quick-task` | Cuneus | Fast, focused tasks | Velites |
| `multi-domain` | Orbis | Complex cross-domain work | Principes |
| `coding-project` | Manipulus | Software development | Hastati-Principes |
| `creative-content` | Turma | Creative writing, content creation | Hastati |

These are starting points. The forge customizes them interactively.

---

## CLAUDE CODE INTEGRATION

### How Claude Code Consumes AGENTS.md

Claude Code reads `AGENTS.md` from the project root at session start. The file acts as persistent agent configuration — it doesn't need to be re-read per message.

The formation template provides Claude Code with:

1. **WHO** — Expert constellation defines which perspectives to adopt
2. **HOW** — Railroad defines execution order, reasoning modes, handoff patterns
3. **WHAT** — Success criteria define "done"
4. **GUARDRAILS** — Constraints define quality gates, confidence thresholds, enforcement modes
5. **CONTEXT** — Prompt bombs provide pre-positioned strategic context

### Runtime Behaviour

Claude Code follows the railroad:

```
1. Read AGENTS.md → load formation
2. Adopt expert perspective for current node
3. Check: any bombs detonating at this node? → incorporate
4. Execute node work using specified reasoning mode
5. Check: ARQ gate at this node? → evaluate
6. Check: confidence gate at phase boundary? → evaluate
7. Handoff to next node per railroad
8. At completion: verify success criteria checkboxes
9. Apply output format + epistemic compliance
```

No custom MCP execution infrastructure needed. Claude Code already does multi-step reasoning, tool use, and self-verification. AGENTS.md just gives it a military-grade battle plan to follow.

### What AGENTS.md Does NOT Control

- Token-level generation (that's the model)
- Tool selection during execution (that's Claude Code's native capability)
- Error recovery (Claude Code handles this)
- User communication (Claude Code handles this)

AGENTS.md is strategy and structure. Execution is Claude Code being Claude Code, but with a formation loaded.

---

## FORGE SESSION EXAMPLE

### Minimal Session (Velites)

```
USER: "Help me write a REST API in Express.js for a todo app"

FORGE [begin]:
  Intent decomposed. Straightforward CRUD API.
  Score: R=3 K=2 Q=5 D=2 E=2 → Velites (Cuneus)

FORGE [clarify]:
  Q: "Auth required, or public API?"
  USER: "Public for now, add auth later"

FORGE [propose]:
  Formation: Cuneus (quick strike)
  Tier: Velites
  Experts: 1 (API specialist)
  Constraints: ARQ=advisory, Anti-Lazy=optional, USC=1-path
  Railroad: 3 nodes (setup → routes → tests)

USER: "Go"

FORGE [seal]: → ./AGENTS.md written
```

### Full Session (Principes)

```
USER: "Build a SaaS dashboard with Next.js, auth, Stripe payments,
       and real-time analytics"

FORGE [begin]:
  Intent decomposed. Multi-domain, 4+ integration points.
  Initial estimate: Principes territory.

FORGE [clarify] ×4:
  Q1: "Multi-tenant or single-tenant?" → A: "Multi-tenant"
  Q2: "Auth provider preference?" → A: "Clerk"
  Q3: "Analytics — custom or third-party?" → A: "Custom with Recharts"
  Q4: "Database?" → A: "PostgreSQL via Prisma"

FORGE [score]:
  R=7 K=6 Q=8 D=7 E=5 → Principes (Triplex Acies)

FORGE [propose]:
  Formation: Triplex Acies
  Tier: Principes
  Experts: 5 (Frontend, Backend, Auth, Payments, Data)
  Constraints: ARQ=hard, Anti-Lazy=enforced, USC=3-candidates
  15 railroad nodes across 4 execution segments

USER: "Add a 6th expert for DevOps/deployment"

FORGE [propose] (revised):
  Expert 6: DevOps added. Railroad adjusted.

USER: "Approved"

FORGE [track]:
  Full railroad laid. 15 nodes. Baton for auth→payments.
  Swarm for frontend components. CoVE top-2 after integration.

FORGE [arm]:
  B-001 ANCHOR: "Multi-tenant isolation" → all data layer nodes
  B-002 CONTINUITY: "Clerk session tokens" → frontend ↔ backend handoff
  B-003 BRIDGE: "Stripe webhook idempotency" → payments → error handling

USER: "Seal it"

FORGE [seal]: → .legio/formations/saas-dashboard-nextjs.agents.md
              → ./AGENTS.md (activated)
```

---

## IMPLEMENTATION NOTES

### MCP Server Architecture

```
legio-forge/
├── src/
│   ├── index.ts              ← MCP server entry (Hono + StreamableHTTP)
│   ├── forge.ts              ← forge tool handler (tag router)
│   ├── imperatus.ts          ← scoring + formation selection logic
│   ├── skeletrain.ts         ← railroad planning logic
│   ├── bombs.ts              ← bomb placement logic
│   ├── templates/
│   │   ├── formations.ts     ← built-in formation templates
│   │   └── agents-md.ts      ← AGENTS.md generator (template → markdown)
│   └── types.ts              ← shared types (Formation, Railroad, Bomb, etc.)
├── formations/               ← built-in formation library
│   ├── triplex-acies.json
│   ├── testudo.json
│   ├── cuneus.json
│   ├── orbis.json
│   ├── manipulus.json
│   └── turma.json
├── package.json
├── tsconfig.json
└── wrangler.jsonc            ← if deploying to Cloudflare
```

### Technology Stack

- **Runtime:** Node.js (stdio for local) or Cloudflare Workers (HTTP for remote)
- **MCP SDK:** @modelcontextprotocol/sdk@1.25.1
- **Schema:** Zod for tool input validation
- **Transport:** StdioServerTransport (local) + StreamableHTTPServerTransport (remote)
- **State:** In-memory session state for forge conversations
- **Output:** Markdown generation for AGENTS.md files
- **Storage:** Filesystem for local, KV/R2 for cloud template library

### State Management

Each forge session maintains:

```typescript
interface ForgeSession {
  id: string;
  intent: string;
  clarifications: Array<{ question: string; answer: string; category: string }>;
  scores: { R: number; K: number; Q: number; D: number; E: number };
  tier: 'Velites' | 'Hastati' | 'Principes' | 'Triarii';
  mode: 'QUICK' | 'ANALYTICAL' | 'DELIBERATE' | 'MAXIMUM';
  formation: Formation;
  railroad: Railroad;
  bombs: Bomb[];
  overrides: Override[];
  tagJourney: string[];
  domainJourney: string[];
  stepNumber: number;
  sealed: boolean;
}
```

Session persists across tool calls within a conversation. Destroyed on seal or timeout.

---

## DESIGN PRINCIPLES

1. **Forge once, execute many** — templates are investments, not overhead
2. **Interactive beats one-shot** — the user knows things the model can't infer
3. **AGENTS.md is the contract** — everything downstream reads this single artifact
4. **Claude Code is the executor** — don't rebuild what already works
5. **Templates are portable** — share formations across projects, teams, community
6. **Sections trace to modules** — every AGENTS.md section has a LEGIO pipeline ancestor
7. **Overrides are first-class** — user can always disagree with the forge
8. **Audit trail preserved** — forge session log shows WHY decisions were made

---

## RELATIONSHIP TO EXISTING SPECS

This spec SUPERSEDES the "18 MCP tools" concept from LEGIO-ARCHITECTURE-v1.md Section 8.

It does NOT supersede the individual module specs (Imperatus, SkeletrainOT, Prompt Bombs). Those specs define the LOGIC that the forge implements. This spec defines HOW that logic is packaged and delivered.

```
LEGIO-00-IMPERATUS        → scoring + formation logic inside forge
LEGIO-07-SKELETRAIN-OT    → railroad planning logic inside forge
LEGIO-08-PROMPT-BOMBS     → bomb placement logic inside forge
LEGIO-FORGE-SCHEMA        → how forge exposes these as interactive MCP + AGENTS.md output
```

The module specs are the engines. This spec is the chassis.

---

*LEGIO v1.0 | Forge Schema Spec | 2026-02-16 | ktg.one*
*Architectural pivot: from runtime pipeline to interactive forge + native execution*
*"Shape the legion before the battle. Execute without hesitation."*
