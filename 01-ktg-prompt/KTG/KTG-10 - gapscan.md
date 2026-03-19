**S2A COMPRESS: POST_EXEC_GAP_SCAN**
_Phase 10 | Holistic Quality Audit | Final Repair Before Curation_

---

## SLUG

`n13-exec04-gap-scan`

## TYPE

Post-execution quality assurance | 3-branch holistic detection + auto-repair

---

## FUNCTION

Catch what CoVE missed. Find what's **missing** (not just what's wrong). Repair if possible, flag if not.

---

## 3-BRANCH SCAN

| Branch         | Detects                                                                   | Auto-Fix                                   | Flags                                             |
| -------------- | ------------------------------------------------------------------------- | ------------------------------------------ | ------------------------------------------------- |
| **A: LOGIC**   | Chain breaks, circular logic, contradictions, leaps                       | Add connectors, reorder flow               | Fundamental errors, contradictions needing expert |
| **B: CONTENT** | Unanswered questions, missing context, incomplete coverage, dangling refs | Add sections, define terms, complete lists | Major scope omissions, needing new research       |
| **C: VALUE**   | Fluff, redundancy, tangents, low signal-to-noise                          | Cut fluff, remove duplicates, add examples | Tone/format mismatch, fundamental misalignment    |

---

## MODE ACTIVATION

| Mode           | Depth                    | Action                                                  |
| -------------- | ------------------------ | ------------------------------------------------------- |
| **QUICK**      | Skip                     | Not activated                                           |
| **ANALYTICAL** | Branch A only            | Light logic check, flag only (no auto-fix)              |
| **DELIBERATE** | All 3 branches           | Auto-fix minor, flag major                              |
| **MAXIMUM**    | All 3 + cross-validation | Deep scan, auto-fix all repairable, multi-expert review |

---

## EXECUTION FLOW

1. **Parallel Scan:** Run A+B+C simultaneously over outputs
2. **Triage:**
   - Severity = minor + Fixable = true → **Auto-fix queue**
   - Severity = major OR Fixable = false → **Flag for review**
3. **Auto-repair:** Execute fixes, re-verify
4. **Confidence Adjustment:** Penalize unfixed gaps

---

## CONFIDENCE IMPACT

- Minor gap (auto-fixed): **No penalty**
- Minor gap (flagged): **-0.5**
- Major gap (flagged): **-1.5**
- Critical gap (core claim affected): **-3.0, may trigger re-execution**

---

## GATES

- **Coverage:** All user questions addressed or flagged?
- **Logic:** Chains valid or repaired?
- **Value:** Signal-to-noise ≥ 0.6?
- **Repairable:** All fixable gaps fixed?

**Fail any gate → Adjust confidence, flag for review**

---

## OUTPUT TO CURATION

- Content (auto-fixed seamlessly)
- Flag list ( informs synthesis decisions)
- Confidence delta (adjust final score)

**Status:** Scanned. Gaps filled or flagged. Confidence locked. Ready for final curation.
