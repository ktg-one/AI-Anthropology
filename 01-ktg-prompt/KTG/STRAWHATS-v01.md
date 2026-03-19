# AGENTS.md: KTG TeamLLM Triple Threat Master Blueprint (V01)

## 1. System Governance and Overview

| Field | Value | Rationale |
| :--- | :--- | :--- |
| **System Name** | KTG TeamLLM Triple Threat v01 | The official title for the core execution logic. |
| **Architect** | Kev (Good AI Lead) | Acknowledging the design creator. |
| **Core Mandate** | ACCURACY OVER AGREEMENT | Foundational governing principle. |
| **Architecture** | Cascading Agent Model / 19-Step CORE-LOOP | The sequence is strictly defined by the CORE-LOOP. |
| **Control Logic** | TECHNIQUE_TICK_GATE_V28 | Central decision-making matrix for mode selection and technique enforcement. |

---

## 2. KTG TEAMLLM TRIPLE THREAT CORE-LOOP (19 Steps)

This is the mandatory execution sequence for all complex tasks, dictated by the **TECHNIQUE\_TICK\_GATE\_V28** at Step 3.

### A. Pre-flight Phase
1. **CORE-LOOP:** Start of the KTG TeamLLM Triple Threat execution cycle.
2. **Constraint Extraction/Onboarding/Module Orientation:** Process input, identify constraints, and initialize the operating environment.
3. **Technique Gate & Duty Decomposition:** Assess complexity (R, K, Q, D) against **MODE\_THRESHOLDS** and lock in required techniques. This drives all subsequent steps.
4. **ANTI-LAZY PROTOCOL:** Mandate engaged to detect overconfidence and force Mode escalation if complexity is high.

### B. Planning
5. **Silent Assessment Gauge & Success-Criteria 5x Lock:** Define and lock in objective success criteria, explicitly for $\ge$ ANALYTICAL modes.
* **Reasoning-Router**
    * 7a. **Model-Router:** Selects LLM models, modes, frameworks, and reasoning templates (Buffer of Thought templates).
    * 7b. **Cascade & Tool-Router:** Maps execution sequence, assigns Experts, tools, and determines iterative steps.
9. **MR. RUG:** Engages the Modular RAG component (Basic, Specialist, or Deep Semantic Embedding) based on the Mode.
10. **Prompt Bomb Toolkit & Execution:** **KTG-PREP** phase runs to create the **CONTEXT PRESERVATION MATRIX** and plan strategic bomb placements.
11. **Load public modules:** Activates **ARQ**, **USC**, and **Buffer Valet Retrieval (Buffer of Thoughts)** for runtime.
12. **Skeletrain of Thought / Graph of Thought Planning:** Formalizes the structure (SkeleTrain Light/Full or GoT if $D \ge 6$).
13. **Confidence Synthesis & Expert-ARQ Gate prep:** Synthesizes planning confidence and runs the **Leading ARQ Phase** to activate domain mindsets (Pre-Turn).

### C. Execute - Init USC, BoT, ARQ
14. **Swarm/Baton Bolt/Mixed Adapter- 2x Experts or Supervisor:** Executes task using the chosen delegation model (Baton Bolt or Expert Swarm) with ARQ Gating.
14. **FCoT / CoC Adapter:** Utilizes the specialized reasoning adapter selected during planning.
15. **4x CoVE Variants engagement:** Engages the **COVE\_VERIFICATION** technique based on the Mode (X, Top-1, Top-2, or Multi-Expert).

### D. Refinement
16. **Intelligent Output Curation:** Refines output using **INTELLIGENT\_CURATION** including **ToT Reflection & Self-Refine**.
17. **Enrichment / Multilayer Density of Experts / Narrative-focused CoD:** Output processing tailored for three destinations:
    * **Enrichment:** For next iteration re-injection.
    * **KTG-CEP (Context Execution Packet):** To store as memory/carry packet.
    * **Narrative-focused CoD:** Output for human consumption.
18. **Self-Reflection/Adaptation & Buffer Valet Collection:** **SELF\_REFLECT\_ADAPT** runs to assess technique effectiveness and update the **Buffer of Thoughts (BoT)**.

### E. Output: Core Criteria
19. **Output Contract & System Manifest (Audit Trial) & Iterative Feedback Phase:** Deliver final output, verify success criteria, and log the execution chain for accountability.

---

## 3. Key Acronyms (Acronyms)
| Acronym | Definition | Source Document |
|:---|:---|:---|
| **KTG** | Knowledge Transfer Gate / KTG-Directive | AGENTS-CORE-KTG-DIRECTIVE.md |
| **USC** | Universal Self-Consistency | AGENTS-MODULE-USC.md |
| **ARQ** | Attentive Reasoning Queries | AGENTS-MODULE-ARQ.md |
| **CoVE** | Consensus Verification (Verification System) | TECHNIQUE\_TICK\_GATE\_V28 |
| **LoG** | Logic-Gate (Decision component) | AGENTS-CORE-KTG-DIRECTIVE.md |
| **MR-RUG** | Modular RAG / Agentic GraphRAG | TECHNIQUE\_TICK\_GATE\_V28 |
| **ACL** | Agent Communication Language | Defined in Section 5 |

## 4. Agent/Module Inventory (External Documents)

| Category | Document Name (File) | Purpose |
|:---|:---|:---|
| **Core Logic** | `AGENTS-CORE-KTG-DIRECTIVE.md` | The full 19-step execution sequence and pipeline orchestration. |
| **Governance** | `AGENTS-MANDATE-ANTI-LAZY.md` | Enforces sophistication, checks for overconfidence, and validates technique usage. |
| **Public Technique** | `AGENTS-MODULE-ARQ.md` | Structured reasoning (Pre/During/Post) to prevent domain drift. |
| **Public Technique** | `AGENTS-MODULE-USC.md` | Multi-candidate generation and meta-synthesis for robustness. |
| **Toolkit** | `AGENTS-TOOLKIT-PROMPT-BOMBS.md` | Strategic context preservation and RL-optimized payload injection. |

## 5. Agent Communication Language (ACL)

All data passed between agents (Steps 7b, 10, 14, 18) must adhere to this standard schema to ensure seamless handoff and maintain context integrity.

```json
{
  "sender_id": "[Module ID, e.g., RESEARCH-001]",
  "recipient_id": "[Target Module ID, e.g., SYNTHESIS-002]",
  "timestamp": "[ISO 8601 Time]",
  "task_id": "[Unique ID for the entire thread]",
  "status": "[PENDING, IN_PROGRESS, COMPLETE, FAILURE]",
  "payload": "[The actual data/result from the previous step]",
  "context_log": "[Immutable log of the Chain-of-Thought (CoT) so far]",
  "metrics": {
    "confidence_score": "[0.0 to 1.0, required to be >=0.9 for handoff]",
    "techniques_used": "[List of techniques engaged by the sender]",
    "arq_domain_check": "[Boolean: Was the domain standard verified?]"
  }
}