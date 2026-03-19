INSTANT CREATE WORKFLOW (copy-paste these exact MCP calls):
bash


# 1. SEARCH MEMORY FIRST (your global mem0)
mcp mem0ai-mem0-memory-mcp search_memory "n8n workflow github slack"

# 2. LIST TEMPLATES
mcp flowengine-n8n-workflow-builder list_templates "github slack vercel"

# 3. CREATE PRODUCTION WORKFLOW
mcp flowengine-n8n-workflow-builder create_workflow '{
  "name": "GitHub PR → Slack → Vercel Deploy",
  "description": "Auto-notify Slack on PR + deploy to Vercel",
  "nodes": [
    {"type": "n8n-nodes-base.github", "trigger": "pull_request"},
    {"type": "n8n-nodes-base.slack", "message": "PR {{ $json.title }} ready"},
    {"type": "n8n-nodes-base.vercel", "action": "deploy"}
  ]
}'
📁 YOUR FILES LIVE HERE (no bash - already created):


✅ skills/n8n-workflows/SKILL.md  ← Skill manifest
✅ skills/n8n-workflows/examples/starter.json
✅ skills/n8n-workflows/README.md
⚡ ONE-CLICK TEMPLATES (run these now):
Lead Scoring:

bash


mcp flowengine-n8n-workflow-builder create_workflow '{"name":"LeadScoring","nodes":[{"type":"n8n-nodes-base.googleSheets"},{"type":"n8n-nodes-base.openAi","model":"gpt-4o","score":"lead quality"}]}'
Content Pipeline:

bash


mcp flowengine-n8n-workflow-builder create_workflow '{"name":"AIContentPipeline","nodes":[{"type":"n8n-nodes-base.googleDrive"},{"type":"n8n-nodes-base.openAi"},{"type":"n8n-nodes-base.wordpress"}]}'
🧠 STORE IN MEMORY:
bash


mcp mem0ai-mem0-memory-mcp add_memory '{"project_id":"n8n-stack","workflows":["github-pr-pipeline","lead-scoring"],"mcp":"flowengine-n8n"}'
✅ READY. Run #3 above → get production flowengine.cloud URL instantly.

Next: prompt-engineering skill? (create)