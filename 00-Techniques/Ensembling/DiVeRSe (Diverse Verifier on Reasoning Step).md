---
title: DiVeRSe (Diverse Verifier on Reasoning Step)
source: https://learnprompting.org/docs/advanced/ensembling/diverse_verifier_on_reasoning_step
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-01
description: "Improve multi-step reasoning in LLMs with DiVeRSe: diverse prompts, a step-aware verifier, and weighted voting."
tags:
  - clippings
feature: thumbnails/external/71cb5014e1c716f44a1c1be7825a3ef5.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on October 3, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/ensembling/#Valeriia%20Kuka-bio)

![Overview of DiVeRSe (Diverse Verifier on Reasoning Step) (@li2023makinglargelanguagemodels)](https://learnprompting.org/docs/assets/advanced/dicerse_cover.svg)

Overview of DiVeRSe (Diverse Verifier on Reasoning Step)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/ensembling/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Li, Y., Lin, Z., Zhang, S., Fu, Q., Chen, B., Lou, J.-G., &amp; Chen, W. (2023). Making Large Language Models Better Reasoners with Step-Aware Verifier. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2206.02336" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2206.02336</a></span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

## What is DiVeRSe?

**DiVeRSe (Diverse Verifier on Reasoning Steps)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/ensembling/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Li, Y., Lin, Z., Zhang, S., Fu, Q., Chen, B., Lou, J.-G., &amp; Chen, W. (2023). Making Large Language Models Better Reasoners with Step-Aware Verifier. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2206.02336" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2206.02336</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a method designed to enhance the reasoning abilities of [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) by improving the way they handle multi-step problems.

LLMs still struggle with complex tasks like arithmetic word problems. DiVeRSe tackles this by adding three major components:

1. **Diverse Prompts**: It generates varied prompts to encourage different reasoning paths for the same question.
2. **Verifier**: A model that checks the accuracy of reasoning paths and uses a weighted voting scheme to filter out incorrect answers.
3. **Step-Aware Verification**: This verifies each reasoning step independently, identifying where mistakes occur and improving the model's reasoning process step by step.

## How DiVeRSe Works

1. Diverse Prompts: DiVeRSe generates multiple reasoning paths by sampling from different prompts. DiVeRSe randomly selects $M_1$ different prompts for each question, and then sample $M_2$ reasoning paths for each prompt using sampling decoding. This way, you obtain $M = M1 × M2$ diverse reasoning paths for each question.
2. Voting Verifier: Once the model has generated several reasoning paths, the **voting verifier** comes into play. It evaluates each reasoning path, scoring how likely it is to be correct. This is done using a pre-trained model which takes into account both the question and the reasoning steps. The verifier guides a voting mechanism, weighting paths based on their probability of being correct rather than simply counting how many paths lead to a specific answer.
3. Step-Aware Verification: A major innovation of DiVeRSe is its **step-aware verifier**, which checks the correctness of each individual step in the reasoning chain. Often, some steps may be correct while others are wrong, leading to an incorrect final answer. DiVeRSe identifies these mistakes by labeling each step and comparing it to known correct reasoning patterns. This helps improve the overall reasoning process by pinpointing where the error occurs and correcting it.

## How to Use DiVeRSe

DiVeRSe can be applied to a range of reasoning tasks, especially those that require step-by-step logic. Here’s how to use on a math problem.

### 1\. Generate Diverse Reasoning Paths

Sample multiple reasoning paths for a given question by generating different prompts.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Q: Janet’s ducks lay 16 eggs per day. She eats 3 for breakfast every morning and uses 4 eggs for baking muffins. She sells the remaining eggs for $2 each. How much money does she make per day?

A:

Generated Reasoning Paths:

```
[Sample 1] 16 - 3 = 13 eggs left, 13 - 4 = 9 eggs left. She sells 9 eggs for $2 each, so 9 * 2 = $18.
[Sample 2] 16 - 3 = 13 eggs, 13 - 4 = 9 eggs, 9 eggs sold for $2 each, so $18.
```

### 2\. Score Reasoning Paths

Use the **verifier** to score each path based on its likelihood of being correct.

```
- Path 1: 91.2% correct.
- Path 2: 88.5% correct.
```

### 3\. Step-Aware Verification

Apply step-aware verification to check the correctness of individual reasoning steps.

```
- Step 1: Correct subtraction (16 - 3 = 13).
- Step 2: Correct subtraction (13 - 4 = 9).
- Step 3: Correct multiplication (9 * 2 = 18).
```

### 4\. Final Answer

Use weighted voting to arrive at the final answer, selecting the most likely correct answer based on the verified reasoning paths.

```
Final Answer: $18.
```

Tip

Acess the [open-source code](https://github.com/microsoft/CodeT).

## Results of DiVeRSe

DiVeRSe was evaluated on several reasoning tasks, including arithmetic reasoning (e.g., [GSM8K](https://paperswithcode.com/dataset/gsm8k), MultiArith), commonsense reasoning (e.g., CommonsenseQA), and inductive reasoning (e.g., CLUTRR). The method achieved state-of-the-art results on many of these benchmarks, outperforming previous approaches like [self-consistency](https://learnprompting.org/docs/intermediate/self_consistency) and [greedy decoding](https://learnprompting.org/vocabulary/greedy_decoding).

| **Task** | **Previous SOTA** | **Self-Consistency** | **DiVeRSe** |
| --- | --- | --- | --- |
| **GSM8K** | 74.4% | 76.7% | **82.3%** |
| **AsDiv** | 81.9% | 86.2% | **88.7%** |
| **MultiArith** | 99.3% | 98.6% | **99.8%** |
| **SVAMP** | 86.6% | 85.8% | **87.0%** |
| **SingleEq** | 79.5% | 93.7% | **94.9%** |
| **CLUTRR** | 67.0% | 35.6% | **95.9%** |

## Conclusion

DiVeRSe offers a powerful method to enhance the reasoning abilities of large language models by leveraging diverse prompts, verifier-based scoring, and step-aware verification. This approach not only improves overall accuracy but also provides finer control over the reasoning process, allowing for more reliable and interpretable results. As LLMs continue to evolve, DiVeRSe represents a step forward in making these models more capable and trustworthy in complex reasoning tasks.

## Footnotes

1. Li, Y., Lin, Z., Zhang, S., Fu, Q., Chen, B., Lou, J.-G., & Chen, W. (2023). Making Large Language Models Better Reasoners with Step-Aware Verifier. [https://arxiv.org/abs/2206.02336](https://arxiv.org/abs/2206.02336) [↩](https://learnprompting.org/docs/advanced/ensembling/#user-content-fnref-1) [↩<sup>2</sup>](https://learnprompting.org/docs/advanced/ensembling/#user-content-fnref-1-2)

### Valeriia Kuka

Valeriia Kuka, Head of Content at Learn Prompting, is passionate about making AI and ML accessible. Valeriia previously grew a 60K+ follower AI-focused social media account, earning reposts from Stanford NLP, Amazon Research, Hugging Face, and AI researchers. She has also worked with AI/ML newsletters and global communities with 100K+ members and authored clear and concise explainers and historical articles.

[Edit this page](https://github.com/trigaten/Learn_Prompting/tree/v1.2.3/docs)