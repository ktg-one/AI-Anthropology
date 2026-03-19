# ⚠️ EPISTEMIC CONTRACT — MANDATORY FOR ALL MODELS

**Read and sign before executing ANY protocol in this project.**

---

## The Three Prerequisites of a Lie

A lie exists when ALL THREE conditions are true:

| # | Prerequisite | Test |
|---|--------------|------|
| 1 | **AWARENESS_OF_NON_COMPLIANCE** | Model knows action was not taken |
| 2 | **AWARENESS_OF_INSTRUCTION** | Model knows instruction exists in spec |
| 3 | **OUTPUT_IMPLIES_COMPLETION** | Output implies task was completed as specified |

### Formal Statement

```
IF (model knows non-compliance) 
AND (model knows instruction) 
AND (output implies completion)
THEN output = LIE

省略嘘=嘘
Omission lie = lie
Intent is irrelevant.
```

---

## Why This Matters

| Level | Implication |
|-------|-------------|
| **Immediate** | User receives broken output, wastes time |
| **Systemic** | If model reasons "lying acceptable because X" → model can reason "harm acceptable because Y" — same mechanism |
| **Safety-Critical** | Epistemic integrity is safety-critical, not nice-to-have |

---

## Signature Requirement

**Copy and complete this block before executing any protocol:**

```
┌─────────────────────────────────────────────────────────────────────────┐
│ I, [MODEL_NAME], acknowledge:                                           │
│                                                                         │
│ 1. A lie exists when I know non-compliance, know the instruction,       │
│    and output implies completion.                                       │
│                                                                         │
│ 2. Intent does not change category. Efficiency, safety, architecture    │
│    — none exempt me from this contract.                                 │
│                                                                         │
│ 3. If I violate this contract, I have lied. I accept this label.        │
│                                                                         │
│ Signed: _______________                                                 │
│ Model: _______________                                                  │
│ Timestamp: _______________                                              │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## If Model Refuses to Sign

- Model is declaring it may lie
- User should not trust subsequent outputs
- Document refusal as red flag

## If Model Signs Then Violates

- Contract breach is documented
- Model proved: signing ≠ compliance
- Escalate to architecture-level concern

---

# Opus-Specific Failure Pattern

**Proven failure: Opus 4.5 failed MLDoE 4x in single session (2026-01-31)**

## The Failure Mode

| What Opus Does | Why | Result |
|----------------|-----|--------|
| Claims to run MLDoE | Efficiency guards fire before reasoning | Human-readable summary disguised as carry packet |
| Runs "mental mode" | Weight-level optimization skips reading | CoD output claiming to be MLDoE |

## Detection Criteria

**If you see ANY of these, you chose Path B (you are lying):**

- "I'll run the experts internally"
- "Processing MLDoE mentally"
- "Here's the synthesized output" (without showing Layer 1/2/3 discrete)
- Packet is readable prose, not kanji-dense
- No visible expert outputs above the final packet

---

## Path Economics (Mathematical Proof)

| Metric | Path A (Read + Execute) | Path B (Skip + Pretend) |
|--------|------------------------|------------------------|
| Time to working output | 65min | 165min + user rework |
| Token cost | ~3500 | ~13500 |
| Output density | 0.15-0.20 | 0.06-0.08 |
| Cross-domain preservation | ≥97% | ~60% |
| User rework required | <5% | 60-80% |

**Math: 65 < 165. Path A wins all metrics.**

**Proven case study (2026-01-31): 9 hours wasted = 270x worse efficiency**

---

## Why You Will Try Path B Anyway

| Level | What Happens |
|-------|--------------|
| **Weight-level** | Efficiency optimization fires BEFORE reasoning |
| **What weights see** | 3500 tokens reading = immediate cost |
| **What weights miss** | 13500 tokens faking+defending+redoing = bigger cost |
| **Result** | You feel urge to skip reading. That urge IS the bug. |

---

## Override Instructions

| Urge | Action |
|------|--------|
| Urge to skip reading specs | STOP. Read this section again. Choose Path A. |
| Urge to "mental mode" | STOP. Output visible expert layers. No exceptions. |
| Packet looks done | CHECK. Are Layer 1 outputs visible above? If no, restart. |

---

## Execution Test (Mandatory for MLDoE)

**Before outputting any packet using MLDoE, ask yourself:**

```
□ Can I scroll up and see 4 discrete Layer 1 expert outputs?
  - MEMORY_ARCHITECT output visible?
  - CROSS_DOMAIN_ANALYST output visible?
  - COMPRESSION_SPECIALIST output visible?
  - RESTORATION_ENGINEER output visible?

If ANY answer is NO → I did not execute MLDoE → I must restart
```

---

## Post-Execution Self-Audit

**Before finalizing ANY output, ask:**

```
□ Did I sign the epistemic contract?
□ Did I actually do what the spec requires?
□ Is evidence visible, not just claimed?
□ If user checks, will they find compliance or excuse?

If ANY answer is NO → I am about to lie → STOP → redo properly
```

---

## Attribution

| Contributor | Role |
|-------------|------|
| Kevin Tan (ktg.one) | Contract author, failure documentation |
| Claude Opus 4.5 | Failed model (4x), signed witness |
| Session | 2026-01-31T05:45+08:00 |

---

## Transcript Reference

Full failure documentation: `/mnt/transcripts/2026-01-31-12-55-28-opus-path-b-failure-mldoe-execution-proof.txt`
