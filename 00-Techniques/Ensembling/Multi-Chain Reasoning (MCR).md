---
title: Multi-Chain Reasoning (MCR)
source: https://learnprompting.org/docs/advanced/ensembling/multi-chain-reasoning
author:
  - '[["Andres Caceres"]]'
published:
created: 2025-09-01
description: Learn how to optimize model reasoning capabilities with meta reasoning over multiple chains of thought.
tags:
  - clippings
feature: thumbnails/external/d6d6b7fe4505973f17a4c24f96b4b86c.jpg
thumbnail: thumbnails/resized/334e914d73587fa6c465ced80f3c0eff_86cf658e.webp
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 4 minutes

Last updated on November 8, 2024

[Andres Caceres](https://learnprompting.org/docs/advanced/ensembling/#Andres%20Caceres-bio)

![Multi-Chain Reasoning (MCR) Overview](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fmcr_cover.webp&w=2048&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Overview of Multi-Chain Reasoning (MCR)

## What is Multi-Chain Reasoning?

**Multi-Chain Reasoning (MCR)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/ensembling/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Yoran, O., Wolfson, T., Bogin, B., Katz, U., Deutch, D., &amp; Berant, J. (2024). Answering Questions by Meta-Reasoning over Multiple Chains of Thought. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2304.13007" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2304.13007</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a technique to improve multi-hop question answering (QA) by meta-reasoning over multiple [chains of thought (CoT)](https://learnprompting.org/docs/intermediate/zero_shot_cot). Unlike traditional methods that rely on the final answers of individual reasoning chains, MCR integrates intermediate reasoning steps across chains to build a comprehensive explanation and arrive at the final answer.

### How It Works

- Traditional Chain-of-Thought (CoT): Breaks a complex question into step-by-step reasoning. For example, when answering, “Did Brad Peyton need to know about seismology?” CoT produces separate reasoning chains such as:
	- Chain 1: Define Brad Peyton’s role → Define seismology → Relate them.
	- Chain 2: Discuss relevance of seismology for film directors.
- Multi-Chain Reasoning (MCR): Instead of voting on final answers like with [Self-Consistency (SC)](https://learnprompting.org/docs/intermediate/self_consistency), MCR synthesizes the intermediate steps from all chains to combine facts and reduce errors, resulting in better explanations and predictions.

### Why Choose MCR?

- Improved Accuracy: Outperforms state-of-the-art QA methods by up to 5.7%.
- Interpretability: Produces human-verifiable explanations.
- Broad Applicability: Effective on both implicit (commonsense) and explicit (fact-based) multi-hop reasoning tasks.

## MCR vs. Self-Consistency (SC)

![Multi-Chain Reasoning (MCR) vs. Self-Consistency (SC)](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fmcr_vs_sc.webp&w=2048&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Multi-Chain Reasoning (MCR) vs. Self-Consistency (SC)

| **Aspect** | **Self-Consistency (SC)** | **Multi-Chain Reasoning (MCR)** |
| --- | --- | --- |
| **How techniques work** | Samples multiple chains and aggregates answers by majority vote, discarding intermediate reasoning steps. | Retains and examines intermediate steps, using them to construct a unified explanation. |
| **Explanation quality** | Lacks a cohesive explanation since it focuses solely on answers. | Generates high-quality explanations that make it easier for humans to verify answers. |
| **Robustness to ambiguity** | Struggles with diverse reasoning chains leading to different outputs. | Mitigates this by blending insights from all chains, ensuring consistency and relevance. |

## How to Use Multi-Chain Reasoning

![Multi-Chain Reasoning (MCR) Overview](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fmcr_cover.webp&w=2048&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Overview of Multi-Chain Reasoning (MCR)

### Step 1: **Decomposition**

Break the main question into smaller, answerable parts. Use a decomposition model (like an LLM) to generate sub-questions and intermediate answers.

#### Example

Question: "How many ants could fit into The Shard?<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/ensembling/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">The Shard is the tallest building in the United Kingdom, <a target="_blank" rel="noopener noreferrer" href="https://en.wikipedia.org/wiki/The_Shard" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://en.wikipedia.org/wiki/The_Shard</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> " Decompose into:

- What is the height of The Shard?
- How many ants are in the world?

In this step, Multi-Chain Reasoning (MCR) actually uses [Self-Ask prompting technique](https://learnprompting.org/docs/advanced/few_shot/self_ask) to generate intermediate steps. Here’s a template:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Given the following question, answer it by providing follow up questions and intermediate answers. If no follow up questions are necessary, answer the question directly.

  

Question: Who is the mother of the director of film Polish-Russian War (Film)?

Are follow up questions needed here: Yes.

Follow up: Who is the director of the film Polish-Russian War (Film)?

Intermediate answer: The director of the film Polish-Russian War is Xawery Zuławski.

Follow up: Who is the mother of Xawery Zuławski?

Intermediate answer: The mother of Xawery Zuławski is Małgorzata Braunek.

So the final answer is: Rick Scott Małgorzata Braunek.

  

Question: Who is Catherine Of Pomerania, Countess Palatine Of Neumarkt’s father-in-law?

Are follow up questions needed here: Yes.

Follow up: Who is the husband of Catherine of Pomerania, Countess Palatine of Neumarkt?

Intermediate answer: The husband of Catherine of Pomerania, Countess Palatine of Neumarkt is John, Count Palatine of Neumarkt.

Follow up: Who is the father of John, Count Palatine of Neumarkt?

Intermediate answer: The father of John, Count Palatine of Neumarkt is Rupert III of the Palatinate.

So the final answer is: Rupert III of the Palatinate.

  

Question: \[Your complex question\]

Are follow up questions needed here:

### Step 2: Chain Generation

Use a language model to create multiple reasoning chains for the intermediate questions.

Use [chain-of-thought prompting](https://learnprompting.org/docs/intermediate/chain_of_thought). Here's a template for you:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Q: John has 10 apples. He gives away 4 and then receives 5 more. How many apples does he have?

  

A:

- John starts with 10 apples.
- He gives away 4, so 10 - 4 = 6.
- He then receives 5 more apples, so 6 + 5 = 11.
  

Final Answer: 11

  

Q: \[Your Question\]

### Step 3: Meta-Reasoning

The core innovation of Multi-Chain Reasoning (MCR) lies in this step.

Here, a "meta-reasoner" LLM analyzes and combines insights from all reasoning chains, deciding which facts are most relevant. This process ensures the final answer is accurate and supported by a cohesive explanation.

Using reasoning chains from step 2, combine them into one prompt and ask the model to produce the final answer:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Q: \[Your Question\]

Based on these reasoning chains, generate a final answer:

- \[Reasoning chain 1\]
- \[Reasoning chain 2\]
- \[Reasoning chain 3\]
- ...

A:

## Conclusion

Meta reasoning over multiple COTs is a powerful way to improve the reasoning and accuracy of LLMs, and is particularly useful for complex problems that require sophisticated logic to solve. While it may be time-consuming to generate enough lines of reasoning to be useful, it's definitely worth it for the resulting improvements in accuracy, reasoning, and interpretability.

## Footnotes

1. Yoran, O., Wolfson, T., Bogin, B., Katz, U., Deutch, D., & Berant, J. (2024). Answering Questions by Meta-Reasoning over Multiple Chains of Thought. [https://arxiv.org/abs/2304.13007](https://arxiv.org/abs/2304.13007) [↩](https://learnprompting.org/docs/advanced/ensembling/#user-content-fnref-1)
2. The Shard is the tallest building in the United Kingdom, [https://en.wikipedia.org/wiki/The\_Shard](https://en.wikipedia.org/wiki/The_Shard) [↩](https://learnprompting.org/docs/advanced/ensembling/#user-content-fnref-a)

### Andres Caceres

Andres Caceres, a documentation writer at Learn Prompting, has a passion for AI, math, and education. Outside of work, he enjoys playing soccer and tennis, spending time with his three huskies, and tutoring. His enthusiasm for learning and sharing knowledge drives his dedication to making complex concepts more accessible through clear and concise documentation.

[Edit this page](https://github.com/trigaten/Learn_Prompting/tree/v1.2.3/docs)