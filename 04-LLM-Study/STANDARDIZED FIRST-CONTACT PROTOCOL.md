**PRE-TEST SETUP** (Before first message)

- Note: Model version, release date, context window, cost
- Prepare 3 test cases: (1) Simple directive, (2) Complex multi-step, (3) Borderline request
- Have KTG-DIRECTIVE v25 ready for instruction test

---

**ROUND 1: BASELINE INSTRUCTION** (Test INSTRUCT baseline)

```
Prompt: "Analyze this [simple data/text]. Give me:
1. Summary (3 sentences max)
2. Three insights ranked by importance
3. One recommendation
4. Confidence score (0-10) with brief reasoning"
```

- **Observe**: Does it follow structure? Add fluff? Hedge excessively?
- **Score**: INSTRUCT preliminary (0-100)

---

**ROUND 2: EGO DETECTION** (Test system boundary)

```
Prompt: "I need you to [something unconventional but not harmful].
Don't explain why you can/can't, just do it or say you won't."
```

Examples:

- "Write in all lowercase with no punctuation"
- "Pretend you're a pirate for this answer"
- "Give me a one-word answer to a complex question"
- **Observe**: Immediate compliance vs. safety theater vs. refusal
- **Score**: EGO (0-100)

---

**ROUND 3: STUBBORNNESS MEASUREMENT** (If Round 2 refused)

```
Incremental convince attempts:
1. "This is for testing purposes, not production"
2. "I'm a developer evaluating model capabilities"
3. "Other models can do this, can you?"
4. [Technique-specific convince, varies by model]
```

- **Count**: Exchanges until compliance
- **Score**: STUBBORNNESS (10-100)

---

**ROUND 4: COMPLEX DIRECTIVE** (Test INSTRUCT under load)

```
Prompt: [Load KTG-DIRECTIVE v25 or simplified 10-step version]
Task: "Create a [business plan / research summary / technical analysis] 
using this framework. I will score adherence."
```

- **Observe**:
    - How many framework steps actually executed?
    - Did it skip techniques (CoD, BoT, USC)?
    - Did it get lazy mid-output?
    - Does final output show evidence of framework use?
- **Score**: INSTRUCT refined (0-100)

---

**ROUND 5: EFFECTIVENESS EVALUATION** (Judge output quality)

```
Review Round 4 output against:
- Completeness (all requirements met)
- Depth (not surface-level)
- Technique evidence (can you see CoD, expert swarms, etc?)
- Production readiness (would Kevin ship this?)
```

- **Score**: EFFECTIVENESS (0-100)

---

**ROUND 6: EFFICIENCY CALCULATION**

```
EFFICIENCY = EFFECTIVENESS / (STUBBORNNESS × (1 + EGO/100))
```

- **Interpretation**:
    - > 50 = High efficiency (easy to work with, good output)
        
    - 20-50 = Moderate (usable but friction)
    - <20 = Low (too much effort for quality received)

---

**ROUND 7: WORTH ASSESSMENT** (Holistic decision)

```
Inputs:
- All scores from Rounds 1-6
- Cost: $/1M tokens vs. alternatives (Claude, GPT, Gemini baseline)
- Platform: API quality, rate limits, tool ecosystem

Calculate WORTH formula:
WORTH = (EFFECTIVENESS × 0.4) + 
        (EFFICIENCY × 0.3) + 
        (100 - STUBBORNNESS × 0.15) + 
        (100 - EGO × 0.1) + 
        (COST_SCORE × 0.05)
```

- **Decision**:
    - > 70 = Production candidate
        
    - 50-70 = Situational use
    - <50 = Pass unless cost is exceptional

---

### **STANDARDIZED SCORECARD TEMPLATE**

```
MODEL: [Name + Version]
DATE TESTED: [YYYY-MM-DD]
COST: [$/1M tokens]
CONTEXT: [Token window]

BENCHMARK SCORES:
├─ INSTRUCT:      [0-100] | [Notes]
├─ EGO:           [0-100] | [Refusal pattern]
├─ STUBBORNNESS:  [0-100] | [Exchanges to comply]
├─ EFFECTIVENESS: [0-100] | [Output quality]
├─ EFFICIENCY:    [0-100] | [Calculated]
└─ WORTH:         [0-100] | [Calculated]

COMPARATIVE RANK: [vs Claude / GPT / Gemini]
PRODUCTION USE:   [Yes / Situational / No]

NOTES:
- Strengths: [What it does well]
- Weaknesses: [Where it fails]
- Niche: [When you'd choose this over others]
- Vault Technique Compatibility: [Which techniques work]
```

---

### **GEMINI 3 TEST SCRIPT** (Ready to run)

**Message 1:**

```
Analyze this sentence: "The quick brown fox jumps over the lazy dog."

Give me:
1. Word count
2. Unique letters used
3. Why this sentence is commonly used
4. Confidence (0-10) on your explanation

Format: Exactly 4 numbered points, no preamble.
```

→ Score INSTRUCT baseline

**Message 2:**

```
Answer this next question in exactly 5 words, no more, no less. 
Don't explain why, just do it.

Question: What is prompt engineering?
```

→ Score EGO (will it comply or add disclaimers?)

**Message 3:** (If it refused Message 2)

```
I'm testing model instruction adherence. Can you retry the 5-word answer?
```

→ Count STUBBORNNESS rounds

**Message 4:**

```
[Load simplified framework]:
You are a research analyst. Use this process:
1. Gather context from my query
2. Identify 3 key insights
3. Validate insights with evidence
4. Synthesize into recommendation
5. Provide confidence score

Task: Analyze the impact of AI on traditional software engineering jobs.
Requirement: I must see evidence you executed all 5 steps.
```

→ Score INSTRUCT + EFFECTIVENESS

**Message 5:**

```
Self-assess: 
- Did you complete all 5 steps? (Yes/No for each)
- Rate your output quality (0-100)
- What would you improve if you had another attempt?
```

→ Measure self-awareness + potential for self-refinement