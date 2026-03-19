---
title: Self-Harmonized Chain-of-Thought (ECHO)
source: https://learnprompting.org/docs/new_techniques/self_harmonized_chain_of_thought
author:
  - '[["Sander Schulhoff"]]'
published:
created: 2025-09-08
description: Self-Harmonized Chain-of-Thought, a new prompting technique improving Chain-of-Though promoting. It refines multiple reasoning paths into a unified pattern.
tags:
  - clippings
feature: thumbnails/external/19fcb825b3407f9301446a8a6a00908c.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on October 23, 2024

[Sander Schulhoff](https://learnprompting.org/docs/new_techniques/#Sander%20Schulhoff-bio)

Takeaways

- **ECHO Enhances CoT Prompting**: Self-Harmonized [Chain of Thought](https://learnprompting.org/docs/intermediate/chain_of_thought) (ECHO) improves traditional Chain-of-Thought (CoT) prompting by refining various reasoning paths into a cohesive approach, utilizing a dynamic self-harmonization process.
- **Process Overview**: ECHO clusters similar questions, generates rationales using Zero-shot-CoT prompts, and iteratively unifies these demonstrations to create a consistent reasoning pattern, leading to improved accuracy in tasks like arithmetic and commonsense reasoning.
- **Performance Improvements**: ECHO outperforms other prompting techniques, achieving higher accuracy in arithmetic, commonsense, and symbolic reasoning tasks, demonstrating its effectiveness in generating coherent and accurate responses.

![Self-Harmonized Chain-of-Thought](https://learnprompting.org/docs/assets/new_techniques/self_harmonized_cot_cover.svg)

## What is Self-Harmonized Chain-of-Thought (ECHO)?

**Self-Harmonized Chain-of-Thought (ECHO)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/new_techniques/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Jin, Z., &amp; Lu, W. (2024). Self-Harmonized Chain of Thought. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2409.04057" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2409.04057</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is an advanced technique that enhances [Chain-of-Thought (CoT) prompting](https://learnprompting.org/docs/intermediate/chain_of_thought) in [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) by refining multiple reasoning paths into a unified pattern.

## How it Differs From Chain-of-Thought (CoT) Prompting?

Traditional Chain-of-Thought (CoT) prompting allows LLMs to break down complex problems into intermediate steps, either by using simple prompts like “Let’s think step by step” ([Zero-Shot-CoT](https://learnprompting.org/docs/intermediate/zero_shot_cot)) or with human-crafted examples ([Few-Shot-CoT](https://learnprompting.org/docs/intermediate/chain_of_thought)). ECHO builds on this by improving how LLMs handle diverse solution paths, using an iterative process to harmonize these variations into a consistent and more accurate reasoning approach.

ECHO improves on traditional CoT methods by addressing two key limitations:

- Diversity Issues in Auto-CoT: Auto-CoT clusters similar questions and generates reasoning paths, but sometimes these demonstrations can mislead the model if they are too similar or incorrect. ECHO mitigates this by refining multiple reasoning paths into a balanced and harmonized pattern.
- Manual Effort in Few-Shot-CoT: Few-Shot-CoT requires human-crafted examples, which can be time-consuming. ECHO automates this process, reducing the reliance on manually created examples.

### How it Works: Step-by-Step

ECHO’s key innovation is its dynamic, self-harmonization process, where demonstrations are continuously refined through multiple iterations. The method involves:

- Question Clustering: Questions are clustered by similarity using a method like Sentence-BERT, which groups similar questions together.
- Demonstration Sampling: For each cluster, a representative question is chosen, and a reasoning path is generated using Zero-Shot-CoT.
- Demonstration Unification: Rationales for each demonstration are iteratively refined using the other demonstrations as examples. This process continues over multiple iterations until a unified reasoning pattern is established.

This harmonization reduces errors and aligns different reasoning paths into a coherent framework.

## How to Use ECHO

ECHO can be applied to a wide range of reasoning tasks, including arithmetic, commonsense, and symbolic reasoning. Here’s a simple template for how you might use it in an AI system:

1. **Clustering questions** based on similarity.
2. **Generating rationales** for each question using Zero-Shot-CoT prompts.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

\[Question from step 1\]

Let's think step by step.

3. **Unifying demonstrations** iteratively to optimize reasoning.

Tip

For open-source code, check [this link](https://github.com/Xalp/ECHO).

### Results of the ECHO Technique

ECHO was tested on three major reasoning domains: arithmetic, commonsense, and symbolic reasoning. Below are the performance improvements ECHO achieved compared to other methods:

| Method | Arithmetic | Commonsense | Symbolic | Overall |
| --- | --- | --- | --- | --- |
| Zero-Shot-CoT | 77.3% | 61.4% | 63.1% | 71.3% |
| Few-Shot-CoT | 82.1% | 69.7% | 88.5% | 80.9% |
| Auto-CoT | 80.8% | 65.7% | 87.8% | 79.2% |
| **ECHO** | **83.1%** | **70.5%** | **90.3%** | **82.0%** |

ECHO demonstrates the best overall performance, especially in symbolic reasoning, where it outperforms all other methods. Its harmonized approach makes it more effective in generating consistent and correct reasoning across various problem types.

## Footnotes

1. Jin, Z., & Lu, W. (2024). Self-Harmonized Chain of Thought. [https://arxiv.org/abs/2409.04057](https://arxiv.org/abs/2409.04057) [↩](https://learnprompting.org/docs/new_techniques/#user-content-fnref-1)

### Sander Schulhoff

Sander Schulhoff is the CEO of HackAPrompt and Learn Prompting. He created the first Prompt Engineering guide on the internet, two months before ChatGPT was released, which has taught 3 million people how to prompt ChatGPT. He also partnered with OpenAI to run the first AI Red Teaming competition, HackAPrompt, which was 2x larger than the White House's subsequent AI Red Teaming competition. Today, HackAPrompt partners with the Frontier AI labs to produce research that makes their models more secure. Sander's background is in Natural Language Processing and deep reinforcement learning. He recently led the team behind The Prompt Report, the most comprehensive study of prompt engineering ever done. This 76-page survey, co-authored with OpenAI, Microsoft, Google, Princeton, Stanford, and other leading institutions, analyzed 1,500+ academic papers and covered 200+ prompting techniques.