**S2A COMPRESS: ARQ MODULE**

---

## MODULE: ARQ (Attentive Reasoning Queries)

**SLUG:** `n03-pre04-arq-mod`  
**TYPE:** Pre-flight reference | Quality introspection protocol  
**FUNCTION:** Domain-specific reasoning checkpoints (replaces CoT)

---

### CORE MECHANISM

| Chain-of-Thought (Inferior) | ARQ (Superior) |
|---------------------------|----------------|
| Free-form reasoning | Structured queries forcing domain attention |
| Can drift from instructions | Locks critical guidelines mid-conversation |
| Buried reasoning steps | Auditable, explicit checkpoints |
| **Lower success rate** | **90.2% success, 29% token reduction** |

---

### THREE-STAGE PROTOCOL

**Stage 1: Leading Phase**  
Model answers pre-determined domain questions before responding:
- "What defines quality in this domain?"
- "What are the critical failure modes?"
- "What standards must I meet?"

**Stage 2: Generation**  
Response grounded in structured reasoning (silent to user).

**Stage 3: Verification**  
Post-execution check:
- "Did I meet domain standards?"
- Confidence ≥0.9 required for handoff.

---

### ACTIVATION MATRIX

| Mode | Trigger | Location |
|------|---------|----------|
| QUICK | O | Non-trivial stakes only |
| ANALYTICAL | R | High-impact nodes (≥8/10) |
| DELIBERATE | R | Full: pre/during/post on ≥8/10 nodes |
| MAXIMUM | R | Full + cross-expert validation |

---

### TOKEN MATH

**Cost:** ~10% overhead  
**ROI:** 40-60% error reduction  
**Net:** Superior performance vs CoT despite overhead

---

### INTEGRATION HOOKS

- **MR.RUG:** Experts activate ARQ on assignment  
- **Baton Pass:** Pre-ARQ → Elaborate → Post-ARQ (≥0.9) → Handoff  
- **CoVE:** ARQ identifies what to verify  
- **Confidence Gates:** ARQ scores feed probability chains

---

### DOMAIN QUERY EXAMPLES

**Code Review:**
- "Did I check for SQL injection, XSS, auth bypass?"
- "Is this maintainable per SOLID?"

**Research:**
- "Are sources credible?"
- "Do conclusions follow from evidence?"

**Writing:**
- "Did I address all key points?"
- "Is tone appropriate for audience?"

---

### OUTPUT SIGNAL

```
ARQ_VALIDATED: true/false
CONFIDENCE: [0.0-1.0]
DOMAIN_STANDARDS: [checklist_status]
```

**Pass threshold:** ≥0.9

---

**Reference complete. Models know ARQ when invoked.**