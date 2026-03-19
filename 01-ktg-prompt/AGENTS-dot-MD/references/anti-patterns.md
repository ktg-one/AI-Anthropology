# AGENTS.md Anti-Patterns

Common mistakes that make AGENTS.md files ineffective or harmful. Check generated files against these.

## Critical Anti-Patterns

### 1. Stale File Paths
**Bad**: `Authentication logic lives in src/auth/handlers.ts`
**Good**: `Authentication logic is in the auth module - search for the auth handler`

File paths change constantly. Describe capabilities and let agents discover paths.
Exception: Entry points and config files that rarely move are OK to reference.

### 2. README Duplication
**Bad**: Copying the project description, installation guide, and contributor guidelines from README.md
**Good**: Only include what agents need that ISN'T already in README

AGENTS.md complements README, not duplicates it. Agents read both files.

### 3. Generic Advice
**Bad**: "Write clean code" / "Follow best practices" / "Use meaningful variable names"
**Good**: "Use camelCase for functions, PascalCase for types, UPPER_SNAKE for constants"

Every line must be actionable and project-specific. If it applies to all projects, don't include it.

### 4. Wall of Text
**Bad**: Multi-paragraph prose explaining the architecture history
**Good**: Bullet points with code blocks that agents can parse and execute

Agents parse structured content (bullets, code blocks, headers) far better than prose.

### 5. Missing Boundaries
**Bad**: Only positive instructions (do this, use that)
**Good**: Explicit "Never" list including protected files, forbidden patterns, security rules

The Boundaries section prevents the most expensive agent mistakes. It's not optional.

### 6. Overly Long Files
**Bad**: 500+ line AGENTS.md trying to cover everything
**Good**: ≤150 lines at root, with pointers to deeper docs

Long files waste tokens on every agent request and increase stale content risk.

### 7. Version-Specific Claims
**Bad**: "We use React 18.2.0 and Node 20.11.1"
**Good**: "React 18+, Node 20+ (check package.json for exact versions)"

Version numbers go stale fast. Point to the source of truth.

### 8. ALL CAPS Forcing
**Bad**: "ALWAYS use TypeScript. NEVER use any."
**Good**: "Use TypeScript strict mode. Avoid `any` - use `unknown` and narrow."

Agents respond better to conversational instructions than aggressive formatting.

### 9. Conflicting Instructions
**Bad**: Different files saying different things about code style
**Good**: Single source of truth, with nested files only OVERRIDING specific rules

Audit all AGENTS.md files in the repo for consistency.

### 10. No Escape Hatch
**Bad**: Rigid instructions with no guidance for ambiguous situations
**Good**: "When stuck" section that tells agents what to do when uncertain

Agents need to know when to stop and ask vs when to proceed.

## Validation Checklist

Run through these before finalizing any AGENTS.md:

- [ ] Would a new team member find this useful on day 1?
- [ ] Can every command be copy-pasted and executed?
- [ ] Is every instruction specific to THIS project?
- [ ] Are there at least 3 explicit boundaries?
- [ ] Is there a "When stuck" section?
- [ ] Is the file under 150 lines?
- [ ] Does it avoid duplicating README content?
- [ ] Would this file still be accurate in 3 months?
