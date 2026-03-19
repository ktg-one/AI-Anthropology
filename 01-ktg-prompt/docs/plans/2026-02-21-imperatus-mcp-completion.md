# Imperatus MCP Server — Completion Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Complete the Imperatus MCP server from working scaffold to production-ready — formation templates, full manifest assembly, Armatura content injection, dual transport, session management, and test coverage.

**Architecture:** The existing `index.ts` (822 lines, stdio) has all tag handlers and phase ordering working. We complete the stubs (marshal, formations, examine content), add StreamableHTTP transport from `server.ts` pattern, add per-session state, and wrap it in tests. No src/ refactor — enhance in place for velocity.

**Tech Stack:** TypeScript, @modelcontextprotocol/sdk ^1.23.0, Express, Node.js >=18, vitest (tests), esbuild (bundle)

---

## Reference Paths

| Alias | Path |
|-------|------|
| `$MCP` | `G:/.ktg-hub/Areas/AI-Anthropology/01-ktg-prompt/KTG/LEGIO-2026/lotus-wisdom-mcp-main` |
| `$SPEC` | `G:/.ktg-hub/Areas/AI-Anthropology/01-ktg-prompt/KTG` |

## Current State Assessment

**Working in `$MCP/index.ts`:**
- ImperatusServer class with all 9 tag handlers
- Phase ordering enforcement (PHASE_ORDER map)
- Tag/journey tracking
- RKQDE regex parsing from content
- Velites fast path with defaults
- Confidence gate → halt mechanism
- Examine block tracking
- Two MCP tools: `imperatus` + `imperatus_manifest`
- StdioServerTransport

**Stubs / Missing:**
- `[marshal]` — doesn't build constellation, bombs, tools, or activation matrix
- `[ground]` — doesn't parse objectives or mission brief structured data
- `[examine]` — tracks blocks but returns no Armatura guidance
- Formation templates — names only, no config content
- No StreamableHTTP transport (exists in `server.ts` for lotus-wisdom)
- No session management for HTTP mode
- No budget estimation
- No tests
- Build untested

---

### Task 1: Add Test Framework

**Files:**
- Modify: `$MCP/package.json`
- Create: `$MCP/vitest.config.ts`
- Create: `$MCP/tests/imperatus-server.test.ts`

**Step 1: Install vitest**

```bash
cd "$MCP" && npm install --save-dev vitest
```

**Step 2: Create vitest config**

Create `$MCP/vitest.config.ts`:

```typescript
import { defineConfig } from 'vitest/config';

export default defineConfig({
  test: {
    globals: true,
    environment: 'node',
  },
});
```

**Step 3: Add test script to package.json**

In `$MCP/package.json`, add to `"scripts"`:

```json
"test": "vitest run",
"test:watch": "vitest"
```

**Step 4: Write first smoke test**

Create `$MCP/tests/imperatus-server.test.ts`:

```typescript
import { describe, it, expect } from 'vitest';

// We'll import ImperatusServer once it's exported
// For now, validate the test framework works
describe('Imperatus MCP Server', () => {
  it('test framework operational', () => {
    expect(true).toBe(true);
  });
});
```

**Step 5: Run test to verify framework works**

Run: `cd "$MCP" && npx vitest run`
Expected: 1 test PASS

**Step 6: Commit**

```bash
cd "$MCP" && git add vitest.config.ts tests/ package.json package-lock.json
git commit -m "chore: add vitest test framework"
```

---

### Task 2: Export ImperatusServer for Testing

**Files:**
- Modify: `$MCP/index.ts`
- Modify: `$MCP/tests/imperatus-server.test.ts`

**Step 1: Write the failing test**

Update `$MCP/tests/imperatus-server.test.ts`:

```typescript
import { describe, it, expect, beforeEach } from 'vitest';
import { ImperatusServer } from '../index.js';

describe('ImperatusServer', () => {
  let server: ImperatusServer;

  beforeEach(() => {
    server = new ImperatusServer();
  });

  it('should instantiate', () => {
    expect(server).toBeDefined();
  });

  it('[begin] returns FRAMEWORK_RECEIVED', () => {
    const result = server.processStep({
      tag: 'begin',
      content: 'Test query',
      stepNumber: 1,
      totalSteps: 6,
      nextStepNeeded: true,
    });
    const data = JSON.parse(result.content[0].text);
    expect(data.status).toBe('FRAMEWORK_RECEIVED');
    expect(data.command_domains).toBeDefined();
    expect(data.scoring).toBeDefined();
  });
});
```

**Step 2: Run test to verify it fails**

Run: `cd "$MCP" && npx vitest run`
Expected: FAIL — `ImperatusServer` not exported

**Step 3: Export the class**

In `$MCP/index.ts`, add `export` keyword to the class declaration (line ~152):

```typescript
export class ImperatusServer {
```

Also export key types and constants needed for testing. Add before the class:

```typescript
export { CORE_TAGS, COMMAND_DOMAINS, EXAMINE_BLOCKS, VELITES_DEFAULTS };
export type { ImperatusStepData, Manifest, RKQDE, CombatMode, Formation };
```

Guard the server bootstrap so it doesn't run during tests. Replace the bottom of the file (lines ~788-821) with:

```typescript
// Only bootstrap when run directly (not imported for tests)
const isDirectRun = process.argv[1]?.includes('index');
if (isDirectRun) {
  const server = new Server(
    { name: "imperatus-server", version: "1.0.0" },
    { capabilities: { tools: {} } }
  );

  const imperatus = new ImperatusServer();

  server.setRequestHandler(ListToolsRequestSchema, async () => ({
    tools: [IMPERATUS_TOOL, MANIFEST_TOOL],
  }));

  server.setRequestHandler(CallToolRequestSchema, async (request: any) => {
    if (request.params.name === "imperatus") {
      return imperatus.processStep(request.params.arguments);
    } else if (request.params.name === "imperatus_manifest") {
      return imperatus.getManifestSummary();
    }
    return {
      content: [{ type: "text", text: `Unknown tool: ${request.params.name}` }],
      isError: true
    };
  });

  async function runServer() {
    const transport = new StdioServerTransport();
    await server.connect(transport);
    console.error("Imperatus MCP Server v1.0.0 — LEGIO Command Engine running");
  }

  runServer().catch((error) => {
    console.error("Fatal error:", error);
    process.exit(1);
  });
}
```

**Step 4: Run tests to verify they pass**

Run: `cd "$MCP" && npx vitest run`
Expected: 2 tests PASS

**Step 5: Commit**

```bash
cd "$MCP" && git add index.ts tests/imperatus-server.test.ts
git commit -m "refactor: export ImperatusServer for testing"
```

---

### Task 3: Test + Complete Phase Ordering

**Files:**
- Modify: `$MCP/tests/imperatus-server.test.ts`
- Verify: `$MCP/index.ts` (existing logic)

**Step 1: Write failing tests for phase ordering**

Add to test file:

```typescript
describe('Phase Ordering', () => {
  let server: ImperatusServer;

  beforeEach(() => {
    server = new ImperatusServer();
  });

  it('rejects [ground] without [begin]', () => {
    const result = server.processStep({
      tag: 'ground',
      content: 'R=5 K=3 Q=6 D=4 E=3',
      stepNumber: 1,
      totalSteps: 6,
      nextStepNeeded: true,
    });
    const data = JSON.parse(result.content[0].text);
    expect(data.error).toContain('Phase violation');
  });

  it('allows [ground] after [begin]', () => {
    server.processStep({ tag: 'begin', content: 'init', stepNumber: 1, totalSteps: 6, nextStepNeeded: true });
    const result = server.processStep({
      tag: 'ground',
      content: 'R=5 K=3 Q=6 D=4 E=3',
      stepNumber: 2,
      totalSteps: 6,
      nextStepNeeded: true,
    });
    const data = JSON.parse(result.content[0].text);
    expect(data.status).toBe('processing');
  });

  it('rejects [examine] without [ground]', () => {
    server.processStep({ tag: 'begin', content: 'init', stepNumber: 1, totalSteps: 6, nextStepNeeded: true });
    const result = server.processStep({
      tag: 'examine',
      content: 'ARQ test',
      stepNumber: 2,
      totalSteps: 6,
      nextStepNeeded: true,
    });
    const data = JSON.parse(result.content[0].text);
    expect(data.error).toContain('Phase violation');
  });

  it('Velites fast path: [ground] → [route] skipping [examine]', () => {
    server.processStep({ tag: 'begin', content: 'init', stepNumber: 1, totalSteps: 4, nextStepNeeded: true });
    server.processStep({ tag: 'ground', content: 'R=2 K=2 Q=3 D=1 E=1', stepNumber: 2, totalSteps: 4, nextStepNeeded: true });
    const result = server.processStep({
      tag: 'route',
      content: 'Velites fast path',
      stepNumber: 3,
      totalSteps: 4,
      nextStepNeeded: true,
    });
    const data = JSON.parse(result.content[0].text);
    expect(data.status).toBe('processing');
    expect(data.routing.mode).toBe('Velites');
  });

  it('[adapt] rejected before [issue]', () => {
    server.processStep({ tag: 'begin', content: 'init', stepNumber: 1, totalSteps: 6, nextStepNeeded: true });
    const result = server.processStep({
      tag: 'adapt',
      content: 'try adapt early',
      stepNumber: 2,
      totalSteps: 6,
      nextStepNeeded: true,
    });
    const data = JSON.parse(result.content[0].text);
    expect(data.error).toBeDefined();
  });

  it('halt blocks forward progress', () => {
    server.processStep({ tag: 'begin', content: 'init', stepNumber: 1, totalSteps: 8, nextStepNeeded: true });
    server.processStep({ tag: 'ground', content: 'R=7 K=6 Q=8 D=5 E=4', stepNumber: 2, totalSteps: 8, nextStepNeeded: true });
    // Examine with low confidence triggers halt
    server.processStep({
      tag: 'examine', content: 'ARQ_GATES: Pre+Post|hard', stepNumber: 3, totalSteps: 8,
      nextStepNeeded: true, examineBlock: 'ARQ_GATES', confidenceScore: 6,
    });
    // Now try to route — should be blocked
    const result = server.processStep({
      tag: 'route', content: 'try routing', stepNumber: 4, totalSteps: 8, nextStepNeeded: true,
    });
    const data = JSON.parse(result.content[0].text);
    expect(data.error).toContain('HALTED');
  });

  it('[reconsider] clears halt', () => {
    server.processStep({ tag: 'begin', content: 'init', stepNumber: 1, totalSteps: 8, nextStepNeeded: true });
    server.processStep({ tag: 'ground', content: 'R=7 K=6 Q=8 D=5 E=4', stepNumber: 2, totalSteps: 8, nextStepNeeded: true });
    server.processStep({
      tag: 'examine', content: 'ARQ_GATES: Pre+Post|hard', stepNumber: 3, totalSteps: 8,
      nextStepNeeded: true, examineBlock: 'ARQ_GATES', confidenceScore: 6,
    });
    // Reconsider
    const result = server.processStep({
      tag: 'reconsider', content: 'Revised ARQ to Pre|standard', stepNumber: 4, totalSteps: 8,
      nextStepNeeded: true, examineBlock: 'ARQ_GATES',
    });
    const data = JSON.parse(result.content[0].text);
    expect(data.status).toBe('processing');
    // Now route should work
    const route = server.processStep({
      tag: 'route', content: 'routing after reconsider', stepNumber: 5, totalSteps: 8, nextStepNeeded: true,
    });
    const routeData = JSON.parse(route.content[0].text);
    expect(routeData.status).toBe('processing');
  });
});
```

**Step 2: Run tests to verify they pass (existing logic should handle all cases)**

Run: `cd "$MCP" && npx vitest run`
Expected: All PASS (these test existing functionality)

**Step 3: Fix any failures, then commit**

```bash
cd "$MCP" && git add tests/imperatus-server.test.ts
git commit -m "test: add phase ordering + halt/reconsider tests"
```

---

### Task 4: Formation Templates

**Files:**
- Modify: `$MCP/index.ts` (add FORMATION_TEMPLATES constant, update [route] handler)
- Modify: `$MCP/tests/imperatus-server.test.ts`

**Step 1: Write the failing test**

```typescript
describe('Formation Templates', () => {
  let server: ImperatusServer;

  beforeEach(() => {
    server = new ImperatusServer();
    server.processStep({ tag: 'begin', content: 'init', stepNumber: 1, totalSteps: 6, nextStepNeeded: true });
  });

  it('Testudo selected for K>=8', () => {
    server.processStep({ tag: 'ground', content: 'R=6 K=9 Q=7 D=4 E=5', stepNumber: 2, totalSteps: 6, nextStepNeeded: true });
    const result = server.processStep({ tag: 'route', content: 'route', stepNumber: 3, totalSteps: 6, nextStepNeeded: true });
    const data = JSON.parse(result.content[0].text);
    expect(data.routing.formation).toBe('Testudo');
    expect(data.formationTemplate).toBeDefined();
    expect(data.formationTemplate.name).toBe('Testudo');
    expect(data.formationTemplate.priority).toBeDefined();
  });

  it('Orbis selected for D>=7', () => {
    server.processStep({ tag: 'ground', content: 'R=5 K=4 Q=6 D=8 E=5', stepNumber: 2, totalSteps: 6, nextStepNeeded: true });
    const result = server.processStep({ tag: 'route', content: 'route', stepNumber: 3, totalSteps: 6, nextStepNeeded: true });
    const data = JSON.parse(result.content[0].text);
    expect(data.routing.formation).toBe('Orbis');
  });

  it('Cuneus selected for R<=3 and Q<=5', () => {
    server.processStep({ tag: 'ground', content: 'R=2 K=2 Q=4 D=2 E=1', stepNumber: 2, totalSteps: 6, nextStepNeeded: true });
    const result = server.processStep({ tag: 'route', content: 'route', stepNumber: 3, totalSteps: 6, nextStepNeeded: true });
    const data = JSON.parse(result.content[0].text);
    expect(data.routing.formation).toBe('Cuneus');
  });

  it('Triplex is default', () => {
    server.processStep({ tag: 'ground', content: 'R=5 K=4 Q=6 D=4 E=3', stepNumber: 2, totalSteps: 6, nextStepNeeded: true });
    const result = server.processStep({ tag: 'route', content: 'route', stepNumber: 3, totalSteps: 6, nextStepNeeded: true });
    const data = JSON.parse(result.content[0].text);
    expect(data.routing.formation).toBe('Triplex');
  });
});
```

**Step 2: Run test to verify it fails**

Run: `cd "$MCP" && npx vitest run`
Expected: FAIL — `formationTemplate` not in response

**Step 3: Add formation templates constant**

In `$MCP/index.ts`, after `VELITES_DEFAULTS`, add:

```typescript
interface FormationTemplate {
  name: Formation;
  description: string;
  priority: string;
  expert_arrangement: string;
  reasoning_pattern: string;
  bomb_strategy: string;
  best_for: string[];
}

const FORMATION_TEMPLATES: Record<Formation, FormationTemplate> = {
  Testudo: {
    name: 'Testudo',
    description: 'Tortoise formation — maximum protection. Shields on all sides. Slow but impenetrable.',
    priority: 'accuracy > speed > breadth',
    expert_arrangement: 'Ring defense: every expert cross-validates. No single point of failure.',
    reasoning_pattern: 'FCoT with full ARQ gates. Every claim verified before advancing.',
    bomb_strategy: 'EVIDENCE bombs at every assertion. CLARIFIER bombs at ambiguity points.',
    best_for: ['high-stakes research', 'knowledge-risk queries (K>=8)', 'regulatory/legal', 'medical/financial'],
  },
  Triplex: {
    name: 'Triplex',
    description: 'Triple line — standard analytical workhorse. Three waves: survey, engage, refine.',
    priority: 'balance(speed, accuracy, breadth)',
    expert_arrangement: 'Sequential waves: scouts (survey) → infantry (produce) → veterans (refine).',
    reasoning_pattern: 'FCoT primary. CoC for sub-problems. Baton handoff between waves.',
    bomb_strategy: 'ANCHOR at phase transitions. CONTINUITY at expert handoffs. SCAFFOLD at iteration boundaries.',
    best_for: ['standard analysis', 'multi-step tasks', 'default formation when no strong signal'],
  },
  Cuneus: {
    name: 'Cuneus',
    description: 'Wedge formation — fast penetration. Single point of attack, maximum velocity.',
    priority: 'speed > accuracy > breadth',
    expert_arrangement: 'Single lead expert, minimal support. Direct generation.',
    reasoning_pattern: 'CoC only. Direct path. No iteration.',
    bomb_strategy: 'CLARIFIER only if ambiguity detected. Minimal bomb deployment.',
    best_for: ['quick tasks (R<=3)', 'low-quality-bar (Q<=5)', 'factual recall', 'simple generation'],
  },
  Orbis: {
    name: 'Orbis',
    description: 'Circle formation — 360-degree coverage. Every direction watched. For complex, surrounded problems.',
    priority: 'breadth > accuracy > speed',
    expert_arrangement: 'All experts face outward covering different domains. Junction merges at center.',
    reasoning_pattern: 'Swarm parallel processing. Each expert works independently, junction synthesizes.',
    bomb_strategy: 'BRIDGE bombs between every domain pair. CONTINUITY at every junction point.',
    best_for: ['multi-domain problems (D>=7)', 'cross-functional', 'novel synthesis', 'architecture decisions'],
  },
};
```

**Step 4: Update [route] handler to include template**

In `handleRoute()`, add `formationTemplate` to the response. After the routing is set, add to the `this.respond()` call:

```typescript
formationTemplate: FORMATION_TEMPLATES[formation],
```

**Step 5: Run tests to verify they pass**

Run: `cd "$MCP" && npx vitest run`
Expected: All PASS

**Step 6: Commit**

```bash
cd "$MCP" && git add index.ts tests/imperatus-server.test.ts
git commit -m "feat: add formation templates with content (Testudo/Triplex/Cuneus/Orbis)"
```

---

### Task 5: Armatura Examine Content Injection

**Files:**
- Modify: `$MCP/index.ts` (update [examine] handler)
- Modify: `$MCP/tests/imperatus-server.test.ts`

**Step 1: Write the failing test**

```typescript
describe('Examine — Armatura Content', () => {
  let server: ImperatusServer;

  beforeEach(() => {
    server = new ImperatusServer();
    server.processStep({ tag: 'begin', content: 'init', stepNumber: 1, totalSteps: 10, nextStepNeeded: true });
    server.processStep({ tag: 'ground', content: 'R=7 K=6 Q=8 D=5 E=4', stepNumber: 2, totalSteps: 10, nextStepNeeded: true });
  });

  it('returns guidance for ARQ_GATES block', () => {
    const result = server.processStep({
      tag: 'examine', content: 'Setting ARQ gates', stepNumber: 3, totalSteps: 10,
      nextStepNeeded: true, examineBlock: 'ARQ_GATES',
    });
    const data = JSON.parse(result.content[0].text);
    expect(data.armatura_guidance).toBeDefined();
    expect(data.armatura_guidance.contemplate).toBeDefined();
    expect(data.armatura_guidance.levels).toBeDefined();
  });

  it('returns guidance for MR_RUG_EXPERTS block', () => {
    const result = server.processStep({
      tag: 'examine', content: 'Setting expert count', stepNumber: 3, totalSteps: 10,
      nextStepNeeded: true, examineBlock: 'MR_RUG_EXPERTS',
    });
    const data = JSON.parse(result.content[0].text);
    expect(data.armatura_guidance).toBeDefined();
    expect(data.armatura_guidance.contemplate).toContain('specialist');
  });

  it('suggests constraint level based on RKQDE', () => {
    const result = server.processStep({
      tag: 'examine', content: 'Setting ARQ gates', stepNumber: 3, totalSteps: 10,
      nextStepNeeded: true, examineBlock: 'ARQ_GATES',
    });
    const data = JSON.parse(result.content[0].text);
    // R=7 → Principes range → should suggest Pre+Post|hard
    expect(data.armatura_guidance.suggested_level).toBeDefined();
  });
});
```

**Step 2: Run test to verify it fails**

Run: `cd "$MCP" && npx vitest run`
Expected: FAIL — `armatura_guidance` not in response

**Step 3: Add Armatura guidance content**

In `$MCP/index.ts`, add the Armatura guidance map after `FORMATION_TEMPLATES`:

```typescript
interface ArmaturGuidance {
  contemplate: string;
  levels: Record<CombatMode, string>;
  set_format: string;
}

const ARMATURA_GUIDANCE: Record<string, ArmaturGuidance> = {
  BUFFER_VALET: {
    contemplate: 'What memory depth does this query need?',
    levels: { Velites: 'Read', Hastati: 'Read', Principes: 'Read + Save Tier 2', Triarii: 'Read + Save Tier 1' },
    set_format: 'Memory depth = [Read / Read+Save-2 / Read+Save-1]',
  },
  SUCCESS_CRITERIA_LOCK: {
    contemplate: 'How rigid do victory conditions need to be?',
    levels: { Velites: 'Implicit (1-2 conditions)', Hastati: 'Type Check (2-3 stated)', Principes: 'Signature Lock (3-5, immutable)', Triarii: 'Multi-Constraint Lock (5+)' },
    set_format: 'Lock rigidity = [Implicit / Type / Signature / Multi], Criteria count = [N]',
  },
  ARQ_GATES: {
    contemplate: 'How strict do quality gates need to be? Where are the failure points?',
    levels: { Velites: 'Pre-Turn|light', Hastati: 'Pre-Turn|standard', Principes: 'Pre+Post|hard', Triarii: 'Full(Pre+During+Post)|HALT-on-fail' },
    set_format: 'Coverage = [Pre / Pre+Post / Full], Strictness = [light / standard / hard / HALT]',
  },
  ANTI_LAZY: {
    contemplate: 'How likely is the model to shortcut this output?',
    levels: { Velites: 'Advisory', Hastati: 'Required (no placeholders)', Principes: 'Required (complete output)', Triarii: 'Enforced (truncation = restart)' },
    set_format: 'Enforcement = [Advisory / Required / Enforced]',
  },
  USC_CANDIDATES: {
    contemplate: 'How many valid approaches exist in the solution space?',
    levels: { Velites: '1-path sanity check', Hastati: '2 candidates', Principes: '3 candidates', Triarii: '5 candidates + meta-synthesis' },
    set_format: 'Candidate count = [1 / 2 / 3 / 5+meta]',
  },
  MR_RUG_EXPERTS: {
    contemplate: 'How many domains need specialist coverage? What formation fits the domain shape?',
    levels: { Velites: '0 experts (basic retrieval)', Hastati: '3 specialists', Principes: '5 specialists', Triarii: '5-8 specialists + deep semantic embedding' },
    set_format: 'Expert count = [0 / 3 / 5 / 5-8], Formation = [Testudo / Triplex / Cuneus / Orbis]',
  },
  SKELETRAIN_SCALE: {
    contemplate: 'How many execution nodes does the task need? Linear or branching?',
    levels: { Velites: 'Direct path', Hastati: 'Light (3-5 nodes)', Principes: 'Full (5-10 nodes)', Triarii: 'GoT if D>=6, else Deep (10+ nodes)' },
    set_format: 'Scale = [Direct / Light / Full / GoT], Estimated nodes = [N]',
  },
  PROMPT_BOMBS: {
    contemplate: 'How many confusion points will execution hit?',
    levels: { Velites: 'Clarifier only (0-1)', Hastati: 'Clarifier+Scaffold (2-3)', Principes: 'Full Arsenal+Registry (4-6)', Triarii: 'Deep Injection (6+, continuous)' },
    set_format: 'Arsenal = [Clarifier / Scaffold / Full / Deep], Count = [N]',
  },
  REASONING_STYLES: {
    contemplate: 'What reasoning approach matches the problem shape?',
    levels: { Velites: 'CoC only', Hastati: 'FCoT', Principes: 'FCoT + ARQ validation', Triarii: 'Mix (CoC+FCoT) + ARQ' },
    set_format: 'Style = [CoC / FCoT / FCoT+ARQ / Mix+ARQ]',
  },
  ITERATION_COUNT: {
    contemplate: 'How many passes will produce the right quality? Diminishing returns after 3.',
    levels: { Velites: '1-shot', Hastati: '1 pass (optional 2nd)', Principes: '3 passes (ADAPT protocol)', Triarii: '3 passes (kTTT protocol)' },
    set_format: 'Count = [1 / 2 / 3], Protocol = [single / ADAPT / kTTT]',
  },
  EXECUTION_PATTERN: {
    contemplate: 'Sequential or parallel? How do experts hand off?',
    levels: { Velites: 'Direct generation', Hastati: 'Baton (sequential handoff)', Principes: 'Baton + ARQ at handoffs', Triarii: 'Swarm (parallel) + ARQ + junction merge' },
    set_format: 'Pattern = [Direct / Baton / Baton+ARQ / Swarm+ARQ]',
  },
  CoVE_DEPTH: {
    contemplate: 'How many verification variants are needed?',
    levels: { Velites: 'Minimum (spot check)', Hastati: 'Top-1 variant verified', Principes: 'Top-2 variants verified', Triarii: 'All variants + multi-model verification' },
    set_format: 'Depth = [Minimum / Top-1 / Top-2 / All+Multi]',
  },
  GAP_SCAN_DEPTH: {
    contemplate: 'How thorough should the post-generation scan be?',
    levels: { Velites: 'Minimum', Hastati: 'Light scan', Principes: '3-branch scan', Triarii: 'Deep scan + auto-fix' },
    set_format: 'Depth = [Minimum / Light / 3-Branch / Deep+AutoFix]',
  },
  CURATION_DENSITY: {
    contemplate: 'What signal-to-noise ratio does the output need?',
    levels: { Velites: 'Lean (essentials only)', Hastati: 'Normal', Principes: 'Normal + nuance', Triarii: 'All-out (maximum signal)' },
    set_format: 'Density = [Lean / Normal / Normal+Nuance / All-Out]',
  },
  SELF_REFLECT_DEPTH: {
    contemplate: 'How much meta-learning should happen after execution?',
    levels: { Velites: 'Minimum', Hastati: 'Note (log what worked)', Principes: 'Audit (formal review)', Triarii: 'Full audit + Buffer-of-Thought update' },
    set_format: 'Depth = [Minimum / Note / Audit / Full+BoT]',
  },
  OUTPUT_FORMAT: {
    contemplate: 'What shape should the final output take?',
    levels: { Velites: 'Narrative', Hastati: 'Narrative', Principes: 'MLDoE (structured)', Triarii: 'CEP carry-packet (compressed)' },
    set_format: 'Format = [Narrative / MLDoE / CEP]',
  },
};

function suggestConstraintLevel(block: ExamineBlock, assessment: RKQDE | undefined): string {
  if (!assessment) return 'Assessment unavailable — set manually';
  const { sigma, danger } = assessment;
  let mode: CombatMode;
  if (sigma <= 12 && danger <= 5) mode = 'Velites';
  else if (sigma <= 25 || danger <= 7) mode = 'Hastati';
  else if (sigma <= 38 || danger <= 8) mode = 'Principes';
  else mode = 'Triarii';
  const guidance = ARMATURA_GUIDANCE[block];
  return guidance ? `${guidance.levels[mode]} (suggested for ${mode})` : 'No guidance available';
}
```

**Step 4: Update [examine] handler to return guidance**

In `handleExamine()`, add `armatura_guidance` to the response. Before the `return this.respond({...})`, build the guidance:

```typescript
const guidance = block ? ARMATURA_GUIDANCE[block] : undefined;
const suggestedLevel = block ? suggestConstraintLevel(block as ExamineBlock, this.manifest.assessment) : undefined;
```

Then add to the response object:

```typescript
armatura_guidance: guidance ? {
  contemplate: guidance.contemplate,
  levels: guidance.levels,
  set_format: guidance.set_format,
  suggested_level: suggestedLevel,
} : undefined,
```

**Step 5: Run tests to verify they pass**

Run: `cd "$MCP" && npx vitest run`
Expected: All PASS

**Step 6: Commit**

```bash
cd "$MCP" && git add index.ts tests/imperatus-server.test.ts
git commit -m "feat: add Armatura guidance injection to [examine] handler"
```

---

### Task 6: Complete [marshal] — Activation Matrix

**Files:**
- Modify: `$MCP/index.ts`
- Modify: `$MCP/tests/imperatus-server.test.ts`

**Step 1: Write the failing test**

```typescript
describe('Marshal — Activation Matrix', () => {
  let server: ImperatusServer;

  function runToMarshal(rkqde: string, mode?: string) {
    server = new ImperatusServer();
    server.processStep({ tag: 'begin', content: 'init', stepNumber: 1, totalSteps: 6, nextStepNeeded: true });
    server.processStep({ tag: 'ground', content: rkqde, stepNumber: 2, totalSteps: 6, nextStepNeeded: true });
    server.processStep({ tag: 'route', content: mode || 'route', stepNumber: 3, totalSteps: 6, nextStepNeeded: true });
    return server.processStep({ tag: 'marshal', content: 'Assemble manifest', stepNumber: 4, totalSteps: 6, nextStepNeeded: true });
  }

  it('generates 18-step activation matrix', () => {
    const result = runToMarshal('R=6 K=5 Q=7 D=4 E=3');
    const data = JSON.parse(result.content[0].text);
    expect(data.activation_matrix).toBeDefined();
    expect(data.activation_matrix.length).toBe(18);
  });

  it('Velites skips 7 optional steps', () => {
    const result = runToMarshal('R=2 K=2 Q=3 D=1 E=1');
    const data = JSON.parse(result.content[0].text);
    const skipped = data.activation_matrix.filter((s: any) => s.status === 'X');
    expect(skipped.length).toBeGreaterThanOrEqual(5);
  });

  it('Triarii activates all steps', () => {
    const result = runToMarshal('R=9 K=9 Q=9 D=8 E=8');
    const data = JSON.parse(result.content[0].text);
    const required = data.activation_matrix.filter((s: any) => s.status === 'R');
    expect(required.length).toBeGreaterThanOrEqual(16);
  });
});
```

**Step 2: Run test to verify it fails**

Run: `cd "$MCP" && npx vitest run`
Expected: FAIL — `activation_matrix` not in response

**Step 3: Add activation matrix builder**

In `$MCP/index.ts`, add before the ImperatusServer class:

```typescript
interface ActivationStep {
  step: number;
  name: string;
  status: 'R' | 'O' | 'X';  // Required | Optional | Off
  detail: string;
}

const PIPELINE_STEPS = [
  { num: 1,  name: 'Buffer Valet' },
  { num: 2,  name: 'Success Criteria Lock' },
  { num: 3,  name: 'ARQ' },
  { num: 4,  name: 'Anti-Lazy Protocol' },
  { num: 5,  name: 'USC' },
  { num: 6,  name: 'Confidence Gate' },
  { num: 7,  name: 'MR.RUG' },
  { num: 8,  name: 'SkeleTraIn-OT' },
  { num: 9,  name: 'Prompt Bombs' },
  { num: 10, name: 'FCoT / CoC' },
  { num: 11, name: 'Iteration Protocol' },
  { num: 12, name: 'Swarm / Baton' },
  { num: 13, name: 'CoVE' },
  { num: 14, name: 'PGScan' },
  { num: 15, name: 'Intelligent Curation' },
  { num: 16, name: 'Self-Reflect-Adapt' },
  { num: 17, name: 'Iteration Output' },
  { num: 18, name: 'MEM / CEP' },
] as const;

// From LEGIO-00 spec — activation matrix per mode
const ACTIVATION_MATRIX: Record<CombatMode, Record<number, { status: 'R' | 'O' | 'X'; detail: string }>> = {
  Velites: {
    1:  { status: 'R', detail: 'Read' },
    2:  { status: 'R', detail: 'Implicit' },
    3:  { status: 'R', detail: 'Pre|light' },
    4:  { status: 'O', detail: 'Advisory' },
    5:  { status: 'R', detail: '1-path' },
    6:  { status: 'R', detail: 'Required' },
    7:  { status: 'O', detail: 'Basic' },
    8:  { status: 'O', detail: 'Direct' },
    9:  { status: 'O', detail: 'Clarifier' },
    10: { status: 'R', detail: 'CoC' },
    11: { status: 'X', detail: 'Skipped' },
    12: { status: 'R', detail: 'Direct' },
    13: { status: 'X', detail: 'Skipped' },
    14: { status: 'X', detail: 'Skipped' },
    15: { status: 'R', detail: 'Lean' },
    16: { status: 'X', detail: 'Skipped' },
    17: { status: 'R', detail: 'Required' },
    18: { status: 'X', detail: 'Skipped' },
  },
  Hastati: {
    1:  { status: 'R', detail: 'Read' },
    2:  { status: 'R', detail: 'Type Check' },
    3:  { status: 'R', detail: 'Pre|standard' },
    4:  { status: 'R', detail: 'Required' },
    5:  { status: 'R', detail: '2 candidates' },
    6:  { status: 'R', detail: 'Required' },
    7:  { status: 'R', detail: 'Specialist' },
    8:  { status: 'R', detail: 'Light' },
    9:  { status: 'R', detail: 'Clarifier+Scaffold' },
    10: { status: 'R', detail: 'FCoT' },
    11: { status: 'O', detail: 'Optional 2nd' },
    12: { status: 'R', detail: 'Baton' },
    13: { status: 'R', detail: '1 variant' },
    14: { status: 'O', detail: 'Light' },
    15: { status: 'R', detail: 'Normal' },
    16: { status: 'O', detail: 'Note' },
    17: { status: 'R', detail: 'Required' },
    18: { status: 'X', detail: 'Skipped' },
  },
  Principes: {
    1:  { status: 'R', detail: 'Read+Save-2' },
    2:  { status: 'R', detail: 'Signature Lock' },
    3:  { status: 'R', detail: 'Pre+Post|hard' },
    4:  { status: 'R', detail: 'Required' },
    5:  { status: 'R', detail: '3 candidates' },
    6:  { status: 'R', detail: 'Required' },
    7:  { status: 'R', detail: 'Full' },
    8:  { status: 'R', detail: 'Full' },
    9:  { status: 'R', detail: 'Full Arsenal' },
    10: { status: 'R', detail: 'FCoT+ARQ' },
    11: { status: 'R', detail: '3 passes' },
    12: { status: 'R', detail: 'Baton+ARQ' },
    13: { status: 'R', detail: '2 variants' },
    14: { status: 'R', detail: '3-branch' },
    15: { status: 'R', detail: 'Normal+Nuance' },
    16: { status: 'R', detail: 'Audit' },
    17: { status: 'R', detail: 'Required' },
    18: { status: 'O', detail: 'Optional' },
  },
  Triarii: {
    1:  { status: 'R', detail: 'Read+Save-1' },
    2:  { status: 'R', detail: 'Multi-Constraint' },
    3:  { status: 'R', detail: 'Full|HALT' },
    4:  { status: 'R', detail: 'Enforced' },
    5:  { status: 'R', detail: '5+ candidates' },
    6:  { status: 'R', detail: 'Required' },
    7:  { status: 'R', detail: 'Deep' },
    8:  { status: 'R', detail: 'GoT' },
    9:  { status: 'R', detail: 'Deep Injection' },
    10: { status: 'R', detail: 'Mix+ARQ' },
    11: { status: 'R', detail: '3 passes kTTT' },
    12: { status: 'R', detail: 'Swarm+ARQ' },
    13: { status: 'R', detail: 'All+Multi' },
    14: { status: 'R', detail: 'Deep+AutoFix' },
    15: { status: 'R', detail: 'All-Out' },
    16: { status: 'R', detail: 'Full+BoT' },
    17: { status: 'R', detail: 'Required' },
    18: { status: 'R', detail: 'Required' },
  },
};

function buildActivationMatrix(mode: CombatMode): ActivationStep[] {
  const matrix = ACTIVATION_MATRIX[mode];
  return PIPELINE_STEPS.map(step => ({
    step: step.num,
    name: step.name,
    status: matrix[step.num].status,
    detail: matrix[step.num].detail,
  }));
}
```

**Step 4: Update [marshal] handler to include activation matrix**

In `handleMarshal()`, replace the response with:

```typescript
private handleMarshal(step: ImperatusStepData) {
  if (step.content && !this.manifest.mission) {
    this.manifest.mission = {
      brief: step.content.substring(0, 500),
      objectives: { complete_when: [], reject_if: [] }
    };
  }

  const mode = this.manifest.routing?.mode || 'Hastati';
  const activationMatrix = buildActivationMatrix(mode);

  const activeCount = activationMatrix.filter(s => s.status === 'R').length;
  const optionalCount = activationMatrix.filter(s => s.status === 'O').length;
  const skippedCount = activationMatrix.filter(s => s.status === 'X').length;

  this.manifest.steps_active = activeCount + optionalCount;
  this.manifest.steps_skipped = activationMatrix.filter(s => s.status === 'X').map(s => s.name);

  return this.respond({
    status: 'processing',
    currentStep: 'marshal',
    commandDomain: 'authority',
    activation_matrix: activationMatrix,
    manifest_preview: {
      assessment: this.manifest.assessment,
      routing: this.manifest.routing,
      constraints_count: Object.keys(this.manifest.constraints).length,
      steps_required: activeCount,
      steps_optional: optionalCount,
      steps_skipped: skippedCount,
    },
    instruction: 'Manifest assembled. Review activation matrix and proceed to [issue] to seal.',
    journey: this.getTagJourney(),
    domainJourney: this.getDomainJourney(),
    stepNumber: step.stepNumber,
    totalSteps: step.totalSteps,
    nextStepNeeded: step.nextStepNeeded,
  });
}
```

**Step 5: Run tests to verify they pass**

Run: `cd "$MCP" && npx vitest run`
Expected: All PASS

**Step 6: Commit**

```bash
cd "$MCP" && git add index.ts tests/imperatus-server.test.ts
git commit -m "feat: add 18-step activation matrix to [marshal] handler"
```

---

### Task 7: Complete [issue] — Full Manifest Seal

**Files:**
- Modify: `$MCP/index.ts`
- Modify: `$MCP/tests/imperatus-server.test.ts`

**Step 1: Write the failing test**

```typescript
describe('Issue — Full Manifest', () => {
  it('produces complete sealed manifest', () => {
    const server = new ImperatusServer();
    server.processStep({ tag: 'begin', content: 'init', stepNumber: 1, totalSteps: 6, nextStepNeeded: true });
    server.processStep({ tag: 'ground', content: 'R=6 K=5 Q=7 D=4 E=3', stepNumber: 2, totalSteps: 6, nextStepNeeded: true });
    server.processStep({ tag: 'route', content: 'route', stepNumber: 3, totalSteps: 6, nextStepNeeded: true });
    server.processStep({ tag: 'marshal', content: 'Build a REST API for user management', stepNumber: 4, totalSteps: 6, nextStepNeeded: true });

    const result = server.processStep({
      tag: 'issue', content: 'Seal manifest', stepNumber: 5, totalSteps: 6,
      nextStepNeeded: false, confidenceScore: 9,
    });
    const data = JSON.parse(result.content[0].text);

    expect(data.status).toBe('MANIFEST_READY');
    expect(data.processComplete).toBe(true);
    expect(data.manifest).toBeDefined();
    expect(data.manifest.assessment).toBeDefined();
    expect(data.manifest.routing).toBeDefined();
    expect(data.manifest.routing.mode).toBeDefined();
    expect(data.manifest.routing.formation).toBeDefined();
    expect(data.manifest.activation_matrix).toBeDefined();
    expect(data.manifest.activation_matrix.length).toBe(18);
    expect(data.tagJourney).toContain('begin');
    expect(data.tagJourney).toContain('issue');
  });
});
```

**Step 2: Run test to verify it fails**

Run: `cd "$MCP" && npx vitest run`
Expected: FAIL — `manifest.activation_matrix` not in sealed manifest

**Step 3: Update [issue] handler**

In `handleIssue()`, build the full manifest with activation matrix:

```typescript
private handleIssue(step: ImperatusStepData) {
  this.issued = true;
  this.manifest.confidence = step.confidenceScore || 8;

  const mode = this.manifest.routing?.mode || 'Hastati';
  const activationMatrix = buildActivationMatrix(mode);
  const formation = this.manifest.routing?.formation || 'Triplex';

  return this.respond({
    status: 'MANIFEST_READY',
    processComplete: true,
    finalStep: 'issue',
    instruction: 'MANIFEST_SEALED_EXECUTE',
    manifest: {
      ...this.manifest,
      activation_matrix: activationMatrix,
      formation_template: FORMATION_TEMPLATES[formation],
    },
    journeyLength: this.journey.length,
    tagJourney: this.getTagJourney(),
    domainJourney: this.getDomainJourney(),
  });
}
```

**Step 4: Run tests to verify they pass**

Run: `cd "$MCP" && npx vitest run`
Expected: All PASS

**Step 5: Commit**

```bash
cd "$MCP" && git add index.ts tests/imperatus-server.test.ts
git commit -m "feat: complete [issue] handler with full sealed manifest"
```

---

### Task 8: StreamableHTTP Transport + Session Management

**Files:**
- Create: `$MCP/http-server.ts`
- Modify: `$MCP/package.json` (add http start script)
- Modify: `$MCP/tests/imperatus-server.test.ts`

**Step 1: Write the failing test — session isolation**

```typescript
describe('Session Isolation', () => {
  it('separate instances have independent state', () => {
    const s1 = new ImperatusServer();
    const s2 = new ImperatusServer();

    s1.processStep({ tag: 'begin', content: 'session 1', stepNumber: 1, totalSteps: 4, nextStepNeeded: true });
    s1.processStep({ tag: 'ground', content: 'R=8 K=7 Q=9 D=6 E=5', stepNumber: 2, totalSteps: 4, nextStepNeeded: true });

    // s2 hasn't begun — should reject ground
    const result = s2.processStep({ tag: 'ground', content: 'R=2 K=2 Q=3 D=1 E=1', stepNumber: 1, totalSteps: 4, nextStepNeeded: true });
    const data = JSON.parse(result.content[0].text);
    expect(data.error).toContain('Phase violation');

    // s1 can still route
    const route = s1.processStep({ tag: 'route', content: 'route', stepNumber: 3, totalSteps: 4, nextStepNeeded: true });
    const routeData = JSON.parse(route.content[0].text);
    expect(routeData.routing.mode).toBe('Triarii');
  });
});
```

**Step 2: Run test to verify it passes (instances are already independent)**

Run: `cd "$MCP" && npx vitest run`
Expected: PASS (class-level state already isolated)

**Step 3: Create HTTP transport server**

Create `$MCP/http-server.ts`:

```typescript
#!/usr/bin/env node

import express from 'express';
import { randomUUID } from 'node:crypto';
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StreamableHTTPServerTransport } from "@modelcontextprotocol/sdk/server/streamableHttp.js";
import {
  CallToolRequestSchema,
  ListToolsRequestSchema,
  isInitializeRequest
} from "@modelcontextprotocol/sdk/types.js";
import { ImperatusServer, IMPERATUS_TOOL, MANIFEST_TOOL } from './index.js';

function createMCPServer(): Server {
  const mcpServer = new Server(
    { name: "imperatus-server", version: "1.0.0" },
    { capabilities: { tools: {} } }
  );

  // Each session gets its own ImperatusServer
  const imperatus = new ImperatusServer();

  mcpServer.setRequestHandler(ListToolsRequestSchema, async () => ({
    tools: [IMPERATUS_TOOL, MANIFEST_TOOL],
  }));

  mcpServer.setRequestHandler(CallToolRequestSchema, async (request: any) => {
    if (request.params.name === "imperatus") {
      return imperatus.processStep(request.params.arguments);
    } else if (request.params.name === "imperatus_manifest") {
      return imperatus.getManifestSummary();
    }
    return {
      content: [{ type: "text", text: `Unknown tool: ${request.params.name}` }],
      isError: true
    };
  });

  return mcpServer;
}

const app = express();
app.use(express.json());

const transports: Record<string, StreamableHTTPServerTransport> = {};

app.post('/mcp', async (req, res) => {
  const sessionId = req.headers['mcp-session-id'] as string | undefined;
  let transport: StreamableHTTPServerTransport;

  if (sessionId && transports[sessionId]) {
    transport = transports[sessionId];
  } else if (!sessionId && isInitializeRequest(req.body)) {
    transport = new StreamableHTTPServerTransport({
      sessionIdGenerator: () => randomUUID(),
      onsessioninitialized: (sid) => {
        transports[sid] = transport;
        console.error(`[IMPERATUS] Session initialized: ${sid}`);
      }
    });

    transport.onclose = () => {
      if (transport.sessionId) {
        console.error(`[IMPERATUS] Session closed: ${transport.sessionId}`);
        delete transports[transport.sessionId];
      }
    };

    const mcpServer = createMCPServer();
    await mcpServer.connect(transport);
  } else {
    res.status(400).json({
      jsonrpc: '2.0',
      error: { code: -32000, message: 'Bad Request: No valid session ID' },
      id: null,
    });
    return;
  }

  await transport.handleRequest(req, res, req.body);
});

app.get('/mcp', async (req, res) => {
  const sessionId = req.headers['mcp-session-id'] as string | undefined;
  if (!sessionId || !transports[sessionId]) {
    res.status(400).send('Invalid or missing session ID');
    return;
  }
  await transports[sessionId].handleRequest(req, res);
});

app.delete('/mcp', async (req, res) => {
  const sessionId = req.headers['mcp-session-id'] as string | undefined;
  if (!sessionId || !transports[sessionId]) {
    res.status(400).send('Invalid or missing session ID');
    return;
  }
  await transports[sessionId].handleRequest(req, res);
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.error(`Imperatus MCP HTTP Server v1.0.0 on port ${PORT}`);
  console.error(`Endpoint: http://localhost:${PORT}/mcp`);
});
```

**Step 4: Export IMPERATUS_TOOL and MANIFEST_TOOL from index.ts**

In `$MCP/index.ts`, add `export` to the tool constants:

```typescript
export const IMPERATUS_TOOL: Tool = {
```

```typescript
export const MANIFEST_TOOL: Tool = {
```

**Step 5: Add scripts to package.json**

Add to `"scripts"`:

```json
"start:http": "tsc && node dist/http-server.js",
"start:stdio": "tsc && node dist/index.js"
```

**Step 6: Update build script**

Update the build script in package.json:

```json
"build": "tsc && npx esbuild index.ts --bundle --platform=node --format=esm --outfile=dist/bundle.js && npx esbuild http-server.ts --bundle --platform=node --format=esm --outfile=dist/http-bundle.js"
```

**Step 7: Run tests to verify nothing broke**

Run: `cd "$MCP" && npx vitest run`
Expected: All PASS

**Step 8: Commit**

```bash
cd "$MCP" && git add http-server.ts index.ts package.json
git commit -m "feat: add StreamableHTTP transport with per-session ImperatusServer"
```

---

### Task 9: Full Journey Integration Test

**Files:**
- Modify: `$MCP/tests/imperatus-server.test.ts`

**Step 1: Write the integration test**

```typescript
describe('Full Journey — Hastati Path', () => {
  it('begin → ground → examine(4 batches) → route → marshal → issue', () => {
    const server = new ImperatusServer();

    // [begin]
    const begin = server.processStep({ tag: 'begin', content: 'init', stepNumber: 1, totalSteps: 10, nextStepNeeded: true });
    expect(JSON.parse(begin.content[0].text).status).toBe('FRAMEWORK_RECEIVED');

    // [ground]
    const ground = server.processStep({
      tag: 'ground',
      content: 'Build a REST API. R=5 K=4 Q=7 D=3 E=3. Brief: User needs CRUD endpoints for task management. Objectives: 1) All CRUD operations work, 2) Input validated, 3) Error responses consistent.',
      stepNumber: 2, totalSteps: 10, nextStepNeeded: true,
    });
    const groundData = JSON.parse(ground.content[0].text);
    expect(groundData.status).toBe('processing');
    expect(groundData.assessment).toBeDefined();

    // [examine] — batch 1: pre-flight
    for (const block of ['BUFFER_VALET', 'SUCCESS_CRITERIA_LOCK', 'ARQ_GATES', 'ANTI_LAZY', 'USC_CANDIDATES'] as const) {
      const result = server.processStep({
        tag: 'examine', content: `Setting ${block}`, stepNumber: 3, totalSteps: 10,
        nextStepNeeded: true, examineBlock: block, confidenceScore: 9,
      });
      const data = JSON.parse(result.content[0].text);
      expect(data.status).toBe('processing');
      expect(data.armatura_guidance).toBeDefined();
    }

    // [examine] — batch 2: pipeline
    for (const block of ['MR_RUG_EXPERTS', 'SKELETRAIN_SCALE', 'PROMPT_BOMBS'] as const) {
      server.processStep({
        tag: 'examine', content: `Setting ${block}`, stepNumber: 4, totalSteps: 10,
        nextStepNeeded: true, examineBlock: block, confidenceScore: 9,
      });
    }

    // [examine] — batch 3: execution
    for (const block of ['REASONING_STYLES', 'ITERATION_COUNT', 'EXECUTION_PATTERN', 'CoVE_DEPTH', 'GAP_SCAN_DEPTH'] as const) {
      server.processStep({
        tag: 'examine', content: `Setting ${block}`, stepNumber: 5, totalSteps: 10,
        nextStepNeeded: true, examineBlock: block, confidenceScore: 9,
      });
    }

    // [examine] — batch 4: output
    for (const block of ['CURATION_DENSITY', 'SELF_REFLECT_DEPTH', 'OUTPUT_FORMAT'] as const) {
      server.processStep({
        tag: 'examine', content: `Setting ${block}`, stepNumber: 6, totalSteps: 10,
        nextStepNeeded: true, examineBlock: block, confidenceScore: 9,
      });
    }

    // [route]
    const route = server.processStep({
      tag: 'route', content: 'Select mode and formation', stepNumber: 7, totalSteps: 10, nextStepNeeded: true,
    });
    const routeData = JSON.parse(route.content[0].text);
    expect(routeData.routing.mode).toBe('Hastati');
    expect(routeData.formationTemplate).toBeDefined();

    // [marshal]
    const marshal = server.processStep({
      tag: 'marshal', content: 'Build REST API for task management with CRUD', stepNumber: 8, totalSteps: 10, nextStepNeeded: true,
    });
    const marshalData = JSON.parse(marshal.content[0].text);
    expect(marshalData.activation_matrix).toBeDefined();
    expect(marshalData.activation_matrix.length).toBe(18);

    // [issue]
    const issue = server.processStep({
      tag: 'issue', content: 'Seal and execute', stepNumber: 9, totalSteps: 10,
      nextStepNeeded: false, confidenceScore: 9,
    });
    const issueData = JSON.parse(issue.content[0].text);
    expect(issueData.status).toBe('MANIFEST_READY');
    expect(issueData.processComplete).toBe(true);
    expect(issueData.manifest.routing.mode).toBe('Hastati');
    expect(issueData.manifest.activation_matrix.length).toBe(18);
    expect(issueData.tagJourney).toContain('begin');
    expect(issueData.tagJourney).toContain('issue');
  });
});

describe('Full Journey — Velites Fast Path', () => {
  it('begin → ground → route → marshal → issue (no examine)', () => {
    const server = new ImperatusServer();

    server.processStep({ tag: 'begin', content: 'init', stepNumber: 1, totalSteps: 5, nextStepNeeded: true });
    server.processStep({ tag: 'ground', content: 'What time is it? R=1 K=1 Q=2 D=1 E=1', stepNumber: 2, totalSteps: 5, nextStepNeeded: true });
    server.processStep({ tag: 'route', content: 'route', stepNumber: 3, totalSteps: 5, nextStepNeeded: true });
    server.processStep({ tag: 'marshal', content: 'Simple time query', stepNumber: 4, totalSteps: 5, nextStepNeeded: true });

    const issue = server.processStep({
      tag: 'issue', content: 'Seal', stepNumber: 5, totalSteps: 5,
      nextStepNeeded: false, confidenceScore: 10,
    });
    const data = JSON.parse(issue.content[0].text);
    expect(data.status).toBe('MANIFEST_READY');
    expect(data.manifest.routing.mode).toBe('Velites');
    // Velites should have defaults applied
    expect(data.manifest.constraints).toBeDefined();
    expect(Object.keys(data.manifest.constraints).length).toBeGreaterThan(0);
  });
});
```

**Step 2: Run tests to verify they pass**

Run: `cd "$MCP" && npx vitest run`
Expected: All PASS

**Step 3: Commit**

```bash
cd "$MCP" && git add tests/imperatus-server.test.ts
git commit -m "test: add full journey integration tests (Hastati + Velites paths)"
```

---

### Task 10: Build Verification + TypeScript Compilation

**Files:**
- Modify: `$MCP/tsconfig.json` (add http-server.ts)
- Verify: Build pipeline

**Step 1: Update tsconfig to include new files**

Verify `$MCP/tsconfig.json` `include` covers `*.ts` (it does — `"include": ["*.ts"]`). Verify `http-server.ts` compiles.

**Step 2: Run TypeScript compilation**

Run: `cd "$MCP" && npx tsc --noEmit`
Expected: No errors

**Step 3: Fix any type errors**

Address any compilation issues.

**Step 4: Run full build**

Run: `cd "$MCP" && npm run build`
Expected: `dist/bundle.js` and `dist/http-bundle.js` created

**Step 5: Run all tests one final time**

Run: `cd "$MCP" && npx vitest run`
Expected: All PASS

**Step 6: Commit**

```bash
cd "$MCP" && git add -A
git commit -m "chore: verify build pipeline — TypeScript + esbuild green"
```

---

### Task 11: Update README

**Files:**
- Modify: `$MCP/README.md`

**Step 1: Read current README**

Read `$MCP/README.md` to understand current content.

**Step 2: Update with Imperatus documentation**

Update the README to reflect Imperatus (not Lotus Wisdom), including:
- Server name and purpose
- Two transports (stdio for Claude Code, HTTP for other clients)
- Tool schema (imperatus + imperatus_manifest)
- Tag flow diagram
- Mode descriptions
- Formation templates
- Usage examples

**Step 3: Commit**

```bash
cd "$MCP" && git add README.md
git commit -m "docs: update README for Imperatus MCP server"
```

---

## Dependency Graph

```
Task 1 (test framework)
  └→ Task 2 (export for testing)
       └→ Task 3 (phase ordering tests) ←── verifies existing
       └→ Task 4 (formation templates)
       └→ Task 5 (Armatura examine content)
       └→ Task 6 (activation matrix)
            └→ Task 7 (full [issue] manifest)
                 └→ Task 9 (integration tests)
       └→ Task 8 (HTTP transport)
  Task 10 (build verification) ←── depends on all code tasks
  Task 11 (README) ←── depends on all feature tasks
```

### Task 12: CLI Scripts (MCP CLI Scripts Pattern)

**Files:**
- Modify: `$MCP/package.json` (add tsx)
- Create: `$MCP/scripts/imperatus-run.ts`
- Create: `$MCP/scripts/imperatus-manifest.ts`
- Create: `$MCP/scripts/_shared.ts`
- Create: `$MCP/SCRIPTS.md`

**Step 1: Install tsx**

```bash
cd "$MCP" && npm install --save-dev tsx
```

**Step 2: Create shared helpers**

Create `$MCP/scripts/_shared.ts`:

```typescript
#!/usr/bin/env npx tsx
import { ImperatusServer } from '../index.js';

export function createServer(): ImperatusServer {
  return new ImperatusServer();
}

export function output(data: unknown): void {
  console.log(JSON.stringify(data, null, 2));
}

export function error(message: string): never {
  console.log(JSON.stringify({ success: false, error: message }, null, 2));
  process.exit(1);
}

export function parseArgs(args: string[]): Record<string, string | boolean> {
  const parsed: Record<string, string | boolean> = {};
  for (let i = 0; i < args.length; i++) {
    const arg = args[i];
    if (arg.startsWith('--')) {
      const key = arg.slice(2);
      const next = args[i + 1];
      if (!next || next.startsWith('--')) {
        parsed[key] = true;
      } else {
        parsed[key] = next;
        i++;
      }
    } else if (!parsed._positional) {
      parsed._positional = arg;
    }
  }
  return parsed;
}
```

**Step 3: Create imperatus-run script**

Create `$MCP/scripts/imperatus-run.ts`:

```typescript
#!/usr/bin/env npx tsx
/**
 * Run a full Imperatus journey from a query string.
 * Outputs the sealed manifest as JSON.
 *
 * Usage:
 *   npx tsx scripts/imperatus-run.ts "Build a REST API"
 *   npx tsx scripts/imperatus-run.ts --input query.txt
 *   npx tsx scripts/imperatus-run.ts "Quick question" --mode velites
 *   npx tsx scripts/imperatus-run.ts "Deep research" --rkqde "R=8 K=7 Q=9 D=6 E=5"
 *   npx tsx scripts/imperatus-run.ts "Task" --output manifest.json
 */

import { readFileSync, writeFileSync } from 'node:fs';
import { createServer, output, error, parseArgs } from './_shared.js';

const args = parseArgs(process.argv.slice(2));

if (args.help) {
  output({
    usage: 'npx tsx scripts/imperatus-run.ts <query> [options]',
    options: {
      '--input <file>': 'Read query from file',
      '--output <file>': 'Write manifest to file',
      '--rkqde <scores>': 'RKQDE scores (e.g. "R=5 K=4 Q=7 D=3 E=3")',
      '--mode <mode>': 'Force mode: velites|hastati|principes|triarii',
      '--verbose': 'Include journey details in output',
      '--help': 'Show this help',
    },
  });
  process.exit(0);
}

// Get query
let query = args._positional as string;
if (args.input) {
  query = readFileSync(args.input as string, 'utf-8').trim();
}
if (!query) error('No query provided. Pass a query string or use --input <file>');

// RKQDE scores
const rkqde = (args.rkqde as string) || 'R=5 K=4 Q=6 D=3 E=3';

// Mode override
const modeOverride = args.mode
  ? (args.mode as string).charAt(0).toUpperCase() + (args.mode as string).slice(1)
  : undefined;

// Run journey
const server = createServer();

// [begin]
server.processStep({ tag: 'begin', content: query, stepNumber: 1, totalSteps: 6, nextStepNeeded: true });

// [ground]
server.processStep({
  tag: 'ground',
  content: `${query}. ${rkqde}`,
  stepNumber: 2, totalSteps: 6, nextStepNeeded: true,
});

// [route]
const routeResult = server.processStep({
  tag: 'route',
  content: 'Auto-route',
  stepNumber: 3, totalSteps: 6, nextStepNeeded: true,
  ...(modeOverride ? { modeOverride } : {}),
} as any);

// [marshal]
server.processStep({
  tag: 'marshal',
  content: query,
  stepNumber: 4, totalSteps: 6, nextStepNeeded: true,
});

// [issue]
const issueResult = server.processStep({
  tag: 'issue',
  content: 'Seal manifest',
  stepNumber: 5, totalSteps: 6,
  nextStepNeeded: false, confidenceScore: 9,
});

const manifest = JSON.parse(issueResult.content[0].text);

// Output
const result = {
  success: true,
  query,
  ...(args.verbose ? manifest : { manifest: manifest.manifest }),
};

if (args.output) {
  writeFileSync(args.output as string, JSON.stringify(result, null, 2));
  output({ success: true, saved_to: args.output });
} else {
  output(result);
}
```

**Step 4: Create imperatus-manifest script**

Create `$MCP/scripts/imperatus-manifest.ts`:

```typescript
#!/usr/bin/env npx tsx
/**
 * Read and inspect an Imperatus manifest file.
 *
 * Usage:
 *   npx tsx scripts/imperatus-manifest.ts manifest.json
 *   npx tsx scripts/imperatus-manifest.ts manifest.json --summary
 *   npx tsx scripts/imperatus-manifest.ts manifest.json --matrix
 */

import { readFileSync } from 'node:fs';
import { output, error, parseArgs } from './_shared.js';

const args = parseArgs(process.argv.slice(2));

if (args.help || !args._positional) {
  output({
    usage: 'npx tsx scripts/imperatus-manifest.ts <manifest.json> [options]',
    options: {
      '--summary': 'Show mode/formation/expert count only',
      '--matrix': 'Show activation matrix as table',
      '--constraints': 'Show constraint levels',
      '--help': 'Show this help',
    },
  });
  process.exit(0);
}

const file = args._positional as string;
let data: any;
try {
  data = JSON.parse(readFileSync(file, 'utf-8'));
} catch {
  error(`Failed to read or parse: ${file}`);
}

const manifest = data.manifest || data;

if (args.summary) {
  output({
    mode: manifest.routing?.mode,
    formation: manifest.routing?.formation,
    experts: manifest.routing?.experts,
    reasoning: manifest.routing?.reasoning,
    iterations: manifest.routing?.iterations,
    confidence: manifest.confidence,
    steps_active: manifest.steps_active,
  });
} else if (args.matrix) {
  const matrix = manifest.activation_matrix || [];
  output(matrix.map((s: any) => `${s.status} | ${String(s.step).padStart(2)} | ${s.name.padEnd(22)} | ${s.detail}`));
} else if (args.constraints) {
  output(manifest.constraints);
} else {
  output(manifest);
}
```

**Step 5: Create SCRIPTS.md**

Create `$MCP/SCRIPTS.md`:

```markdown
# Imperatus CLI Scripts

Companion CLI scripts for the Imperatus MCP server. Use these in Claude Code / terminal for batch operations, testing, and debugging.

## Prerequisites

```bash
npm install  # installs tsx as dev dependency
```

## Available Scripts

### imperatus-run

Run a full Imperatus journey (begin → ground → route → marshal → issue) and output the sealed manifest.

```bash
# Basic usage
npx tsx scripts/imperatus-run.ts "Build a REST API for user management"

# With RKQDE scores
npx tsx scripts/imperatus-run.ts "Deep research task" --rkqde "R=8 K=7 Q=9 D=6 E=5"

# Force mode
npx tsx scripts/imperatus-run.ts "Quick question" --mode velites

# Save to file
npx tsx scripts/imperatus-run.ts "Complex analysis" --output manifest.json

# Read query from file
npx tsx scripts/imperatus-run.ts --input query.txt --output manifest.json

# Verbose (includes journey tracking)
npx tsx scripts/imperatus-run.ts "Task" --verbose
```

### imperatus-manifest

Inspect a saved manifest file.

```bash
# Full manifest
npx tsx scripts/imperatus-manifest.ts manifest.json

# Summary only
npx tsx scripts/imperatus-manifest.ts manifest.json --summary

# Activation matrix
npx tsx scripts/imperatus-manifest.ts manifest.json --matrix

# Constraints
npx tsx scripts/imperatus-manifest.ts manifest.json --constraints
```

## Output Format

All scripts output JSON to stdout. Pipe to `jq` for filtering:

```bash
npx tsx scripts/imperatus-run.ts "task" | jq '.manifest.routing'
npx tsx scripts/imperatus-run.ts "task" | jq '.manifest.activation_matrix[] | select(.status == "R")'
```
```

**Step 6: Run quick smoke test**

Run: `cd "$MCP" && npx tsx scripts/imperatus-run.ts "Test query" --mode velites`
Expected: JSON output with `success: true` and sealed manifest

**Step 7: Commit**

```bash
cd "$MCP" && git add scripts/ SCRIPTS.md package.json package-lock.json
git commit -m "feat: add CLI scripts for terminal use (imperatus-run, imperatus-manifest)"
```

---

## Dependency Graph

```
Task 1 (test framework)
  └→ Task 2 (export for testing)
       └→ Task 3 (phase ordering tests) ←── verifies existing
       └→ Task 4 (formation templates)
       └→ Task 5 (Armatura examine content)
       └→ Task 6 (activation matrix)
            └→ Task 7 (full [issue] manifest)
                 └→ Task 9 (integration tests)
       └→ Task 8 (HTTP transport)
       └→ Task 12 (CLI scripts) ←── uses exported ImperatusServer
  Task 10 (build verification) ←── depends on all code tasks
  Task 11 (README) ←── depends on all feature tasks (mention CLI scripts)
```

---

## Out of Scope (Future Tasks)

- **Constellation assembly** — expert spec objects in [marshal] (needs MR.RUG integration)
- **Bomb pre-embedding** — strategic bomb planting in [marshal] (needs SkeletrainOT integration)
- **Tool allocation logic** — mapping MCP servers to manifest (needs runtime inventory)
- **Cross-model cascade** — CEP INTER phase (needs multi-model orchestration layer)
- **Budget estimation** — token cost prediction (needs model-specific tokenizer data)
- **Server-side heuristic validation** — replacing model self-report confidence (research needed)
- **Smithery packaging** — npm publish + smithery.yaml update
- **Claude Desktop config** — update desktop_config.json to point at imperatus
