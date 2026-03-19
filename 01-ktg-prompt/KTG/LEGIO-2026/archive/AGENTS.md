# AGENTS.md — ktg.one Full Audit

Generated: 2026-02-26
Source: Git analysis, Vercel deployment logs, local build, deep code audit

---

## 0. GIT STATE (Critical)

**Local and remote have diverged.** Local master is 1 commit ahead, remote master is 4 commits ahead.

- Local ahead: `bcb80a6 feat: add snippets vault hub with KTG v30 DOCS and API routes`
- Remote ahead: 4 commits (GlobalCursor optimization, HeroImages WebGL optimization, two merge PRs)
- **25+ modified files** not committed or pushed (the entire hub, playground, models, AI chat, IntroGate, HomeClient, etc.)
- **13+ untracked files** including new features (models API, playground, IntroGate, HomeClient, scripts)
- **5 stale stashes** and **14 git worktrees** (10 detached HEADs in `.cursor/worktrees/`)
- **Production (`live: false`)**: The Vercel project shows `"live": false` — no deployment is currently promoted to production. Latest deployment targets `null` (preview only).

**Vercel failed deployment** (`dpl_4uoWcRZHCvNrHbfrMRab4EUXvmfQ`):
- Branch: `claude/setup-ai-gateway-nextjs-8eiQ4`
- Error: `TypeError: Cannot read properties of undefined (reading 'trim')` during prerendering `/`
- Build compiled, but static page generation crashed

---

## 1. DUPLICATE / CONFLICTING SYSTEMS (High)

### 1a. Dual intro-skip tracking — localStorage vs sessionStorage

Two independent systems fight over "has user seen intro":

| System | Storage | Key | Files |
|--------|---------|-----|-------|
| IntroGate | `sessionStorage` | `ktg-intro-completed` | `IntroGate.jsx:18,24` |
| HeroSection | `localStorage` | `intro-completed` | `HeroSection.jsx:16,36` |
| HeroImages | `localStorage` | `hero-animated` | `HeroImages.jsx:177` |
| HeroTransition | `localStorage` | `hero-transition-played` | `HeroTransition.jsx:22` |
| ExpertiseSection | `localStorage` | `expertise-revealed` | `ExpertiseSection.jsx:47,96` |
| ExpertiseTransition | `localStorage` | `expertise-transition-played` | `ExpertiseTransition.jsx:22,47` |
| ValidationSection | `localStorage` | `validation-animated` | `ValidationSection.jsx:59,89` |
| BlogPreview | `localStorage` | `blog-animated` | `BlogPreview.jsx:33,97` |

**Problem**: `HomeClient` uses `isFirstVisit` from IntroGate (sessionStorage) to decide whether to render intro. But HeroSection reads localStorage independently. On a new session with stale localStorage, the hero auto-skips even though IntroGate says "first visit". `SkipButton` writes to localStorage keys but never updates IntroGate's sessionStorage.

### 1b. Duplicate Header rendering

`Header` is rendered globally in `layout.jsx:72`. These pages render it again locally:
- `src/app/blog/[slug]/page.jsx:5`
- `src/app/blog/not-found.jsx:9`
- `src/app/expertise/page.jsx:22`
- `src/app/validation/page.jsx:17`

Result: **Two headers stacked** on those pages.

### 1c. Dual cursor system

- `GlobalCursor` (in ClientLayout) — 2 DOM elements, perpetual RAF loop (never stops)
- `CursorDot` (in layout.jsx) — 12 DOM elements, stops on idle

14 cursor DOM elements animating simultaneously. `GlobalCursor` RAF loop never cancels.

---

## 2. MISSING FILES (High)

| Referenced Path | Where Used | Actual File |
|-----------------|------------|-------------|
| `/assets/og-image.jpg` | `layout.jsx:46` (OpenGraph) | Does not exist |
| `/assets/ktg-one.svg` | `blog/page.jsx:50,58`, `blog/[slug]/page.jsx:38,86,96` | Should be `ktg.svg` |
| `extracted-snippets/legio-snippets.json` | `api/hub/snippets/route.js:33`, `api/hub/snippets/[id]/route.js:28` | Does not exist (only `outside-snippets.json`) |
| `/assets/art/Colours-of-Haki-*.webp` (14 files) | `ScrollTransition.jsx:12-15` | Directory does not exist (dead code) |
| `api/hub/snippets/search/route.js` | Documented in hub README | Empty directory, no route file |

---

## 3. DEAD CODE (Medium)

### Unused components (never imported anywhere):
- `src/components/CareerTimeline.jsx`
- `src/components/ScrollTransition.jsx`
- `src/components/SplitText.jsx`
- `src/components/ToolsSection.jsx`
- `src/components/shadcn-studio/` (entire directory)
- `src/components/ui/matter-button.jsx`
- `src/components/ui/navigation-menu.jsx`
- `src/components/ui/skeleton.jsx`

### Unused exports:
- `searchSnippets`, `createSnippet` in `src/lib/snippets/queries.js:23-54`
- `uploadSnippet` in `src/lib/snippets/storage.js`
- `src/lib/performance-monitor.js` — never imported
- `src/lib/performance-capture.js` — never imported

### Unused imports:
- `GeometricBackground` in `src/app/page.jsx:1` — imported, never rendered
- `GeometricBackground` in `src/components/ClientLayout.jsx:4` — imported, never rendered
- `Header` in `src/components/HomeClient.jsx:4` — imported, never rendered
- `useCallback` in `src/components/ValidationSection.jsx:6` — imported, never called
- `useMemo` in `src/components/ExpertiseSection.jsx:5` — imported, never used

---

## 4. CSS / TAILWIND ISSUES (Medium-High)

### 4a. Invalid Tailwind utility classes
- `z-35` → should be `z-[35]` — `ExpertiseTransition.jsx:73`
- `z-60` → should be `z-[60]` — `BlogPreview.jsx:107,120`
- `z-70` → should be `z-[70]` — `Footer.jsx:5`
- `content-visibility-auto` → should be `[content-visibility:auto]` — `ExpertiseSection.jsx:174`
- `scrollbar-hide` → not defined anywhere — `BlogPreview.jsx:171`

### 4b. Tailwind v3/v4 config conflict (HIGH)
- `postcss.config.mjs` uses `@tailwindcss/postcss` (Tailwind 4 plugin)
- `tailwind.config.js` exists with Tailwind 3 format (ignored by TW4)
- `@tailwindcss/typography` plugin in `tailwind.config.js` is **not loaded** — `prose` classes do nothing
- Blog post content rendered via `react-markdown` relies on `prose` — **blog post content is unstyled**

### 4c. Gradient syntax inconsistency
- `bg-linear-to-b` (TW4 syntax) in `ExpertiseTransition.jsx`, `ToolsSection.jsx`
- `bg-gradient-to-b` (TW3 syntax) in `HeroTransition.jsx`

---

## 5. SEO ISSUES (High)

- **Broken OG image** — `og-image.jpg` does not exist. Every page shares this broken image.
- **Wrong logo path** — `ktg-one.svg` referenced in blog JSON-LD. Actual file is `ktg.svg`.
- **No Twitter card metadata** on root layout, blog index, hub pages (only on `blog/[slug]`)
- **Sitemap missing pages**: `/hub`, `/hub/snippets`, `/hub/models`, `/hub/playground`, `/expertise`, `/validation` not in `sitemap.js`
- **No metadata exports** on: `/hub` page, `/hub/models` page, `/hub/playground` page
- **No `authors` field** in root layout metadata
- **`lang="en"` vs `locale: "en_AU"`** — inconsistent. Should be `lang="en-AU"`

---

## 6. API ISSUES (High)

### 6a. Chat API — no protection
- `src/app/api/chat/route.js` — no authentication, no rate limiting, no input length cap
- Messages array not validated for content/size before sending to AI Gateway
- Could be abused to burn API credits

### 6b. Missing POST handler
- `src/app/api/hub/snippets/route.js` only has `GET`. No `POST` for creating snippets.
- `createSnippet` and `uploadSnippet` exist in lib but are unreachable via API.

### 6c. Sync fs in API route
- `src/app/api/hub/snippets/route.js` uses `fs.existsSync` and `fs.readFileSync` — blocks event loop
- Should use `fs.promises`

### 6d. Error response format mismatch
- `src/app/api/hub/models/route.js` returns array on success, object on error
- Client-side code silently swallows errors (checks `Array.isArray` only)

---

## 7. PERFORMANCE ISSUES (Medium)

- **GlobalCursor unbounded RAF** — `requestAnimationFrame(animate)` runs every frame forever, even idle. `GlobalCursor.jsx:25-46`
- **Dual cursor = 14 DOM elements** animating on every mousemove
- **Three.js bundle (~500-600KB)** loaded for a single hero shader effect. Lazy-loaded but still massive.
- **`require()` in useEffect** — `src/libs/lenis.jsx:19` uses CJS require inside effect, bypasses tree shaking
- **Multiple `console.warn` in production** — `ValidationSection.jsx:118,157,170`
- **Hardcoded 500ms timeout for ScrollTrigger refresh** — `PhilosophySection.jsx:122`
- **HeroImages resize listener leak on mobile** — early return path doesn't clean up resize listener when `hasPlayed && mobile`

---

## 8. GSAP / LENIS ISSUES (Medium)

- **8 separate `gsap.registerPlugin(ScrollTrigger)` calls** across components. 3 lack SSR `typeof window` guard: `BlogPreview.jsx:13`, `HeroTransition.jsx:8`, `ExpertiseTransition.jsx:8`
- **`ScrollTrigger.scrollerProxy` cleanup passes empty object** — `lenis.jsx:78`. Should pass `null` or call `clearScrollMemory()`.
- **`useMemo` for localStorage reads** — `ExpertiseTransition.jsx:20-23`, `HeroTransition.jsx:20-23`. `useMemo` is not guaranteed stable; should use `useState` + `useEffect`.
- **ValidationSection creates ScrollTriggers even for returning visitors** — always runs `setupScrollTrigger` after 300ms timeout regardless of `hasPlayed`

---

## 9. ACCESSIBILITY ISSUES (Medium)

- **No skip-to-content link** — WCAG 2.1 AA requirement. Missing from layout.
- **ValidationSection horizontal scroll** — keyboard-inaccessible. No keyboard navigation for cards 2-5.
- **SkipButton invisible if GSAP fails** — starts `opacity-0` in className, relies on GSAP to show. Keyboard-focusable but invisible without JS.
- **`<article>` inside `<Link>`** — `BlogPreview.jsx` wraps block-level `<article>` inside inline `<a>`. Invalid HTML nesting.
- **`lang="en"` should be `lang="en-AU"`** — site targets Australian audience per OG metadata.

---

## 10. NAVIGATION ISSUES (Medium)

- **Orphan pages**: `/expertise` and `/validation` have no inbound links from any navigation
- **Footer has zero nav links** — copyright only, dead end for users
- **`/hub/models` not in header nav** — only reachable through `/hub` landing page
- **Header links on hub sub-pages**: users on `/hub/playground` or `/hub/models` have no breadcrumb or back-to-hub link

---

## 11. DATABASE ISSUES (Low-Medium)

- **No indexes** beyond PK on `snippets` table — `ilike` search does full table scan
- **`updated_at` never auto-updates** — missing `.$onUpdateFn()` in Drizzle schema
- **Connection pool of 1** — `src/lib/db/index.js:12` — fine for serverless, queues in dev
- **Drizzle config module format mismatch** — `drizzle.config.js` uses ESM, `next.config.js` uses CJS

---

## 12. BUILD / CONFIG ISSUES (High)

- **`experimental.optimizeCss: true`** — Next.js 16 uses LightningCSS internally (build succeeds locally), but this flag is still experimental and may behave differently across environments.
- **ESLint completely missing** — no ESLint config file exists in the project root. `npm run lint` fails: `Invalid project directory provided, no such directory: lint`. There's one inside `my-project-design/` (wrong project).
- **`turbopack.root`** set in config but `dev` script doesn't use `--turbopack` flag
- **1 high severity npm vulnerability** — shown in Vercel build logs

---

## 13. WORKTREE / BRANCH HYGIENE (Low)

- **14 git worktrees**, 10 are detached HEADs on old commits
- **5 stashes** accumulated
- **`.worktrees/` directories** tracked in repo (should be in `.gitignore`)
- **`my-project-design/`** untracked directory in root — this is an entire separate Vite/React project (has its own `package.json`, `vite.config.ts`, `tsconfig.json`, `eslint.config.js`, `index.html`). Should not be inside this repo.

---

## 14. STRAY FILES IN SOURCE (Medium)

- **`src/in-memoria.db`** — 224KB SQLite database sitting inside the `src/` directory. This is a development artifact from an agent/memory tool. Should not be in source, partially gitignored (`.in-memoria.db` is ignored but `src/in-memoria.db` path may not match).
- **`scripts/scroll-screenshot-simple.md`** — markdown doc inside scripts directory (not a script)
- **`scripts/scroll-screenshot.js`** — uses Puppeteer (devDep) for visual testing, not part of app

---

## 15. ESLINT CONFIG MISSING (High)

No ESLint config file exists in root (`eslint.config.js`, `.eslintrc`, `.eslintrc.json` — none found). The `next lint` command fails with `Invalid project directory provided, no such directory: lint`. There's an `eslint.config.js` inside `my-project-design/` (the stray Vite project), but nothing for the actual Next.js app.

---

## 16. DRIZZLE CONFIG MODULE FORMAT (Low)

`drizzle.config.js` uses ESM syntax (`import`/`export default`) in a `.js` file. The project has no `"type": "module"` in `package.json` (it's CommonJS by default). Running `npx drizzle-kit` commands will fail with `SyntaxError: Cannot use import statement in a module` unless Node resolves it differently. `next.config.js` uses `module.exports` (CJS) — confirming the project is CJS-default.

---

## 17. REACT DOCTOR FINDINGS (Score: 93/100)

18 warnings across 11/21 changed files:

| Warning | Count | Location |
|---------|-------|----------|
| `SnippetsPage` has 6 `useState` calls | 1 | `src/app/hub/snippets/page.jsx` — use `useReducer` for related state |
| Array index used as key | 8 | Multiple components — use stable IDs (`item.id`, `item.slug`) |
| Unknown DOM property | 1 | Stray prop on an element |
| 4 `setState` calls in single `useEffect` | 1 | Combine into `useReducer` or derive state |
| `dangerouslySetInnerHTML` usage | 1 | Blog content — XSS risk from WordPress HTML |
| Permanent `will-change` | 2 | Apply only during animation, remove after — wastes GPU memory |
| `ValidationSection` is 322 lines | 1 | Break into smaller focused components |
| `scroll` listener without `{ passive: true }` | 2 | Blocks main-thread scroll perf |
| Default prop `[]` creates new ref each render | 1 | Extract to module-level constant |

---

## PRIORITY MATRIX

| Priority | Issues | Impact |
|----------|--------|--------|
| **P0 — Blocks Deploy** | Git divergence (local/remote split), missing OG image, duplicate Headers on 4 pages, ESLint config missing entirely, Vercel `live: false` (no production deployment active) | Site can't deploy clean |
| **P1 — Breaks UX** | Dual intro tracking conflict (8 localStorage/sessionStorage keys fighting), dual cursor system (14 DOM elements), Tailwind v3/v4 config conflict (prose/typography plugin dead), blog `ktg-one.svg` 404s | Users see broken experience |
| **P2 — Security/Cost** | Chat API zero rate limit/auth, no input length cap on AI Gateway calls | Financial risk from abuse |
| **P3 — SEO** | 6 pages missing from sitemap, no Twitter cards, broken JSON-LD logo, 3 hub pages have no metadata export, broken OG image | Discovery/sharing broken |
| **P4 — Code Quality** | 8 dead components, 5 unused imports, 5 invalid Tailwind classes, sync fs in API, GlobalCursor RAF leak, stray SQLite DB in src/, stray Vite project in root, drizzle config module format wrong | Tech debt accumulation |
| **P5 — Accessibility** | No skip-to-content link, keyboard-trapped horizontal scroll, invisible SkipButton without GSAP, article inside anchor | WCAG non-compliance |
