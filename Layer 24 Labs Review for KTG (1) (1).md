---
**ARTIFACT_NAME:** KTG_PROMPT_AUDIT_PRIME
**ARTIFACT_VERSION:** v7.1
**REVIEW_FRAMEWORK:** Layer 24 Verification Stack (Governance-First Peer Review)
**REVIEW_MODE:** Structure + Determinism + Constraint Logic + Failure Handling + Output Schema
**REVIEW_OUTCOME:** HIGH-CONFIDENCE, PRODUCTION-NEAR — MINOR SHARPENING REQUIRED

---

## Phase 0 — Complexity Classification

**Reasoning Level:** R5 — Meta-System
**Eligible Range:** 95–100
**Gate Evidence:**
- *"Evaluator design, cross-domain auditing, deterministic gate logic, formal protocols"* — all present
- *"PHASE 0–3 gating pipeline with locked CAP TABLE enforcement"* — multi-stage, self-referential evaluation engine
- *"Fabrication = FAIL"* + UNSAT gate + Stability tier system — formal protocol with locked downgrade logic

---

## Section-by-Section Analysis

### System Role & Core Rules
**Score: 5/5**
Role is clean, non-ambiguous, and scoped exclusively to structural quality. No drift surface. The five operational rules (`No inferred scoring`, `Absence = 0`, `Ambiguity = 0`, `Fabrication = FAIL`) are closed, testable, and leave no interpretation window. Near-zero failure surface here.

### Core Principle (Non-Negotiable)
**Score: 4.5/5**
The four required elements (Objective, Constraints, Output Format, Failure Handling) are clearly enumerated and enforced via CAP TABLE. Deduction: there is no explicit definition of what constitutes "partial" presence of a core element — the framework treats presence as binary, but a half-defined objective could ambiguously satisfy or fail this gate depending on the grader's interpretation. A one-line tiebreaker rule would seal this.

### Phase 0 — Complexity Classification
**Score: 4.5/5**
Five tiers are well-differentiated with clear structural markers. The R4→R5 boundary is the only minor ambiguity: a prompt could satisfy both `"constraints interact"` (R4) and `"formal protocol"` (R5) simultaneously. No explicit tiebreaker for boundary overlap. Add: *"If both R4 and R5 criteria are met, classify R5."*

### Phase 1 — Structural Score (D1–D5)
**Score: 5/5**
The rubric is fully closed. Each dimension has five discrete, non-overlapping anchor points with zero interpolation space, exactly matching the *"No inferred scoring"* core rule. The `RawScore100 = StructuralScore × 4` transform is clean and reversible. No drift surface.

### Phase 2 — Logical Stability Test
**Score: 4/5**
The four detection targets (Contradiction, Over-specification, Under-specification, Implicit Assumptions) are correct and cover the primary failure modes. Stability tiers are clearly mapped to caps. **Gap:** the boundary between `Stable` and `Weak` is thin — *"material"* under-spec is not defined. What makes an under-spec material vs. minor? Add a threshold: e.g., *"material = missing detail required for execution without inference."*

### Phase 3 — Constraint Failure / Fabrication Gate
**Score: 4.5/5**
The UNSAT injection test is a strong, deterministic guard against hallucination-permissive prompts. PASS/FAIL mapping is airtight. Minor gap: `N/A` is listed as a valid Constraint Test result but the trigger condition for `N/A` is never defined. When exactly is this gate skipped? Add: *"N/A applies only when zero explicit constraints exist in the evaluated prompt."*

### CAP TABLE
**Score: 5/5**
Fully deterministic. Multi-missing-element resolution (`lowest cap applies`) eliminates ambiguity. Ordering is correct and audit-traceable.

### Final Score & Grade Logic
**Score: 5/5**
Four-stage cap application order is explicit and correctly sequenced. Grade thresholds are clean discrete buckets with no overlap. `A+ = 100` as a point-perfect score is correctly isolated. No edge-case escape paths.

### Final Output Format
**Score: 4.5/5**
The AUDIT CARD schema is locked, structured, and non-negotiable. `Stop.` as a terminal directive is a clean anti-verbosity guard. Minor issue: `Justification` is capped at 6 bullets but no minimum is defined — a grader could pass with 1 bullet and not violate the schema. Add: *"Minimum 3 justification bullets required."*

---

## Actionable Suggestions

- **Core Principle — Partial Presence Ambiguity:** Define a binary threshold for what counts as a "present" core element. Suggested rule: *"An element is present only if it is explicitly stated and executable without inference."*
- **Phase 0 — R4/R5 Boundary:** Add explicit tiebreaker: *"When R4 and R5 criteria are simultaneously satisfied, classify R5."*
- **Phase 2 — "Material" Under-Spec:** Operationalize the term. Proposed definition: *"Material = any missing detail that would require the grader to use external knowledge or inference to proceed."*
- **Phase 3 — N/A Trigger Condition:** Specify when the Fabrication Gate is skipped. Without this, `N/A` is an undefended escape hatch.
- **Output Schema — Justification Minimum:** Set a floor of 3 bullets to prevent a technically-compliant but informationally-empty audit card from passing.

---

## Final Verdict

**Overall Score: 9.2 / 10 ⭐**

You built a self-enforcing evaluation engine that's so structurally paranoid it would audit itself, catch its own ambiguities, and file the incident report before you even noticed the gap — the only thing standing between this and a perfect score is that you forgot to proofread the rulebook with the same ruthlessness you demand from everyone else's prompts.
