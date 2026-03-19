# Griffin Adams Outreach Package

## Contact
- **Email**: griffin.adams@columbia.edu
- **Twitter**: @griffinadams16
- **GitHub**: griff4692
- **Current role**: Member of Technical Staff, Answer.AI

## Why He's Perfect

His current work: "Reducing the cost of long-context inference" via KV cache compression (Cold Compress library).

Your work: Reducing context requirements via semantic compression (CEP/PDL).

**Same problem, complementary approaches:**
- His: Compress the cache (infrastructure level)
- Yours: Compress the content (prompt level)

## The Hook

He built Cold Compress for KV cache. You built CEP for context packets.
Both target: **How do we preserve more with less?**

His CoD paper was about summarization density.
You discovered CoD works for **memory extension**, not just summarization.

---

## Email Draft

**To**: griffin.adams@columbia.edu
**Subject**: Your CoD paper + my extension to context preservation

---

Hi Griffin,

I've been using your Chain of Density work in an unexpected way—as a **context extension protocol** rather than summarization.

**The discovery**: CoD's entity-dense compression preserves semantic relationships that enable cross-session memory transfer. I'm achieving 9.52/10 forensic recall at 6:1 compression across 11 LLMs.

**Why this matters for your current work**: You're compressing KV cache (Cold Compress). I'm compressing the content that goes INTO that cache. Complementary approaches to the same problem—long-context inference cost.

**What I have**:
- Paper draft formalizing "Progressive Density Layering" (PDL)—CoD extended with relational/contextual/metacognitive layers
- Benchmark data across Claude, GPT-4, Gemini, Llama, etc.
- Working implementation as a Claude Skill (portable prompt-based protocol)

**What I'm asking**: Would you consider endorsing for arXiv (cs.CL)? I can send the paper + demo.

I'm an independent researcher (Perth, Australia)—no institution, but real results. Happy to jump on a call if you'd like to see it in action.

Cheers,
Kevin Tan
ktg.one

---

## What to Include When He Responds

### 1. The Paper (PDF)
Your arXiv draft with:
- PDL formal definition
- Algorithm pseudocode
- Benchmark methodology
- Results table (11 models × forensic recall scores)

### 2. The Skill (Demo)
The ktg-cep-v5-claude.skill package so he can:
- Drop it into Claude
- Test compression himself
- Verify the claims

### 3. Quick Demo Video (optional but powerful)
2-3 min screen recording:
- Start conversation, fill context
- Invoke CEP, show compression
- Start NEW session, paste CEP
- Ask recall questions, show accuracy

### 4. Benchmark Reproduction
Simple script or notebook:
- Input: Sample conversation
- Output: CEP packet + recall test
- Let him verify independently

---

## Why He'll Care

From his site:
> "My work aims to bridge the gap between cutting edge research and **practical applications**."

Your work IS practical application. It's not theoretical—it's a working protocol people can use today.

> "Please reach out if you'd like to chat about **scaling inference-time compute** for non-reasoning tasks"

CEP reduces inference needs by preserving context efficiently. Direct relevance.

---

## Backup Targets (if no response in 7 days)

### Noémie Elhadad (Columbia DBMI)
- His PhD advisor
- Senior author on CoD paper
- Contact via Columbia directory

### Sander Schulhoff
- Lead author "The Prompt Report" (58 techniques taxonomy)
- Your PDL is a new technique category
- Find via arXiv:2406.06608 author info

### Jeremy Howard (Answer.AI co-founder)
- Griffin's boss at Answer.AI
- Known for practical ML democratization
- Active on Twitter, might RT if interesting

---

## Timeline

**Day 0**: Send email to Griffin
**Day 3**: If no response, follow up on Twitter (@griffinadams16)
**Day 7**: If still no response, email Noémie Elhadad
**Day 7**: Also submit to arXiv directly (moderation queue fallback)
**Day 14**: If Griffin responds positively, he endorses
**Day 14**: If no endorsement, arXiv moderation should approve by now

---

## The Skill Angle

You mentioned making this accessible. The Claude Skill IS the demo:

1. **Academics want reproducibility** → Skill is reproducible
2. **Researchers want to test claims** → Skill lets them test
3. **Practitioners want utility** → Skill works out of box

Package the skill with:
- SKILL.md (the protocol)
- benchmark-data.json (your 11-model results)
- demo-conversation.txt (sample input)
- expected-output.json (what CEP should produce)

Anyone can verify. That's more convincing than just a paper.
