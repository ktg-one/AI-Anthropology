# Imperatus MCP Server

Strategic command engine for the LEGIO cascade. Decomposes, scores (RKQDE), routes, arms, and seals execution manifests.

## Architecture

Imperatus is SYSTEM-CORE #1 of LEGIO — the 17-module prompt engineering cascade. It sits at the top of the command chain: nothing moves without the manifest.

```
User Query → [begin] → [ground] → [examine]... → [route] → [marshal] → [issue] → MANIFEST_SEALED
```

### Command Domains

| Domain | Tags | Function |
|--------|------|----------|
| **Entry** | `begin` | Load command framework. First call. |
| **Reconnaissance** | `ground` | Decompose. Score (RKQDE). Brief. Objectives. |
| **Strategy** | `examine`, `route` | Set constraint levels. Select mode + formation. |
| **Authority** | `marshal`, `issue` | Assemble manifest. Seal and send. |
| **Control** | `halt`, `reconsider`, `adapt` | Gate failures. Revisions. Mid-flight re-routing. |

### Mode Tiers

| Tier | Name | Trigger | Experts |
|------|------|---------|---------|
| QUICK | **Velites** | Σ≤12 ∧ Danger≤5 | 0 |
| ANALYTICAL | **Hastati** | Σ=13-25 ∨ Danger=6-7 | 3 |
| DELIBERATE | **Principes** | Σ=26-38 ∨ Danger=8 | 5 |
| MAXIMUM | **Triarii** | Σ≥39 ∨ Danger≥9 | 5-8 |

### RKQDE Scoring

- **R** — Reasoning depth (1-10)
- **K** — Knowledge complexity (1-10)
- **Q** — Quality stakes (1-10)
- **D** — Decomposition breadth (1-10)
- **E** — Edge-case density (1-10)
- **Σ** — Sum (max 50)
- **Danger** — max(R,K,Q)

## Available Tools

### `imperatus`

Strategic command engine. Call iteratively with tags to build an execution manifest.

**Workflow:** Always start with `tag='begin'` (returns full protocol). Then `[ground]` → `[examine]...` → `[route]` → `[marshal]` → `[issue]`. Do NOT output work product until `status='MANIFEST_READY'`.

**Parameters:**

| Param | Type | Required | Description |
|-------|------|----------|-------------|
| `tag` | string | yes | Command phase: begin, ground, examine, route, marshal, issue, halt, reconsider, adapt |
| `content` | string | yes | Content of the current step |
| `stepNumber` | integer | yes | Current step number |
| `totalSteps` | integer | yes | Estimated total steps |
| `nextStepNeeded` | boolean | yes | Whether another step is needed |
| `query` | string | no | User request (pass on begin/ground) |
| `modeOverride` | string | no | Force mode: Velites, Hastati, Principes, Triarii |
| `verbose` | boolean | no | Show manifest to user before execution |
| `examineBlock` | string | no | Which Armatura constraint block to set |
| `confidenceScore` | number | no | Confidence gate 1-10 (halt if <9) |

### `imperatus_manifest`

Get current state of the execution manifest and journey summary at any point. No parameters.

## Usage

### Claude Code (stdio)

```bash
claude mcp add imperatus -- node G:/.ktg-hub/Areas/Ai-Anthropology/01-ktg-prompt/KTG/LEGIO-2026/lotus-wisdom-mcp-main/dist/bundle.js
```

### Claude Desktop

```json
{
  "mcpServers": {
    "imperatus": {
      "command": "node",
      "args": ["G:/.ktg-hub/Areas/Ai-Anthropology/01-ktg-prompt/KTG/LEGIO-2026/lotus-wisdom-mcp-main/dist/bundle.js"]
    }
  }
}
```

### HTTP Transport

```bash
cd lotus-wisdom-mcp-main
npm run start:http
# Endpoint: http://localhost:3000/mcp
# Health: http://localhost:3000/health
```

## Build

```bash
npm install
npm run build    # tsc + esbuild → dist/bundle.js + dist/http-bundle.js
```

### Scripts

| Command | Description |
|---------|-------------|
| `npm run build` | Compile TypeScript + bundle with esbuild |
| `npm run start:stdio` | Run stdio transport (tsc + node) |
| `npm run start:http` | Run HTTP transport (tsc + node) |
| `npm run dev` | Development mode (tsc + node) |

### Debug Mode

```bash
IMPERATUS_DEBUG=true node dist/bundle.js
```

## Files

| File | Purpose |
|------|---------|
| `index.ts` | Core Imperatus engine + stdio MCP server |
| `http-server.ts` | HTTP/StreamableHTTP transport (imports from index.ts) |
| `cli.js` | CLI entry point |

## License

MIT — Kevin Tan (ktg.one)
