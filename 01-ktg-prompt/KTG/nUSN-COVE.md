**L5: VERIFY_10R** (ADVANCED) - CoVE + USC + Negentropy

┌─ STEP 1: USC CANDIDATES ────────────────────┐
│ Generate N candidates per mode:             │
│ ANALYTICAL=2 | DELIBERATE=3 | MAXIMUM=5     │
│ Each uses different expert config           │
└─────────────────────────────────────────────┘

┌─ STEP 2: CoVE PER CANDIDATE ────────────────┐
│ Auto-select variants by problem:            │
│ ├─ FACTUAL: claims>10 ∨ K≥6                 │
│ ├─ LOGICAL: chains>5 ∨ R≥7                  │
│ ├─ CONSISTENCY: nodes≥5 (SkeleTraIn used)   │
│ └─ MULTI_EXPERT: experts≥3 (conflicts)      │
│                                             │
│ Mode depth:                                 │
│ ANALYTICAL=top-1 | DELIBERATE=top-2 | MAX=all│
└─────────────────────────────────────────────┘

┌─ STEP 3: 10R EPISTEMIC SCAN ────────────────┐
│ Per candidate score (0-20):                 │
│                                             │
│ CORE 5 (required):                          │
│ ├─ Reasonable: confidence ∝ evidence?       │
│ ├─ Relevant: answers actual question?       │
│ ├─ Respectful: alternatives informative?    │
│ ├─ Responsive: engages counters directly?   │
│ └─ Regulated: no affect driving reasoning?  │
│                                             │
│ DEEP 5 (tie-breaker):                       │
│ ├─ Rational: premises → conclusion valid?   │
│ ├─ Realistic: matches actual behavior?      │
│ ├─ Reciprocal: symmetric standards?         │
│ ├─ Repair-Oriented: reduces confusion?      │
│ └─ Responsible: acknowledges consequences?  │
│                                             │
│ SCORING: ✅=2 ⚠️=1 ❌=0                       │
│ ≥14 TRUST | 10-13 PATCH | <10 REWORK        │
└─────────────────────────────────────────────┘

┌─ STEP 4: SELECTION ─────────────────────────┐
│ Highest 10R score wins                      │
│ Tie: Synthesize IFF non-redundant + entropy↓│
│ All <12: Flag "epistemically unstable"      │
└─────────────────────────────────────────────┘

┌─ STEP 5: NEGENTROPY GATE ───────────────────┐
│ Output uncertainty < Input uncertainty?     │
│ YES → proceed                               │
│ NO → simplify or flag gaps                  │
│                                             │
│ Fail-closed: ≥3 Core + ≥2 Deep missing      │
│ → DISENGAGE/REWORK                          │
└─────────────────────────────────────────────┘