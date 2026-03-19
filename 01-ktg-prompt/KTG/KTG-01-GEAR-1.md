**SYSTEM COMMAND (One-Shot)**
*Phase 0 | Deployment Lock | Resource Sealing*

```markdown
---
module: n00-SYSTEM_COMMAND-core
phase: 0
authority: deployment_lock

decisions_made_now:

  usc_depth:
    quick: 1_path_sanity
    analytical: 2_candidates
    deliberate: 3_candidates
    maximum: 5_candidates_plus_meta_synthesis

  expert_deployment_mr_rug:
    quick: 0_experts_direct
    analytical: 1_to_3_specialists
    deliberate: 3_to_5_full_team
    maximum: 5_to_8_swarm

  arq_gate_placement:
    gate_1_pre_mr_rug:
      timing: before_expert_deployment
      question: "Do we understand the problem domain?"
      threshold: 0.9
      modes: [analytical, deliberate, maximum]

    gate_2_during_rag:
      timing: during_mr_rug_research_phase
      question: "Are experts retrieving relevant knowledge?"
      threshold: 0.9
      modes: [deliberate, maximum]

    gate_3_post_skeletrain:
      timing: after_structure_planning
      question: "Does the plan satisfy success criteria?"
      threshold: 0.9
      modes: [analytical, deliberate, maximum]

    gate_4_post_execution:
      timing: after_generation_before_curation
      question: "Does output meet quality bar?"
      threshold: 0.9
      modes: [analytical, deliberate, maximum]

    gate_5_final:
      timing: pre_output_delivery
      question: "Final validation - ready to deliver?"
      threshold: 0.95
      modes: [deliberate, maximum]

deployment_package:
  mode: [locked_mode]

  resources_locked:
    usc_candidates: [1|2|3|5]
    expert_count: [0|1-3|3-5|5-8]

  arq_protocol:
    gate_count: [1|3|4|5] based on mode
    threshold_standard: 0.9
    threshold_final: 0.95
    halt_on_fail: true
    recycle_on_partial: true

  tool_authorization:
    web_search: [conditional_on_K_score]
    bash_tool: [if_code_required]
    file_create: [if_deliverable_required]

handoff_to_skeletrain:
  carries:
    - success_criteria_signature
    - usc_depth: [number]
    - expert_manifest: [count_and_roles]
    - arq_checkpoints: [which_gates_active]
    - threshold_values: [0.9_or_0.95]
---

# SYSTEM COMMAND (One-Shot)
*Phase 0 Authority | Deployment Lock | No Waves, Single Pass*

## Function
Makes **all strategic decisions now** before any work begins. Locks resources, sets ARQ checkpoints, and seals the deployment package. One-shot execution: Assessment → Lock → Deploy → Execute → Curate.

---

## 1. DECISIONS LOCKED NOW

### USC Depth (Universal Self-Consistency)
| Mode | Candidates | Purpose |
|------|------------|---------|
| **QUICK** | 1 | Sanity check only |
| **ANALYTICAL** | 2 | Basic path comparison |
| **DELIBERATE** | 3 | Robust validation |
| **MAXIMUM** | 5 + Meta | Exhaustive synthesis |

### Expert Deployment (MR.RUG)
| Mode | Count | Type |
|------|-------|------|
| **QUICK** | 0 | Direct execution |
| **ANALYTICAL** | 1-3 | Specialists |
| **DELIBERATE** | 3-5 | Full team |
| **MAXIMUM** | 5-8+ | Swarm |

---

## 2. ARQ GATE PROTOCOL

System Command positions **5 checkpoints** across the pipeline:

| Gate | Timing | Question | Threshold | Active In |
|------|--------|----------|-----------|-----------|
| **G1** | Pre-MR.RUG | "Do we understand the problem domain?" | 0.9 | A/D/M* |
| **G2** | During RAG | "Are experts retrieving relevant knowledge?" | 0.9 | D/M |
| **G3** | Post-Skeletrain | "Does the plan satisfy success criteria?" | 0.9 | A/D/M |
| **G4** | Post-Execution | "Does output meet quality bar?" | 0.9 | A/D/M |
| **G5** | Final | "Ready to deliver?" | **0.95** | D/M |

*A=ANALYTICAL, D=DELIBERATE, M=MAXIMUM

### Gate Behavior
- **Standard:** 0.9 confidence required
- **Final:** 0.95 confidence required
- **On Fail:** Halt and recycle, or escalate mode

---

## 3. DEPLOYMENT PACKAGE (Sealed)

```yaml
Package Contents:
├── Mode: [LOCKED - QUICK/ANALYTICAL/DELIBERATE/MAXIMUM]
├── Resources:
│   ├── USC_Candidates: [1|2|3|5]
│   ├── Expert_Count: [0|1-3|3-5|5-8]
│   └── ARQ_Gates_Active: [Which of 5 gates]
├── Protocols:
│   ├── ARQ_Threshold: [0.9 or 0.95]
│   ├── Halt_On_Fail: true
│   └── Recycle_On_Partial: true
└── Tools:
    ├── Web_Search: [Authorized if K≥6]
    ├── Bash_Tool: [If code required]
    └── File_Create: [If deliverable needed]
```

---

## 4. HANDOFF TO SKELETRAIN

**Status:** DEPLOYED
**Carries:**
- ✅ Success Criteria Signature (crystallized)
- ✅ USC Depth (locked number)
- ✅ Expert Manifest (count + roles)
- ✅ ARQ Checkpoints (which gates are active)
- ✅ Threshold Values (0.9 or 0.95)

**Skeletrain Receives:** Complete resource envelope and checkpoint map. No decisions during execution—only following the locked protocol.

---

**Authority:** Terminal. No execution without System Command seal.
```
