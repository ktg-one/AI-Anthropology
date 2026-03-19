---
title: Memory-of-Thought (MoT)
source: https://learnprompting.org/docs/advanced/thought_generation/memory_of_thought
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Memory-of-Thought (MoT)enables LLMs to self-improve without fine-tuning. Learn how MoT leverages external memory to enhance reasoning.
tags:
  - clippings
feature: thumbnails/external/c52bb7a3639d71d62365457c027ed291.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on October 3, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/thought_generation/#Valeriia%20Kuka-bio)

![Overview of Memory-of-Thought (MoT) Prompting](https://learnprompting.org/docs/assets/advanced/thought_gen_covers/mot_cover.svg)

Overview of Memory-of-Thought (MoT) Prompting

### Information and Links

| Technique | Institution | Date of Publication | Paper | Code |
| --- | --- | --- | --- | --- |
| Memory-of-Thought (MoT) Prompting | Fudan University | May 2023 | [MoT: Memory-of-Thought Enables ChatGPT to Self-Improve](https://arxiv.org/abs/2305.05181) | [LeeSureman/MoT](https://github.com/LeeSureman/MoT) |

## What is Memory-of-Thought (MoT)?

**Memory-of-Thought (MoT)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/thought_generation/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Li, X., &amp; Qiu, X. (2023). MoT: Memory-of-Thought Enables ChatGPT to Self-Improve. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2305.05181" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2305.05181</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a novel framework designed to let [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) like ChatGPT **self-improve** without requiring high-quality labeled datasets or computationally expensive fine-tuning. Inspired by human self-reflection and memory, MoT equips LLMs with the ability to pre-think, store, and recall past reasoning paths, enhancing their performance on various reasoning tasks.

## How MoT Differs from Existing Techniques

This approach contrasts traditional methods that rely heavily on annotated datasets and fine-tuning, both of which are costly and limit the accessibility of improvement for LLMs. MoT leverages **external memory** to improve performance across various reasoning tasks, including arithmetic, commonsense, and factual reasoning.

## How Does MoT Work?

The framework operates in two key stages:

1. **Pre-thinking**: Before the test stage, the LLM thinks over an **unlabeled dataset** and saves the high-confidence reasoning paths (called **thoughts**) in an external memory system.
2. **Recalling**: During the test stage, when the LLM encounters a new question, it retrieves the relevant thoughts from memory to aid its reasoning process.

This method allows the LLM to **improve its reasoning capabilities** without updating its parameters, making it more efficient and scalable.

### Why It Works

MoT mimics human cognition by allowing the LLM to **think, store, and recall**. Just as humans remember past decisions to make better future ones, the LLM can rely on stored reasoning chains to enhance its current reasoning. This improves performance across a wide range of tasks by eliminating reliance on random or irrelevant examples, focusing instead on high-quality, relevant memories.

## How to Use MoT

### Step 1. Pre-thinking

In this stage, the LLM processes unlabeled examples and saves the **most consistent** reasoning paths (thoughts) as memory. This process involves the following steps:

- The LLM generates multiple reasoning paths for each question.
- A **majority-vote** system selects the most frequent (and thus consistent) answer and saves the corresponding reasoning chain as memory.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Q1: \[Question 1\] A1: \[Answer 1\] Q2: \[Question 1\] A2: \[Answer 1\]

Qn: \[Sample question\]

### Step 2. Recalling

When the LLM encounters a new test question:

- It **retrieves relevant thoughts** from memory, based on the similarity between the current question and stored questions.
- The LLM uses its own understanding to select the most useful thought and then uses it to aid in answering the test question.

### Example of MoT in Action:

```
Test Question: Maddie has 24 apples. If she gives 12 to Mike, how many does she have left?

Memory Retrieval: A similar thought retrieved from memory involves someone giving away apples:
- "If Tom has 30 apples and gives 15 away, he has 30 - 15 = 15 apples left."

Answer: Using the thought from memory, Maddie has 24 - 12 = 12 apples left.
```

By recalling a similar scenario from its memory, the LLM quickly resolves the new question using an analogous reasoning process.

Tip

The code for MoT is open-sourced by Fudan University and available for further research and implementation at [LeeSureman/MoT](https://github.com/LeeSureman/MoT).

## Results of MoT

MoT was tested on multiple reasoning benchmarks, demonstrating significant improvements in various tasks compared to standard techniques.

| **Task** | **Few-Shot CoT** | **MoT** | **Improvement** |
| --- | --- | --- | --- |
| **Arithmetic Reasoning** | 49.7% | 54.1% | +4.4% |
| **Commonsense Reasoning** | 80.0% | 82.3% | +2.3% |
| **Natural Language Inference** | 67.7% | 71.5% | +3.8% |
| **Factual Reasoning** | 65.2% | 68.0% | +2.8% |

## Conclusion

Memory-of-Thought (MoT) enhances LLMs' reasoning capabilities by enabling them to learn from their own past experiences and leverage stored memories. MoT offers a cost-effective and efficient solution compared to traditional methods relying on extensive datasets and fine-tuning.