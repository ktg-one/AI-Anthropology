# n8n + Imperatus MCP Dashboard — Integration Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Connect n8n as the orchestration dashboard for Imperatus MCP, enabling chat-driven planning, webhook-triggered manifest generation, execution logging, and visual monitoring of LEGIO command operations.

**Architecture:** n8n's native MCP Client Tool (v1.2, `httpStreamable` transport) connects to Imperatus running as a StreamableHTTP server. Three workflows: (1) Chat Agent for interactive planning, (2) API Gateway for programmatic access, (3) Manifest Execution Pipeline for consuming sealed manifests. All workflows deploy to the existing n8n instance at `https://ai-yah-old.taile6f11d.ts.net`.

**Tech Stack:** n8n v2.27.2, `@n8n/n8n-nodes-langchain.mcpClientTool` v1.2, `@n8n/n8n-nodes-langchain.agent`, Imperatus MCP HTTP server (Express + StreamableHTTP), Google Gemini / Claude as LLM backend.

**Prerequisite:** Task 8 from `docs/plans/2026-02-21-imperatus-mcp-completion.md` (StreamableHTTP transport) MUST be completed first. Imperatus needs an HTTP endpoint for n8n's MCP Client to connect to.

---

## Reference Paths

| Alias | Path |
|-------|------|
| `$MCP` | `G:/.ktg-hub/Areas/AI-Anthropology/01-ktg-prompt/KTG/LEGIO-2026/lotus-wisdom-mcp-main` |
| `$SPEC` | `G:/.ktg-hub/Areas/AI-Anthropology/01-ktg-prompt/KTG` |
| `$N8N` | `https://ai-yah-old.taile6f11d.ts.net` |

## Architecture Diagram

```
                          ┌─────────────────────────────────┐
                          │          n8n Dashboard           │
                          │   ($N8N)                         │
                          │                                  │
  User ──Chat──►  ┌───────┴────────┐                         │
                  │ WF1: Chat Agent │                         │
                  │ chatTrigger     │                         │
                  │   → AI Agent    │                         │
                  │     → MCP Client├──httpStreamable──┐      │
                  └────────────────┘                   │      │
                                                       ▼      │
  API ──Webhook──► ┌───────────────┐     ┌─────────────────┐  │
                   │ WF2: API GW   │     │ Imperatus MCP   │  │
                   │ webhook       │     │ HTTP Server      │  │
                   │   → Code      │     │ localhost:3000   │  │
                   │   → HTTP Req  ├────►│   /mcp           │  │
                   └───────────────┘     │                  │  │
                                         │ Tools:           │  │
  WF3 ◄── manifest ──────────────────────┤  - imperatus     │  │
  ┌────────────────┐                     │  - imperatus_    │  │
  │ WF3: Executor  │                     │    manifest      │  │
  │ subworkflow    │                     └─────────────────┘  │
  │   → parse      │                                          │
  │   → log        │                                          │
  │   → route exec │                                          │
  └────────────────┘                                          │
                          └──────────────────────────────────┘
```

## n8n MCP Client Tool v1.2 — Key Config

```
Node type: @n8n/n8n-nodes-langchain.mcpClientTool
Version: 1.2
Parameters:
  endpointUrl: "http://localhost:3000/mcp"  (or Tailscale URL)
  serverTransport: "httpStreamable"
  authentication: "none"
  include: "all"  (exposes both imperatus + imperatus_manifest tools)
```

---

### Task 1: Verify Imperatus HTTP Server Accessibility

**Files:**
- Verify: `$MCP/http-server.ts` (must exist — from completion plan Task 8)
- Verify: `$MCP/package.json` (must have `start:http` script)

**Step 1: Start Imperatus HTTP server**

```bash
cd "$MCP" && npm run start:http
```

Expected: `Imperatus MCP HTTP Server v1.0.0 on port 3000`

**Step 2: Test MCP endpoint responds**

```bash
curl -X POST http://localhost:3000/mcp \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","method":"initialize","params":{"protocolVersion":"2025-03-26","capabilities":{},"clientInfo":{"name":"test","version":"1.0"}},"id":1}'
```

Expected: JSON response with `result.serverInfo.name: "imperatus-server"` and a `mcp-session-id` header

**Step 3: Test tool listing**

Using the session ID from Step 2:

```bash
curl -X POST http://localhost:3000/mcp \
  -H "Content-Type: application/json" \
  -H "mcp-session-id: <SESSION_ID>" \
  -d '{"jsonrpc":"2.0","method":"tools/list","params":{},"id":2}'
```

Expected: Response listing `imperatus` and `imperatus_manifest` tools

**Step 4: Test a [begin] call**

```bash
curl -X POST http://localhost:3000/mcp \
  -H "Content-Type: application/json" \
  -H "mcp-session-id: <SESSION_ID>" \
  -d '{"jsonrpc":"2.0","method":"tools/call","params":{"name":"imperatus","arguments":{"tag":"begin","content":"Test from curl","stepNumber":1,"totalSteps":4,"nextStepNeeded":true}},"id":3}'
```

Expected: `FRAMEWORK_RECEIVED` status in result

**Step 5: Document the endpoint URL**

If running locally: `http://localhost:3000/mcp`
If accessible via Tailscale: note the Tailscale URL for n8n to reach it

---

### Task 2: Create n8n Workflow — Imperatus Chat Agent

**Approach:** Use n8n's `n8n_create_workflow` MCP tool to deploy the workflow directly.

**Step 1: Create the workflow via n8n MCP tool**

Use `mcp__n8n-docs__n8n_create_workflow` with:
- **Name:** `LEGIO: Imperatus Chat Agent`
- **Nodes:**
  1. `chatTrigger` — Chat interface entry point
  2. `agent` — AI Agent (Claude or Gemini as LLM)
  3. `mcpClientTool` — MCP Client connected to Imperatus HTTP
  4. `lmChatOpenAi` or `lmChatGoogleGemini` — LLM model sub-node
  5. `memoryBufferWindow` — Conversation memory (5 turns)

Node configuration:

```json
{
  "chatTrigger": {
    "type": "@n8n/n8n-nodes-langchain.chatTrigger",
    "typeVersion": 1.1,
    "parameters": {
      "options": {
        "title": "LEGIO Imperatus"
      }
    }
  },
  "agent": {
    "type": "@n8n/n8n-nodes-langchain.agent",
    "typeVersion": 2,
    "parameters": {
      "options": {
        "systemMessage": "You are LEGIO Imperatus — a strategic command engine. When the user provides a task or query, use the `imperatus` tool to process it through the LEGIO planning pipeline.\n\nWorkflow:\n1. Call imperatus with tag='begin' and the user's query\n2. Call imperatus with tag='ground' and RKQDE scores (assess R=Reasoning, K=Knowledge, Q=Quality, D=Domain interdependency, E=Expert perspectives needed, each 1-10)\n3. Call imperatus with tag='route' to select combat mode and formation\n4. Call imperatus with tag='marshal' to assemble the activation matrix\n5. Call imperatus with tag='issue' to seal the manifest\n6. Present the sealed manifest to the user in a clear format\n\nAfter sealing, use `imperatus_manifest` to show the summary.\n\nImportant: Each call must include stepNumber, totalSteps, and nextStepNeeded. Set nextStepNeeded=false only on the final [issue] call."
      }
    }
  },
  "mcpClientTool": {
    "type": "@n8n/n8n-nodes-langchain.mcpClientTool",
    "typeVersion": 1.2,
    "parameters": {
      "endpointUrl": "http://localhost:3000/mcp",
      "serverTransport": "httpStreamable",
      "authentication": "none",
      "include": "all"
    }
  }
}
```

**Step 2: Verify workflow created in n8n**

Run: `mcp__n8n-docs__n8n_list_workflows` and confirm `LEGIO: Imperatus Chat Agent` appears

**Step 3: Activate the workflow**

Use `mcp__n8n-docs__n8n_update_partial_workflow` to set `active: true`

**Step 4: Test via n8n chat interface**

Open `$N8N` in browser, navigate to the workflow, open the chat panel, and send:
```
Plan a REST API for user authentication with JWT tokens
```

Expected: The AI Agent calls imperatus through all 5 tags and returns a sealed manifest with:
- Combat mode (likely Hastati or Principes)
- Formation template
- 18-step activation matrix
- Constraint levels

**Step 5: Verify manifest output**

Check that the chat response includes:
- RKQDE scores
- Mode + formation selection
- Activation matrix summary
- The manifest is properly sealed (status: MANIFEST_READY)

---

### Task 3: Create n8n Workflow — Imperatus API Gateway

**Purpose:** Webhook-triggered workflow for programmatic access. External systems POST a query + optional RKQDE scores, receive a sealed manifest back.

**Step 1: Create the workflow via n8n MCP tool**

Use `mcp__n8n-docs__n8n_create_workflow` with:
- **Name:** `LEGIO: Imperatus API Gateway`
- **Nodes:**
  1. `webhook` — POST `/imperatus/plan` with JSON body
  2. `code` (JavaScript) — Orchestrate the full Imperatus journey
  3. `httpRequest` — Call Imperatus MCP HTTP endpoint directly
  4. `respondToWebhook` — Return sealed manifest

Node configuration:

```json
{
  "webhook": {
    "type": "n8n-nodes-base.webhook",
    "typeVersion": 2,
    "parameters": {
      "path": "imperatus/plan",
      "httpMethod": "POST",
      "responseMode": "responseNode",
      "options": {}
    }
  },
  "code": {
    "type": "n8n-nodes-base.code",
    "typeVersion": 2,
    "parameters": {
      "jsCode": "// Extract query and optional RKQDE from webhook body\nconst { query, rkqde, mode } = $input.first().json.body;\n\nif (!query) {\n  return [{ json: { error: 'Missing required field: query' } }];\n}\n\nconst scores = rkqde || 'R=5 K=4 Q=6 D=3 E=3';\n\nreturn [{ json: { query, scores, mode: mode || null } }];"
    }
  }
}
```

The `httpRequest` nodes make sequential JSON-RPC calls to `http://localhost:3000/mcp`:
1. Initialize (get session ID)
2. `tools/call` with `tag=begin`
3. `tools/call` with `tag=ground` + RKQDE
4. `tools/call` with `tag=route`
5. `tools/call` with `tag=marshal`
6. `tools/call` with `tag=issue`

**Step 2: Verify workflow created**

Run: `mcp__n8n-docs__n8n_list_workflows` and confirm `LEGIO: Imperatus API Gateway` appears

**Step 3: Test the webhook endpoint**

```bash
curl -X POST "$N8N/webhook/imperatus/plan" \
  -H "Content-Type: application/json" \
  -d '{"query": "Build a React dashboard with authentication", "rkqde": "R=7 K=5 Q=8 D=4 E=3"}'
```

Expected: JSON response with sealed manifest

**Step 4: Test with minimal input (defaults)**

```bash
curl -X POST "$N8N/webhook/imperatus/plan" \
  -H "Content-Type: application/json" \
  -d '{"query": "What is the capital of France?"}'
```

Expected: Velites mode manifest (low RKQDE defaults → simple query)

---

### Task 4: Create n8n Workflow — Manifest Logger

**Purpose:** Sub-workflow that receives sealed manifests and logs them for dashboard visibility. Stores to Google Sheets or a JSON file for history tracking.

**Step 1: Create the workflow via n8n MCP tool**

Use `mcp__n8n-docs__n8n_create_workflow` with:
- **Name:** `LEGIO: Manifest Logger`
- **Nodes:**
  1. `executeWorkflowTrigger` — Sub-workflow entry point
  2. `dateTime` — Add timestamp
  3. `set` — Extract key fields (mode, formation, RKQDE sigma, confidence, steps_active)
  4. `googleSheets` or `code` — Append row to tracking sheet

Fields to log per manifest:

| Column | Source |
|--------|--------|
| timestamp | Current datetime |
| query | manifest.mission.brief |
| mode | manifest.routing.mode |
| formation | manifest.routing.formation |
| sigma | manifest.assessment.sigma |
| danger | manifest.assessment.danger |
| confidence | manifest.confidence |
| steps_active | manifest.steps_active |
| journey | tagJourney |

**Step 2: Verify workflow created**

Run: `mcp__n8n-docs__n8n_list_workflows`

**Step 3: Wire WF1 and WF2 to call this logger**

Add a `executeWorkflow` node at the end of both the Chat Agent and API Gateway workflows that calls this sub-workflow with the sealed manifest data.

**Step 4: Test logging**

Run a query through WF1 (chat) or WF2 (webhook), then verify the manifest was logged.

---

### Task 5: Create n8n Workflow — Manifest Execution Router (Future-Ready)

**Purpose:** Placeholder sub-workflow that receives a sealed manifest and routes to the appropriate execution pattern. This is where LEGIO formations would dispatch work. For now, it logs and returns the activation matrix as a task list.

**Step 1: Create the workflow via n8n MCP tool**

Use `mcp__n8n-docs__n8n_create_workflow` with:
- **Name:** `LEGIO: Manifest Executor`
- **Nodes:**
  1. `executeWorkflowTrigger` — Entry point (receives sealed manifest)
  2. `code` — Parse activation matrix into task list
  3. `switch` — Route by formation (Testudo/Triplex/Cuneus/Orbis)
  4. `set` (per branch) — Apply formation-specific execution config
  5. `respondToWebhook` or output — Return execution plan

Code node logic:

```javascript
const manifest = $input.first().json;
const matrix = manifest.activation_matrix || [];
const mode = manifest.routing?.mode || 'Hastati';
const formation = manifest.routing?.formation || 'Triplex';

// Convert activation matrix to task list
const tasks = matrix
  .filter(step => step.status === 'R' || step.status === 'O')
  .map(step => ({
    step: step.step,
    name: step.name,
    required: step.status === 'R',
    config: step.detail,
  }));

return [{
  json: {
    mode,
    formation,
    total_tasks: tasks.length,
    required_tasks: tasks.filter(t => t.required).length,
    optional_tasks: tasks.filter(t => !t.required).length,
    tasks,
    status: 'EXECUTION_PLAN_READY',
    note: 'Future: each task dispatches to formation-specific execution sub-workflows'
  }
}];
```

**Step 2: Verify workflow created**

**Step 3: Test with a sample manifest**

Call via `executeWorkflow` from WF2 with a sealed Hastati manifest.

Expected: Task list with ~13 required steps, ~3 optional, formation=Triplex

---

### Task 6: Network Accessibility — Tailscale or Port Forwarding

**Purpose:** Ensure n8n (running on Tailscale at `ai-yah-old.taile6f11d.ts.net`) can reach Imperatus HTTP server.

**Step 1: Determine where Imperatus will run**

Options:
- **Same machine as n8n** → `http://localhost:3000/mcp` works directly
- **Different machine on Tailscale** → Use Tailscale IP/hostname
- **Different machine, no Tailscale** → Port forward or deploy to cloud

**Step 2: If same machine, verify**

```bash
curl http://localhost:3000/mcp -X POST -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","method":"initialize","params":{"protocolVersion":"2025-03-26","capabilities":{},"clientInfo":{"name":"n8n","version":"1.0"}},"id":1}'
```

**Step 3: If different machine, use Tailscale**

Update MCP Client Tool `endpointUrl` in all workflows to use the Tailscale hostname:
```
http://<imperatus-machine>.taile6f11d.ts.net:3000/mcp
```

**Step 4: Test connectivity from n8n's perspective**

Run a simple test execution of WF1 (Chat Agent) to confirm the MCP Client can reach Imperatus.

---

### Task 7: End-to-End Integration Test

**Step 1: Start Imperatus HTTP server**

```bash
cd "$MCP" && npm run start:http
```

**Step 2: Test WF1 — Chat Agent**

Open n8n chat interface, send:
```
Design a multi-tenant SaaS authentication system with OAuth2, role-based access, and audit logging
```

Expected:
- AI Agent makes 5-6 imperatus tool calls
- Mode: Principes or Triarii (high RKQDE)
- Formation: Testudo (K>=8) or Orbis (D>=7)
- Activation matrix with 16-18 required steps
- Manifest logged to Google Sheet

**Step 3: Test WF2 — API Gateway**

```bash
curl -X POST "$N8N/webhook/imperatus/plan" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "Quick factual lookup — what frameworks support MCP?",
    "rkqde": "R=2 K=3 Q=4 D=1 E=1"
  }'
```

Expected:
- Mode: Velites
- Formation: Cuneus
- Fast path (no examine blocks)
- Activation matrix with ~7 required steps

**Step 4: Test WF2 with high complexity**

```bash
curl -X POST "$N8N/webhook/imperatus/plan" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "Cross-domain analysis of climate change impact on global supply chains, financial markets, and food security",
    "rkqde": "R=9 K=8 Q=9 D=9 E=7"
  }'
```

Expected:
- Mode: Triarii
- Formation: Orbis (D=9)
- All 18 steps required
- Full expert constellation

**Step 5: Verify manifest logging**

Check Google Sheet (or log output) for all 3 test manifests with correct metadata.

---

## Dependency Graph

```
Task 1 (verify HTTP server) ←── prerequisite: completion plan Task 8
  └→ Task 6 (network accessibility)
       └→ Task 2 (Chat Agent workflow)
       └→ Task 3 (API Gateway workflow)
            └→ Task 4 (Manifest Logger sub-workflow)
            └→ Task 5 (Manifest Executor sub-workflow)
  Task 7 (E2E integration test) ←── depends on Tasks 2-6
```

## Out of Scope (Future)

- **Formation-specific execution sub-workflows** — Testudo/Triplex/Cuneus/Orbis each get their own n8n workflow with mode-appropriate logic (sequential Baton, parallel Swarm, etc.)
- **Multi-model routing** — Imperatus manifest specifies which LLM handles each pipeline step; n8n routes to Claude/Gemini/GPT accordingly
- **Real-time dashboard** — n8n webhook → WebSocket → live manifest progress visualization
- **Manifest diff/comparison** — Side-by-side comparison of manifests from different RKQDE scores
- **CEP cross-model cascade** — LEGIO-15 INTER module for cross-model handoff via n8n
- **Cost estimation** — Token budget prediction per manifest step, surfaced in dashboard
- **Authentication** — Bearer/OAuth2 for Imperatus HTTP endpoint (production hardening)
