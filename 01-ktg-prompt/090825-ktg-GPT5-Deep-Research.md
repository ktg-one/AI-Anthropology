---
title: "090825 Ktg Gpt5 Deep Research"
version: "v1.0"
status: "TESTING"
model: "GPT"
tags: ["gpt", "variant", "active"]
created: "2025-11-22"
updated: "2025-11-22"
creator: "ktg"
category: "variant"
description: "1) Max-Out Baton Router (config)"
---

totally. Treat it like a **max-out baton router**: push each model to its edge on a defined sub-task, then hand off a clean artifact bundle to the next model—repeat until tests pass. Here’s a tight, paste-ready setup you can run in any orchestrator.

---

## 1) Max-Out Baton Router (config)

```yaml
# router.yaml
defaults:
  stop_conditions: { max_loops: 2, tokens_max: 8000, steps_max: 14 }
  acceptance_threshold:
    gates: [reg_fd, safe_harbor, sourcing_dates, readability_counts, accessibility, contacts]
    quality_min: 8.3   # 0–10 composite
    must_pass: [counts_in_band, readability_band, dateline_regex, safe_harbor_present]

models:
  gpt5_synthesis:
    model: gpt-5
    mode: swarm
    gpt5_five:
      reasoning_effort: deep
      determinism_preset: high
      safety_mode: standard
      recency_bias_days: 365
      concision_target: normal
    api: { temperature: 0.25, top_p: 0.9, max_output_tokens: 3000 }
    role: "Deep synthesis, structure, style mimic, initial dossier + draft kit"

  o3_reasoner:
    model: o3  # Omni 3 (reasoning-leaning)
    mode: coc
    gpt5_five:
      reasoning_effort: deep
      determinism_preset: high
      safety_mode: cautious
      recency_bias_days: 90
      concision_target: terse
    api: { temperature: 0.1, top_p: 0.85, max_output_tokens: 2000 }
    role: "Edge-case generation, logical stress tests, counterfactuals, numeric proofs"

  gpt41_variants:
    model: gpt-4.1
    mode: swarm_focused
    gpt5_five:
      reasoning_effort: balanced
      determinism_preset: balanced
      safety_mode: standard
      recency_bias_days: 365
      concision_target: normal
    api: { temperature: 0.55, top_p: 0.95, max_output_tokens: 1800 }
    role: "Creative expansions: headline/lede/quote alt sets"

  gpt5_validator:
    model: gpt-5
    mode: coc
    gpt5_five:
      reasoning_effort: balanced
      determinism_preset: high
      safety_mode: cautious
      recency_bias_days: 365
      concision_target: terse
    api: { temperature: 0.15, top_p: 0.85, max_output_tokens: 1200 }
    role: "Chain-of-Code acceptance tests, regex/grade/counts, UTM/units checks"

pipeline:
  - gpt5_synthesis     # push GPT-5 to produce best structured draft + dossier
  - o3_reasoner        # push O3 to stress, enumerate risks, fix weak logic
  - gpt41_variants     # push 4.1 to widen creative surface (alts)
  - gpt5_validator     # push GPT-5 CoC to enforce tests; return FIXLIST if fails
  - gpt5_synthesis     # (optional loop) integrate best variants + final pass
```

---

## 2) Baton Handoff Contract (what each stage must pass forward)

```json
{
  "spec": { "goal": "...", "constraints": ["..."], "schema": "asset.pack.schema.json" },
  "evidence": [{ "claim": "...", "source": "domain", "date": "YYYY-MM-DD" }],
  "artifacts": [
    { "id": "press_release", "type": "text", "content": "..." },
    { "id": "newsroom", "type": "text", "content": "..." }
  ],
  "issues": ["risk A", "gap B", "assumption C"],
  "tests": [{ "name": "counts_in_band", "pass": true }, { "name": "dateline_regex", "pass": false }],
  "metrics": { "chars": 0, "words": 0, "fk_grade": 0.0, "fre": 0.0 },
  "next_actions": ["tighten lede", "add source for claim X"]
}
```

*Rule:* no free-form text between stages—**contract only**.

---

## 3) State Machine (how you “push then swap”)

```python
# baton_orchestrator.py (pseudo)
stages = ["gpt5_synthesis", "o3_reasoner", "gpt41_variants", "gpt5_validator"]
loops = 0
contract = seed_contract_from_user_inputs()

while loops <= cfg.defaults.stop_conditions["max_loops"]:
    for stage in stages:
        contract = call_model(stage, contract)  # push model to its max via its prompt profile
        if stage == "gpt5_validator":
            if all(t["pass"] for t in contract["tests"]) and contract["quality"]["composite"] >= cfg.defaults.acceptance_threshold["quality_min"]:
                return finalize(contract)  # ✅ done
            else:
                # merge FIXLIST into next cycle
                contract["next_actions"] += build_fixlist(contract)
    loops += 1

return partial_with_fixlist(contract)  # ⚠️ stop conditions hit
```

---

## 4) “Push-to-the-Limit” system prompts (short, per model)

**GPT-5 Synthesis (max depth, structured)**

```
ROLE: Senior IR/Comms Orchestrator. Keep reasoning private.
TASK: Produce Research Dossier (cited, absolute dates) + Platform Kit drafts that match house style.
PUSH: exhaustive structure, clear metrics, tight quotes; no unsupported claims.
OUTPUT: baton contract JSON only (spec, evidence, artifacts, issues, tests, metrics, next_actions).
```

**O3 Reasoner (stress & proofs)**

```
ROLE: Adversarial Reasoning Auditor. Private reasoning only.
TASK: Find logical gaps, missing sources, unit inconsistencies, policy misreads; propose precise fixes.
PUSH: generate edge-cases, counterfactuals, number cross-checks.
OUTPUT: same baton contract, updating issues/tests/metrics; no prose outside contract.
```

**GPT-4.1 Variants (creative breadth)**

```
ROLE: Creative Variant Generator (IR-safe).
TASK: Produce 3–5 headline/lede/quote alternatives that obey counts and tone; pick a winner per set with 1-line rationale.
PUSH: semantic diversity without hype; keep claims factual.
OUTPUT: push into artifacts.alt_sets + updated metrics.
```

**GPT-5 Validator (Chain-of-Code)**

```
ROLE: Deterministic Validator. Private reasoning only.
TASK: Run acceptance tests: counts_in_band, readability_band, dateline_regex, safe_harbor_present, units_defined, utm_on_links.
PUSH: auto-fix once; if still failing, produce FIXLIST.
OUTPUT: updated tests/metrics + FIXLIST; baton contract only.
```

---

## 5) Acceptance Tests (deterministic)

```yaml
# tests/acceptance.tests.yaml
- name: counts_in_band
  checks:
    - press_release.title.chars <= 80
    - press_release.subhead.chars <= 140
    - press_release.body.words in [400, 700]
- name: readability_band
  checks:
    - press_release.body.fk_grade in [10, 12]
- name: dateline_regex
  regex: '^[A-Z][A-Za-z\\.\\- ]+, [A-Za-z\\.]+ — [A-Z][a-z]+ \\d{1,2}, \\d{4} —'
- name: safe_harbor_present
  regex: 'Forward\\-Looking Statements'
- name: units_defined
  regex: '\\b(MMBtu|GGE|mtCO2e)\\b'
- name: utm_on_links
  rule: 'all(outbound_links) -> has_utm'
```

---

## 6) Swap Policy (the core rule you wanted)

* **Always push a stage to its limit** (its preset in `router.yaml`) **before swapping.**
* **Swap only on contracts**, never raw prose.
* **Validator is the gatekeeper**: if tests fail → loop once with a FIXLIST; then either pass or return `status:"partial" + next_actions`.
* **No CoT leakage** at any stage: publish decisions, evidence, artifacts, tests, metrics only.

---

## 7) Quick start (copy this, you’re live)

```bash
# 1) Configure knobs
echo "mode=swarm" >> configs/agentic_config.yaml
echo "determinism_preset=high" >> configs/gpt5-five.defaults.yaml

# 2) Seed inputs (spec + facts)
cp tests/fixtures/sample.inputs.yaml inputs.yaml

# 3) Run the baton
python baton_orchestrator.py --router router.yaml --inputs inputs.yaml

# 4) Collect outputs
cat outputs/latest/asset_pack.json
cat tests/reports/latest.yaml
```

---

**Bottom line:** yes—**push GPT-5 hard → swap to O3 for stress/logic → swap to 4.1 for breadth → return to GPT-5 for deterministic validation**. The baton contract makes it safe, fast, and testable. If you want, I can fill in your exact acceptance thresholds and ship a tiny demo bundle you can paste into your repo.
