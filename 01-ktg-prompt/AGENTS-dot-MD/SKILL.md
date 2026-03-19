---
name: agents-md-generator
description: Generate perfect AGENTS.md files for any codebase so AI coding agents (Codex, Cursor, Claude Code, Jules, Aider, Windsurf, Copilot, etc.) work effectively with the project. Use this skill whenever the user mentions AGENTS.md, wants to set up a project for AI agents, asks about coding agent configuration, mentions .cursorrules or CLAUDE.md, or wants to onboard a codebase for AI-assisted development. Also triggers on "set up my repo for AI", "configure coding agents", "agent instructions", or any request to create project-level AI guidance files.
---

# AGENTS.md Generator

Generate cross-compatible, validated AGENTS.md files that work across 20+ AI coding agents.

## When to Use

- User asks to create or improve an AGENTS.md file
- User wants to configure their project for AI coding agents
- User mentions Codex, Cursor, Claude Code, Jules, Aider, Windsurf, Copilot agent setup
- User asks about .cursorrules, CLAUDE.md, or similar agent config files
- User wants to onboard a client project for AI-assisted development
- User says "set up my repo for AI agents" or similar

## Generation Modes

### Mode A: Codebase Scan (preferred when files are available)

1. Look for project markers: `package.json`, `Cargo.toml`, `go.mod`, `pyproject.toml`, `pom.xml`, `Gemfile`, `*.csproj`
2. Detect package manager: npm/pnpm/yarn/bun, pip/uv/poetry, cargo, go, maven/gradle
3. Scan for test frameworks: jest, vitest, pytest, go test, cargo test, etc.
4. Identify linter/formatter: eslint, prettier, ruff, rustfmt, gofmt, etc.
5. Check for CI config: `.github/workflows/`, `.gitlab-ci.yml`, `Jenkinsfile`
6. Detect architecture patterns from directory structure
7. Fill gaps with targeted interview questions

### Mode B: Guided Interview (no codebase access)

Ask these questions in order, skip what's already known:

1. **Project type**: What language/framework? (React, Next.js, Python/FastAPI, Go, Rust, etc.)
2. **Package manager**: How do you install dependencies?
3. **Build & run**: What commands to build, start dev server, run production?
4. **Testing**: What test framework? How to run all tests? How to run a single test?
5. **Linting/formatting**: What tools? How to run them?
6. **Project structure**: What are the key directories and their purposes?
7. **Code conventions**: Any specific patterns, naming conventions, or anti-patterns?
8. **Git workflow**: Branch naming, commit format, PR process?
9. **Boundaries**: What should agents NEVER do in this project?
10. **Monorepo?**: Multiple packages/services? If yes, which ones need their own AGENTS.md?

## The Six Pillars

Every AGENTS.md MUST cover these six areas (from analysis of 2,500+ successful repos):

### 1. Commands (REQUIRED)
Exact, copy-pasteable commands in backticks:
- Install dependencies
- Build
- Start dev server
- Run all tests
- Run single test (with pattern syntax)
- Lint
- Format
- Type check (if applicable)

### 2. Testing (REQUIRED)
- Test framework and runner
- How to run the full suite
- How to run a single test file or test name
- How to run tests for a specific package (monorepo)
- CI pipeline location
- "Fix all tests before committing" instruction

### 3. Project Structure (REQUIRED)
- Key entry points (NOT exhaustive file trees)
- Describe capabilities, not hardcoded paths
- Point to exemplar files for patterns
- Call out legacy files to avoid copying

### 4. Code Style (REQUIRED)
- Language mode (strict TypeScript, Python type hints, etc.)
- Formatting rules (quotes, semicolons, indentation)
- Naming conventions
- Import ordering
- Architecture patterns (if any)
- Good/bad examples referencing REAL project files

### 5. Git Workflow (RECOMMENDED)
- Branch naming convention
- Commit message format
- PR title format
- Pre-commit checks to run

### 6. Boundaries (CRITICAL)
- What agents should NEVER do
- Files/directories that are off-limits
- Security considerations
- "When stuck" escape hatch instructions

## Quality Rules

Before outputting any AGENTS.md, verify against these rules:

### MUST
- [ ] Total length ≤ 150 lines (root file)
- [ ] Every command is in backticks and copy-pasteable
- [ ] All six pillars are addressed (at minimum: commands, testing, structure, style, boundaries)
- [ ] No generic advice - every line is project-specific
- [ ] Boundaries section exists with at least 3 items
- [ ] "When stuck" section exists

### MUST NOT
- [ ] No hardcoded file paths that will go stale (describe capabilities instead)
- [ ] No duplication of README.md content
- [ ] No walls of text - use bullet points and code blocks
- [ ] No version numbers that will go stale
- [ ] No "always" or "never" in ALL CAPS (agents respond better to conversational tone)
- [ ] No multi-paragraph prose blocks (agents parse bullets and commands better)

### SHOULD
- [ ] Include good/bad example file references
- [ ] Include file-scoped test/lint commands (faster feedback)
- [ ] Include a "When stuck" escape hatch
- [ ] Reference deeper docs via progressive disclosure

## Output Format

Generate the AGENTS.md with this structure:

```markdown
# AGENTS.md

## Project overview
[1-2 sentences: what this project is, what tech stack]

## Setup commands
- Install: `[exact command]`
- Dev server: `[exact command]`
- Build: `[exact command]`
- Type check: `[exact command]`

## Testing
- Run all: `[exact command]`
- Run single test: `[exact command with pattern placeholder]`
- Run specific package: `[exact command]` (monorepo only)
- CI config: `[path to CI config]`
- Fix all tests before committing.

## Project structure
- [capability description] → see `[file/dir]`
- [capability description] → see `[file/dir]`
- [capability description] → see `[file/dir]`

## Code style
- [Language] [mode]
- [formatting rules as bullets]
- Preferred patterns: see `[exemplar file]`
- Avoid patterns in: `[legacy file]`

## Good and bad examples
- prefer: `[good pattern file]` (why)
- avoid: `[bad pattern file]` (why)

## Git workflow
- Branch: `[format]`
- Commits: `[format]`
- PRs: `[format]`
- Before committing: `[pre-commit commands]`

## Boundaries
- Never [specific prohibition]
- Never [specific prohibition]
- Never [specific prohibition]
- Do not modify: `[protected files/dirs]`
- Security: [security-specific rules]

## When stuck
- Ask a clarifying question before guessing
- Propose a short plan and wait for approval
- Open a draft PR with notes explaining the blocker
```

## Cross-Agent Compatibility

After generating AGENTS.md, offer these optional extras:

1. **Claude Code symlink**: `ln -s AGENTS.md CLAUDE.md`
2. **Aider config**: Add `read: AGENTS.md` to `.aider.conf.yml`
3. **Gemini CLI config**: Add `{ "contextFileName": "AGENTS.md" }` to `.gemini/settings.json`
4. **Cursor**: AGENTS.md is auto-detected, no extra config needed
5. **Codex**: AGENTS.md is auto-detected at project root

## Monorepo Support

For monorepos, generate:
1. **Root AGENTS.md** - global conventions, monorepo-wide commands
2. **Package AGENTS.md** - package-specific overrides in each `packages/*/AGENTS.md`

Root file should include:
- How to navigate packages
- Global lint/test/build commands
- Package-specific command patterns
- Which package manager workspace commands to use

## Progressive Disclosure

If a section would exceed 10 lines, extract it:

```
For TypeScript conventions, see `docs/TYPESCRIPT_CONVENTIONS.md`
For API documentation, see `docs/API_GUIDE.md`
For deployment procedures, see `docs/DEPLOY.md`
```

Offer to generate these referenced files as well.

## Templates

For project-type-specific templates, read: `references/templates.md`
For common anti-patterns to avoid, read: `references/anti-patterns.md`

## Validation

After generating, run the validation script:
```bash
python scripts/validate_agents_md.py [path-to-generated-file]
```

This checks line count, section completeness, command formatting, and anti-patterns.

## Workflow Summary

1. Detect project type (scan or ask)
2. Select template from `references/templates.md`
3. Customize with project-specific details
4. Apply quality rules
5. Validate with script
6. Output AGENTS.md
7. Offer cross-agent compatibility setup
8. Offer monorepo nested files if applicable
9. Offer progressive disclosure extraction if any section is long
