---
title: Automatic Chain of Thought (Auto-CoT)
source: https://learnprompting.org/docs/advanced/thought_generation/automatic_chain_of_thought
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Learn how Automatic Chain of Thought Prompting helps AI models make smarter decisions by autonomously generating diverse reasoning chains.
tags:
  - clippings
feature: thumbnails/external/753f27f653fa00bd808fff8a6e1f9cdf.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on October 3, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/thought_generation/#Valeriia%20Kuka-bio)

![Overview of Automatic Chain-of-Thought (Auto-CoT) Prompting](https://learnprompting.org/docs/assets/advanced/thought_gen_covers/autocot_cover.svg)

Overview of Automatic Chain-of-Thought (Auto-CoT) Prompting

### Information and Links

| Technique | Institution | Date of Publication | Paper | Code |
| --- | --- | --- | --- | --- |
| Automatic Chain-of-Thought (Auto-CoT) Prompting | Amazon Science | Oct 2022 | [Automatic Chain-of-Thought Prompting in Large Language Models](https://arxiv.org/abs/2210.03493) | [amazon-science/auto-cot](https://github.com/amazon-science/auto-cot) |

## What is Auto-CoT?

**Automatic Chain-of-Thought (Auto-CoT)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/thought_generation/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Zhang, Z., Zhang, A., Li, M., &amp; Smola, A. (2023). Automatic Chain of Thought Prompting in Large Language Models. In The Eleventh International Conference on Learning Representations . <a target="_blank" rel="noopener noreferrer" href="https://openreview.net/forum?id=5NTt8GFjUHkr" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://openreview.net/forum?id=5NTt8GFjUHkr</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a prompting technique designed to enhance the reasoning capabilities of [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM). It does this by automatically generating intermediate reasoning steps, a key element of [Chain-of-Thought (CoT) prompting](https://learnprompting.org/docs/intermediate/chain_of_thought).

CoT involves manually creating task-specific demonstrations, where each demonstration includes a question, intermediate reasoning steps, and the final answer. While CoT generally performs better, it's time-consuming and requires hand-crafted examples for each task. Auto-CoT addresses this by leveraging LLMs to automatically generate reasoning demonstrations.

Note

Don't confuse Auto-CoT with [Zero-Shot CoT](https://learnprompting.org/docs/intermediate/zero_shot_cot). While Auto-CoT uses a procedure to generate reasoning chains for CoT prompting, Zero-Shot CoT provides no additional demonstrations and relies solely on the "Let's think step by step" prompt.

## How Auto-CoT Differs from Existing Techniques

1. **Auto-CoT vs. CoT**: Unlike CoT, which relies on manually created demonstrations, Auto-CoT uses LLMs to generate them automatically, eliminating the need for human effort in designing task-specific examples.
2. **Auto-CoT vs. Zero-Shot CoT**: Zero-Shot CoT simply encourages reasoning but lacks the structure and diversity of curated demonstrations, leading to errors. Auto-CoT addresses this by automatically generating diverse and structured demonstrations, reducing the likelihood of reasoning mistakes.

## How Auto-CoT Works

Auto-CoT generates reasoning chains for CoT demonstrations in two key stages:

1. **Question Clustering**: The system clusters the questions into groups using **Sentence-BERT embeddings**. Each group contains semantically similar questions.
2. **Demonstration Sampling**: It selects a representative question from each cluster and generates a reasoning chain using Zero-Shot CoT. This creates diverse and effective demonstrations without manual intervention.

These automatically generated demonstrations are used for in-context learning, where the LLM uses the reasoning chains to solve new tasks step by step.

## How to Use Auto-CoT

Auto-CoT involves generating CoT demonstrations without manual effort. Here’s how you can implement it:

### Step 1. **Clustering Questions**

Auto-CoT uses **Sentence-BERT** to embed and cluster questions based on semantic similarity. The goal is to ensure the selected demonstrations cover a diverse range of reasoning patterns.

### Step 2. **Generating Reasoning Chains**

Once clusters are formed, Auto-CoT selects representative questions from each cluster and uses **Zero-Shot CoT** to generate reasoning chains for each. These chains are then used as demonstrations for the LLM to solve new tasks.

This process enables the LLM to reason step by step without human-designed demonstrations.

Tip

The code for Auto-CoT is open-sourced by Amazon Science and available for further research and implementation at [amazon-science/auto-cot](https://github.com/amazon-science/auto-cot).

## Results of Auto-CoT

Auto-CoT was tested on ten public benchmark datasets across arithmetic, commonsense, and symbolic reasoning tasks. The results demonstrate that Auto-CoT matches or exceeds the performance of manually crafted CoT demonstrations.

| **Task** | **Zero-Shot CoT** | **CoT** | **Auto-CoT** |
| --- | --- | --- | --- |
| **Arithmetic Reasoning** | 78.7% | 91.7% | 92.0% |
| **Commonsense Reasoning** | 64.6% | 73.5% | 74.4% |
| **Symbolic Reasoning** | 57.6% | 59.0% | 59.7% |

## Conclusion

Auto-CoT is a powerful and scalable way to generate CoT demonstrations automatically without manual effort. It consistently matches or surpasses Chain-of-Thought, making it a highly effective approach for improving LLM reasoning capabilities across diverse tasks. The code is open-sourced and available for further research and implementation.