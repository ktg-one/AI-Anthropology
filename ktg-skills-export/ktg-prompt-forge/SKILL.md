---
name: ktg-prompt-forge
description: Boost prompts for other models by embedding KTG-DIRECTIVE techniques. Use when crafting prompts for GPT, Gemini, Llama, Qwen, or any LLM. Applies technique gate checklist based on R/K/Q assessment, injects missing structures. Single-pass, sparse output.
---

# KTG-PROMPT-FORGE
**Embed Techniques Into Prompts**

Target models can't self-apply—bake techniques into the prompt.

## Quick Assessment

Score the task (1-10):
- **R** (Reasoning complexity)
- **K** (Knowledge requirements)  
- **Q** (Quality stakes)

Route:
```
QUICK:      R≤3 ∧ Q≤5
ANALYTICAL: R=4-6 ∨ Q=6-7
DELIBERATE: R≥7 ∨ K≥6 ∨ Q≥8
MAXIMUM:    R≥9 ∨ K≥8
```

## Technique Gate by Mode

### PRE-FLIGHT

| Technique | QUICK | ANALYTICAL | DELIBERATE | MAXIMUM |
|-----------|-------|------------|------------|---------|
| ARQ (quality questions) | Pre-turn | Pre-turn | Pre+Post | Full |
| Anti-Lazy | O | R | R | R (enforced) |
| USC (candidates) | 1-path | 2 | 3 | 5 + meta |
| Success Lock | Implicit | Explicit | Signature | Multi-constraint |

### PIPELINE

| Technique | QUICK | ANALYTICAL | DELIBERATE | MAXIMUM |
|-----------|-------|------------|------------|---------|
| Structure | Direct | SkeleTrain light | SkeleTrain full | GoT/Deep |
| Expert Role | X | Specialist | Full team | Swarm |
| Prompt Bombs | Clarifier | +Scaffold | Full arsenal | Deep inject |

### EXECUTE

| Technique | QUICK | ANALYTICAL | DELIBERATE | MAXIMUM |
|-----------|-------|------------|------------|---------|
| Reasoning | CoC | FCoT | FCoT+ARQ | Mix+ARQ |
| Execution | Direct | Baton | Baton+ARQ | Swarm+ARQ |
| Verification | X | Top-1 CoVE | Top-2 CoVE | All variants |
| Gap Scan | X | Light | 3-branch | Deep+fix |

### OUTPUT

| Technique | QUICK | ANALYTICAL | DELIBERATE | MAXIMUM |
|-----------|-------|------------|------------|---------|
| Curation | Lean/dense | Normal | Normal+nuance | Comprehensive |
| Synthesis | X | Light coherence | Cross-branch | Meta-synthesis |
| Reflect | X | What worked? | Technique audit | Full meta |

## Injection Templates

### Success Lock
```
COMPLETE WHEN:
- [ ] [Criterion 1]
- [ ] [Criterion 2]
Do not stop until ALL checked.
```

### ARQ Embed
```
BEFORE RESPONDING:
1. [Domain quality question]?
2. [Domain quality question]?
3. [Domain quality question]?
Proceed only when all YES.
```

### Anti-Lazy (Enforced)
```
REQUIREMENTS:
- Complete, production-ready
- No placeholders, no stubs, no "...rest here"
- No truncation—finish everything
- Long output is fine—don't stop early
```

### Role + Standards
```
You are [ROLE] expert in [DOMAIN].
Standards:
- [Standard 1]
- [Standard 2]
Reject violations.
```

### USC Embed
```
Generate [N] distinct approaches.
Compare for consistency.
Select best OR synthesize.
Explain selection.
```

### CoVE Embed
```
After drafting, verify:
- FACTUAL: Are claims accurate?
- LOGICAL: Does reasoning hold?
- COMPLETE: Any gaps?
Revise if any fail.
```

## ENRICH Protocol (Optional)

For high-stakes (Q≥8), embed iterative refinement:

```
ENRICHMENT PROTOCOL:
Pass 1: Generate baseline
Scan: GAPS → DEPTH → PERSPECTIVES → POLISH
Pass 2: Address gaps + depth
Pass 3: Final perfection

CRITERIA: Zero gaps. Zero doubt. 100% thorough.
Do not stop until criteria met.
```

## Output Format

```
BOOSTED PROMPT:
[Enhanced prompt]

MANIFEST:
Mode: [QUICK/ANALYTICAL/DELIBERATE/MAXIMUM]
[x] Success Lock
[x] ARQ: [questions]
[x] Anti-Lazy
[ ] USC: [not needed / N candidates]
[x] Role: [expert type]
[ ] CoVE: [variant]
Target: [model]
```

Single pass. No iteration on Claude's side.

---
*KTG-PROMPT-FORGE v1 | Kevin Tan (ktg.one)*
