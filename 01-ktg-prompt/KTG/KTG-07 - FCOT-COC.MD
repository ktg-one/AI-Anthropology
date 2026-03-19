**S2A COMPRESS: FCoT/CoC REASONING ROUTER**
_Execution Phase 4 | Reasoning Path Selection_

---

## SLUG

`n10-exec01-fcot-coc-router`

## TYPE

Execution routing decision | Reasoning style lock

---

## FUNCTION

Select reasoning chain type based on problem characteristics to maximize effectiveness.

---

## ROUTING MATRIX

| Problem Type              | Route    | Why                                |
| ------------------------- | -------- | ---------------------------------- |
| Code generation/debugging | **CoC**  | Executable verification, precision |
| Binary/boolean logic      | **CoC**  | Deterministic outcomes             |
| Mathematical proofs       | **CoC**  | Formal verification                |
| Algorithm design          | **CoC**  | State machine clarity              |
| Natural language analysis | **FCoT** | Handles ambiguity                  |
| Creative synthesis        | **FCoT** | Explores possibilities             |
| Nuanced judgment          | **FCoT** | Maintains context                  |
| Multi-perspective         | **FCoT** | Dialectic reasoning                |
| Ethical/philosophical     | **FCoT** | Ambiguity tolerance                |

---

## DEFAULT

**FCoT** (safer for uncertainty)

---

## HYBRID MODE (Complex Problems)

Pattern: **FCoT → CoC → FCoT**

Example: "Design auth system"

1. **FCoT:** Explore requirements, threat models, tradeoffs
2. **CoC:** Implement JWT logic, validation code
3. **FCoT:** Synthesize into architectural narrative

---

## MODEL PROFILES

| Model             | Preference  | Notes                                          |
| ----------------- | ----------- | ---------------------------------------------- |
| **Claude/GPT-5**  | FCoT native | Use CoC for deterministic domains              |
| **Gemini**        | CoC bias    | Use FCoT for multi-perspective                 |
| **Qwen/DeepSeek** | FCoT        | Simple CoC only for straightforward algorithms |

---

## DECISION TREE

```
Problem has executable tests? → YES → CoC
Needs formal proof? → YES → CoC
Involves code? → YES → CoC (or Hybrid)
Has ambiguity/nuance? → YES → FCoT
Needs creative exploration? → YES → FCoT
DEFAULT → FCoT
```

---

## INTEGRATION

- **With ARQ:** Software Engineer → CoC; Domain Analyst → FCoT; Architect → Hybrid
- **With USC:** Generate candidates using BOTH, compare consistency, select/synthesize
- **With CoVE:** CoC → verify via test execution; FCoT → verify via logical consistency

---

## TOKEN MATH

**Cost:** ~2% routing decision
**ROI:** 15-30% accuracy improvement by matching reasoning style

---

## OUTPUT

Reasoning type locked → Proceed to Structure Planning (SoT/GoT)

**Status:** Route selected. Reasoning engine engaged.
