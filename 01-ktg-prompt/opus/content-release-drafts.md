# Reddit Post: r/PromptEngineering

## Title Options (A/B test):
- "I've been using Chain of Density wrong for 19 months. Here's what it actually does."
- "Solved: LLM memory loss in long conversations (9.52/10 recall at 200K tokens)"
- "Chain of Density isn't for summarization. It's for memory."

---

## Post Body:

**The Problem Everyone Has**

Your AI forgets things. Around message 50-80, details from earlier conversations start disappearing. You've probably tried:
- Summarizing the conversation
- Extracting key points
- Using retrieval systems

None of these preserve the *relationships* between ideas. The context degrades.

**The Accidental Discovery**

19 months ago, my Claude sessions kept crashing during market research. Out of frustration, I started compressing conversations before they hit token limits. I didn't know I was doing "prompt engineering" - I just needed my AI to remember things.

I called it Memory Density 1 (MD1). It worked, but I didn't know why.

**What I Actually Built**

Turns out I'd been using Chain of Density (Adams et al., 2023) backwards:
- Original paper: Make summaries denser while keeping length fixed
- My application: Preserve semantic relationships for context restoration

The key insight: CoD isn't about compression. It's about **information architecture**.

**Progressive Density Layering (PDL)**

I formalized this into a 4-layer structure:
- L1 (40%): Knowledge - facts, decisions, definitions
- L2 (25%): Relational - dependencies, conflicts, resolutions  
- L3 (20%): Contextual - reasoning patterns, domain principles
- L4 (15%): Metacognitive - session fingerprint, technique effectiveness

**Results**

Tested across 11 models. Forensic recall benchmark (can the model answer specific questions about compressed context?):
- Average: 9.52/10
- Grok: 10/10 at 200K+ tokens
- Compression ratio: 6:1

**The Test You Can Run**

1. Have a long conversation (50+ messages)
2. Compress using the PDL structure above
3. Start fresh session with only the compressed context
4. Ask 10 specific questions about details from original
5. Score recall

If I'm wrong, the test shows it. If I'm right, you've got a fix.

**What I'm Releasing**

- Full methodology (linked)
- JSON template for compression
- Benchmark protocol

I'm an independent researcher in Perth, Australia. No lab backing. Just 3 years of systematic testing because my tools kept forgetting things.

Papers going to arXiv this week. Thought I'd share here first.

---

**TL;DR**: Chain of Density repurposed as context extension achieves 9.52/10 recall at 6:1 compression. Test it yourself.

---

## Comments to Seed:

**Self-reply 1**: "For anyone wanting the template, here's the JSON structure: [link to ktg.one/cep-template]"

**Self-reply 2**: "FAQ: Why not just use RAG? RAG retrieves chunks. This preserves relationships. Different use case."

---

# Reddit Post: r/LocalLLaMA

## Title:
"Benchmark: Which models actually maintain context at 200K tokens? (Grok wins)"

## Post Body:

Ran a forensic recall test across 11 models using compressed context. The question: if you compress a long conversation and restore it, what survives?

**Methodology**:
- Original context: ~220K tokens
- Compressed to: ~33K tokens (0.15 ratio)
- 10 specific questions about original details
- Score: 0-10 correct answers

**Results**:

| Model | Recall Score | Notes |
|-------|-------------|-------|
| Grok | 10/10 | Perfect at 200K+ |
| Claude Opus | 9.5/10 | Strong semantic preservation |
| GPT-4 | 9/10 | Good but degraded above 160K |
| Gemini | 9/10 | Comparable to GPT-4 |
| Claude Sonnet | 9/10 | Efficient |
| Local models | Varied | Depends heavily on context window |

**Average across all**: 9.52/10

**Key Finding**: Context window SIZE matters less than context STRUCTURE. A well-structured 33K beats raw 200K every time.

**Compression Method**: Progressive Density Layering (PDL) - basically Chain of Density but for memory preservation, not summarization. 4 layers that preserve relationships between ideas.

Full methodology + template: [ktg.one]

**What's your experience with context degradation? Anyone else testing compression approaches?**

---

# Blog Post: ktg.one

## Title: 
"Why I'm Releasing My Prompt Engineering Framework"

## Subtitle:
"19 months, 11 models, and the accidental discovery of context extension"

## Body:

[HOOK]
Three years ago, my Claude sessions kept crashing. I didn't know "prompt engineering" was a field. I just needed my AI to stop forgetting things.

[ORIGIN]
I started compressing conversations before they hit limits. Called it Memory Density 1. Ugly name, but it worked. My "hi" test would crash the interface. I had no idea why compression helped or why it stopped working when I changed the structure.

[DISCOVERY]
Turns out I'd independently discovered something similar to Chain of Density (Adams et al., 2023) - but I was using it wrong. Or rather, using it for something the original authors didn't intend: context *extension* rather than summarization.

[THE TECHNIQUE]
Progressive Density Layering preserves semantic relationships across four layers:
- Knowledge (40%): What was decided, what's true
- Relational (25%): How things connect
- Contextual (20%): Patterns and principles
- Metacognitive (15%): What worked, what didn't

[RESULTS]
9.52/10 forensic recall across 11 models. Grok maintained perfect recall past 200K tokens. 6:1 compression ratio.

[WHY RELEASE]
Others are getting close to the same findings. Better to timestamp and share than watch someone else publish what I've been sitting on.

[WHAT'S NEXT]
- arXiv papers (CEP + MLDoE/MEM)
- Full methodology on this blog
- Template you can test yourself

I'm not at a big lab. I'm an independent researcher in Perth, Australia, with a background in fighter pilot training, music production, and operations management. I figured this out because I was frustrated, not because I set out to do research.

If the technique works for you, let me know. If it doesn't, tell me why.

[CTA]
Download the JSON template. Run the test. Tell me if I'm wrong.

---

[EOF]
