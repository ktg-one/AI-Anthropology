---
title: Consistency-based Self-adaptive Prompting (COSP)
source: https://learnprompting.org/docs/advanced/ensembling/consistency_based_self_adaptive_prompting
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-01
description: Improve LLM reasoning with Consistency-based Self-adaptive Prompting (COSP) without needing labeled data. Learn how COSP works and see results!
tags:
  - clippings
feature: thumbnails/external/7c7d8b166c524d12a18863c811b5de8c.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on October 3, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/ensembling/#Valeriia%20Kuka-bio)

![MoRE Overview](https://learnprompting.org/docs/assets/advanced/cosp_cover.svg)

Overview of Consistency-based Self-adaptive Prompting (COSP)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/ensembling/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wan, X., Sun, R., Dai, H., Arik, S. O., &amp; Pfister, T. (2023). Better Zero-Shot Reasoning with Self-Adaptive Prompting. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2305.14106" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2305.14106</a></span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

## What is COSP?

**Consistency-based Self-Adaptive Prompting (COSP)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/ensembling/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wan, X., Sun, R., Dai, H., Arik, S. O., &amp; Pfister, T. (2023). Better Zero-Shot Reasoning with Self-Adaptive Prompting. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2305.14106" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2305.14106</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a novel technique designed to improve the reasoning capabilities of [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) in [Zero-Shot](https://learnprompting.org/docs/basics/few_shot) settings. LLMs have demonstrated impressive abilities, but their performance in reasoning tasks often varies significantly depending on the approach used.

Two main methods—[Few-Shot Prompting](https://learnprompting.org/docs/basics/few_shot) (providing the model with handpicked examples) and [Zero-Shot Chain-of-Thought (CoT)](https://learnprompting.org/docs/intermediate/zero_shot_cot) prompting (triggering step-by-step reasoning)—have shown success, but each has limitations. COSP addresses these by automatically selecting useful in-context examples from the LLM’s own generated responses, without needing labeled data or handcrafted prompts.

### Why is COSP Needed?

- **Few-Shot prompting** requires careful selection of examples, which is time-consuming and task-specific.
- **Zero-Shot CoT prompting** often underperforms due to lack of guidance, leading to spurious reasoning paths.
- **COSP** solves these problems by leveraging the model's own generated outputs, selecting the most useful examples based on consistency, diversity, and minimal repetition.

## How COSP Differs from Existing Techniques

### Zero-Shot CoT vs. COSP

While **Zero-Shot CoT** relies on trigger phrases alone to prompt the model, **COSP** takes this further by:

- Generating multiple outputs for each question.
- Selecting the best in-context examples based on consistency and diversity.
- Using majority voting to improve the reliability of the final answer.

### Few-Shot CoT vs. COSP

**Few-Shot CoT** requires manually selecting a small number of example questions and answers to guide the model. This is effective but labor-intensive and not scalable across tasks. COSP achieves similar or better performance **without any labeled data**, automatically selecting relevant in-context examples from the model's own outputs.

## Benefits and Applications

- **Higher accuracy**: COSP consistently outperforms Zero-Shot and even Few-Shot baselines on reasoning tasks, improving accuracy by up to 15%.
- **No labeled data needed**: COSP works without any labeled data or handcrafted examples, making it scalable and efficient.
- **Consistency-driven**: By focusing on consistency and diversity, COSP improves the reliability of predictions in Zero-Shot scenarios.

## How COSP Works

- **Stage 1: Generating Responses**: The model generates multiple reasoning paths for each test question using Zero-Shot CoT. These paths are then assessed for their reliability based on consistency across answers.
- **Stage 2: Selecting Demonstrations**: The best responses are selected as in-context demonstrations based on criteria like consistency (whether the same answer is repeated), minimal repetition, and diversity of reasoning paths. These selected examples are then used to guide the model’s final prediction.
- **Majority Vote**: The final prediction is chosen by majority vote across multiple generated reasoning paths.

## How to Use COSP

COSP can be applied to any reasoning-based task where Zero-Shot performance is needed. It requires:

- Access to a Large Language Model
- Unlabeled test questions

The system will then follow these steps:

### 1\. Generate responses

Run the model multiple times on each test question using Zero-Shot CoT.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

\[Test question\]

Let's think step by step.

For example:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Henry had 11 dollars. For his birthday, he got 18 more dollars but spent 10 on a new game. How much money does he have now?

Let's think step by step.

AI Outputs for this example:

```
1. "11 + 18 = 29, 29 - 10 = 19"
2. "Henry has 27 dollars."
3. "He has 11 + 18 - 10 = 19."
4. "He bought 11 games and added 18. Then subtracted 10 for the game."
```

### 2\. Select demonstrations

COSP automatically selects the most consistent and diverse reasoning paths to use as in-context examples.

Selected Example:

```
"11 + 18 = 29, 29 - 10 = 19."
```

### 3\. Final prediction

COSP uses the selected examples to prompt the model again and choose the best answer based on a majority vote.

```
Final Answer: "19 dollars."
```

## Results of COSP

COSP significantly improves performance on reasoning tasks when compared to Zero-Shot and even Few-Shot CoT. Here are the results from COSP applied to multiple reasoning benchmarks:

| **Task** | **Zero-Shot CoT** | **Few-Shot CoT** | **COSP** |
| --- | --- | --- | --- |
| **MultiArith** | 67.2% | 81.0% | **85.0%** |
| **AddSub** | 69.1% | 72.4% | **78.9%** |
| **GSM-8K** | 20.9% | 30.3% | **30.2%** |
| **StrategyQA** | 57.2% | 67.9% | **64.7%** |

## Conclusion

**COSP** offers a powerful solution for improving zero-shot reasoning in LLMs. It removes the need for manual example crafting, instead relying on the model’s own outputs to guide reasoning. By combining consistency, diversity, and repetition analysis, COSP leads to significant performance improvements across multiple reasoning tasks. This makes it a scalable and efficient approach for improving LLM reasoning in real-world applications.

## Footnotes

1. Wan, X., Sun, R., Dai, H., Arik, S. O., & Pfister, T. (2023). Better Zero-Shot Reasoning with Self-Adaptive Prompting. [https://arxiv.org/abs/2305.14106](https://arxiv.org/abs/2305.14106) [↩](https://learnprompting.org/docs/advanced/ensembling/#user-content-fnref-1) [↩<sup>2</sup>](https://learnprompting.org/docs/advanced/ensembling/#user-content-fnref-1-2)

### Valeriia Kuka

Valeriia Kuka, Head of Content at Learn Prompting, is passionate about making AI and ML accessible. Valeriia previously grew a 60K+ follower AI-focused social media account, earning reposts from Stanford NLP, Amazon Research, Hugging Face, and AI researchers. She has also worked with AI/ML newsletters and global communities with 100K+ members and authored clear and concise explainers and historical articles.

[Edit this page](https://github.com/trigaten/Learn_Prompting/tree/v1.2.3/docs)