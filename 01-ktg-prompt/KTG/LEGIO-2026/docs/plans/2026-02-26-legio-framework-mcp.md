# LEGIO Framework MCP Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build the LEGIO agentic framework as 7 MCP servers (4 TypeScript + 3 Python) plus a Forge MCP that produces reusable AGENTS.md formation templates.

**Architecture:** The Forge MCP runs interactive sessions to produce AGENTS.md templates (offline, once per use case). At runtime, Claude Code reads AGENTS.md and executes with formation loaded. TS servers handle orchestration/state/gates. Python servers handle semantic verification, synthesis, and compression. 5 permanent expert agents replace dynamic MR.RUG assembly. Embeddings + skeleton imprinting replace prompt bombs.

**Tech Stack:** TypeScript (MCP SDK ^1.23, ESM, Node >=18), Python (mcp[cli], FastMCP), esbuild bundling, no test framework (verify via `npm run build` + manual MCP smoke tests)

**Reference Specs:**
- `LEGIO-FORGE-SCHEMA_SPEC_.md` — Forge architecture, AGENTS.md output schema, interactive flow
- `LEGIO-DUPLEX-IMBUED-MODULE-MAP.md` — Imperatus full protocol (10 tags, RKQDE, activation matrix)
- `LEGIO-OVERVIEW.md` — 17-module pipeline, command chain, mode tiers
- `lotus-wisdom-mcp-main/index.ts` — Existing ImperatusServer (reuse scoring/routing logic)

**Module → Runtime Map:**

| # | Module | Runtime | Server |
|---|--------|---------|--------|
| 00 | Imperatus | AGENTS.md | legio-forge |
| 01 | Armatura | AGENTS.md | legio-forge |
| 02 | The Seal | TS MCP | legio-seal |
| 03 | USC | TS MCP | legio-dispatch |
| 04 | Consilium | AGENTS.md | legio-forge (permanent agents) |
| 05 | Legatus | AGENTS.md | legio-forge (railroad) |
| 06 | Bombs | **Eliminated** | Embeddings + skeleton imprint |
| 07 | FCoT/CoC | AGENTS.md | Per-node instruction |
| 08 | Baton/Swarm | TS MCP | legio-dispatch |
| 09 | CoVE | Python MCP | legio-verify |
| 10 | PGScan+ARQ | TS MCP | legio-gates |
| 11 | Censor | Python MCP | legio-censor |
| 12 | Self-Reflect | TS MCP | legio-gates |
| 13 | Output Format | AGENTS.md | legio-forge |
| 14 | Final Reflect | TS MCP | legio-seal |
| 15 | QMDR | Python MCP | legio-censor |
| 16 | CEP | Python MCP | legio-cep |

**Server Summary:**

| Server | Modules | Lang | Function |
|--------|---------|------|----------|
| legio-forge | 00,01,04,05,07,13 | TS | Interactive forge → AGENTS.md |
| legio-seal | 02, 14 | TS | Contract enforcement + final reflection |
| legio-dispatch | 03, 08 | TS | USC candidate dispatch + Baton/Swarm orchestration |
| legio-gates | 10, 12 | TS | ARQ/PGScan enforcement + Self-Reflect audit |
| legio-verify | 09 | Python | CoVE variants + 10Rs + negentropy |
| legio-censor | 11, 15 | Python | Censor synthesis/curation + QMDR enrichment |
| legio-cep | 16 | Python | CEP packet generation + PDL + NCL |

---

## Phase 1: Forge MCP (Tasks 1-8)

The forge is the entry point. Everything downstream depends on AGENTS.md templates it produces. Reuses `ImperatusServer` scoring/routing logic from existing `imperatus-mcp`.

### Task 1: Scaffold legio-forge project

**Files:**
- Create: `LEGIO-2026/legio-forge/package.json`
- Create: `LEGIO-2026/legio-forge/tsconfig.json`
- Create: `LEGIO-2026/legio-forge/src/types.ts`

**Step 1: Create package.json**

```json
{
  "name": "legio-forge",
  "version": "0.1.0",
  "description": "LEGIO formation forge — interactive planning engine that produces AGENTS.md templates",
  "main": "dist/bundle.js",
  "type": "module",
  "bin": { "legio-forge": "cli.js" },
  "scripts": {
    "build": "tsc && npx esbuild src/index.ts --bundle --platform=node --format=esm --outfile=dist/bundle.js",
    "start": "node dist/bundle.js",
    "dev": "tsc && node dist/index.js"
  },
  "dependencies": {
    "@modelcontextprotocol/sdk": "^1.23.0"
  },
  "devDependencies": {
    "@types/node": "^20.11.5",
    "typescript": "^5.9.0"
  },
  "engines": { "node": ">=18.0.0" }
}
```

**Step 2: Create tsconfig.json**

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "outDir": "dist",
    "rootDir": "src",
    "strict": true,
    "esModuleInterop": true,
    "declaration": true,
    "sourceMap": true
  },
  "include": ["src/**/*"]
}
```

**Step 3: Create core types**

File: `LEGIO-2026/legio-forge/src/types.ts`

```typescript
// ═══════════════════════════════════════════════════════
// LEGIO FORGE — Core Types
// ═══════════════════════════════════════════════════════

export type CombatMode = 'Velites' | 'Hastati' | 'Principes' | 'Triarii';
export type Formation = 'Testudo' | 'Triplex' | 'Cuneus' | 'Orbis' | 'Manipulus' | 'Turma';
export type ForgeTag = 'begin' | 'clarify' | 'score' | 'propose' | 'track' | 'seal' | 'load' | 'list';
export type ClarifyCategory = 'scope' | 'quality' | 'constraints' | 'risk' | 'domain' | 'output';
export type ReasoningStyle = 'FCoT' | 'CoC' | 'HYBRID';
export type ExecutionPattern = 'baton' | 'swarm' | 'hybrid';

export interface RKQDE {
  R: number; K: number; Q: number; D: number; E: number;
  sigma: number;
  danger: number;
}

export interface Clarification {
  question: string;
  answer: string;
  category: ClarifyCategory;
}

export interface ExpertDefinition {
  role: string;
  domain: string;
  reasoning: ReasoningStyle;
  tools: string[];
  owns_nodes: string[];
}

export interface RailroadNode {
  id: string;
  name: string;
  expert: string;
  reasoning: ReasoningStyle;
  input: string;
  output: string;
  cove: 'skip' | 'top-1' | 'top-2' | 'full';
  arq_gate: 'none' | 'pre' | 'post' | 'both';
  handoff_to: string[];
}

export interface RailroadSegment {
  nodes: string[];
  pattern: ExecutionPattern;
  reason: string;
}

export interface Constraints {
  buffer_valet: { mode: string; context_budget?: number };
  arq_gates: { depth: string; strictness: string };
  anti_lazy: { mode: string; enforcement?: string };
  usc: { candidates: number; selection: string };
  confidence_gate: { threshold: number; halt_on_fail: boolean };
  cove_depth: string;
  gap_scan_depth: string;
  curation_density: string;
  self_reflect_depth: string;
}

export interface Railroad {
  segments: RailroadSegment[];
  nodes: RailroadNode[];
  quality_stations: {
    cove_checkpoints: string[];
    pgscan: string;
    curation_mode: string;
  };
}

export interface AgentsMdTemplate {
  // Frontmatter
  formation: Formation;
  tier: CombatMode;
  use_case: string;
  forged: string;
  rkqde: RKQDE;
  mode: string;
  iterations: number;

  // Body sections
  success_criteria: string[];
  constraints: Constraints;
  experts: ExpertDefinition[];
  railroad: Railroad;
  output_format: { format: string; density: string; epistemic: boolean; reflection: boolean };

  // Session log
  session_log: {
    intent: string;
    clarifications: Clarification[];
    scoring_rationale: string;
    formation_choice: string;
    overrides: string[];
  };
}

export interface ForgeSession {
  id: string;
  intent: string;
  clarifications: Clarification[];
  scores: RKQDE | null;
  tier: CombatMode | null;
  formation: Formation | null;
  experts: ExpertDefinition[];
  railroad: Railroad | null;
  overrides: string[];
  tagJourney: ForgeTag[];
  stepNumber: number;
  sealed: boolean;
}

export interface ForgeStepInput {
  tag: ForgeTag;
  content: string;
  stepNumber: number;
  totalSteps: number;
  nextStepNeeded: boolean;
  clarification?: { question: string; answer: string; category: ClarifyCategory };
  override?: { section: string; from: string; to: string; reason: string };
  template_name?: string;
}
```

**Step 4: Install dependencies and build**

```bash
cd LEGIO-2026/legio-forge
npm install
npm run build
```

Expected: TypeScript compiles, esbuild produces `dist/bundle.js`. May warn about missing `src/index.ts` — that's Task 2.

**Step 5: Commit**

```bash
git add LEGIO-2026/legio-forge/package.json LEGIO-2026/legio-forge/tsconfig.json LEGIO-2026/legio-forge/src/types.ts
git commit -m "feat(forge): scaffold legio-forge MCP project with core types"
```

---

### Task 2: Port RKQDE scoring from imperatus-mcp

**Files:**
- Create: `LEGIO-2026/legio-forge/src/scoring.ts`
- Read: `LEGIO-2026/lotus-wisdom-mcp-main/index.ts:63-67,396-415,467-546` (existing RKQDE + routing logic)

**Context:** The existing `ImperatusServer` has RKQDE parsing (regex), mode selection (Σ + Danger thresholds), and formation auto-selection. Extract and refine these into standalone functions.

**Step 1: Create scoring module**

```typescript
import type { RKQDE, CombatMode, Formation } from './types.js';

// ── RKQDE Parsing (from LLM content) ──
export function parseRKQDE(content: string): RKQDE | null {
  const patterns: Record<string, RegExp> = {
    R: /R\s*[=:]\s*(\d+)/i,
    K: /K\s*[=:]\s*(\d+)/i,
    Q: /Q\s*[=:]\s*(\d+)/i,
    D: /D\s*[=:]\s*(\d+)/i,
    E: /E\s*[=:]\s*(\d+)/i,
  };
  const scores: Partial<Record<string, number>> = {};
  for (const [key, pattern] of Object.entries(patterns)) {
    const match = content.match(pattern);
    if (match) scores[key] = Math.min(10, Math.max(1, parseInt(match[1])));
  }
  if (scores.R && scores.K && scores.Q && scores.D && scores.E) {
    const sigma = scores.R + scores.K + scores.Q + scores.D + scores.E;
    const danger = Math.max(scores.R, scores.K, scores.Q);
    return { R: scores.R, K: scores.K, Q: scores.Q, D: scores.D, E: scores.E, sigma, danger };
  }
  return null;
}

// ── Mode Selection (RLoT-adaptive) ──
export function selectMode(rkqde: RKQDE, override?: CombatMode): CombatMode {
  if (override) return override;
  const { sigma, danger } = rkqde;
  if (sigma <= 12 && danger <= 5) return 'Velites';
  if (sigma <= 25 || danger <= 7) return 'Hastati';
  if (sigma <= 38 || danger <= 8) return 'Principes';
  return 'Triarii';
}

// ── Formation Selection ──
export function selectFormation(rkqde: RKQDE): Formation {
  if (rkqde.D >= 7) return 'Orbis';
  if (rkqde.K >= 8) return 'Testudo';
  if (rkqde.R <= 3 && rkqde.Q <= 5) return 'Cuneus';
  return 'Triplex';
}

// ── Expert Count by Mode ──
export function expertCount(mode: CombatMode): number {
  switch (mode) {
    case 'Velites': return 1;
    case 'Hastati': return 3;
    case 'Principes': return 5;
    case 'Triarii': return 5;
  }
}

// ── Iteration Count by Mode ──
export function iterationCount(mode: CombatMode): number {
  switch (mode) {
    case 'Velites': return 1;
    case 'Hastati': return 1;
    case 'Principes': return 3;
    case 'Triarii': return 3;
  }
}

// ── Constraints Defaults by Mode ──
export function defaultConstraints(mode: CombatMode) {
  const defaults: Record<CombatMode, Record<string, string>> = {
    Velites: {
      buffer_valet: 'read_only', arq_depth: 'pre', arq_strictness: 'advisory',
      anti_lazy: 'optional', usc_candidates: '1', usc_selection: 'best_of',
      confidence_threshold: '7', cove: 'skip', gap_scan: 'skip',
      curation: 'lean', self_reflect: 'skip',
    },
    Hastati: {
      buffer_valet: 'read_only', arq_depth: 'pre', arq_strictness: 'standard',
      anti_lazy: 'required', usc_candidates: '2', usc_selection: 'best_of',
      confidence_threshold: '8', cove: 'top-1', gap_scan: 'light',
      curation: 'normal', self_reflect: 'optional',
    },
    Principes: {
      buffer_valet: 'read_save', arq_depth: 'pre_post', arq_strictness: 'hard',
      anti_lazy: 'enforced', usc_candidates: '3', usc_selection: 'consensus',
      confidence_threshold: '9', cove: 'top-2', gap_scan: '3-branch',
      curation: 'normal_nuance', self_reflect: 'required',
    },
    Triarii: {
      buffer_valet: 'full', arq_depth: 'full', arq_strictness: 'halt',
      anti_lazy: 'enforced', usc_candidates: '5', usc_selection: 'meta_analysis',
      confidence_threshold: '9', cove: 'full', gap_scan: 'deep',
      curation: 'all_out', self_reflect: 'full_bot',
    },
  };
  return defaults[mode];
}
```

**Step 2: Build to verify types**

```bash
cd LEGIO-2026/legio-forge && npm run build
```

Expected: Compiles clean.

**Step 3: Commit**

```bash
git add LEGIO-2026/legio-forge/src/scoring.ts
git commit -m "feat(forge): port RKQDE scoring + mode/formation selection from imperatus"
```

---

### Task 3: AGENTS.md template generator

**Files:**
- Create: `LEGIO-2026/legio-forge/src/generator.ts`

**Context:** Takes a completed `AgentsMdTemplate` and renders it as the AGENTS.md markdown file per the schema in `LEGIO-FORGE-SCHEMA_SPEC_.md`. This is the output artifact.

**Step 1: Create generator**

```typescript
import type { AgentsMdTemplate, ExpertDefinition, RailroadNode, RailroadSegment } from './types.js';

export function generateAgentsMd(template: AgentsMdTemplate): string {
  const lines: string[] = [];

  // ── YAML Frontmatter ──
  lines.push('---');
  lines.push(`formation: "${template.formation.toLowerCase()}"`);
  lines.push(`tier: "${template.tier}"`);
  lines.push(`use_case: "${template.use_case}"`);
  lines.push(`forged: "${template.forged}"`);
  lines.push(`forged_by: "legio-forge v0.1.0"`);
  lines.push(`imperatus_version: "v30.2"`);
  lines.push('rkqde:');
  lines.push(`  reasoning: ${template.rkqde.R}`);
  lines.push(`  knowledge_risk: ${template.rkqde.K}`);
  lines.push(`  quality_bar: ${template.rkqde.Q}`);
  lines.push(`  domain_interdependency: ${template.rkqde.D}`);
  lines.push(`  expert_perspectives: ${template.rkqde.E}`);
  lines.push(`mode: "${template.mode}"`);
  lines.push(`iterations: ${template.iterations}`);
  lines.push('---');
  lines.push('');

  // ── Title ──
  lines.push(`# AGENTS.md — ${template.use_case}`);
  lines.push(`## Formation: ${template.formation} | Tier: ${template.tier} | Mode: ${template.mode}`);
  lines.push('');
  lines.push('---');
  lines.push('');

  // ── Success Criteria ──
  lines.push('## SUCCESS CRITERIA');
  lines.push('');
  for (const criterion of template.success_criteria) {
    lines.push(`- [ ] ${criterion}`);
  }
  lines.push('');
  lines.push('---');
  lines.push('');

  // ── Constraints ──
  lines.push('## CONSTRAINTS');
  lines.push('');
  const c = template.constraints;
  lines.push('### Buffer Valet');
  lines.push(`mode: ${c.buffer_valet.mode}`);
  if (c.buffer_valet.context_budget) lines.push(`context_budget: ${c.buffer_valet.context_budget}`);
  lines.push('');
  lines.push('### ARQ Gates');
  lines.push(`depth: ${c.arq_gates.depth}`);
  lines.push(`strictness: ${c.arq_gates.strictness}`);
  lines.push('positions:');
  lines.push('  - gate_1: "During expert summoning — does this expert belong?"');
  lines.push('  - gate_2: "After planning — plan validates against success criteria"');
  lines.push('  - gate_3: "Before execution finishes — content matches plan"');
  lines.push('  - gate_4: "Before output — final success criteria verification"');
  lines.push('');
  lines.push('### Anti-Lazy Protocol');
  lines.push(`mode: ${c.anti_lazy.mode}`);
  if (c.anti_lazy.enforcement) lines.push(`enforcement: "${c.anti_lazy.enforcement}"`);
  lines.push('');
  lines.push('### USC (Universal Self-Consistency)');
  lines.push(`candidates: ${c.usc.candidates}`);
  lines.push(`selection: ${c.usc.selection}`);
  lines.push('');
  lines.push('### Confidence Gate');
  lines.push(`threshold: ${c.confidence_gate.threshold} out of 10`);
  lines.push(`halt_on_fail: ${c.confidence_gate.halt_on_fail}`);
  lines.push('');
  lines.push('---');
  lines.push('');

  // ── Expert Constellation ──
  lines.push('## EXPERT CONSTELLATION');
  lines.push('');
  template.experts.forEach((expert, i) => {
    lines.push(`### Expert ${i + 1}: ${expert.role}`);
    lines.push(`- **domain:** ${expert.domain}`);
    lines.push(`- **reasoning:** ${expert.reasoning}`);
    lines.push(`- **tools:** ${expert.tools.join(', ')}`);
    lines.push(`- **owns_nodes:** ${expert.owns_nodes.join(', ')}`);
    lines.push('');
  });
  lines.push('---');
  lines.push('');

  // ── Railroad ──
  lines.push('## RAILROAD');
  lines.push('');
  lines.push('### Execution Pattern');
  for (const seg of template.railroad.segments) {
    lines.push(`- nodes: [${seg.nodes.join(', ')}]`);
    lines.push(`  pattern: ${seg.pattern}`);
    lines.push(`  reason: "${seg.reason}"`);
  }
  lines.push('');
  lines.push('### Node Map');
  lines.push('');
  for (const node of template.railroad.nodes) {
    lines.push(`#### ${node.id}: ${node.name}`);
    lines.push(`- **expert:** ${node.expert}`);
    lines.push(`- **reasoning:** ${node.reasoning}`);
    lines.push(`- **input:** ${node.input}`);
    lines.push(`- **output:** ${node.output}`);
    lines.push(`- **cove:** ${node.cove}`);
    lines.push(`- **arq_gate:** ${node.arq_gate}`);
    lines.push(`- **handoff_to:** ${node.handoff_to.join(', ')}`);
    lines.push('');
  }
  lines.push('### Quality Stations');
  const qs = template.railroad.quality_stations;
  lines.push(`- **CoVE checkpoints:** ${qs.cove_checkpoints.join(', ')}`);
  lines.push(`- **PGScan:** ${qs.pgscan}`);
  lines.push(`- **Curation mode:** ${qs.curation_mode}`);
  lines.push('');
  lines.push('---');
  lines.push('');

  // ── Output Format ──
  lines.push('## OUTPUT FORMAT');
  lines.push('');
  const of = template.output_format;
  lines.push(`format: ${of.format}`);
  lines.push(`density: ${of.density}`);
  lines.push(`epistemic: ${of.epistemic}`);
  lines.push(`reflection: ${of.reflection}`);
  lines.push('');
  lines.push('---');
  lines.push('');

  // ── Forge Session Log ──
  lines.push('## FORGE SESSION LOG');
  lines.push('');
  const log = template.session_log;
  lines.push('### Intent');
  lines.push(`"${log.intent}"`);
  lines.push('');
  if (log.clarifications.length > 0) {
    lines.push('### Clarifications');
    log.clarifications.forEach((c, i) => {
      lines.push(`${i + 1}. Q: "${c.question}" → A: "${c.answer}"`);
    });
    lines.push('');
  }
  lines.push('### Scoring Rationale');
  lines.push(`"${log.scoring_rationale}"`);
  lines.push('');
  lines.push('### Formation Choice');
  lines.push(`"${log.formation_choice}"`);
  lines.push('');
  if (log.overrides.length > 0) {
    lines.push('### User Overrides');
    log.overrides.forEach(o => lines.push(`- "${o}"`));
    lines.push('');
  }

  return lines.join('\n');
}
```

**Step 2: Build to verify**

```bash
cd LEGIO-2026/legio-forge && npm run build
```

**Step 3: Commit**

```bash
git add LEGIO-2026/legio-forge/src/generator.ts
git commit -m "feat(forge): AGENTS.md template generator from ForgeSchema spec"
```

---

### Task 4: Forge session state machine

**Files:**
- Create: `LEGIO-2026/legio-forge/src/forge.ts`

**Context:** The forge is a tag-driven state machine mirroring the lotus-wisdom pattern. Tags: `begin → clarify → score → propose → track → seal`. Plus `load` and `list` for template library. Session state persists across tool calls within a conversation.

**Step 1: Create forge engine**

```typescript
import { randomUUID } from 'node:crypto';
import type {
  ForgeSession, ForgeStepInput, ForgeTag, RKQDE,
  CombatMode, Formation, ExpertDefinition, Railroad,
  Clarification, AgentsMdTemplate
} from './types.js';
import { parseRKQDE, selectMode, selectFormation, expertCount, iterationCount, defaultConstraints } from './scoring.js';
import { generateAgentsMd } from './generator.js';

// ── Tag prerequisites ──
const TAG_ORDER: Record<ForgeTag, ForgeTag[]> = {
  begin:   [],
  clarify: ['begin'],
  score:   ['begin'],
  propose: ['score'],
  track:   ['propose'],
  seal:    ['track'],
  load:    [],
  list:    [],
};

export class ForgeEngine {
  private session: ForgeSession | null = null;

  public processStep(input: ForgeStepInput): { content: Array<{ type: string; text: string }>; isError?: boolean } {
    try {
      // Library operations don't need a session
      if (input.tag === 'list') return this.handleList();
      if (input.tag === 'load') return this.handleLoad(input);

      // Begin creates new session
      if (input.tag === 'begin') {
        this.session = this.createSession(input.content);
        return this.handleBegin();
      }

      // All other tags require active session
      if (!this.session) throw new Error('No active forge session. Start with tag=begin.');
      if (this.session.sealed) throw new Error('Session already sealed. Start new session with tag=begin.');

      // Prereq check
      const prereqs = TAG_ORDER[input.tag] || [];
      for (const prereq of prereqs) {
        if (!this.session.tagJourney.includes(prereq)) {
          throw new Error(`[${input.tag}] requires [${prereq}] first. Journey: ${this.session.tagJourney.join(' → ')}`);
        }
      }

      this.session.tagJourney.push(input.tag);
      this.session.stepNumber = input.stepNumber;

      switch (input.tag) {
        case 'clarify': return this.handleClarify(input);
        case 'score':   return this.handleScore(input);
        case 'propose': return this.handlePropose(input);
        case 'track':   return this.handleTrack(input);
        case 'seal':    return this.handleSeal(input);
        default:        throw new Error(`Unknown tag: ${input.tag}`);
      }
    } catch (error) {
      return {
        content: [{ type: 'text', text: JSON.stringify({
          error: error instanceof Error ? error.message : String(error),
          status: 'failed',
          journey: this.session?.tagJourney.join(' → ') || 'none',
        }, null, 2) }],
        isError: true,
      };
    }
  }

  private createSession(intent: string): ForgeSession {
    return {
      id: randomUUID(),
      intent,
      clarifications: [],
      scores: null,
      tier: null,
      formation: null,
      experts: [],
      railroad: null,
      overrides: [],
      tagJourney: ['begin'],
      stepNumber: 1,
      sealed: false,
    };
  }

  // ── [begin] ──
  private handleBegin() {
    return this.respond({
      status: 'FRAMEWORK_RECEIVED',
      session_id: this.session!.id,
      intent: this.session!.intent,
      forge_flow: 'begin → clarify(×N) → score → propose → track → seal',
      instruction: 'Decompose the intent. Ask 1-3 clarifying questions using tag=clarify. Then score with tag=score.',
      clarification_categories: ['scope', 'quality', 'constraints', 'risk', 'domain', 'output'],
      do_not_ask_about: [
        'Things you can score from intent (RKQDE dimensions)',
        'Things that are always the same (ARQ gate count = 4)',
        'Things with safe defaults (Anti-Lazy = required)',
      ],
    });
  }

  // ── [clarify] ──
  private handleClarify(input: ForgeStepInput) {
    if (input.clarification) {
      this.session!.clarifications.push(input.clarification as Clarification);
      return this.respond({
        status: 'CLARIFICATION_RECEIVED',
        clarification_count: this.session!.clarifications.length,
        instruction: 'Continue clarifying or proceed to tag=score when ready.',
        journey: this.session!.tagJourney.join(' → '),
      });
    }
    // LLM is asking a question — pass through
    return this.respond({
      status: 'CLARIFICATION_NEEDED',
      question: input.content,
      instruction: 'Wait for user answer, then call tag=clarify with clarification.answer filled.',
      journey: this.session!.tagJourney.join(' → '),
    });
  }

  // ── [score] ──
  private handleScore(input: ForgeStepInput) {
    const rkqde = parseRKQDE(input.content);
    if (!rkqde) throw new Error('Could not parse RKQDE from content. Provide R=N K=N Q=N D=N E=N format.');

    const tier = selectMode(rkqde);
    const formation = selectFormation(rkqde);

    this.session!.scores = rkqde;
    this.session!.tier = tier;
    this.session!.formation = formation;

    return this.respond({
      status: 'SCORED',
      rkqde,
      tier,
      formation,
      experts: expertCount(tier),
      iterations: iterationCount(tier),
      constraints: defaultConstraints(tier),
      instruction: `Scored: ${tier} / ${formation}. Proceed to tag=propose to define expert constellation and constraints.`,
      journey: this.session!.tagJourney.join(' → '),
    });
  }

  // ── [propose] ──
  private handlePropose(input: ForgeStepInput) {
    // LLM proposes expert constellation + constraints in content
    // Parse experts from structured content or accept as-is
    return this.respond({
      status: 'PROPOSED',
      tier: this.session!.tier,
      formation: this.session!.formation,
      instruction: 'Show formation preview to user. If approved, proceed to tag=track to lay railroad. If user wants changes, call tag=propose again with adjustments.',
      note: 'Expert definitions and constraints should be finalized before track. Content should include expert roster with roles, domains, reasoning styles, and tools.',
      journey: this.session!.tagJourney.join(' → '),
    });
  }

  // ── [track] ──
  private handleTrack(input: ForgeStepInput) {
    // LLM provides railroad layout in content
    return this.respond({
      status: 'TRACKED',
      instruction: 'Show railroad preview to user. If approved, proceed to tag=seal. Nodes should have: id, name, expert, reasoning, input, output, cove, arq_gate, handoff_to.',
      journey: this.session!.tagJourney.join(' → '),
    });
  }

  // ── [seal] ──
  private handleSeal(input: ForgeStepInput) {
    this.session!.sealed = true;
    const templateName = input.template_name || this.session!.intent.toLowerCase().replace(/\s+/g, '-').replace(/[^a-z0-9-]/g, '');

    // Build the template from session state
    // NOTE: In real usage, the LLM assembles the full AgentsMdTemplate
    // from the propose+track outputs and passes it. The forge validates and writes.
    return this.respond({
      status: 'FORMATION_SEALED',
      session_id: this.session!.id,
      template_name: `${templateName}.agents.md`,
      paths: {
        template: `.legio/formations/${templateName}.agents.md`,
        active: './AGENTS.md',
      },
      instruction: 'AGENTS.md written. Formation sealed. Claude Code reads this at session start and executes with formation loaded.',
      journey: this.session!.tagJourney.join(' → '),
      session_summary: {
        intent: this.session!.intent,
        clarifications: this.session!.clarifications.length,
        tier: this.session!.tier,
        formation: this.session!.formation,
        overrides: this.session!.overrides,
      },
    });
  }

  // ── [list] ──
  private handleList() {
    // TODO: scan .legio/formations/ directory
    return this.respond({
      status: 'TEMPLATE_LIST',
      templates: [],
      instruction: 'No templates found yet. Use tag=begin to create the first formation.',
    });
  }

  // ── [load] ──
  private handleLoad(input: ForgeStepInput) {
    const name = input.template_name;
    if (!name) throw new Error('template_name required for load.');
    // TODO: read from .legio/formations/{name}.agents.md
    return this.respond({
      status: 'TEMPLATE_LOADED',
      template_name: name,
      instruction: 'Template loaded. Modify with tag=propose, then tag=seal to save.',
    });
  }

  private respond(data: Record<string, unknown>) {
    return { content: [{ type: 'text', text: JSON.stringify(data, null, 2) }] };
  }
}
```

**Step 2: Build to verify**

```bash
cd LEGIO-2026/legio-forge && npm run build
```

**Step 3: Commit**

```bash
git add LEGIO-2026/legio-forge/src/forge.ts
git commit -m "feat(forge): session state machine with tag-driven flow (begin→clarify→score→propose→track→seal)"
```

---

### Task 5: MCP server entry point + tool definition

**Files:**
- Create: `LEGIO-2026/legio-forge/src/index.ts`
- Create: `LEGIO-2026/legio-forge/cli.js`

**Step 1: Create MCP server**

```typescript
import { Server } from '@modelcontextprotocol/sdk/server/index.js';
import { StdioServerTransport } from '@modelcontextprotocol/sdk/server/stdio.js';
import {
  CallToolRequestSchema,
  ListToolsRequestSchema,
  type Tool,
} from '@modelcontextprotocol/sdk/types.js';
import { ForgeEngine } from './forge.js';

const FORGE_TOOL: Tool = {
  name: 'forge',
  description: `LEGIO formation forge — interactive planning engine that produces AGENTS.md templates.

**Workflow:** tag=begin (receive intent) → tag=clarify (×N, ask/answer questions) → tag=score (RKQDE scoring) → tag=propose (expert constellation + constraints) → tag=track (lay railroad) → tag=seal (write AGENTS.md).

**Library:** tag=list (show templates) → tag=load (load existing template for modification).

Produces reusable formation templates. Forge once, execute many.`,
  inputSchema: {
    type: 'object',
    properties: {
      tag: {
        type: 'string',
        enum: ['begin', 'clarify', 'score', 'propose', 'track', 'seal', 'load', 'list'],
        description: 'Current forge phase',
      },
      content: {
        type: 'string',
        description: 'Phase content — intent, answer, RKQDE scores, expert roster, railroad layout, or adjustment',
      },
      stepNumber: { type: 'integer', description: 'Current step in forge session', minimum: 1 },
      totalSteps: { type: 'integer', description: 'Estimated total steps', minimum: 1 },
      nextStepNeeded: { type: 'boolean', description: 'Whether another step is needed' },
      clarification: {
        type: 'object',
        properties: {
          question: { type: 'string' },
          answer: { type: 'string' },
          category: { type: 'string', enum: ['scope', 'quality', 'constraints', 'risk', 'domain', 'output'] },
        },
        description: 'For clarify tag — the Q&A pair',
      },
      override: {
        type: 'object',
        properties: {
          section: { type: 'string' },
          from: { type: 'string' },
          to: { type: 'string' },
          reason: { type: 'string' },
        },
        description: 'User override of forge recommendation',
      },
      template_name: { type: 'string', description: 'For load/seal — template identifier' },
    },
    required: ['tag', 'content', 'stepNumber', 'totalSteps', 'nextStepNeeded'],
  },
};

const forge = new ForgeEngine();

const server = new Server(
  { name: 'legio-forge', version: '0.1.0' },
  { capabilities: { tools: {} } },
);

server.setRequestHandler(ListToolsRequestSchema, async () => ({
  tools: [FORGE_TOOL],
}));

server.setRequestHandler(CallToolRequestSchema, async (request: any) => {
  if (request.params.name === 'forge') {
    return forge.processStep(request.params.arguments);
  }
  return {
    content: [{ type: 'text', text: `Unknown tool: ${request.params.name}` }],
    isError: true,
  };
});

async function main() {
  const transport = new StdioServerTransport();
  await server.connect(transport);
  console.error('LEGIO Forge MCP v0.1.0 — Formation forge running (stdio)');
}

main().catch((error) => {
  console.error('Fatal error:', error);
  process.exit(1);
});
```

**Step 2: Create CLI entry**

File: `LEGIO-2026/legio-forge/cli.js`

```javascript
#!/usr/bin/env node
import './dist/bundle.js';
```

**Step 3: Build and verify**

```bash
cd LEGIO-2026/legio-forge && npm run build
```

Expected: `dist/bundle.js` created. Server ready for MCP registration.

**Step 4: Register with Claude Code**

```bash
claude mcp add legio-forge -- node G:/.ktg-hub/Areas/AI-Anthropology/01-ktg-prompt/KTG/LEGIO-2026/legio-forge/dist/bundle.js
```

**Step 5: Smoke test**

Start a new Claude Code session and call:
```
forge tag=begin content="Build a Next.js SaaS dashboard with auth and Stripe"
```

Expected: `FRAMEWORK_RECEIVED` status with session ID and flow instructions.

**Step 6: Commit**

```bash
git add LEGIO-2026/legio-forge/src/index.ts LEGIO-2026/legio-forge/cli.js
git commit -m "feat(forge): MCP server entry point with forge tool definition"
```

---

### Task 6: Template library filesystem operations

**Files:**
- Create: `LEGIO-2026/legio-forge/src/library.ts`
- Modify: `LEGIO-2026/legio-forge/src/forge.ts` (wire in library calls for list/load/seal)

**Step 1: Create library module**

```typescript
import { readdir, readFile, writeFile, mkdir } from 'node:fs/promises';
import { join, basename } from 'node:path';
import { existsSync } from 'node:fs';

const FORMATIONS_DIR = '.legio/formations';

export async function ensureFormationsDir(projectRoot: string): Promise<string> {
  const dir = join(projectRoot, FORMATIONS_DIR);
  if (!existsSync(dir)) {
    await mkdir(dir, { recursive: true });
  }
  return dir;
}

export async function listTemplates(projectRoot: string): Promise<string[]> {
  const dir = join(projectRoot, FORMATIONS_DIR);
  if (!existsSync(dir)) return [];
  const files = await readdir(dir);
  return files.filter(f => f.endsWith('.agents.md'));
}

export async function loadTemplate(projectRoot: string, name: string): Promise<string> {
  const filePath = join(projectRoot, FORMATIONS_DIR, name.endsWith('.agents.md') ? name : `${name}.agents.md`);
  return readFile(filePath, 'utf-8');
}

export async function saveTemplate(projectRoot: string, name: string, content: string): Promise<{ templatePath: string; activePath: string }> {
  const dir = await ensureFormationsDir(projectRoot);
  const fileName = name.endsWith('.agents.md') ? name : `${name}.agents.md`;
  const templatePath = join(dir, fileName);
  const activePath = join(projectRoot, 'AGENTS.md');

  await writeFile(templatePath, content, 'utf-8');
  await writeFile(activePath, content, 'utf-8');

  return { templatePath, activePath };
}
```

**Step 2: Wire into forge.ts**

Update `handleList`, `handleLoad`, and `handleSeal` in `forge.ts` to call library functions. Pass `process.cwd()` as projectRoot.

**Step 3: Build and verify**

```bash
cd LEGIO-2026/legio-forge && npm run build
```

**Step 4: Commit**

```bash
git add LEGIO-2026/legio-forge/src/library.ts LEGIO-2026/legio-forge/src/forge.ts
git commit -m "feat(forge): template library — list/load/save formations to .legio/formations/"
```

---

### Task 7: Register forge in project .mcp.json

**Files:**
- Modify: `LEGIO-2026/../.mcp.json` (root project config)

**Step 1: Add legio-forge to .mcp.json**

Add alongside existing imperatus and lotus-wisdom entries:

```json
{
  "mcpServers": {
    "imperatus": { ... },
    "lotus-wisdom": { ... },
    "legio-forge": {
      "type": "stdio",
      "command": "node",
      "args": ["G:/.ktg-hub/Areas/AI-Anthropology/01-ktg-prompt/KTG/LEGIO-2026/legio-forge/dist/bundle.js"],
      "env": {}
    }
  }
}
```

**Step 2: Commit**

```bash
git add .mcp.json
git commit -m "feat(forge): register legio-forge MCP in project config"
```

---

### Task 8: End-to-end forge session test

**Files:**
- No new files — manual smoke test

**Step 1: Start fresh Claude Code session**

Verify `legio-forge` appears in available MCP tools.

**Step 2: Run minimal forge session (Velites)**

```
1. forge tag=begin content="REST API in Express.js for a todo app"
   → Expect: FRAMEWORK_RECEIVED

2. forge tag=clarify content="Auth required?" clarification={question:"Auth?",answer:"Public for now",category:"scope"}
   → Expect: CLARIFICATION_RECEIVED

3. forge tag=score content="R=3 K=2 Q=5 D=2 E=2"
   → Expect: SCORED, tier=Velites, formation=Cuneus

4. forge tag=propose content="Expert 1: API Specialist..."
   → Expect: PROPOSED

5. forge tag=track content="Node 1: Setup, Node 2: Routes, Node 3: Tests"
   → Expect: TRACKED

6. forge tag=seal content="Seal formation" template_name="express-todo-api"
   → Expect: FORMATION_SEALED, files written
```

**Step 3: Verify output**

Check that `.legio/formations/express-todo-api.agents.md` and `AGENTS.md` exist in project root.

**Step 4: Commit**

```bash
git commit -m "test(forge): verified end-to-end forge session (Velites)"
```

---

## Phase 2: TypeScript Runtime Servers (Tasks 9-12)

These servers enforce the AGENTS.md plan during execution. All follow the same MCP scaffold pattern as legio-forge.

### Task 9: legio-seal (Modules 02 + 14)

**Files:**
- Create: `LEGIO-2026/legio-seal/package.json` (copy from legio-forge, change name)
- Create: `LEGIO-2026/legio-seal/tsconfig.json` (copy)
- Create: `LEGIO-2026/legio-seal/src/types.ts`
- Create: `LEGIO-2026/legio-seal/src/seal.ts`
- Create: `LEGIO-2026/legio-seal/src/index.ts`

**Purpose:** Two tools:
- `seal_contract` — 嘘契約 enforcement. Called at session start after AGENTS.md loads. Binds the model to the formation. Detects shortcuts (skipped nodes, lowered confidence, bypassed gates). On violation: restart verbose.
- `final_reflect` — Called before output delivery. Binary success criteria check against AGENTS.md criteria. Confidence 0-10 scoring. 嘘契約 final enforcement. Returns RELEASE or HOLD.

**Key interfaces:**

```typescript
interface ContractState {
  signed: boolean;
  formation_loaded: string;  // AGENTS.md hash
  violations: Array<{ type: string; detail: string; timestamp: string }>;
  nodes_completed: string[];
  nodes_skipped: string[];
}

interface ReflectionResult {
  criteria_met: Record<string, boolean>;
  all_met: boolean;
  confidence: number;
  disposition: 'RELEASE' | 'HOLD' | 'RESTART';
  violations_total: number;
}
```

**Verification:** `npm run build` clean. Smoke test: call `seal_contract` with an AGENTS.md path, verify SIGNED status. Call with a skipped node, verify VIOLATION logged.

**Commit:**
```bash
git commit -m "feat(seal): legio-seal MCP — contract enforcement + final reflection"
```

---

### Task 10: legio-dispatch (Modules 03 + 08)

**Files:**
- Create: `LEGIO-2026/legio-dispatch/` (same scaffold)

**Purpose:** Two tools:
- `usc_dispatch` — Spawns N parallel candidate executions (via Claude Code Task tool or subagents). Collects results. Selects best or synthesizes consensus. N comes from AGENTS.md constraints.usc.candidates.
- `baton_swarm` — Orchestrates execution pattern per railroad segment. Baton: sequential handoff with context accumulation. Swarm: parallel dispatch with merge point conflict resolution. Reads pattern from AGENTS.md railroad.segments.

**Key interfaces:**

```typescript
interface DispatchState {
  active_pattern: 'baton' | 'swarm' | 'hybrid';
  current_segment: number;
  nodes_in_progress: string[];
  nodes_completed: Record<string, { output: string; confidence: number }>;
  handoff_context: string;  // accumulated for baton
  merge_conflicts: Array<{ node_a: string; node_b: string; resolution: string }>;
}
```

**Verification:** `npm run build` clean. Smoke test: call `baton_swarm` with a 3-node baton segment, verify sequential handoff tracking.

**Commit:**
```bash
git commit -m "feat(dispatch): legio-dispatch MCP — USC candidate dispatch + Baton/Swarm orchestration"
```

---

### Task 11: legio-gates (Modules 10 + 12)

**Files:**
- Create: `LEGIO-2026/legio-gates/` (same scaffold)

**Purpose:** Two tools:
- `arq_gate` — Quality gate enforcement at 4 fixed positions. Reads strictness from AGENTS.md constraints.arq_gates. Returns PROCEED or HALT. At HALT: blocks execution, requires reconsideration.
- `self_reflect` — Technique effectiveness audit. 4-phase: inventory what was used → score effectiveness → detect patterns → emit metadata for future sessions. Pure checklist logic.

**Key interfaces:**

```typescript
interface GateResult {
  gate_number: 1 | 2 | 3 | 4;
  position: string;
  confidence: number;
  strictness: 'advisory' | 'standard' | 'hard' | 'halt';
  disposition: 'PROCEED' | 'HALT';
  reason?: string;
}

interface ReflectionAudit {
  techniques_used: Array<{ name: string; effectiveness: number }>;
  patterns_detected: string[];
  recommendations: string[];
}
```

**Verification:** `npm run build` clean. Smoke test: call `arq_gate` with confidence=7 and strictness=halt, verify HALT.

**Commit:**
```bash
git commit -m "feat(gates): legio-gates MCP — ARQ gate enforcement + Self-Reflect audit"
```

---

### Task 12: Register all TS servers in .mcp.json

**Files:**
- Modify: `.mcp.json`

**Step 1: Add all three TS servers**

```json
{
  "legio-seal": {
    "type": "stdio",
    "command": "node",
    "args": ["G:/.../LEGIO-2026/legio-seal/dist/bundle.js"]
  },
  "legio-dispatch": {
    "type": "stdio",
    "command": "node",
    "args": ["G:/.../LEGIO-2026/legio-dispatch/dist/bundle.js"]
  },
  "legio-gates": {
    "type": "stdio",
    "command": "node",
    "args": ["G:/.../LEGIO-2026/legio-gates/dist/bundle.js"]
  }
}
```

**Step 2: Commit**

```bash
git commit -m "feat: register legio-seal, legio-dispatch, legio-gates in .mcp.json"
```

---

## Phase 3: Python Runtime Servers (Tasks 13-16)

Python servers handle semantic computation: embeddings, similarity, NLP classification, compression. All use FastMCP pattern.

### Task 13: legio-verify (Module 09 — CoVE)

**Files:**
- Create: `LEGIO-2026/legio-verify/pyproject.toml`
- Create: `LEGIO-2026/legio-verify/server.py`

**Purpose:** CoVE verification engine. Four variants auto-selected by output characteristics:
- `FACTUAL` — Claim-by-claim evidence matching (needs embeddings for claim↔source similarity)
- `LOGICAL` — Premise-conclusion tracing (inference chain validation)
- `CONSISTENCY` — Cross-node coherence (pairwise contradiction scan)
- `MULTI_EXPERT` — Expert consensus validation

Plus 10Rs epistemic overlay (Principes+) and negentropy gate.

**Tech:** `mcp[cli]`, `sentence-transformers` (for claim-evidence matching), `numpy` (for similarity)

**Key tool:** `cove_verify` — Takes elaborated output + variant selection + mode tier. Returns issues found, remediation applied, 10R scores, negentropy pass/fail.

**pyproject.toml:**

```toml
[project]
name = "legio-verify"
version = "0.1.0"
description = "LEGIO CoVE verification — claim matching, 10Rs, negentropy"
requires-python = ">=3.11"
dependencies = [
    "mcp[cli]>=1.2.0",
    "sentence-transformers>=3.0.0",
    "numpy>=1.26.0",
]
```

**Verification:** `uv run mcp dev server.py` — verify tool appears. Call with a sample claim set.

**Commit:**
```bash
git commit -m "feat(verify): legio-verify Python MCP — CoVE variants + 10Rs + negentropy"
```

---

### Task 14: legio-censor (Modules 11 + 15 — Censor + QMDR)

**Files:**
- Create: `LEGIO-2026/legio-censor/pyproject.toml`
- Create: `LEGIO-2026/legio-censor/server.py`

**Purpose:** Two tools:
- `censor_synthesize` — Tree of Thought synthesis (5 integration paths), 3-stage curation (relevance → quality → density), Chain of Density compression, success criteria enforcement. Returns RELEASE or HOLD.
- `qmdr_enrich` — 3-pass enrichment weaving. 6 priorities per pass (gaps → depth → perspectives → validation → sparkle → narrative). Returns woven manifest with enrichment directions.

**Tech:** `mcp[cli]`, `sentence-transformers` (relevance/quality scoring), `numpy`

**Verification:** `uv run mcp dev server.py` — verify both tools. Call `censor_synthesize` with multi-expert output.

**Commit:**
```bash
git commit -m "feat(censor): legio-censor Python MCP — synthesis/curation + QMDR enrichment"
```

---

### Task 15: legio-cep (Module 16 — CEP)

**Files:**
- Create: `LEGIO-2026/legio-cep/pyproject.toml`
- Create: `LEGIO-2026/legio-cep/server.py`

**Purpose:** CEP context packet generation. PDL (Progressive Density Layering) across L1-L4. MLDoE council (4 iterations: ARCHITECT → ANALYST → COMPRESSOR → ENGINEER). Kanji token arbitrage. NCL lattice validation. 97% cross-model acceptance target.

**Tool:** `cep_generate` — Takes session transcript + RKQDE scores. Returns compressed carry-packet at ≥0.15 ent/tok density. Includes NCL validation scores.

**Tech:** `mcp[cli]`, `tiktoken` (tokenizer awareness for density calculation), `sentence-transformers` (entity fusion, edge detection)

**Verification:** `uv run mcp dev server.py` — verify tool. Call with a sample transcript.

**Commit:**
```bash
git commit -m "feat(cep): legio-cep Python MCP — CEP packets + PDL + NCL validation"
```

---

### Task 16: Register Python servers in .mcp.json

**Files:**
- Modify: `.mcp.json`

**Step 1: Add Python servers**

```json
{
  "legio-verify": {
    "type": "stdio",
    "command": "uv",
    "args": ["run", "--directory", "G:/.../LEGIO-2026/legio-verify", "mcp", "run", "server.py"]
  },
  "legio-censor": {
    "type": "stdio",
    "command": "uv",
    "args": ["run", "--directory", "G:/.../LEGIO-2026/legio-censor", "mcp", "run", "server.py"]
  },
  "legio-cep": {
    "type": "stdio",
    "command": "uv",
    "args": ["run", "--directory", "G:/.../LEGIO-2026/legio-cep", "mcp", "run", "server.py"]
  }
}
```

**Step 2: Commit**

```bash
git commit -m "feat: register legio-verify, legio-censor, legio-cep Python MCPs"
```

---

## Phase 4: Integration (Tasks 17-18)

### Task 17: Update LEGIO-2026/CLAUDE.md

**Files:**
- Modify: `LEGIO-2026/CLAUDE.md`

Update to reflect the new architecture:
- Replace "Forge MCP — not yet built" with server locations and build commands
- Add the 7-server map with module assignments
- Add build/run commands for each server
- Document the forge→AGENTS.md→runtime flow
- Remove "Known Cleanup Items" that are addressed

**Commit:**
```bash
git commit -m "docs: update LEGIO-2026 CLAUDE.md with 7-server framework architecture"
```

---

### Task 18: End-to-end integration test

**Files:**
- No new files — manual integration test

**Step 1: Full forge session → AGENTS.md**

Run a Principes-tier forge session for a real use case (e.g., "Build voice agent with Twilio + ElevenLabs"). Verify AGENTS.md output has all sections populated.

**Step 2: Runtime tool calls against AGENTS.md**

1. `seal_contract` — bind to the forged formation
2. `arq_gate` gate_1 — verify expert belongs
3. `baton_swarm` — execute first baton segment
4. `cove_verify` — verify output of first segment
5. `arq_gate` gate_4 — final gate
6. `final_reflect` — check success criteria
7. `cep_generate` — generate carry-packet

**Step 3: Verify each tool reads from AGENTS.md correctly**

All tools should reference the same formation, tier, constraints, and success criteria.

**Commit:**
```bash
git commit -m "test: end-to-end integration — forge session → runtime execution verified"
```

---

## Dependency Graph

```
Phase 1 (Forge):  Task 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8
Phase 2 (TS):     Task 9, 10, 11 (parallel) → 12
Phase 3 (Python): Task 13, 14, 15 (parallel) → 16
Phase 4 (Glue):   Task 17 → 18

Phase 2 and 3 can run in parallel.
Phase 4 requires Phase 1-3 complete.
```

## Priority Order

1. **Tasks 1-8 (Forge)** — Foundation. Everything depends on AGENTS.md templates.
2. **Tasks 9-11 (TS runtime)** — Orchestration + gates. Needed for runtime enforcement.
3. **Tasks 13-15 (Python runtime)** — Semantic verification + compression. Quality elevation.
4. **Tasks 12, 16-18 (Registration + Integration)** — Wiring and validation.
