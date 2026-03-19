---
title: Complexity-Based Prompting
source: https://learnprompting.org/docs/advanced/thought_generation/complexity_based_prompting
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Complexity-Based Prompting leverages complex reasoning chains to improve accuracy of Large Language Models in tasks like math and common sense.
tags:
  - clippings
feature: thumbnails/external/f22423716eac23e86455f4718ba17116.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 4 minutes

Last updated on October 3, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/thought_generation/#Valeriia%20Kuka-bio)

![Overview of Complexity-Based Prompting](https://learnprompting.org/docs/assets/advanced/thought_gen_covers/complex_based_prompting_cover.svg)

Overview of Complexity-Based Prompting

### Information and Links

| Technique | Institution | Date of Publication | Paper | Code |
| --- | --- | --- | --- | --- |
| Complexity-Based Prompting | University of Edinburgh, Allen Institute for AI | Jan 2023 | [Complexity-Based Prompting for Multi-Step Reasoning](https://arxiv.org/abs/2210.00720) | [FranxYao/Complexity-Based-Prompting](https://github.com/FranxYao/Complexity-Based-Prompting) |

## What is Complexity-Based Prompting?

**Complexity-Based Prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/thought_generation/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Fu, Y., Peng, H., Sabharwal, A., Clark, P., &amp; Khot, T. (2023). Complexity-Based Prompting for Multi-step Reasoning. In The Eleventh International Conference on Learning Representations . <a target="_blank" rel="noopener noreferrer" href="https://openreview.net/forum?id=yf1icZHC-l9" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://openreview.net/forum?id=yf1icZHC-l9</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a new technique for improving multi-step reasoning in [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM). The main idea is to use **complex reasoning chains** (those with more steps) as examples when prompting the model. This method improves performance in reasoning tasks like math problems and commonsense reasoning by focusing on both **input prompts** and **output selection**.

## How This Technique Differs from Existing Methods

Standard prompting techniques, such as [Chain-of-Thought (CoT) Prompting](https://learnprompting.org/docs/intermediate/chain_of_thought), have shown success in multi-step reasoning by asking LLMs to generate intermediate reasoning steps before providing a final answer. However, it wasn’t clear which types of examples make the best prompts. Complexity-Based Prompting shows that **more complex examples**, which require more reasoning steps, result in **better model performance** compared to simpler ones.

The method also applies to output selection: when multiple reasoning chains are generated, the model chooses the majority answer from the more complex reasoning chains. This process, called **complexity-based consistency**, further boosts accuracy.

1. [Chain-of-Thought (CoT) Prompting](https://learnprompting.org/docs/intermediate/chain_of_thought): CoT prompting improves multi-step reasoning by breaking down a problem into smaller steps, but **complexity-based prompting** goes further by selecting examples with **more steps**, improving overall accuracy.
2. [Self-Consistency](https://learnprompting.org/docs/intermediate/self_consistency): Self-Consistency selects the most common answer from multiple reasoning chains, while **complexity-based consistency** focuses on the most complex and robust reasoning paths, leading to more accurate results.
3. **Annotation Efficiency**: Unlike retrieval-based methods that require large-scale annotated datasets, complexity-based prompting can be applied with only a Few-Shot learning setup, making it more efficient.

## Benefits

- **Richness of reasoning**: Complex prompts provide a more detailed view of problem-solving, making the model capable of handling a wide range of reasoning tasks.
- **Avoiding shortcuts**: Complex reasoning chains prevent the model from relying on shortcuts, which can lead to mistakes, especially in tasks requiring detailed logic.
- **Better generalization**: Using complex prompts improves generalization, meaning the model performs better not only on difficult tasks but also on simpler tasks.

## How Complexity-Based Prompting Works

1. **Selecting Complex Prompts**: In complexity-based prompting, examples with **longer reasoning chains** (more steps) are chosen as input prompts. The intuition is that complex examples provide richer reasoning patterns, covering a wider range of reasoning skills. These prompts teach the model to handle both simple and complex reasoning cases.
2. **Complexity-Based Consistency**: When generating reasoning chains for a new problem, the model produces multiple possible solutions. Instead of selecting the majority answer from all generated chains (as in self-consistency), **complexity-based consistency** focuses on selecting the majority answer from the **most complex reasoning chains**. This ensures that the most thorough reasoning processes influence the final decision.

## How to Use Complexity-Based Prompting

1. **Select Complex Prompts**: When constructing a prompt, choose examples with a **higher number of reasoning steps**.
2. **Generate Multiple Outputs**: Sample multiple reasoning paths from the model for each test question.
3. **Vote Among Complex Chains**: Choose the final answer based on the majority from the **most complex reasoning paths** rather than all paths.

Tip

The code for Complexity-Based Prompting is open-sourced and available for further research and implementation at [FranxYao/Complexity-Based-Prompting](https://github.com/FranxYao/Complexity-Based-Prompting).

## Results of Complexity-Based Prompting

This method was tested on multiple benchmarks and significantly outperformed existing prompting techniques like CoT and Self-Consistency, setting new state-of-the-art results.

| **Task** | **Previous SOTA** | **Complex Prompt (Codex)** | **\+ Voting Complex** |
| --- | --- | --- | --- |
| **GSM8K (Math)** | 74.4% | 82.6% | 82.9% |
| **MultiArith** | 99.3% | 99.7% | 99.8% |
| **MathQA** | 37.4% | 47.3% | 60.0% |
| **Date Understanding** | 79.2% | 86.8% | N/A |
| **Penguins** | 78.1% | 80.8% | N/A |

- **Substantial Improvement**: Complexity-based prompting improves performance by an average of **+5.3%** and up to **+18%** on benchmarks like MathQA.
- **Efficient**: Requires fewer examples to train while achieving better results.
- **Robust**: Works consistently across various tasks, including math, temporal reasoning, and referential tasks.

## Conclusion

**Complexity-Based Prompting** offers a straightforward yet highly effective method for improving multi-step reasoning in large language models. By selecting prompts and outputs based on the complexity of reasoning chains, this method significantly enhances accuracy across multiple benchmarks.