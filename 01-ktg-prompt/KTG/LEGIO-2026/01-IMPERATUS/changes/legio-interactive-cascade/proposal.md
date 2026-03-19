# OpenSpec Proposal: LEGIO Interactive Cascade

## Problem Statement

The LEGIO cascade currently operates in two modes that don't talk to each other:

1. **MCP Server Mode** — The imperatus MCP tool processes 10 tags sequentially (begin→ground→examine×16→route→marshal→issue). The calling model drives every step. The server is a calculator — it responds, never initiates. The user sees nothing until the agent outputs the Aquila at the end.

2. **Agent Definition Mode** — The imperatus-commander agent definition (.claude/agents/) tells the model HOW to drive the MCP. But it's a static document. The agent reads it once and follows the prescription. No user interaction during the flow.

**The gap:** Neither mode lets the user participate in the scoring/calibration process. The user has domain knowledge the model doesn't. RKQDE scores could be better with user input. Armatura dials could be user-tuned. But today, the user fires a query and waits for the Aquila to appear — zero collaboration during the 10-tag flow.

## Proposed Change

Make the LEGIO cascade **optionally interactive** — a hybrid mode where:

- The user can participate in RKQDE scoring (confirm, adjust, challenge)
- The user can see and override Armatura recommendations at examine time
- The user can approve/reject the mode tier before routing commits
- The Aquila becomes a co-signed document (user + Imperatus)
- Downstream agents know whether the manifest was user-validated or auto-scored

This is NOT replacing the autonomous flow. It's adding an interactive layer that activates when the user wants to co-pilot.

## Scope

### ADDED
- Interactive mode flag on `begin` tag (user opts in)
- User checkpoints at ground (RKQDE review), examine (dial review), route (tier confirm)
- Co-signature on Aquila when user participated
- MCP server returns `interaction_points` metadata so agents know where to pause

### MODIFIED
- `handleBegin` — accepts `interactive: true` flag, returns interaction protocol
- `handleGround` — returns RKQDE for user review before committing
- `handleExamine` — returns recommendation + asks for user confirmation
- `handleRoute` — returns suggested tier for user approval
- `handleIssue` — Aquila includes participation record
- imperatus-commander agent definition — adds AskUserQuestion integration

### REMOVED
- Nothing removed. Autonomous flow remains the default.

## Stakeholders

| Who | Interest |
|-----|----------|
| User (Kevin) | Domain expert input, quality control, learning the system |
| Imperatus (agent) | Better RKQDE accuracy, reduced downstream rejections |
| Legatus (downstream) | Knows if manifest was user-validated (higher confidence) |
| Censor (downstream) | Knows participation level for verification depth |

## Success Criteria

1. A user can run LEGIO in fully autonomous mode (zero change to current behavior)
2. A user can opt into interactive mode and see/adjust RKQDE at ground
3. A user can see/adjust each Armatura dial at examine
4. The Aquila records whether user participated and at which checkpoints
5. Downstream agents receive participation metadata
6. The interaction adds genuine value — not just "confirm Y/N" rubber stamping

## Risk Assessment

| Risk | Mitigation |
|------|-----------|
| Interactive mode slows down simple queries | Velites tier auto-skips interaction (too fast to bother) |
| User doesn't understand RKQDE dimensions | Ground checkpoint includes plain-English explanations |
| 16 examine blocks = too many confirmations | Batch by zone (4 confirmations instead of 16) |
| Agent can't use AskUserQuestion mid-MCP-flow | Agent pauses between MCP calls to interact |
