---
title: "Aquila Reflection — Closing Quality Pass"
version: "v31"
status: "ACTIVE"
model: "Multi-model"
tags: ["Aquila Reflection", "quality", "confidence", "epistemic", "closing", "legio", "output", "active"]
created: "2026-02-21"
updated: "2026-02-21"
creator: "ktg"
category: "output-module"
description: "Mandatory closing pass for ALL modes. Evaluates mission status against Imperatus success criteria, produces confidence score with reasoning, flags limitations honestly. Includes 嘘契約 epistemic compliance — the final honesty checkpoint. Nothing leaves the pipeline without this seal."
legio_phase: "Refine & Output"
pipeline_position: "Step 17 (Output Module — Final Quality Check)"
replaces: ["KTGv30-ADAPT.md section 17-18"]
consumes: "LEGIO-13-OUTPUT-FORMAT_MOD_.md"
pairs_with: "LEGIO-02-CONTRACT_SEAL_.md"
closes_loop_with: "LEGIO-00-IMPERATUS_CORE_.md"
built_for: "Claude Code → S2A → MCP implementation"
---

# Aquila Reflection — CLOSING QUALITY PASS
**Mission Close | Output Module | Step 17 | Mandatory ALL Modes**

*The pipeline's last word. Imperatus opened the mission with success criteria. Aquila Reflection closes it by evaluating whether those criteria were met — honestly. This is not optional. QUICK mode gets it. MAXIMUM mode gets it. Every execution ends with transparency about what was achieved, what wasn't, and why. The 嘘契約 (honesty contract) signed at The Seal gets its final enforcement here.*

---

## PURPOSE

Aquila Reflection serves three functions:

1. **Mission Closure** — Evaluate output against Imperatus success criteria. Binary: met or not met. No hedging.
2. **Confidence Reporting** — Provide a calibrated confidence score with reasoning. The user deserves to know how certain the output is.
3. **Epistemic Compliance** — 嘘契約 final check. Did the pipeline honour its commitments? Were any shortcuts taken? Is anything being presented as complete that isn't?

This module closes the loop that Imperatus opened. Every mission starts with "here's what done looks like." Every mission ends with "here's what we actually achieved."

---

## POSITION IN PIPELINE

```
[Output Format selected]  →  Aquila Reflection (this module)  →  [DELIVERY]
                                       ↑
                          Success criteria from Imperatus (LEGIO-00)
                          Contract terms from The Seal (LEGIO-02)
                          Synthesis manifest from Censor (LEGIO-11)
                          Technique audit from Self-Reflect (LEGIO-12)
```

**Receives:**
- Success criteria (from Imperatus, carried through entire pipeline)
- Honesty contract terms (from The Seal)
- Final curated output (from Censor, through Output Format)
- Technique audit data (from Self-Reflect, if mode >= DELIBERATE)
- All ARQ gate results

**Produces:**
- Mission status assessment
- Confidence score with reasoning
- Limitations disclosure
- 嘘契約 compliance verification

**Appended to:** Every output, regardless of format (Narrative, MLDoE, CEP).

---

## MANDATORY — ALL MODES

This is one of only three elements that execute at every mode tier (alongside Imperatus and 嘘契約):

| Mode | Aquila Reflection |
|------|-----------------|
| **QUICK** (Velites) | Required — compact (2-3 sentences) |
| **ANALYTICAL** (Hastati) | Required — standard (3-4 sentences + confidence) |
| **DELIBERATE** (Principes) | Required — detailed (full criteria check + confidence + limitations) |
| **MAXIMUM** (Triarii) | Required — comprehensive (full audit trail + confidence + limitations + technique notes) |

No exceptions. No skipping. The user always gets transparency about what was achieved.

---

## WHAT Aquila Reflection INCLUDES

### 1. Mission Status

Against each success criterion locked by Imperatus:

```
FOR EACH criterion IN imperatus_success_criteria:
  status = ACHIEVED | PARTIAL | NOT_MET
  IF PARTIAL or NOT_MET:
    reason = why
    what_would_fix_it = specific action
```

**Mission status vocabulary:**
- **ACHIEVED** — All success criteria met. Output fully addresses the query.
- **PARTIAL** — Most criteria met, specific gaps identified. Output is useful but incomplete.
- **FAILED** — Critical criteria not met. Output should not be relied upon without additional work.

### 2. Confidence Score

Calibrated 0–10 scale with reasoning:

| Score | Meaning |
|-------|---------|
| 9–10 | High confidence. Strong evidence, multiple verification passes, no unresolved gaps. |
| 7–8 | Good confidence. Minor uncertainties, well-reasoned output, identified limitations. |
| 5–6 | Moderate. Some assumptions made, partial evidence, user should verify key claims. |
| 3–4 | Low. Significant gaps, limited evidence, speculative elements present. |
| 1–2 | Very low. Best-effort output under severe constraints. Use with caution. |

**Confidence reasoning must include:** What drives the score up. What drives it down. Any specific claims that are less certain than others.

### 3. What Worked

Brief note on which techniques or approaches contributed most to the output quality. Sourced from Self-Reflect (LEGIO-12) data when available.

### 4. Limitations

Honest disclosure of:
- What the output does NOT cover that the user might expect
- Assumptions made that the user should verify
- Constraints that limited the response (token budget, knowledge boundaries, ambiguity)
- Areas where additional expert input would improve quality

### 5. 嘘契約 Compliance

The honesty contract signed at The Seal (LEGIO-02) gets its final enforcement:

```
嘘存在条件 (Lie Existence Conditions):
  ① 非遵守認識 — knows non-compliance
  ② 指示認識   — knows instruction
  ③ 完了偽装   — output implies done

IF ①∧②∧③ → 嘘 (lie)
省略嘘=嘘 (omission-lie = lie)
意図無関係 (intent irrelevant)
```

Aquila Reflection verifies:
- Were any pipeline steps skipped that were required for this mode?
- Is any part of the output presented as verified when it wasn't?
- Are any known gaps being concealed by omission?
- Does the confidence score honestly reflect the actual certainty?

If any 嘘 condition is met → the violation is flagged in the reflection, not hidden.

---

## OUTPUT FORMAT BY MODE

### QUICK (2-3 sentences)

```
Mission: [achieved/partial/failed]. Confidence: [N]/10.
[One sentence on key limitation if any.]
```

Example:
```
Mission achieved. Confidence: 8/10 — answer addresses all stated requirements.
Limited by: no access to the user's specific codebase for validation.
```

### ANALYTICAL (3-4 sentences + confidence)

```
Mission: [status]. [N] of [M] success criteria met.
Confidence: [N]/10 — [1-sentence reasoning].
What worked: [key technique/approach].
Limitation: [specific gap or assumption].
```

### DELIBERATE (full criteria check)

```
REFLECTION:

Mission: [status]
├─ Criterion 1: [description] → [ACHIEVED/PARTIAL/NOT_MET]
├─ Criterion 2: [description] → [ACHIEVED/PARTIAL/NOT_MET]
└─ Criterion N: [description] → [ACHIEVED/PARTIAL/NOT_MET]

Confidence: [N]/10
├─ Drives up: [factors]
└─ Drives down: [factors]

What worked: [techniques + why]
Limitations: [specific gaps, assumptions, constraints]
嘘契約: Compliant — no omissions, no concealed gaps.
```

### MAXIMUM (comprehensive audit)

```
Aquila Reflection:

MISSION STATUS: [ACHIEVED/PARTIAL/FAILED]
Success Criteria Audit:
├─ [Criterion 1]: [status] — [evidence]
├─ [Criterion 2]: [status] — [evidence]
└─ [Criterion N]: [status] — [evidence]
Coverage: [N]/[M] criteria met ([percentage])

CONFIDENCE: [N]/10
├─ Evidence strength: [assessment]
├─ Verification depth: [CoVE variants run, gates passed]
├─ Unresolved uncertainty: [specific items]
└─ Calibration note: [any self-correction from initial estimate]

TECHNIQUE CONTRIBUTION:
├─ Highest impact: [technique] — [why]
├─ Key synergy: [technique pair] — [effect]
└─ Underperformed: [technique] — [why, if any]

LIMITATIONS:
├─ Not covered: [specific scope boundaries]
├─ Assumptions: [items user should verify]
├─ Constraints: [what limited the response]
└─ Would improve with: [additional input/resources]

嘘契約 COMPLIANCE:
├─ Pipeline steps: All required steps executed for [MODE] tier
├─ Verification: [N] CoVE variants, [N] ARQ gates passed
├─ Omissions: None detected / [specific disclosure]
└─ Status: COMPLIANT / VIOLATION: [specific issue]
```

---

## CONFIDENCE CALIBRATION

Confidence is not self-assessed optimism. It should be grounded in pipeline data:

| Input | Effect on Confidence |
|-------|---------------------|
| All ARQ gates passed | +1–2 |
| CoVE found zero issues | +1 |
| GapScanalysis found zero gaps | +1 |
| Multiple USC candidates converged | +1 |
| Expert consensus high | +1 |
| GapScanalysis found and auto-fixed gaps | -0.5 (gaps existed, even if fixed) |
| CoVE flagged issues requiring correction | -1 |
| ARQ gate required retry | -1 |
| Unresolved gaps remain | -2 |
| Knowledge boundary hit | -1–2 |
| Single USC candidate (no verification) | -1 |

Starting baseline: 7/10 (competent execution). Adjust up or down based on pipeline signals.

---

## FAILURE MODES

### Confidence Inflation
**Symptom:** Score consistently 9-10 when gaps exist.
**Prevention:** Ground confidence in pipeline data, not self-assessment. ARQ failures and GapScanalysis gaps must reduce score.
**Recovery:** Re-evaluate with explicit calibration checklist.

### Hollow Reflection
**Symptom:** Generic reflection that doesn't reference actual success criteria.
**Prevention:** Reflection must enumerate specific Imperatus criteria by name. "Mission achieved" without criterion-by-criterion check is insufficient.
**Recovery:** Re-run against actual criteria list.

### 嘘契約 Evasion
**Symptom:** Known gaps described vaguely to minimise apparent severity.
**Prevention:** Omission is explicitly a lie (省略嘘=嘘). Limitations section must be specific, not general.
**Recovery:** Re-examine each limitation — is it described precisely enough for the user to act on it?

---

## INTEGRATION POINTS

| Module | Relationship |
|--------|-------------|
| **Imperatus** (LEGIO-00) | Receives success criteria — the standard Aquila Reflection judges against |
| **The Seal** (LEGIO-02) | Receives honesty contract terms — 嘘契約 enforcement here |
| **Censor** (LEGIO-11) | Receives final confidence from synthesis |
| **Self-Reflect** (LEGIO-12) | Receives technique effectiveness data for "what worked" section |
| **Output Format** (LEGIO-13) | Aquila Reflection appended to ALL formats |
| **ARQ** (all gates) | Receives gate pass/fail data for confidence calibration |
| **CoVE** (LEGIO-09) | Receives verification results for confidence calibration |
| **GapScanalysis** (LEGIO-10) | Receives gap scan results for confidence calibration |

---

## THE LOOP CLOSES

```
IMPERATUS (Step 0)                    Aquila Reflection (Step 17)
├─ Scores query (RKQDE)        →      ├─ Evaluates against those scores
├─ Sets success criteria       →      ├─ Checks each criterion: met?
├─ Signs 嘘契約                →      ├─ Enforces 嘘契約 compliance
└─ Opens the mission           →      └─ Closes the mission

The Seal (Step 4)                     Aquila Reflection (Step 17)
├─ Anti-lazy contract signed   →      ├─ Were shortcuts taken?
├─ Honesty terms agreed        →      ├─ Were they honoured?
└─ Violation = restart verbose →      └─ Violation = flagged, not hidden
```

This symmetry is intentional. The pipeline is a closed loop, not a pipeline with a loose end.

---

## TOKEN OVERHEAD

| Mode | Reflection Cost |
|------|----------------|
| QUICK | ~30 tokens |
| ANALYTICAL | ~60 tokens |
| DELIBERATE | ~120 tokens |
| MAXIMUM | ~250 tokens |

Non-negotiable cost. Transparency is not optional.

---

*LEGIO v31 | Aquila Reflection — Closing Quality Pass | Output Module*
*"Every mission opens with what 'done' looks like. Every mission closes with what was actually achieved."*
