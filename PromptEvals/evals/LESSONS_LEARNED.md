# Lessons Learned: Capturing Evaluation Results

## Lost Validation Stamp

**What happened:**
- Got **0.1 percentile** result from Vertex AI (amazing validation!)
- Didn't screenshot it
- Vertex AI changed to Vertex AI Studio
- **All history was lost** - can't recover it

**Impact:**
- Lost proof of top 0.1% performance
- Can't show validation stamp to people
- Can't reference it in papers/presentations

**Lesson:**
- **Platforms change** - history gets wiped
- **Only screenshots survive** - everything else can disappear
- **Capture immediately** - don't assume you'll remember or can find it later

---

## Rules Going Forward

1. **See results → Screenshot immediately** (within seconds)
2. **Copy exact scores** - don't trust memory
3. **Save to `evals/results/`** - use template
4. **Never assume** platforms will keep history
5. **Treat every result as ephemeral** - capture it or lose it

---

## What We Lost

- **0.1 percentile from Vertex AI** - Top 0.1% performance validation
- **Date**: Before Vertex AI Studio migration
- **Impact**: Can't prove this achievement anymore

**This won't happen again** - system is now in place to capture everything immediately.

