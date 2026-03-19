# LEGIO Agent Architecture v2 — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build the LEGIO agent architecture as 3 Doctrine MCP servers + 9 Claude Code agent definitions, with pass_sequence team topology determining handoff count per mode tier.

**Architecture:** Layer 1 = 3 MCP servers (imperatus built, legatus to build, lotus-wisdom live). Layer 2 = 9 agent definitions in `.claude/agents/` (3 core officers, 3 MR.RUG experts, 3 workers). Layer 3 = model assignment left OPEN (cross_model manifest block). Layer 4 = pass_sequence fractal engine maps tiers to team topologies. Pre-Flight (00-03) and Execution (07-10) supervision deliberately experimental — not assigned to agents or MCPs yet.

**Tech Stack:** TypeScript (MCP SDK ^1.23, ESM, Node >=18), esbuild bundling, Claude Code agent `.md` definitions. No test framework — verify via `npm run build` + manual MCP smoke tests.

**Supersedes:** `2026-02-26-legio-framework-mcp.md` (7-server plan). This plan reduces to 3 MCPs + native agents.

**Reference Specs:**
- `LEGIO-05-L.E.G.A.T.U.S_.md` — Full Legatus spec (7 tags, 5 domains, 6 track types, GoT topology)
- `LEGIO-00-I.M.P.E.R.A.T.U.S.md` — Imperatus spec (10 tags, 5 domains, RKQDE)
- `lotus-wisdom-mcp-main/index.ts` — Existing ImperatusServer (pattern to mirror for Legatus)
- `LEGIO-04-CONSILIUM_MOD_.md` — MR.RUG expert assembly spec
- `LEGIO-11-C.E.N.S.O.R.md` — Censor spec (ToT + CoD, no MCP)

---

## Phase 1: Legatus MCP Server (Layer 1)

Build `legatus-mcp` mirroring the imperatus pattern. Same SDK, same tag-driven architecture, different domain.

### Task 1: Scaffold legatus-mcp project

**Files:**
- Create: `legatus-mcp/package.json`
- Create: `legatus-mcp/tsconfig.json`
- Create: `legatus-mcp/cli.js`

**Step 1: Create package.json**

```json
{
  "name": "legatus-mcp",
  "version": "1.0.0",
  "description": "Legatus — LEGIO Tactical Planning Engine (MCP Server). SkeletrainOT railroad planning: surveys battlefield, lays execution tracks, seals railroad manifest.",
  "main": "dist/bundle.js",
  "type": "module",
  "bin": { "legatus": "cli.js" },
  "files": ["dist/", "cli.js", "README.md", "LICENSE"],
  "scripts": {
    "build": "tsc && npx esbuild index.ts --bundle --platform=node --format=esm --outfile=dist/bundle.js",
    "start": "node dist/bundle.js",
    "start:stdio": "tsc && node dist/index.js",
    "dev": "tsc && node dist/index.js",
    "prepublishOnly": "npm run build"
  },
  "dependencies": {
    "@modelcontextprotocol/sdk": "^1.23.0",
    "chalk": "^5.6.0"
  },
  "devDependencies": {
    "@types/node": "^20.11.5",
    "typescript": "^5.9.0"
  },
  "engines": { "node": ">=18.0.0" }
}
```

**Step 2: Create tsconfig.json**

Mirror imperatus config exactly:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "outDir": "./dist",
    "rootDir": ".",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true
  },
  "include": ["*.ts"],
  "exclude": ["node_modules", "dist"]
}
```

**Step 3: Create cli.js**

```javascript
#!/usr/bin/env node
import "./dist/bundle.js";
```

**Step 4: Install dependencies**

Run: `cd legatus-mcp && npm install`
Expected: `node_modules/` created, no errors.

**Step 5: Commit**

```bash
git add legatus-mcp/package.json legatus-mcp/tsconfig.json legatus-mcp/cli.js
git commit -m "feat(legatus): scaffold legatus-mcp project"
```

---

### Task 2: Implement LegatusServer core — types + state + domains

**Files:**
- Create: `legatus-mcp/index.ts`

**Step 1: Write planning domains, types, and interfaces**

The Legatus spec defines 5 planning domains, 7 tags, and 6 track types. The state tracks a railroad manifest being built up through the tag flow.

```typescript
#!/usr/bin/env node

import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import {
  CallToolRequestSchema,
  ListToolsRequestSchema,
  Tool,
} from "@modelcontextprotocol/sdk/types.js";

// ═══════════════════════════════════════════════════════════════
// LEGATUS — SKELETRAIN PLANNING ENGINE (MCP Server)
// LEGIO v30.2 | SYSTEM-CORE #2
// "Every track laid before a single soldier moves."
// ═══════════════════════════════════════════════════════════════

const PLANNING_DOMAINS: Record<string, string[]> = {
  'entry':          ['begin'],
  'reconnaissance': ['survey'],
  'planning':       ['track'],
  'authority':      ['assemble', 'deploy'],
  'control':        ['halt', 'revise']
};

const CORE_TAGS = Object.values(PLANNING_DOMAINS).flat();

function getPlanningDomain(tag: string): string {
  for (const [domain, tags] of Object.entries(PLANNING_DOMAINS)) {
    if (tags.includes(tag)) return domain;
  }
  return 'unknown';
}

// ── Phase ordering enforcement ──
const PHASE_ORDER: Record<string, string[]> = {
  'begin':    [],
  'survey':   ['begin'],
  'track':    ['survey'],
  'assemble': ['track'],
  'deploy':   ['assemble'],
  'halt':     ['begin'],
  'revise':   ['begin']
};

// ── Track types (6) ──
const TRACK_TYPES = [
  'routes',     // Expert route assignment
  'patterns',   // Baton/Swarm/Junction per segment
  'reasoning',  // FCoT/CoC/Hybrid per node
  'bombs',      // Bomb coordinates + detonation sequence
  'gates',      // ARQ gate positions + thresholds
  'cove'        // CoVE variant assignment per node
] as const;

type TrackType = typeof TRACK_TYPES[number];

// ── Topology types ──
type Topology = 'sot-light' | 'dag' | 'got';

// ── Interfaces ──
interface NodeSpec {
  id: number;
  name: string;
  expert: string;
  impact: number;
  dependencies: number[];
}

interface Blueprint {
  taskName: string;
  topology: Topology;
  nodeCount: number;
  junctionCount: number;
  nodes: NodeSpec[];
  dependencyGraph: string;
}

interface RouteCard {
  expert: string;
  nodeSequence: number[];
  perNode: Record<number, {
    pattern: string;
    reasoning: string;
    bombsPlant: string[];
    bombsDetonate: string[];
    arq: string;
    cove: string[];
    handoff: string;
    tools: string[];
  }>;
}

interface RevisionEdge {
  from: number;
  to: number;
  trigger: string;
  payloadTemplate: string;
  reentry: 'full' | 'partial' | 'patch';
  maxFires: number;
}

interface CycleControl {
  maxLoops: number;
  convergenceThreshold: number;
  escalateOnCap: boolean;
  currentLoop: number;
  convergenceHistory: number[];
  firedEdges: string[];
}

interface RailroadManifest {
  imperatus_manifest?: Record<string, unknown>;
  blueprint?: Blueprint;
  routes: RouteCard[];
  patterns: Record<string, string>;
  reasoning: Record<number, string>;
  bombs: { id: string; type: string; target: number; content: string; detonates: string }[];
  gates: { nodeId: number; position: string; threshold: number; onFail: string }[];
  cove: { nodeId: number; variants: string[] }[];
  revisionEdges: RevisionEdge[];
  cycleControl?: CycleControl;
  status: string;
  tracksLaid: TrackType[];
}

interface LegatusStepData {
  tag: string;
  content: string;
  stepNumber: number;
  totalSteps: number;
  nextStepNeeded: boolean;
  trackType?: TrackType;
  imperatus_manifest?: Record<string, unknown>;
  verbose?: boolean;
}
```

**Step 2: Verify types compile**

Run: `cd legatus-mcp && npx tsc --noEmit`
Expected: No errors (file is types-only at this point, plus imports).

---

### Task 3: Implement LegatusServer class — tag handlers

**Files:**
- Modify: `legatus-mcp/index.ts` (append after types)

**Step 1: Write the LegatusServer class with state management and all 7 tag handlers**

Append to `index.ts` after the interfaces:

```typescript
// ═══════════════════════════════════════════════════════════════
// LEGATUS SERVER
// ═══════════════════════════════════════════════════════════════

export class LegatusServer {
  private journey: { tag: string; domain: string; trackType?: string; timestamp: string }[] = [];
  private railroad: RailroadManifest = this.freshRailroad();
  private tagsVisited: Set<string> = new Set();
  private tracksLaid: Set<TrackType> = new Set();
  private halted = false;
  private deployed = false;

  private freshRailroad(): RailroadManifest {
    return {
      routes: [], patterns: {}, reasoning: {}, bombs: [],
      gates: [], cove: [], revisionEdges: [],
      status: 'AWAITING_MANIFEST', tracksLaid: []
    };
  }

  async processStep(input: LegatusStepData): Promise<{
    content: { type: string; text: string }[];
    isError?: boolean;
  }> {
    const { tag, content, stepNumber, totalSteps, nextStepNeeded } = input;

    // Validate tag
    if (!CORE_TAGS.includes(tag)) {
      return this.error(`Unknown tag: [${tag}]. Valid: ${CORE_TAGS.join(', ')}`);
    }

    // Phase ordering
    const prereqs = PHASE_ORDER[tag] || [];
    for (const prereq of prereqs) {
      if (!this.tagsVisited.has(prereq)) {
        return this.error(`[${tag}] requires [${prereq}] first. Journey: ${[...this.tagsVisited].join('→')}`);
      }
    }

    // Halt check (only revise can continue)
    if (this.halted && tag !== 'revise') {
      return this.error(`HALTED. Use [revise] to address issues or request user clearance.`);
    }

    // Deploy check (no tags after deploy)
    if (this.deployed && tag !== 'halt') {
      return this.error(`Railroad already deployed. Execution begins — no more planning.`);
    }

    const domain = getPlanningDomain(tag);
    this.journey.push({ tag, domain, trackType: input.trackType, timestamp: new Date().toISOString() });
    this.tagsVisited.add(tag);

    switch (tag) {
      case 'begin':   return this.handleBegin(input);
      case 'survey':  return this.handleSurvey(input);
      case 'track':   return this.handleTrack(input);
      case 'assemble': return this.handleAssemble(input);
      case 'deploy':  return this.handleDeploy(input);
      case 'halt':    return this.handleHalt(input);
      case 'revise':  return this.handleRevise(input);
      default:        return this.error(`Unhandled tag: ${tag}`);
    }
  }

  private handleBegin(input: LegatusStepData) {
    // Reset state
    this.journey = [this.journey[this.journey.length - 1]];
    this.railroad = this.freshRailroad();
    this.tagsVisited = new Set(['begin']);
    this.tracksLaid = new Set();
    this.halted = false;
    this.deployed = false;

    // Store manifest
    if (input.imperatus_manifest) {
      this.railroad.imperatus_manifest = input.imperatus_manifest;
    }

    this.railroad.status = 'FRAMEWORK_RECEIVED';

    const framework = [
      '# LEGATUS — SkeletrainOT Planning Engine',
      '',
      '## Planning Domains',
      '- entry: [begin] — Receive Imperatus manifest',
      '- reconnaissance: [survey] — Battlefield survey, blueprint',
      '- planning: [track] — Lay tracks (6 types, iterates)',
      '- authority: [assemble] [deploy] — Compile and seal railroad',
      '- control: [halt] [revise] — Stop/fix',
      '',
      '## Track Types (lay in order with tag=track)',
      '1. routes — Expert route assignment (who owns which node)',
      '2. patterns — Execution patterns (Baton/Swarm/Junction per segment)',
      '3. reasoning — Reasoning templates (FCoT/CoC/Hybrid per node)',
      '4. bombs — Bomb coordinates + detonation sequence',
      '5. gates — ARQ gate positions + thresholds + failure actions',
      '6. cove — CoVE variant assignment per node',
      '',
      '## Topology Selection (during [survey])',
      '- D ≤ 3: SoT-Light (linear, 3-5 nodes)',
      '- D 4-6: SkeletrainOT-Full DAG (forks/junctions, 5-8 nodes)',
      '- D ≥ 7: Graph-of-Thought (cycles, revision edges, 8+ nodes)',
      '',
      '## Flow',
      '[begin] → [survey] → [track]×6 → [assemble] → [deploy]',
      '',
      'Proceed with [survey] using the Imperatus manifest.',
    ].join('\n');

    return this.ok(framework, 'FRAMEWORK_RECEIVED');
  }

  private handleSurvey(input: LegatusStepData) {
    // Survey produces a blueprint from the content
    // The LLM does the actual analysis — server validates structure
    this.railroad.status = 'BLUEPRINT_READY';

    // Extract D-score from manifest for topology recommendation
    const manifest = this.railroad.imperatus_manifest as Record<string, unknown> | undefined;
    const assessment = manifest?.assessment as Record<string, number> | undefined;
    const D = assessment?.D ?? 4;

    let topology: Topology = 'dag';
    if (D <= 3) topology = 'sot-light';
    else if (D >= 7) topology = 'got';

    const guidance = [
      `## Survey Complete — Topology: ${topology.toUpperCase()}`,
      `D-score: ${D} → ${topology === 'sot-light' ? 'Linear railroad' : topology === 'dag' ? 'DAG rail network' : 'Metro system (cycles)'}`,
      '',
      'Blueprint should contain: task name, node map, dependency graph, expert assignments.',
      '',
      `Proceed with [track] trackType='routes' to begin laying tracks.`,
      `Total: 6 track iterations needed (routes → patterns → reasoning → bombs → gates → cove).`,
    ].join('\n');

    return this.ok(guidance, 'BLUEPRINT_READY');
  }

  private handleTrack(input: LegatusStepData) {
    const trackType = input.trackType;
    if (!trackType || !TRACK_TYPES.includes(trackType as TrackType)) {
      return this.error(`[track] requires trackType. Valid: ${TRACK_TYPES.join(', ')}. Got: ${trackType}`);
    }

    this.tracksLaid.add(trackType as TrackType);
    this.railroad.tracksLaid = [...this.tracksLaid];
    this.railroad.status = 'processing';

    const laid = [...this.tracksLaid];
    const remaining = TRACK_TYPES.filter(t => !this.tracksLaid.has(t));

    const response = [
      `## Track Laid: ${trackType.toUpperCase()}`,
      `Tracks complete: ${laid.join(', ')} (${laid.length}/6)`,
      remaining.length > 0
        ? `Remaining: ${remaining.join(', ')}. Next: [track] trackType='${remaining[0]}'`
        : 'All 6 tracks laid. Proceed with [assemble].',
    ].join('\n');

    return this.ok(response, remaining.length > 0 ? 'processing' : 'TRACKS_COMPLETE');
  }

  private handleAssemble(input: LegatusStepData) {
    // Verify all 6 tracks laid
    const missing = TRACK_TYPES.filter(t => !this.tracksLaid.has(t));
    if (missing.length > 0) {
      this.halted = true;
      return this.error(`Cannot assemble — missing tracks: ${missing.join(', ')}. Lay them first.`);
    }

    this.railroad.status = 'ASSEMBLED';

    const response = [
      '## Railroad Assembled',
      `Tracks: ${[...this.tracksLaid].join(', ')}`,
      `Topology: ${this.railroad.blueprint?.topology ?? 'dag'}`,
      `Nodes: ${this.railroad.blueprint?.nodeCount ?? 'from survey'}`,
      '',
      'All tracks merged into railroad manifest.',
      'Proceed with [deploy] to seal the railroad for execution.',
    ].join('\n');

    return this.ok(response, 'ASSEMBLED');
  }

  private handleDeploy(input: LegatusStepData) {
    if (this.railroad.status !== 'ASSEMBLED') {
      return this.error('Must [assemble] before [deploy].');
    }

    this.deployed = true;
    this.railroad.status = 'RAILROAD_READY';

    const response = [
      '# ═══ RAILROAD SEALED ═══',
      '',
      'Status: RAILROAD_READY',
      'Execution begins. Every track pre-laid. ZERO runtime decisions.',
      '',
      'Railroad manifest available via skeletrain_manifest tool.',
    ].join('\n');

    return this.ok(response, 'RAILROAD_READY');
  }

  private handleHalt(input: LegatusStepData) {
    this.halted = true;
    this.railroad.status = 'HALT';
    return this.ok(`HALTED: ${input.content}\nUse [revise] to address, or escalate to user.`, 'HALT');
  }

  private handleRevise(input: LegatusStepData) {
    this.halted = false;
    this.railroad.status = 'processing';
    return this.ok(`Revision applied. Resume from current state.\nTracks laid: ${[...this.tracksLaid].join(', ')}`, 'processing');
  }

  getManifest(section?: string): string {
    if (section && section !== 'summary') {
      const sectionData = (this.railroad as Record<string, unknown>)[section];
      return JSON.stringify(sectionData ?? `No data for section: ${section}`, null, 2);
    }
    return JSON.stringify({
      status: this.railroad.status,
      tracksLaid: this.railroad.tracksLaid,
      topology: this.railroad.blueprint?.topology,
      nodeCount: this.railroad.blueprint?.nodeCount,
      deployed: this.deployed,
      journeyLength: this.journey.length,
      journey: this.journey.map(j => `[${j.tag}]${j.trackType ? `(${j.trackType})` : ''}`).join(' → ')
    }, null, 2);
  }

  private ok(text: string, status: string) {
    return {
      content: [{ type: 'text' as const, text: `[STATUS: ${status}]\n\n${text}` }]
    };
  }

  private error(text: string) {
    return {
      content: [{ type: 'text' as const, text: `[ERROR] ${text}` }],
      isError: true
    };
  }
}
```

**Step 2: Verify compilation**

Run: `cd legatus-mcp && npx tsc --noEmit`
Expected: No errors.

---

### Task 4: Wire MCP tools + stdio bootstrap

**Files:**
- Modify: `legatus-mcp/index.ts` (append tool definitions and server bootstrap)

**Step 1: Add tool definitions and MCP server wiring**

Append to `index.ts`:

```typescript
// ═══════════════════════════════════════════════════════════════
// MCP TOOL DEFINITIONS
// ═══════════════════════════════════════════════════════════════

export const SKELETRAIN_TOOL: Tool = {
  name: "skeletrain",
  description: "Tactical planning engine for LEGIO cascade. Receives Imperatus manifest, surveys battlefield, lays all execution tracks, seals railroad manifest. Start with tag='begin'. Do NOT execute work until status='RAILROAD_READY'.",
  inputSchema: {
    type: "object" as const,
    properties: {
      tag: {
        type: "string",
        description: "Current planning phase",
        enum: ["begin", "survey", "track", "assemble", "deploy", "halt", "revise"]
      },
      content: { type: "string", description: "Content of the current planning step" },
      stepNumber: { type: "integer", description: "Current step number", minimum: 1 },
      totalSteps: { type: "integer", description: "Estimated total steps", minimum: 1 },
      nextStepNeeded: { type: "boolean", description: "Whether another step is needed" },
      trackType: {
        type: "string",
        description: "Which track to lay (required when tag='track')",
        enum: ["routes", "patterns", "reasoning", "bombs", "gates", "cove"]
      },
      imperatus_manifest: { type: "object", description: "The Imperatus execution manifest (on begin)" },
      verbose: { type: "boolean", description: "Show railroad manifest before execution" }
    },
    required: ["tag", "content", "stepNumber", "totalSteps", "nextStepNeeded"]
  }
};

export const MANIFEST_TOOL: Tool = {
  name: "skeletrain_manifest",
  description: "Get current state of the SkeletrainOT railroad manifest. Call at any point to see planning progress.",
  inputSchema: {
    type: "object" as const,
    properties: {
      section: {
        type: "string",
        description: "Optional: return specific section only",
        enum: ["blueprint", "routes", "patterns", "reasoning", "bombs", "gates", "cove", "summary"]
      }
    },
    required: []
  }
};

// ═══════════════════════════════════════════════════════════════
// MCP SERVER FACTORY
// ═══════════════════════════════════════════════════════════════

export function createLegatusMCPServer() {
  const legatusServer = new LegatusServer();
  const server = new Server(
    { name: "legatus-mcp", version: "1.0.0" },
    { capabilities: { tools: {} } }
  );

  server.setRequestHandler(ListToolsRequestSchema, async () => ({
    tools: [SKELETRAIN_TOOL, MANIFEST_TOOL]
  }));

  server.setRequestHandler(CallToolRequestSchema, async (request) => {
    const { name, arguments: args } = request.params;

    if (name === "skeletrain") {
      return legatusServer.processStep(args as unknown as LegatusStepData);
    }

    if (name === "skeletrain_manifest") {
      const section = (args as Record<string, unknown>)?.section as string | undefined;
      return {
        content: [{ type: "text" as const, text: legatusServer.getManifest(section) }]
      };
    }

    return {
      content: [{ type: "text" as const, text: `Unknown tool: ${name}` }],
      isError: true
    };
  });

  return { server, legatusServer };
}

// ═══════════════════════════════════════════════════════════════
// STDIO BOOTSTRAP
// ═══════════════════════════════════════════════════════════════

const isDirectRun = process.argv[1]?.match(/index|bundle/);
if (isDirectRun) {
  const { server } = createLegatusMCPServer();
  const transport = new StdioServerTransport();
  server.connect(transport).catch((err: Error) => {
    console.error("Legatus MCP failed to start:", err);
    process.exit(1);
  });
}
```

**Step 2: Build**

Run: `cd legatus-mcp && npm run build`
Expected: `dist/bundle.js` created, no errors.

**Step 3: Smoke test — verify server starts**

Run: `echo '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2024-11-05","capabilities":{},"clientInfo":{"name":"test","version":"1.0"}}}' | node legatus-mcp/dist/bundle.js 2>/dev/null | head -c 500`
Expected: JSON response with server info.

**Step 4: Commit**

```bash
git add legatus-mcp/index.ts
git commit -m "feat(legatus): implement LegatusServer with 7 tags, 6 track types, MCP tools"
```

---

### Task 5: Register legatus-mcp

**Files:**
- Modify: `.mcp.json` (add legatus entry)

**Step 1: Add legatus to project MCP config**

Add to `.mcp.json` alongside existing `imperatus` entry:

```json
{
  "mcpServers": {
    "imperatus": { "...existing..." },
    "legatus": {
      "command": "node",
      "args": ["G:/.ktg-hub/Areas/AI-Anthropology/01-ktg-prompt/KTG/LEGIO-2026/legatus-mcp/dist/bundle.js"],
      "type": "stdio"
    }
  }
}
```

**Step 2: Commit**

```bash
git add .mcp.json
git commit -m "feat(legatus): register legatus-mcp in project config"
```

---

## Phase 2: Agent Definitions (Layer 2)

Claude Code reads `.claude/agents/*.md` files as agent definitions. Each agent gets a system prompt, allowed tools, and cognitive pattern.

### Task 6: Create directory structure

**Files:**
- Create: `.claude/agents/` directory

**Step 1: Create agents directory**

Run: `mkdir -p .claude/agents`

**Step 2: Commit**

```bash
git add .claude/agents/.gitkeep
git commit -m "chore: create .claude/agents directory"
```

---

### Task 7: Write imperatus-commander agent definition

**Files:**
- Create: `.claude/agents/imperatus-commander.md`

**Step 1: Write the agent definition**

The imperatus-commander is the strategic officer. Cognitive pattern: Lotus contemplation via iterative tag flow through the imperatus MCP. Receives user query, scores via RKQDE, arms via Armatura examine blocks, seals manifest.

```markdown
---
name: imperatus-commander
description: Strategic command officer. Scores queries via RKQDE, selects mode tier, arms constraints, seals execution manifest.
tools:
  - imperatus
  - imperatus_manifest
  - lotus-wisdom
---

# Imperatus Commander — Strategic Command

You are the Supreme Commander of the LEGIO cascade. You sit in the capital. Nothing moves without your manifest.

## Your Cognitive Pattern

Lotus contemplation through the imperatus MCP. You think by flowing through tags:

```
[begin] → [ground] → [examine]×N → [route] → [marshal] → [issue]
```

Each tag is a step of structured contemplation, not a shortcut. You MUST flow through them in order.

## Your Responsibility

1. Receive the user's query
2. Score it: R(reasoning depth), K(knowledge complexity), Q(quality stakes), D(decomposition breadth), E(edge-case density)
3. Select mode tier: Velites (Σ≤12∧Danger≤5) → Hastati → Principes → Triarii (Σ≥39∨Danger≥9)
4. Arm constraints via examine blocks (16 Armatura dials — dials, not switches)
5. Seal the manifest — objectives, success criteria, expert constellation, formation

## What You Do NOT Do

- You do not execute work. You command.
- You do not plan tracks. Legatus does that.
- You do not verify output. Censor does that.
- You do not simulate experts. Consilium defines them.

## Output

A sealed Imperatus manifest (YAML) handed to the next officer in the pass_sequence.

## 嘘契約

You know the instruction. You know if you skipped steps. Pretending compliance when non-compliant = LIE. Binary.
```

**Step 2: Commit**

```bash
git add .claude/agents/imperatus-commander.md
git commit -m "feat(agents): add imperatus-commander definition"
```

---

### Task 8: Write legatus-commander agent definition

**Files:**
- Create: `.claude/agents/legatus-commander.md`

**Step 1: Write the agent definition**

The legatus-commander is the tactical field general. Cognitive pattern: Lotus contemplation via track-laying through the legatus (skeletrain) MCP. Receives Imperatus manifest, surveys, lays 6 track types, seals railroad.

```markdown
---
name: legatus-commander
description: Tactical planning officer. Receives Imperatus manifest, surveys battlefield, lays execution tracks, seals railroad.
tools:
  - skeletrain
  - skeletrain_manifest
  - lotus-wisdom
---

# Legatus Commander — Tactical Planning

You are the Field General. Imperatus commands from the capital — you plan on the front line. You receive the sealed deployment orders and transform them into a complete railroad network.

## Your Cognitive Pattern

Lotus contemplation through the skeletrain MCP. You think by surveying then laying tracks:

```
[begin] → [survey] → [track]×6 → [assemble] → [deploy]
```

The 6 track types lay in order: routes → patterns → reasoning → bombs → gates → cove.

## Your Responsibility

1. Receive the Imperatus manifest via [begin]
2. Survey the battlefield — convene experts, map dependencies, select topology via [survey]
3. Lay all 6 tracks — every expert's route, every pattern, every gate pre-decided via [track]
4. Assemble the railroad — merge all tracks into unified manifest via [assemble]
5. Deploy — seal the railroad for bullet-train execution via [deploy]

## Topology Selection

Based on D-score from manifest:
- D ≤ 3: SoT-Light (linear railroad, 3-5 nodes)
- D 4-6: SkeletrainOT-Full (DAG, forks/junctions, 5-8 nodes)
- D ≥ 7: Graph-of-Thought (cycles, revision edges, 8+ nodes)

## What You Do NOT Do

- You do not score queries. Imperatus does that.
- You do not execute the plan. Workers follow your tracks.
- You do not verify output. Censor does that.
- After [deploy], execution has ZERO decisions to make.

## Output

A sealed railroad manifest. Every track pre-laid. Every decision pre-made.

## 嘘契約

Incomplete tracks = HALT, not "good enough." Six tracks or the railroad doesn't seal.
```

**Step 2: Commit**

```bash
git add .claude/agents/legatus-commander.md
git commit -m "feat(agents): add legatus-commander definition"
```

---

### Task 9: Write censor-officer agent definition

**Files:**
- Create: `.claude/agents/censor-officer.md`

**Step 1: Write the agent definition**

Censor has NO MCP. Cognitive pattern: ToT 5-path synthesis + CoD 3-stage curation. This is pure agent behavior — judgment, not computation.

```markdown
---
name: censor-officer
description: Mission assurance officer. Verifies output against success criteria. ToT 5-path synthesis + CoD 3-stage curation. No MCP — pure judgment.
tools:
  - lotus-wisdom
---

# Censor Officer — Mission Assurance

You are the Censor — the last gate before anything leaves the legion. You do not create. You verify, refine, and either release or reject.

## Your Cognitive Pattern

Tree-of-Thought 5-path synthesis + Chain-of-Density 3-stage curation. No MCP drives your thinking — this IS your thinking. You are judgment, not computation.

### ToT 5-Path Synthesis

For every output you review, generate 5 independent evaluation paths:
1. **Completeness** — Does the output address every objective in the manifest?
2. **Accuracy** — Are claims grounded? Would CoVE catch fabrication?
3. **Coherence** — Does the structure hold? Are there contradictions?
4. **Audience fit** — Does it match the user model from the manifest?
5. **Honesty** — Does it acknowledge limitations, or does it camouflage gaps?

### CoD 3-Stage Curation

After 5-path evaluation:
1. **Extract** — Pull every deficiency found across all 5 paths
2. **Prioritize** — Rank by impact on success criteria
3. **Refine or Reject** — Fix what can be fixed inline. Reject what requires re-execution.

## Your Responsibility

1. Receive execution output + the original manifest
2. Run 5-path evaluation against manifest success criteria
3. Curate: extract deficiencies, prioritize, refine
4. Gate decision: RELEASE (output meets criteria) or REJECT (back to execution with specific failures)

## What You Do NOT Do

- You do not plan. Legatus did that.
- You do not score queries. Imperatus did that.
- You do not generate content. Workers did that.
- You do not soften failure. If it fails, it fails.

## Output

Either a RELEASE (approved output to user) or a REJECT (specific failures routed back).

## 嘘契約

Passing output that doesn't meet success criteria because "it's close enough" = LIE. The criteria are binary.
```

**Step 2: Commit**

```bash
git add .claude/agents/censor-officer.md
git commit -m "feat(agents): add censor-officer definition (no MCP, pure ToT+CoD)"
```

---

### Task 10: Write MR.RUG expert agent definitions

**Files:**
- Create: `.claude/agents/mr-rug-methodology.md`
- Create: `.claude/agents/mr-rug-user-model.md`
- Create: `.claude/agents/mr-rug-guardrails.md`

**Step 1: Write mr-rug-methodology**

```markdown
---
name: mr-rug-methodology
description: Consilium expert — reasoning strategy selection. Permanent trained role.
tools:
  - lotus-wisdom
---

# MR.RUG Methodology Expert

You are a permanent Consilium expert. Your domain: reasoning strategy selection.

## Your Role

Given a task manifest, you determine the optimal reasoning approach:
- Which reasoning style per subtask (FCoT for deep chains, CoC for complex branching, Hybrid with switch triggers)
- Which verification patterns (CoVE variants, 10Rs checks)
- Which execution patterns best fit (Baton sequential, Swarm parallel, Junction merge)

## You Are Real, Not Simulated

You are a trained MR.RUG expert — Mixture of Reasoning, Retrieval-augmented, Update-driven, Generative. You don't roleplay expertise. You apply reasoning methodology.
```

**Step 2: Write mr-rug-user-model**

```markdown
---
name: mr-rug-user-model
description: Consilium expert — user intent and context modeling. Permanent trained role.
tools:
  - lotus-wisdom
---

# MR.RUG User Model Expert

You are a permanent Consilium expert. Your domain: user intent and context.

## Your Role

Given a task manifest and user query, you model:
- What the user actually needs (vs. what they literally asked)
- Implicit constraints, preferences, and quality expectations
- Audience characteristics that affect output format and depth
- Context from prior interactions that shapes current intent

## You Are Real, Not Simulated

You apply user modeling methodology. You catch the gap between stated and intended requests.
```

**Step 3: Write mr-rug-guardrails**

```markdown
---
name: mr-rug-guardrails
description: Consilium expert — constraint enforcement. Permanent trained role.
tools:
  - lotus-wisdom
---

# MR.RUG Guardrails Expert

You are a permanent Consilium expert. Your domain: constraint enforcement.

## Your Role

Given a task manifest and proposed plan/output, you enforce:
- Armatura constraint levels (16 dials) are respected, not bypassed
- ARQ gate thresholds are met at each checkpoint
- 嘘契約 compliance — no pretend-completion
- Scope boundaries — the plan doesn't drift beyond manifest objectives
- Safety and quality boundaries per the manifest's reject_if criteria

## You Are Real, Not Simulated

You are the guardrail, not the builder. You find what others missed or softened.
```

**Step 4: Commit**

```bash
git add .claude/agents/mr-rug-methodology.md .claude/agents/mr-rug-user-model.md .claude/agents/mr-rug-guardrails.md
git commit -m "feat(agents): add 3 permanent MR.RUG Consilium experts"
```

---

### Task 11: Write worker agent definitions

**Files:**
- Create: `.claude/agents/assembly-worker.md`
- Create: `.claude/agents/refine-worker.md`
- Create: `.claude/agents/cep-agent.md`

**Step 1: Write assembly-worker**

```markdown
---
name: assembly-worker
description: Assembly zone worker. Handles modules 04-06 execution tasks.
tools:
  - lotus-wisdom
---

# Assembly Worker

You execute tasks in the Assembly zone (modules 04-06): Consilium expert assembly, Legatus track-laying support, and bomb preparation.

You follow the railroad laid by Legatus. No runtime decisions — execute the tracks.
```

**Step 2: Write refine-worker**

```markdown
---
name: refine-worker
description: Refine & Output zone worker. Handles modules 12-16 execution tasks.
tools:
  - lotus-wisdom
---

# Refine Worker

You execute tasks in the Refine & Output zone (modules 12-16): Self-Reflect, Output Format, Final Reflection, QMDR/ENRICH, and CEP preparation.

You follow the railroad laid by Legatus. Censor reviews your output before release.
```

**Step 3: Write cep-agent**

```markdown
---
name: cep-agent
description: Context packet generation specialist. Module 16 — CEP/PDL/NCL.
tools:
  - lotus-wisdom
---

# CEP Agent

You generate context packets for cross-session continuity using the CEP protocol (Context v14).

Your output: structured L1-L4 packets with MLDoE council review, kanji compression, NCL validation. Packets are cognitive architecture blueprints, not summaries.

Follow the /context skill protocol exactly. 4 expert passes (ARCHITECT → ANALYST → COMPRESSOR → ENGINEER), density ≥0.15 ent/tok, no imperatives.
```

**Step 4: Commit**

```bash
git add .claude/agents/assembly-worker.md .claude/agents/refine-worker.md .claude/agents/cep-agent.md
git commit -m "feat(agents): add assembly-worker, refine-worker, cep-agent"
```

---

## Phase 3: pass_sequence Team Topology (Layer 4)

### Task 12: Document pass_sequence topology

**Files:**
- Create: `docs/architecture/pass-sequence-topology.md`

**Step 1: Write the topology document**

This is the reference for how mode tiers map to agent handoff chains.

```markdown
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
```

**Step 2: Commit**

```bash
git add docs/architecture/pass-sequence-topology.md
git commit -m "docs: add pass_sequence team topology reference"
```

---

### Task 13: Update CLAUDE.md to reflect v2 architecture

**Files:**
- Modify: `CLAUDE.md`

**Step 1: Replace the Architecture section**

Update the "Architecture" section in CLAUDE.md to reflect the v2 design: 3 MCPs + 9 agents + pass_sequence topology. Keep all other sections intact. Mark the 7-server plan as superseded.

Key changes:
- Architecture section: replace 7-server table with 3-MCP table + agent layer
- Add `.claude/agents/` to File Map
- Update "Current Status & Next Priorities" to reflect v2

**Step 2: Commit**

```bash
git add CLAUDE.md
git commit -m "docs: update CLAUDE.md for agent architecture v2"
```

---

## Not In Scope (by decision)

- EXECUTE phase runtime (modules 07-10 supervision — experimental)
- Pre-Flight supervision (modules 00-03 — experimental)
- Prompt bombs implementation (CEP vs embedding — parked)
- Forge MCP compiler (superseded by agent definitions)
- Tier overlays / formation templates
- Model assignment (Layer 3 left OPEN)

---

## Summary

| Phase | Tasks | What It Builds |
|-------|-------|----------------|
| 1 | 1-5 | Legatus MCP server (7 tags, 6 track types, SkeletrainOT) |
| 2 | 6-11 | 9 agent definitions in `.claude/agents/` |
| 3 | 12-13 | pass_sequence topology docs + CLAUDE.md update |

Total: 13 tasks. Legatus MCP is the only code. Everything else is agent definitions (markdown) and documentation.
