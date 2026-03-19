# AGENTS.md Templates

Project-type-specific templates. Select the closest match and customize.

## Table of Contents
- [React/Vite](#reactvite)
- [Next.js](#nextjs)
- [Python FastAPI](#python-fastapi)
- [Python ML/Data](#python-mldata)
- [Go Service](#go-service)
- [Rust CLI/Library](#rust-clilibrary)
- [Node.js Backend](#nodejs-backend)
- [Monorepo (Turborepo/Nx)](#monorepo)
- [Generic/Minimal](#generic)

---

## React/Vite

```markdown
# AGENTS.md

## Project overview
[Name] is a React [version] application built with Vite, TypeScript, and [UI library].

## Setup commands
- Install: `pnpm install`
- Dev server: `pnpm dev`
- Build: `pnpm build`
- Type check: `pnpm tsc --noEmit`
- Preview production: `pnpm preview`

## Testing
- Run all: `pnpm test`
- Run single: `pnpm vitest run -t "<test name>"`
- Run file: `pnpm vitest run src/components/Button.test.tsx`
- Watch mode: `pnpm test -- --watch`
- Coverage: `pnpm test -- --coverage`
- Fix all tests before committing.

## Project structure
- Routing and app shell → see `src/App.tsx`
- Reusable components → `src/components/`
- Page-level components → `src/pages/`
- API client and data fetching → `src/api/`
- Shared types → `src/types/`
- Design tokens and theme → `src/theme/`

## Code style
- TypeScript strict mode
- Single quotes, no semicolons
- Functional components with hooks only
- Named exports (no default exports except pages)
- Prefer: `src/components/DataTable.tsx` (composable, typed props)
- Avoid: patterns with `any` types or inline styles

## Git workflow
- Branch: `feat/short-description` or `fix/short-description`
- Commits: conventional commits (`feat:`, `fix:`, `chore:`)
- Before committing: `pnpm lint && pnpm tsc --noEmit && pnpm test`

## Boundaries
- Never install new dependencies without asking
- Never modify `vite.config.ts` or `tsconfig.json` without approval
- Never use `any` type - use `unknown` and narrow
- Never use class components
- Do not modify files in `public/` or `dist/`

## When stuck
- Ask a clarifying question before guessing
- Check the component's test file for usage examples
- Propose a plan and wait for approval
```

---

## Next.js

```markdown
# AGENTS.md

## Project overview
[Name] is a Next.js [version] application using the App Router, TypeScript, and [styling solution].

## Setup commands
- Install: `pnpm install`
- Dev server: `pnpm dev`
- Build: `pnpm build`
- Type check: `pnpm tsc --noEmit`
- Lint: `pnpm lint`

## Testing
- Run all: `pnpm test`
- Run single: `pnpm vitest run -t "<test name>"`
- E2E tests: `pnpm playwright test`
- Single E2E: `pnpm playwright test tests/auth.spec.ts`
- Fix all tests before committing.

## Project structure
- App routes and layouts → `app/`
- Server actions → `app/actions/`
- API routes → `app/api/`
- Shared components → `components/`
- Database schema and queries → `lib/db/`
- Server-only utilities → `lib/server/`
- Client-only utilities → `lib/client/`

## Code style
- TypeScript strict mode
- Use Server Components by default, add `'use client'` only when needed
- Prefer Server Actions over API routes for mutations
- Use `next/image` for all images, `next/link` for all links
- Data fetching in Server Components, not in client components
- Colocate styles with components

## Git workflow
- Branch: `feat/ticket-id-description`
- Commits: conventional commits
- Before committing: `pnpm lint && pnpm tsc --noEmit && pnpm test`

## Boundaries
- Never use `getServerSideProps` or `getStaticProps` (App Router only)
- Never put secrets in client components
- Never modify `next.config.js` or middleware without approval
- Do not bypass TypeScript with `@ts-ignore`
- Do not add dependencies without approval

## When stuck
- Check Next.js docs for App Router patterns
- Ask before choosing between Server Component vs Client Component
- Propose a plan and wait for approval
```

---

## Python FastAPI

```markdown
# AGENTS.md

## Project overview
[Name] is a Python [version] REST API built with FastAPI, SQLAlchemy, and [database].

## Setup commands
- Create venv: `python -m venv .venv && source .venv/bin/activate`
- Install: `pip install -e ".[dev]"` or `uv sync`
- Dev server: `uvicorn app.main:app --reload`
- Lint: `ruff check .`
- Format: `ruff format .`
- Type check: `mypy app/`

## Testing
- Run all: `pytest`
- Run single: `pytest tests/test_users.py::test_create_user -v`
- Run marked: `pytest -m "not slow"`
- Coverage: `pytest --cov=app --cov-report=term-missing`
- Fix all tests before committing.

## Project structure
- App entry and middleware → `app/main.py`
- Route handlers → `app/routers/`
- Business logic → `app/services/`
- Database models → `app/models/`
- Pydantic schemas → `app/schemas/`
- Database connection → `app/db.py`
- Migrations → `alembic/`

## Code style
- Python 3.11+ with type hints on all functions
- Use Pydantic models for all request/response schemas
- Dependency injection via FastAPI `Depends()`
- Async handlers where I/O is involved
- Snake_case everywhere, PascalCase for classes only
- Docstrings on all public functions (Google style)

## Git workflow
- Branch: `feat/description` or `fix/description`
- Commits: conventional commits
- Before committing: `ruff check . && ruff format --check . && mypy app/ && pytest`

## Boundaries
- Never use raw SQL - use SQLAlchemy ORM or query builder
- Never commit `.env` files or secrets
- Never modify alembic migrations after they've been applied
- Do not add dependencies without updating `pyproject.toml`
- Do not bypass type checking with `# type: ignore` without explanation

## When stuck
- Check existing routers for patterns
- Ask before making architectural decisions (new services, models)
- Propose a plan and wait for approval
```

---

## Python ML/Data

```markdown
# AGENTS.md

## Project overview
[Name] is a Python [version] ML/data project using [framework: PyTorch/TF/scikit-learn] with [data tools].

## Setup commands
- Create env: `conda env create -f environment.yml` or `uv sync`
- Activate: `conda activate [env-name]`
- Install dev: `pip install -e ".[dev]"`
- Jupyter: `jupyter lab`

## Testing
- Run all: `pytest tests/`
- Run unit only: `pytest tests/unit/`
- Run integration: `pytest tests/integration/ -m "not gpu"`
- Fix all tests before committing.

## Project structure
- Training scripts → `src/train/`
- Model definitions → `src/models/`
- Data loading and transforms → `src/data/`
- Evaluation metrics → `src/eval/`
- Notebooks (exploration only) → `notebooks/`
- Config files → `configs/`
- Experiment outputs → `outputs/` (gitignored)

## Code style
- Type hints on all functions
- Docstrings with shapes: `Args: x (Tensor): Input tensor of shape (B, C, H, W)`
- Config-driven experiments (no magic numbers in code)
- Reproducibility: always set random seeds
- Logging over print statements

## Boundaries
- Never commit model weights, datasets, or large files
- Never modify configs for published experiments
- Never hardcode paths - use config files or environment variables
- Do not install GPU-specific packages without checking CUDA version
- Notebooks are for exploration only - production code goes in `src/`

## When stuck
- Check existing training scripts for patterns
- Ask before changing model architecture or data pipeline
- Propose experiment config changes and wait for approval
```

---

## Go Service

```markdown
# AGENTS.md

## Project overview
[Name] is a Go [version] [service type] using [framework/router] and [database].

## Setup commands
- Install deps: `go mod download`
- Build: `go build ./cmd/[service]`
- Run: `go run ./cmd/[service]`
- Lint: `golangci-lint run`

## Testing
- Run all: `go test ./...`
- Run single: `go test ./internal/[package] -run TestName -v`
- Race detection: `go test -race ./...`
- Coverage: `go test -coverprofile=coverage.out ./... && go tool cover -html=coverage.out`
- Fix all tests before committing.

## Project structure
- Entry point and CLI → `cmd/`
- Core business logic → `internal/`
- Public API types → `pkg/`
- Database migrations → `migrations/`
- API definitions → `api/` (proto/openapi)

## Code style
- Follow Effective Go and Go Code Review Comments
- Accept interfaces, return structs
- Table-driven tests
- Errors: `fmt.Errorf("operation: %w", err)` wrapping
- No init() functions, no globals

## Boundaries
- Never use `panic` for error handling
- Never add external dependencies without discussion
- Never use `interface{}` - use generics or specific types
- Do not modify generated code (protobuf, sqlc, etc.)

## When stuck
- Check `internal/` for existing patterns
- Ask before adding new packages to `go.mod`
- Propose a plan and wait for approval
```

---

## Rust CLI/Library

```markdown
# AGENTS.md

## Project overview
[Name] is a Rust [type: CLI tool/library/service] using [key crates].

## Setup commands
- Build: `cargo build`
- Run: `cargo run -- [args]`
- Check: `cargo check`
- Lint: `cargo clippy -- -D warnings`
- Format: `cargo fmt`

## Testing
- Run all: `cargo test`
- Run single: `cargo test test_name -- --exact`
- Run module: `cargo test module_name`
- Doc tests: `cargo test --doc`
- Fix all tests before committing.

## Project structure
- Binary entry point → `src/main.rs`
- Library root → `src/lib.rs`
- Core types → `src/types/`
- Error handling → `src/error.rs`
- CLI argument parsing → `src/cli.rs`

## Code style
- No `unwrap()` in library code - use `?` operator
- Custom error types with `thiserror`
- Document all public items with `///` doc comments
- Use `#[must_use]` on functions returning Result/Option
- Clippy pedantic where practical

## Boundaries
- Never use `unsafe` without documented safety proof
- Never add dependencies without checking license compatibility
- Never use `.unwrap()` or `.expect()` in library code
- Do not suppress Clippy warnings without justification

## When stuck
- Check existing modules for error handling patterns
- Ask before adding new dependencies to Cargo.toml
- Propose a plan and wait for approval
```

---

## Monorepo

```markdown
# AGENTS.md

## Project overview
[Name] is a [pnpm/npm/yarn] monorepo managed by [Turborepo/Nx/Lerna] containing [N] packages.

## Setup commands
- Install all: `pnpm install`
- Build all: `pnpm turbo run build`
- Dev all: `pnpm turbo run dev`
- Navigate to package: `cd packages/[name]`

## Testing
- Run all: `pnpm turbo run test`
- Run package: `pnpm turbo run test --filter [package-name]`
- Run single in package: `cd packages/[name] && pnpm test -- -t "test name"`
- Fix all tests before committing.

## Packages
- `packages/[name]` - [description] (see `packages/[name]/AGENTS.md`)
- `packages/[name]` - [description] (see `packages/[name]/AGENTS.md`)
- `apps/[name]` - [description] (see `apps/[name]/AGENTS.md`)

## Code style
- Shared TypeScript config in `tsconfig.base.json`
- Shared ESLint config in `packages/eslint-config/`
- Each package owns its own build and test config
- Cross-package imports via workspace protocol

## Git workflow
- Branch: `feat/[package]/description`
- Commits: `[package]: conventional commit message`
- PRs: `[package] Title`
- Before committing: `pnpm turbo run lint test --filter=[changed-packages]`

## Boundaries
- Never modify root config without approval
- Never add cross-package dependencies without discussion
- Never bypass workspace protocol for internal deps
- Check the correct `packages/[name]/AGENTS.md` for package-specific rules

## When stuck
- Check if it's a package-specific or monorepo-level issue
- Ask which package you should be working in
- Propose a plan and wait for approval
```

---

## Generic

```markdown
# AGENTS.md

## Project overview
[Name] is a [language] project that [purpose].

## Setup commands
- Install: `[command]`
- Build: `[command]`
- Run: `[command]`

## Testing
- Run all: `[command]`
- Run single: `[command with pattern]`
- Fix all tests before committing.

## Project structure
- Entry point → `[path]`
- Core logic → `[directory]`
- Tests → `[directory]`
- Config → `[directory/files]`

## Code style
- [Key conventions as bullets]
- Preferred patterns: see `[exemplar file]`
- Avoid: `[anti-pattern file or description]`

## Boundaries
- Never [critical prohibition]
- Never [critical prohibition]
- Never [critical prohibition]
- Do not modify: `[protected files]`

## When stuck
- Ask a clarifying question before guessing
- Propose a short plan and wait for approval
```
