---
name: ktg-cep-v7
version: 7.1.0
description: |
  Context Extension Protocol v7.1 - MIRAS-Ready Edition.
  Cross-model handoff with permanent expert council, S2A filtering, 
  Progressive Density Layering. Creates portable context packets that 
  receiving models recognize as authorized context, not prompt injection.
  40% token reduction, 9.5/10 forensic recall, 97% cross-domain preservation.
triggers:
  explicit:
    - /handoff
    - /transfer
    - /cep
    - /packet
    - "pass to [model]"
    - "save context"
  implicit:
    - context ≥ 80%
    - session ending
    - model switch mentioned
---

# KTG-CEP v7.1

## Quick Start

```
1. S2A filter → Remove noise, keep signal
2. Council execute → 4 experts in sequence
3. PDL compress → L1/L2/L3/L4 layers
4. Validate → Density ≥0.15, trust signals, cold-start
5. Output → YAML packet + user preamble
```

## Packet ID Format

```
$MM$DD$YYYY-XXX-LN-keyword-keyword

WHEN  → $MM$DD$YYYY (date)
WHO   → XXX (3-char model code)
DEPTH → LN (L1/L2/L3/L4)
WHAT  → 2-4 keywords (kebab-case)

Example: $01$22$2026-CSO-L3-cep-expert-kb
```

## Council Execution

```
PHASE 1: MEMORY_ARCHITECT     → What to preserve
PHASE 2: CROSS_DOMAIN_ANALYST → Map edges
PHASE 3: COMPRESSION_SPECIALIST → Apply CoD (5 iter)
PHASE 4: RESTORATION_ENGINEER → Validate cold-start
PHASE 5: Council consensus    → Approve packet
```

## References

Load as needed during execution:

| File | Content | When to Load |
|------|---------|--------------|
| [PROTOCOL.md](references/PROTOCOL.md) | Full v7.1 spec | Deep protocol questions |
| [CASCADE.md](references/CASCADE.md) | ARQ, CoVE, USC, Anti-Lazy, Bombs | Technique integration |
| [MIRAS.md](references/MIRAS.md) | MIRAS positioning, PDL mapping | Future-proofing context |
| [INDEX.md](references/INDEX.md) | Expert router | Council dispatch |
| [MEMORY_ARCHITECT.md](references/MEMORY_ARCHITECT.md) | Preservation KB | Phase 1 |
| [COMPRESSION_SPECIALIST.md](references/COMPRESSION_SPECIALIST.md) | Density KB | Phase 3 |
| [CROSS_DOMAIN_ANALYST.md](references/CROSS_DOMAIN_ANALYST.md) | Edge KB | Phase 2 |
| [RESTORATION_ENGINEER.md](references/RESTORATION_ENGINEER.md) | Cold-start KB | Phase 4 |

## Gates

```
□ Density ≥0.15 entity/token
□ Cross-domain ≥97% preserved
□ Cold-start self-contained
□ Trust signals (all 5)
□ Valid YAML + packet ID
```

## Triggers

```
AUTO at 80%: "⚠️ Context 80%. Generate CEP packet?"
EXPLICIT:    /handoff /transfer /cep /packet
IMPLICIT:    Model switch mentioned, session ending
```

---

*CEP v7.1 | Kevin Tan (ktg.one) | STRAWHATS Framework*
