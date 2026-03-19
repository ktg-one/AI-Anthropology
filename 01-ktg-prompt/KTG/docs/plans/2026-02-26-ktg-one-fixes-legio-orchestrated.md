# ktg.one P0-P4 Fixes — LEGIO-Orchestrated CLI Execution Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Fix the 70+ issues identified in AGENTS.md (ktg.one audit) by dispatching gemini-cli and codex-cli as LEGIO-mapped agents, validating the CLI orchestration pattern on real work.

**Architecture:** LEGIO mental model — Claude acts as Imperatus (score/route) + Legatus (plan/seal) + Censor (verify). gemini-cli acts as Consilium (analysis/judgment). codex-cli acts as Primus Pilus (mechanical execution). Fixes flow through the P0 critical chain first (git → eslint → tailwind → vercel), then fan out to parallel workstreams.

**Tech Stack:** Next.js 16, React 19, Tailwind CSS 4, Drizzle ORM, GSAP/Lenis, Vercel deployment. CLI tools: gemini-cli (`gemini -p`), codex-cli (`codex exec`).

**Target codebase:** `D:/projects/sites/ktg-one/`
**Audit source:** `G:/.ktg-hub/.../LEGIO-2026/AGENTS.md`

**Why not ExtendedManifest first:** YAGNI. The manifest interface is theoretical until we've validated CLI orchestration on real problems. This plan IS the validation. Build infrastructure from experience, not speculation.

---

## Phase 0: Imperatus — Assess & Route

### Task 0.1: Verify ktg-one state

**Files:**
- Read: `D:/projects/sites/ktg-one/package.json`
- Read: `D:/projects/sites/ktg-one/next.config.js`

**Step 1: Check git status**

Run: `cd D:/projects/sites/ktg-one && git status && git log --oneline -5`
Expected: See diverged state (local 1 ahead, remote 4 ahead, 25+ modified)

**Step 2: Check remote divergence**

Run: `cd D:/projects/sites/ktg-one && git fetch origin && git log --oneline HEAD..origin/master`
Expected: See the 4 remote commits (GlobalCursor optimization, HeroImages WebGL, merge PRs)

**Step 3: Document actual state vs AGENTS.md assumptions**

Compare git status output against Section 0 of AGENTS.md. Note any changes since audit was written (2026-02-26). Record in a scratch note.

**Step 4: Commit — N/A (read-only assessment)**

---

### Task 0.2: RKQDE scoring for fix execution

**Files:**
- Read: `G:/.ktg-hub/.../LEGIO-2026/AGENTS.md` (priority matrix section)

**Step 1: Score the fix execution**

```
R: 5 (moderate reasoning — most fixes are known, few judgment calls)
K: 6 (need Next.js 16, TW4, GSAP, Drizzle knowledge)
Q: 8 (production site, wrong fix = broken deploy)
D: 7 (17 issue categories, multi-file, multi-system)
E: 4 (edge cases are known from audit)
Σ: 30, Danger: 8
```

**Step 2: Route**

Mode: **Principes** (Deliberate). Formation: **Orbis** (D≥7).
3-pass iteration. 5 experts (Claude + gemini + codex + gemini-verify + claude-censor).

---

## Phase 1: Git Sync — P0 Root Blocker (Claude-direct, SEQUENTIAL)

> **LEGIO role:** Imperatus decision — this blocks everything. No CLI delegation.

### Task 1.1: Stash local changes

**Files:**
- Modify: working tree at `D:/projects/sites/ktg-one/`

**Step 1: Stash all uncommitted work**

Run: `cd D:/projects/sites/ktg-one && git stash push -m "pre-merge-stash-$(date +%Y%m%d)" --include-untracked`
Expected: "Saved working directory and index state"

**Step 2: Verify clean state**

Run: `git status`
Expected: "nothing to commit, working tree clean"

---

### Task 1.2: Merge remote changes

**Files:**
- Modify: git history at `D:/projects/sites/ktg-one/`

**Step 1: Merge remote into local**

Run: `cd D:/projects/sites/ktg-one && git merge origin/master`
Expected: Either clean merge or conflict list

**Step 2: If conflicts — resolve**

Run: `git diff --name-only --diff-filter=U`
List conflicted files. For each: read both versions, pick correct resolution. These will be in GlobalCursor/HeroImages (the remote optimizations) — likely no overlap with stashed local work.

**Step 3: Complete merge**

Run: `git add . && git commit -m "merge: reconcile with remote (GlobalCursor+HeroImages optimizations)"`

**Step 4: Pop stash**

Run: `git stash pop`
Expected: Clean pop or conflict list. Resolve any conflicts.

**Step 5: Commit reconciled state**

Run: `git add -A && git commit -m "chore: reconcile stashed work after remote merge"`

---

## Phase 2: Codex Batch — Mechanical P0-P1 Fixes (PARALLEL)

> **LEGIO role:** Primus Pilus. Codex follows the railroad. Zero judgment.
> All tasks in this phase are independent — dispatch as parallel codex agents.

### Task 2.1: Remove duplicate Headers (P0)

**Files:**
- Modify: `src/app/blog/[slug]/page.jsx:5` — remove Header import+render
- Modify: `src/app/blog/not-found.jsx:9` — remove Header import+render
- Modify: `src/app/expertise/page.jsx:22` — remove Header import+render
- Modify: `src/app/validation/page.jsx:17` — remove Header import+render

**Step 1: Dispatch to codex**

Run:
```bash
cd D:/projects/sites/ktg-one && codex exec "In these 4 files, remove the local Header import and its JSX render. The Header is already rendered globally in layout.jsx:72. Files: src/app/blog/[slug]/page.jsx, src/app/blog/not-found.jsx, src/app/expertise/page.jsx, src/app/validation/page.jsx. Remove the import line and the <Header /> or <Header> JSX element. Do NOT touch layout.jsx."
```

**Step 2: Verify no double header**

Run: `grep -rn "import.*Header" src/app/blog/ src/app/expertise/ src/app/validation/`
Expected: No matches (all local Header imports removed)

**Step 3: Commit**

```bash
git add src/app/blog/ src/app/expertise/ src/app/validation/
git commit -m "fix: remove duplicate Header renders on 4 pages (already in layout.jsx)"
```

---

### Task 2.2: Fix ktg-one.svg → ktg.svg (P1)

**Files:**
- Modify: `src/app/blog/page.jsx:50,58`
- Modify: `src/app/blog/[slug]/page.jsx:38,86,96`

**Step 1: Dispatch to codex**

Run:
```bash
cd D:/projects/sites/ktg-one && codex exec "Replace all references to 'ktg-one.svg' with 'ktg.svg' in src/app/blog/page.jsx and src/app/blog/[slug]/page.jsx. This fixes a 404 on the blog logo."
```

**Step 2: Verify**

Run: `grep -rn "ktg-one.svg" src/`
Expected: No matches

**Step 3: Commit**

```bash
git add src/app/blog/
git commit -m "fix: correct blog logo path ktg-one.svg → ktg.svg"
```

---

### Task 2.3: Create ESLint config (P0)

**Files:**
- Create: `D:/projects/sites/ktg-one/eslint.config.js`

**Step 1: Dispatch to codex**

Run:
```bash
cd D:/projects/sites/ktg-one && codex exec "Create an eslint.config.js for a Next.js 16 project using the flat config format. Use @next/eslint-plugin-next and eslint-config-next. The project uses JSX (not TypeScript). Keep it minimal — just the Next.js recommended rules. The project has no existing ESLint config."
```

**Step 2: Verify lint runs**

Run: `npm run lint 2>&1 | head -20`
Expected: Lint output (warnings OK, no "config not found" error)

**Step 3: Commit**

```bash
git add eslint.config.js
git commit -m "chore: add ESLint flat config for Next.js 16"
```

---

### Task 2.4: Fix lang attribute (P3)

**Files:**
- Modify: `src/app/layout.jsx` — `lang="en"` → `lang="en-AU"`

**Step 1: Dispatch to codex**

Run:
```bash
cd D:/projects/sites/ktg-one && codex exec "In src/app/layout.jsx, change lang=\"en\" to lang=\"en-AU\" on the <html> tag. The site targets an Australian audience per the OG metadata locale en_AU."
```

**Step 2: Verify**

Run: `grep 'lang=' src/app/layout.jsx`
Expected: `lang="en-AU"`

**Step 3: Commit**

```bash
git add src/app/layout.jsx
git commit -m "fix: set html lang to en-AU to match OG locale"
```

---

### Task 2.5: Add missing sitemap routes (P3)

**Files:**
- Modify: `src/app/sitemap.js`

**Step 1: Dispatch to codex**

Run:
```bash
cd D:/projects/sites/ktg-one && codex exec "In src/app/sitemap.js, add these 6 missing routes to the sitemap array: /hub, /hub/snippets, /hub/models, /hub/playground, /expertise, /validation. Match the existing entry format (url, lastModified, changeFrequency, priority). Use priority 0.7 for hub pages, 0.5 for expertise/validation."
```

**Step 2: Verify**

Run: `grep -c "url:" src/app/sitemap.js`
Expected: Count increased by 6

**Step 3: Commit**

```bash
git add src/app/sitemap.js
git commit -m "fix: add 6 missing routes to sitemap (hub, expertise, validation)"
```

---

### Task 2.6: Remove unused imports (P4)

**Files:**
- Modify: `src/app/page.jsx:1` — remove GeometricBackground import
- Modify: `src/components/ClientLayout.jsx:4` — remove GeometricBackground import
- Modify: `src/components/HomeClient.jsx:4` — remove Header import
- Modify: `src/components/ValidationSection.jsx:6` — remove useCallback import
- Modify: `src/components/ExpertiseSection.jsx:5` — remove useMemo import

**Step 1: Dispatch to codex**

Run:
```bash
cd D:/projects/sites/ktg-one && codex exec "Remove these unused imports (they are imported but never used):
1. GeometricBackground from src/app/page.jsx
2. GeometricBackground from src/components/ClientLayout.jsx
3. Header from src/components/HomeClient.jsx
4. useCallback from src/components/ValidationSection.jsx
5. useMemo from src/components/ExpertiseSection.jsx
Only remove the import statement, do not modify anything else in these files."
```

**Step 2: Verify**

Run: `grep -n "GeometricBackground" src/app/page.jsx src/components/ClientLayout.jsx && grep -n "import.*Header" src/components/HomeClient.jsx`
Expected: No matches

**Step 3: Commit**

```bash
git add src/app/page.jsx src/components/ClientLayout.jsx src/components/HomeClient.jsx src/components/ValidationSection.jsx src/components/ExpertiseSection.jsx
git commit -m "chore: remove 5 unused imports across components"
```

---

### Task 2.7: Add GSAP SSR guards (P4)

**Files:**
- Modify: `src/components/BlogPreview.jsx:13`
- Modify: `src/components/HeroTransition.jsx:8`
- Modify: `src/components/ExpertiseTransition.jsx:8`

**Step 1: Dispatch to codex**

Run:
```bash
cd D:/projects/sites/ktg-one && codex exec "In these 3 files, the gsap.registerPlugin(ScrollTrigger) call runs without a typeof window check, which breaks SSR. Wrap each call with: if (typeof window !== 'undefined') { gsap.registerPlugin(ScrollTrigger); }. Files: src/components/BlogPreview.jsx:13, src/components/HeroTransition.jsx:8, src/components/ExpertiseTransition.jsx:8."
```

**Step 2: Verify**

Run: `grep -A1 "registerPlugin" src/components/BlogPreview.jsx src/components/HeroTransition.jsx src/components/ExpertiseTransition.jsx`
Expected: All wrapped in `typeof window` guard

**Step 3: Commit**

```bash
git add src/components/BlogPreview.jsx src/components/HeroTransition.jsx src/components/ExpertiseTransition.jsx
git commit -m "fix: add SSR guards to 3 GSAP registerPlugin calls"
```

---

### Task 2.8: Fix sync fs in API route (P4)

**Files:**
- Modify: `src/app/api/hub/snippets/route.js`

**Step 1: Dispatch to codex**

Run:
```bash
cd D:/projects/sites/ktg-one && codex exec "In src/app/api/hub/snippets/route.js, replace fs.existsSync and fs.readFileSync with their async equivalents (fs.promises.access and fs.promises.readFile). Make the handler async if it isn't already. Keep the same logic, just async I/O."
```

**Step 2: Verify**

Run: `grep -n "Sync" src/app/api/hub/snippets/route.js`
Expected: No matches

**Step 3: Commit**

```bash
git add src/app/api/hub/snippets/route.js
git commit -m "fix: replace sync fs calls with async in snippets API route"
```

---

### Task 2.9: Add passive scroll listeners (P4)

**Files:**
- Modify: 2 files with scroll listeners missing `{ passive: true }`

**Step 1: Dispatch to codex**

Run:
```bash
cd D:/projects/sites/ktg-one && codex exec "Search src/components/ for addEventListener('scroll' calls that don't include { passive: true } in the options. Add { passive: true } to each. This prevents blocking the main thread during scroll."
```

**Step 2: Verify**

Run: `grep -rn "addEventListener.*scroll" src/components/ | grep -v passive`
Expected: No matches without passive

**Step 3: Commit**

```bash
git add src/components/
git commit -m "perf: add passive:true to scroll event listeners"
```

---

### Task 2.10: Clean up stray files (P4)

**Files:**
- Delete: `src/in-memoria.db`
- Modify: `.gitignore` — add `*.db` or `in-memoria.db`

**Step 1: Dispatch to codex**

Run:
```bash
cd D:/projects/sites/ktg-one && codex exec "Delete src/in-memoria.db (stray SQLite database from development). Add 'in-memoria.db' to .gitignore if not already present."
```

**Step 2: Verify**

Run: `ls src/in-memoria.db 2>/dev/null && echo "STILL EXISTS" || echo "DELETED"`
Expected: DELETED

**Step 3: Commit**

```bash
git add .gitignore
git rm --cached src/in-memoria.db 2>/dev/null
git commit -m "chore: remove stray SQLite DB from src/, add to gitignore"
```

---

## Phase 3: Gemini Batch — Structural Fixes (SEQUENTIAL per group)

> **LEGIO role:** Consilium. Gemini does analysis + judgment before code changes.
> These require reading multiple files and making design decisions.

### Task 3.1: Tailwind v3/v4 resolution (P1 — ARCHITECTURAL DECISION)

**Files:**
- Read: `postcss.config.mjs`
- Read: `tailwind.config.js`
- Modify: one or both depending on decision

**Step 1: Dispatch analysis to gemini**

Run:
```bash
cd D:/projects/sites/ktg-one && cat postcss.config.mjs tailwind.config.js | gemini -p "This Next.js 16 project has a Tailwind conflict: postcss.config.mjs uses @tailwindcss/postcss (TW4 plugin), but tailwind.config.js exists with TW3 format (ignored by TW4). The @tailwindcss/typography plugin in tailwind.config.js is not loaded, so prose classes do nothing — blog content is unstyled.

Two options:
A) Commit to TW4: delete tailwind.config.js, add typography via @theme in CSS
B) Revert to TW3: change postcss plugin back to tailwindcss

Which is correct for Next.js 16? Provide the exact file changes for the right option. Show the CSS needed for typography/prose to work."
```

**Step 2: Apply gemini's recommendation**

Based on gemini output, make the changes. Most likely: commit to TW4 (Next.js 16 ships with TW4), delete tailwind.config.js, add `@plugin '@tailwindcss/typography'` to main CSS.

**Step 3: Verify prose renders**

Run: `npm run dev` — visit blog post, confirm prose content is styled.

**Step 4: Fix gradient syntax inconsistency**

Replace any remaining `bg-gradient-to-b` (TW3) with `bg-linear-to-b` (TW4) or vice versa — pick one syntax consistently.

**Step 5: Commit**

```bash
git add postcss.config.mjs tailwind.config.js src/app/globals.css
git commit -m "fix: resolve Tailwind v3/v4 conflict — commit to TW4 with typography plugin"
```

---

### Task 3.2: Dual intro tracking unification (P1)

**Files:**
- Read: `src/components/IntroGate.jsx`
- Read: `src/components/HeroSection.jsx`
- Read + Modify: 8 components with localStorage/sessionStorage keys

**Step 1: Dispatch mapping to gemini**

Run:
```bash
cd D:/projects/sites/ktg-one && cat src/components/IntroGate.jsx src/components/HeroSection.jsx src/components/HeroImages.jsx src/components/HeroTransition.jsx src/components/ExpertiseSection.jsx src/components/ExpertiseTransition.jsx src/components/ValidationSection.jsx src/components/BlogPreview.jsx | gemini -p "These 8 components each independently track 'has user seen this animation' using different localStorage/sessionStorage keys:
- IntroGate: sessionStorage ktg-intro-completed
- HeroSection: localStorage intro-completed
- HeroImages: localStorage hero-animated
- HeroTransition: localStorage hero-transition-played
- ExpertiseSection: localStorage expertise-revealed
- ExpertiseTransition: localStorage expertise-transition-played
- ValidationSection: localStorage validation-animated
- BlogPreview: localStorage blog-animated

Design a unified system: one canonical key in localStorage. Show the exact code changes for each file. The SkipButton should set this key. IntroGate should read it. All other components should derive their hasPlayed state from it."
```

**Step 2: Apply gemini's unification**

Make the changes per gemini output. Key principle: single `ktg-intro-completed` in localStorage, all components read from it.

**Step 3: Test**

Run: `npm run dev` — clear localStorage, visit site, verify intro plays once then skips on reload.

**Step 4: Commit**

```bash
git add src/components/
git commit -m "fix: unify 8 intro tracking keys into single localStorage entry"
```

---

### Task 3.3: Dual cursor system merge (P1)

**Files:**
- Read: `src/components/GlobalCursor.jsx`
- Read: `src/components/CursorDot.jsx` (or wherever CursorDot lives)
- Modify: `src/app/layout.jsx` — remove one cursor system
- Modify: survivor component — add idle cleanup

**Step 1: Dispatch analysis to gemini**

Run:
```bash
cd D:/projects/sites/ktg-one && cat src/components/GlobalCursor.jsx | gemini -p "This GlobalCursor component has a perpetual requestAnimationFrame loop (never stops, even when idle). There's also a CursorDot component with 12 DOM elements that stops on idle. Together = 14 cursor DOM elements animating simultaneously.

Produce code that:
1. Picks one system (recommend CursorDot since it has idle cleanup)
2. Adds cancelAnimationFrame cleanup to the RAF loop
3. Shows which file to remove the other cursor from (layout.jsx or ClientLayout.jsx)

Show exact code."
```

**Step 2: Apply and remove duplicate**

**Step 3: Verify** — one cursor system, RAF cancels on unmount

**Step 4: Commit**

```bash
git add src/components/ src/app/layout.jsx
git commit -m "fix: merge dual cursor systems into single with RAF cleanup"
```

---

### Task 3.4: Chat API protection (P2 — SECURITY)

**Files:**
- Modify: `src/app/api/chat/route.js`

**Step 1: Dispatch to gemini**

Run:
```bash
cd D:/projects/sites/ktg-one && cat src/app/api/chat/route.js | gemini -p "This chat API route has zero authentication, no rate limiting, and no input length cap. It forwards messages directly to an AI Gateway. This could be abused to burn API credits.

Add:
1. Input validation: max message length (4000 chars), max messages array length (20)
2. Simple rate limiting: in-memory Map with IP-based 10 req/min window
3. Request size validation

Show the exact modified route.js. Keep it simple — no external packages. This is a portfolio site, not enterprise."
```

**Step 2: Apply**

**Step 3: Verify** — test with curl, confirm rate limit and length validation work

**Step 4: Commit**

```bash
git add src/app/api/chat/route.js
git commit -m "security: add rate limiting + input validation to chat API"
```

---

## Phase 4: Censor Gate — Verify All Fixes

> **LEGIO role:** Censor (Module 11). Claude verifies against original success criteria.

### Task 4.1: Build verification

**Step 1: Run build**

Run: `cd D:/projects/sites/ktg-one && npm run build 2>&1 | tail -30`
Expected: Clean build, no errors

**Step 2: Run lint**

Run: `npm run lint 2>&1 | tail -20`
Expected: Runs successfully (warnings OK, no config errors)

---

### Task 4.2: Audit re-check

**Step 1: Dispatch verification to gemini**

Run:
```bash
cd D:/projects/sites/ktg-one && gemini -p "Re-audit this Next.js project against the original AGENTS.md issues. Check:
- No duplicate Header imports in blog/expertise/validation pages
- No ktg-one.svg references (should be ktg.svg)
- ESLint config exists and lint runs
- lang is en-AU
- Sitemap has hub/expertise/validation routes
- No fs.existsSync in API routes
- GSAP registerPlugin calls have SSR guards
- No in-memoria.db in src/
Report which P0-P1 issues are FIXED vs REMAINING."
```

**Step 2: Document remaining issues**

Any P3-P5 issues not addressed in this plan remain for the next iteration.

---

### Task 4.3: Final commit + push readiness

**Step 1: Review all commits**

Run: `git log --oneline -15`
Expected: Clean commit history with descriptive messages

**Step 2: Do NOT push** — wait for user approval

---

## Phase Summary

| Phase | LEGIO Module | Agent | Tasks | Est. Issues Fixed |
|-------|-------------|-------|-------|-------------------|
| 0 | Imperatus (00) | Claude | 2 | 0 (assessment) |
| 1 | N/A (blocker) | Claude | 2 | 1 (git sync) |
| 2 | Baton (08) | codex-cli | 10 | 16 (mechanical) |
| 3 | Consilium (04) | gemini-cli | 4 | 8 (structural) |
| 4 | Censor (11) | Claude+gemini | 3 | 0 (verification) |
| **Total** | | | **21 tasks** | **~25 issues** |

**Not in this plan (deferred to next iteration):**
- P5 accessibility issues (skip-to-content, keyboard nav)
- Drizzle schema indexes + updated_at
- Dead component deletion (needs dynamic import verification)
- Remaining P4 code quality (useReducer, stable keys, will-change)
- OG image creation (needs actual asset)
- Vercel live promotion (after all fixes verified)
