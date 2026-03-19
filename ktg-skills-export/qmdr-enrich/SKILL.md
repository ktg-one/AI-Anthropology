---
name: qmdr-enrich
description: "3-pass systematic enrichment framework. Use when output needs quality elevation from baseline 60-70% to publication-grade 95-99%. Triggers on research enrichment, gap analysis, depth injection, quality improvement, or when KTG-DIRECTIVE output needs refinement. Deploys 8 expert roles across 6 priorities. Modes: QUICK 80-85%, STANDARD 92-95%, DEEP 97-99%."
---

# QMDR-ENRICH
**Extract • Normalize • Reason • Integrate • Compress • Harmonize**

3-pass quality elevation: 60% → 85% → 99%

## Quick Reference

| Mode | Time | Quality | Priorities Used |
|------|------|---------|-----------------|
| QUICK | 5-10 min | 80-85% | 1, 4 (critical only) |
| STANDARD | 20-30 min | 92-95% | 1, 2, 3 (light), 4 |
| DEEP | 40-60 min | 97-99% | All 1-6 + compression |

## 6 Priorities

| # | Priority | Expert | Detects | Embeds |
|---|----------|--------|---------|--------|
| 1 | **Gaps** | Gap Expert | A→C jumps, undefined terms, missing context | Inline definitions, bridge content |
| 2 | **Depth** | Evidence + Mechanism | Unsupported claims, no "why" | Statistics, sources, mechanism |
| 3 | **Perspective** | Perspective Expert | One-sided, absolutes, no tradeoffs | Counter-views, conditions |
| 4 | **Structure** | Flow Expert | Abrupt shifts, disconnected sections | Bridge sentences, transitions |
| 5 | **History** | History Expert | Arbitrary recommendations, no precedent | Origin stories, validation |
| 6 | **Mission** | Mission Expert | Generic output, user constraints ignored | Context-specific application |

Compression Expert (MLDoE): Removes redundancy, consolidates examples, extracts meta-patterns.

## 3-Pass Execution

### Pass 1: Baseline (60-70%)
```
Execute standard research:
├─ MR.RUG: 3-5 experts per domain
├─ Reasoning: FCoT (nuanced) / CoC (deterministic)
├─ Structure: SoT light
├─ Verification: CoVE-1 (basic)
└─ Output: Functional but gap-heavy
Time: 40-60% of budget
```

### Pass 2: Enrich (85-90%)
```
Priority 1 (Gaps):
├─ Scan line-by-line for jumps, undefined terms
├─ Score severity 1-10, prioritize highest
├─ Embed inline, validate claim stands alone
├─ Cross-check: fix doesn't create new gaps

Priority 2 (Depth):
├─ Identify unsupported claims, missing mechanism
├─ Research evidence (stats, studies, cases)
├─ Explain WHY not just WHAT
├─ Compress: stat + mechanism + example in 1-2 sentences

Priority 4 (Structure):
├─ Find disconnected sections, abrupt shifts
├─ Create bridge: why does B follow A?
├─ Test: read A→Bridge→B, no backtracking needed
Time: 35-45% of budget
```

### Pass 3: Polish (95-99%)
```
Priority 3 (Perspective):
├─ Find one-sided views, absolutes ("always"/"never")
├─ Add tradeoffs, conditions, failure scenarios
├─ Transform: "X is best" → "X when Y, else Z"

Priority 5 (History):
├─ Ground recommendations in precedent
├─ Add origin stories for "best practices"
├─ Validate patterns with real examples

Priority 6 (Mission):
├─ Align to user's actual goal
├─ Embed user constraints (regulatory, technical)
├─ Ensure output is executable by user

Compression (MLDoE):
├─ Remove redundancy from enrichments
├─ Consolidate weak examples
├─ Extract meta-patterns
└─ Target: same pages, 5x density
Time: 15-25% of budget
```

## Quality Gates

| Gate | PASS | FAIL |
|------|------|------|
| **Gap** | Standalone comprehension | Needs background, undefined acronyms, skipped steps |
| **Evidence** | Claims traceable to source, mechanism explained | "It works" without why, stats without context |
| **Perspective** | Benefits AND drawbacks, explicit tradeoffs | Only benefits, absolutes, no conditions |
| **Flow** | Sections naturally follow, no backtracking | Abrupt shifts, isolated sections |
| **History** | Principles grounded in precedent | Arbitrary recommendations, patterns seem timeless |
| **Mission** | Output helps user accomplish goal | Generic answer, user constraints ignored |

**Action on FAIL:** Research → embed → re-test.

## Mode Selection

```
QUICK:      Urgent deadline, breadth over depth
            Skip: P2, P3, P5, P6
            
STANDARD:   Balanced research, most use cases
            Skip: Full P5, P6
            
DEEP:       High stakes, regulated, expert audience
            All priorities + cascading improvements
```

## Integration

```
KTG-DIRECTIVE → generates baseline (60-70%)
QMDR-ENRICH  → elevates to target quality
Output Gate  → routes to delivery format
```

## Cascading Patterns

**Pattern 1:** Definition gap → depth cascade
```
P1: Acronym undefined
P2: Acronym explained but mechanism missing  
P3: Mechanism shown but no alternative comparison
→ Insert once: definition + mechanism + comparison (solves all 3)
```

**Pattern 2:** Structure break → missing history
```
P4: Flow broken between A→B
Why? → B seems arbitrary without history
→ Add history of why B invented (fixes both P4 + P5)
```

**Pattern 3:** Mission goal → multi-priority trigger
```
User: "Present to HIPAA compliance officer"
→ P1: Too high-level for compliance
→ P2: Needs regulatory citations
→ P3: Compliance implications + benefits
→ P5: Historical precedent for approach
→ P6: Execution-ready for officer
```

## Troubleshooting

| Issue | Cause | Solution |
|-------|-------|----------|
| Enrichment creates new gaps | New concept introduced without definition | Embed context immediately or mark out-of-scope |
| Document growing too long | Compression layer not applied | MLDoE pass: consolidate, extract patterns |
| Output doesn't match mission | Missed P6 alignment | Revisit user goal, add context-specific recs |

---
*QMDR-ENRICH v11 | Kevin Tan (ktg.one)*
