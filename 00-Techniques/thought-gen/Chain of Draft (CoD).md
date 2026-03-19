---
title: Chain of Draft (CoD)
source: https://learnprompting.org/docs/advanced/thought_generation/chain-of-draft
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Chain of Draft (CoD) is an efficient prompting technique that enables faster reasoning by generating minimalistic intermediate outputs.
tags:
  - clippings
feature: thumbnails/external/5de24f6b17105b6ecdcb56bec84e49c5.jpg
thumbnail: thumbnails/resized/51258d65c0a62dfdf028932f67f38555_86cf658e.webp
---
🟢 This article is rated [easy](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on March 11, 2025

[Valeriia Kuka](https://learnprompting.org/docs/advanced/thought_generation/#Valeriia%20Kuka-bio)

Large Language Models (LLMs) have revolutionized complex reasoning through [Chain-of-Thought (CoT) prompting](https://learnprompting.org/docs/intermediate/chain_of_thought). While effective, CoT's verbose approach often results in high computational costs and increased latency. This limitation becomes particularly significant in real-world applications where efficiency is crucial.

**Chain of Draft (CoD)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/thought_generation/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Xu, S., Xie, W., Zhao, L., &amp; He, P. (2025). Chain of Draft: Thinking Faster by Writing Less. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> addresses these challenges by introducing a more efficient approach to LLM reasoning. Inspired by human problem-solving patterns, where we typically jot down only essential information, CoD demonstrates that effective reasoning doesn't require lengthy explanations.

CoD transforms traditional LLM reasoning through three key principles:

1. **Minimalist expression:** Instead of verbose explanations, CoD generates concise, information-dense outputs
2. **Token efficiency:** Achieves comparable or better accuracy while using as little as 7.6% of the tokens compared to CoT
3. **Human-inspired design:** Mirrors natural problem-solving patterns where only critical information is recorded

## Implementing CoD

To leverage Chain of Draft effectively, use this streamlined prompt template:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Template

---

Think step by step, but only keep a minimum draft for each thinking step, with 5 words at most. Return the answer at the end of the response after a separator ####.

Guidelines:

- Limit each step to 5 words
- Focus on essential calculations/transformations
- Maintain logical progression
- Mark final answer with ####

## Practical Example: Solving Problems with CoD

Let's examine how different prompting approaches handle a simple arithmetic problem:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Problem

---

Jason had 20 lollipops. He gave Denny some lollipops. Now Jason has 12 lollipops. How many lollipops did Jason give to Denny?

### Three Approaches Compared

1. **Standard Prompting** (Direct Answer)

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

A: 8

2. **Chain-of-Thought Prompting** (Detailed Reasoning)

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Let's think through this step by step:

1. Initially, Jason had 20 lollipops.
2. After giving some to Denny, Jason now has 12 lollipops.
3. To find out how many lollipops Jason gave to Denny, we need to calculate the difference between the initial number of lollipops and the remaining number.
4. We can set up a simple subtraction problem: Initial number - Remaining number = Lollipops given
5. Putting in the numbers: 20 - 12 = Lollipops given to Denny
6. Solving the subtraction: 20 - 12 = 8

Therefore, Jason gave 8 lollipops to Denny.

#### 8

3. **Chain-of-Draft Prompting** (Minimal Essential Steps)

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

20 - x = 12 x = 20 - 12 = 8

#### 8

This comparison clearly demonstrates how CoD maintains problem-solving clarity while dramatically reducing verbosity.

## Advantages and Limitations

### Key Benefits

1. **Enhanced efficiency**
	- Significantly reduced response generation time
	- Lower computational resource requirements
	- Minimal token consumption
2. **Practical advantages**
	- More cost-effective for production deployment
	- Faster user response times
	- Reduced infrastructure requirements

### Current Limitations

While powerful, CoD has several important constraints:

- **Model dependencies**
	- Requires larger models (>3B parameters) for optimal performance
	- Less effective in zero-shot scenarios
	- May need specific training data
- **Application constraints**
	- Best suited for structured reasoning tasks
	- May require few-shot examples
	- Performance varies by task type

Note

For optimal results, use CoD with larger language models and provide few-shot examples. The technique's effectiveness can vary significantly based on model size and task complexity.

## Conclusion

Chain of Draft represents a significant step forward in making LLM reasoning more practical and efficient. By maintaining accuracy while dramatically reducing computational overhead, CoD enables broader deployment of LLM capabilities in resource-constrained environments. As the field evolves, this technique's balance of efficiency and effectiveness positions it as a valuable tool for the future of AI applications.