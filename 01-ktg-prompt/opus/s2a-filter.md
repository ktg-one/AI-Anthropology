# S2A Filter Stage (Claude-Specific)

## Purpose

Strip noise before PDL extraction. Claude tends to include hedging, process narration, and pleasantries in context—S2A removes this before compression begins.

## When to Apply

- **Always** before CEP compression
- Run in **extended thinking** (Opus) or **silently** (Sonnet)
- Output is `filtered_context[]`, not shown to user

## Filter Rules

### KEEP (→ filtered_context)

| Category | Examples | Why Keep |
|----------|----------|----------|
| **Explicit decisions** | "We decided to use JWT", "The approach is X" | Core knowledge |
| **Definitions introduced** | "CEP = Context Extension Protocol" | Vocabulary |
| **Facts with sources** | "Grok achieves 10/10 at 200K tokens" | Evidence |
| **Constraints stated** | "Must fit in 32K context", "Budget is $500" | Boundaries |
| **Code/artifacts produced** | Functions, JSON schemas, configs | Deliverables |
| **Errors + resolutions** | "This failed because X, fixed by Y" | Lessons |
| **User preferences** | "I prefer minimal formatting" | Personalization |
| **Confidence markers** | "High confidence", "8/10" | Quality signals |

### DISCARD (→ noise)

| Category | Examples | Why Discard |
|----------|----------|-------------|
| **Pleasantries** | "Thanks!", "Great question" | No information |
| **Hedging** | "I think maybe...", "It's possible that..." | Low confidence = noise |
| **Process narration** | "Let me think about this...", "First I'll analyze..." | Meta, not content |
| **Redundant confirmations** | "Yes, that's correct", "Exactly" | No new information |
| **Failed attempts** | Unless lesson learned | Clutter |
| **Apologies** | "Sorry for the confusion" | Social, not informational |
| **Filler phrases** | "In other words", "To put it simply" | Restatements |

## Implementation (Claude)

### Opus (Extended Thinking)

```
<thinking>
S2A FILTER EXECUTING...

SCANNING conversation for:
- Decisions: [list]
- Definitions: [list]
- Facts: [list]
- Constraints: [list]
- Artifacts: [list]
- Errors+Resolutions: [list]

DISCARDING:
- Pleasantries: [count] instances
- Hedging: [count] instances
- Process narration: [count] instances

FILTERED_CONTEXT size: ~[X] tokens (down from ~[Y])
S2A reduction: [Z]%

Proceeding to Phase 1 with filtered_context only.
</thinking>
```

### Sonnet (Silent)

Sonnet doesn't have extended thinking in the same way—run S2A as first internal step, don't output, proceed directly to RKQDE.

## Quality Check

After S2A, verify:

```
FILTERED_CONTEXT_VALIDATION:
  ✓ At least 1 decision preserved
  ✓ At least 1 definition preserved (or N/A if genuinely none)
  ✓ Core facts retained
  ✓ No pleasantries remaining
  ✓ No process narration remaining
  
IF validation fails:
  → Re-run S2A with stricter/looser filter
  → Document filter adjustment in L4 metacognitive
```

## Edge Cases

### Conversation is mostly hedging

```
IF >80% of conversation is hedging/uncertainty:
  → Flag: "Low-confidence session"
  → Preserve hedging in L4 as "session_fingerprint.key_tension"
  → Don't compress to 0.15—preserve uncertainty markers
```

### User explicitly wants process preserved

```
IF user said "I want to see your reasoning":
  → Keep process narration in L3 (reasoning_archetypes)
  → Tag: "process_preserved_by_request"
```

### Very short conversation

```
IF conversation < 10K tokens:
  → S2A may remove too much
  → Lighter filter: keep more context
  → Target ratio can be 0.20-0.25 instead of 0.15
```

## Metrics

Track in compression_stats:

```json
{
  "s2a_reduction": "35%",
  "noise_categories_removed": [
    "pleasantries: 12 instances",
    "hedging: 8 instances",
    "process_narration: 15 instances"
  ],
  "filtered_context_tokens": 117000,
  "original_tokens": 180000
}
```

## Why This Matters for Claude

Claude (especially Sonnet) tends to include process narration and hedging to appear thoughtful. This inflates context without adding information. S2A strips this before compression, ensuring PDL layers contain only signal, not noise.

**Result**: Same 0.15 compression ratio captures more actual information because we're compressing signal, not signal+noise.
