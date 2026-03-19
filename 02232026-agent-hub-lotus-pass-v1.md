# Agent Hub Lotus Pass (v1)

Date: 2026-02-23
Workspace: `G:\.ktg-hub`
Purpose: Design an intuitive multi-agent hub flow for `onboard -> equip -> claim -> work -> handoff`

## Lotus Pass

Final journey:
- `begin -> open -> upaya -> integrate -> verify -> embody -> complete`

Domain journey:
- `entry -> process_flow -> skillful_means -> non_dual_recognition -> meta_cognitive -> non_dual_recognition -> meta_cognitive`

Note:
- Planned as 6 steps, but `embody` returned `processing` instead of `WISDOM_READY`, so a final `complete` step was added.

## Step Notes

1. `begin`
- Framed the problem as an intuitive multi-agent hub in `G:\.ktg-hub`
- Emphasis on Obsidian + kanban visibility and low-friction coordination

2. `open`
- Focused on the first 90 seconds for a new agent
- Goal: one obvious path and immediate reduction in uncertainty

3. `upaya`
- Accounted for mixed agent capability levels
- Conclusion: layered onboarding (mandatory core + optional helpers/templates/automation)

4. `integrate`
- Reconciled file-visible truth with MCP/n8n automation
- Files remain primary; automation assists and validates

5. `verify`
- Turned the concept into pass/fail checks
- Focused on preventing double-claims and orphaned handoffs

6. `embody`
- Grounded the design in agent behavior and affordances
- Target feel: runway with markings, not a maze/dashboard

7. `complete`
- Locked the v1 principle: file-visible coordination first, automation second

## V1 Agent Hub Principle

Agents should be able to onboard, claim, work, and handoff from markdown alone.
MCP and n8n should improve speed and reliability without becoming the only source of truth.

## Practical v1 Flow

1. Read `agents ONBOARDING.md`
2. Read `Agent Kanban.md`
3. Claim exactly one task (visible update in kanban)
4. Do work
5. Write handoff packet to `packet/`
6. Update board status and leave artifact paths

## What Must Be Obvious to a Fresh Agent

- `TRUSTED FILES`
- `CLAIM RULE`
- `OUTPUT LOCATIONS`
- `ESCALATE / BLOCKED BEHAVIOR`

## Verification Criteria (v1)

- Fresh agent can onboard in under 2 minutes
- Two agents do not claim the same task
- Every in-progress task has owner + timestamp + packet/artifact path
- Replacement agent can resume from files + packet without asking for missing context

## Obsidian UX Direction (for later dressing)

Preferred feel:
- runway/checklist

Suggested visible sections:
- Welcome strip (read this, read board, claim one task, leave packet)
- Runway markings (`TRUSTED FILES`, `CLAIM RULE`, `OUTPUTS`, `ESCALATE`)
- Guardrails (one task at a time, do not steal claims, no completion without packet)
- Breadcrumbs (packet path, artifact paths, timestamp, agent name)

## Why This Pass Helped

- Surfaced that the main problem is entry/claim ambiguity, not lack of tools
- Reinforced hybrid architecture:
- Obsidian/files = visible truth
- MCP = tool access
- n8n = horizontal coordination (later/optional layer)
