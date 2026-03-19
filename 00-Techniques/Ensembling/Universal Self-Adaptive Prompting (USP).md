---
title: Universal Self-Adaptive Prompting (USP)
source: https://learnprompting.org/docs/advanced/ensembling/universal_self_adaptive_prompting
author:
  - '[["Bhuwan Bhatt"]]'
published:
created: 2025-09-01
description: Universal Self-Adaptive Prompting boosts LLM zero-shot performance using pseudo-demonstrations.
tags:
  - clippings
feature: thumbnails/external/990318c8df008ca6236f0e22e7faca19.jpg
thumbnail: thumbnails/resized/59ba36700b2c938fef4e588518ec2a7a_86cf658e.webp
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 4 minutes

Last updated on November 22, 2024

[Bhuwan Bhatt](https://learnprompting.org/docs/advanced/ensembling/#Bhuwan%20Bhatt-bio)

![USP alongside similar techniques](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fadvanced_covers%2Fusp_cover.webp&w=1920&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Overview of Zero-Shot, Few-Shot, COSP, and USP techniques.

### Information and Links

| Technique | Institution | Date of Publication | Paper |
| --- | --- | --- | --- |
| Universal Self-Adaptive Prompting (USP) | Google, University of Oxford | October 2023 | [Universal Self-Adaptive Prompting](https://arxiv.org/abs/2305.14926) |

## Introduction

Modern [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) possess impressive zero-shot abilities making them ideal for numerous applications like classification, text generation, etc. This versatility has driven widespread adoption. However, [zero-shot prompting](https://learnprompting.org/docs/basics/few_shot) often suffers from inconsistent or suboptimal performance due to the lack of clear directions. This variability can lead to unreliable results for the same query.

[Few-shot prompting](https://learnprompting.org/docs/basics/few_shot)—providing examples alongside the query—can significantly improve performance but requires labeled data, which is expensive and time-consuming to obtain. This challenge becomes more pronounced as LLMs are applied across diverse tasks, each requiring its own labeled examples.

Methods like [Self-Consistency (SC)](https://learnprompting.org/docs/intermediate/self_consistency) and [Consistency-based Self-Adaptive Prompting (COSP)](https://learnprompting.org/docs/advanced/ensembling/consistency_based_self_adaptive_prompting) have attempted to improve zero-shot performance but have notable limitations:

1. **Self-Consistency (SC):** Generates multiple few-shot responses and aggregates them—an approach that is computationally expensive and time-intensive.
2. **Consistency-based Self-Adaptive Prompting (COSP):** Task-specific and lacks versatility, making it less applicable across diverse scenarios.

## Introducing Universal Self-Adaptive Prompting (USP)

Universal Self-Adaptive Prompting (USP)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/ensembling/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wan, X., Sun, R., Nakhost, H., Dai, H., Eisenschlos, J. M., Arik, S. O., &amp; Pfister, T. (2023). Universal Self-Adaptive Prompting. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2305.14926" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2305.14926</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is an innovative prompt design method developed for **zero-shot** learning in large language models (LLMs). Zero-shot learning involves prompting a model to perform a task without using any labeled examples for guidance. USP was created to help LLMs perform consistently well across diverse tasks without requiring human-generated examples for tuning. Instead, it generates **pseudo-demonstrations**—examples made from model predictions that guide the model to produce better answers on subsequent prompts.

### Key USP Components:

1. **Pseudo-Demonstrations**: USP leverages model predictions to create examples that resemble a few-shot learning context, thereby improving model accuracy without labeled data.
2. **Task-Type Adaptation**: USP identifies the type of task—such as classification (CLS), short-form generation (SFG), or long-form generation (LFG) and applies specific scoring functions to adapt prompts effectively.
3. **Scoring and Selection**: For each task type, USP uses a selector that scores pseudo-demonstrations based on model confidence, choosing only the most reliable ones to improve prompt quality.

## Why USP Stands Out?

Unlike traditional prompting techniques, USP is:

- **Fully Zero-Shot:** Operates without labeled data, making it cost-effective and scalable.
- **Flexible:** Adapts to diverse task types, including classification, reasoning, and text generation.
- **Performance-Driven**: Achieves results comparable to or better than few-shot prompting, even in complex tasks.

| **Method** | **USP** | **Few-Shot Prompting** | **COSP** |
| --- | --- | --- | --- |
| **Label Requirement** | Unlabeled, model-generated examples | Requires labeled examples | Limited to reasoning tasks |
| **Flexibility** | Adapts to all task types (e.g., classification, generation) | Typically works well on most tasks | Reasoning and specific queries |
| **Performance Gains** | Strong, often comparable to few-shot | High, but depends on availability of labels | Moderate gains with consistency |

## How to Use Universal Self-Adaptive Prompting (USP)?

USP selects task-specific prompts and uses model-generated examples as in-context “demos”, essentially guiding the model as if it were in a few-shot setting. Here's how it works for each task type:

### 1\. **Classification (CLS) Tasks**

- **Example Task**: Sentiment analysis.
- **Scoring**: USP uses entropy of class probabilities to gauge confidence and ensures coverage across all possible classes.
- **Template**: Selects pseudo-demos with the highest confidence, balancing class representation.

### 2\. **Short-Form Generation (SFG) Tasks**

- **Example Task**: Fact-based question answering.
- **Scoring**: USP evaluates self-consistency by comparing model responses generated multiple times, selecting the most consistent answers.
- **Template**: USP compiles the most frequent and confident responses as demos.

### 3\. **Long-Form Generation (LFG) Tasks**

- **Example Task**: Summarization.
- **Scoring**: USP measures consistency in outputs using similarity metrics (e.g., ROUGE scores) across repeated responses.
- **Template**: Identifies pseudo-demos by selecting the most consistent long-form responses, adjusted for diversity.

### Algorithm Overview

1. Select a subset of test queries to generate initial pseudo-demos.
2. For each query:
- Generate responses for classification tasks or multiple outputs for generation tasks using a non-zero temperature setting.
- Add candidates to the pseudo-demo pool.
3. Score candidates and build a final pseudo-demo set.
4. Use the refined pseudo-demos to create a few-shot-like prompt and query the LLM for the final response.

## Results of the Universal Self-Adaptive Prompting (USP)

In testing with various models (e.g., PaLM-540B, PaLM 2), USP often outperformed standard zero-shot methods and, in many cases, approached or even surpassed few-shot baselines across over 40 tasks.

| **Model** | **Task Type** | **Zero-Shot Baseline Accuracy** | **USP Accuracy** | **Few-Shot Baseline Accuracy** |
| --- | --- | --- | --- | --- |
| PaLM-540B | Classification | 68.2% | 73.8% | 73.3% |
| PaLM-540B | Short-Form Generation | 52.4% | 60.6% | 62.0% |
| PaLM-540B | Long-Form Generation | 19.3 ROUGE | 24.9 ROUGE | 26.7 ROUGE |
| PaLM 2-M | Reasoning (BIG-Bench Hard) | 49.5% | 54.2% | 60.4% |

These results highlight USP's capacity to significantly improve zero-shot accuracy by generating more effective prompts.

![USP vs Zero-Shot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fusp_results.webp&w=1920&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

USP vs Zero-Shot

## What Are the Limitations of Universal Self-Adaptive Prompting (USP)?

Despite its strengths, USP has a few limitations:

- **Focus on In-Context Learning:** It optimizes in-context examples but does not refine other input components.
- **Dependence on Model Capabilities:** USP requires models with strong in-context learning abilities and well-calibrated uncertainty outputs, favoring larger, more capable models.
- **Generative Task Variability:** While USP improves zero-shot performance for generative tasks, it may not always surpass few-shot prompting.
- **Limited Evaluation on Non-Text Outputs:** USP has not been extensively tested on tasks requiring non-text outputs, such as code generation.

## Conclusion

Universal Self-Adaptive Prompting (USP) offers a groundbreaking solution for zero-shot learning in LLMs, bridging the gap between performance and scalability by leveraging pseudo-demonstrations. Its ability to adapt to diverse tasks without requiring labeled data makes it a versatile and cost-effective approach, paving the way for more efficient and accessible AI applications.

## Footnotes

1. Wan, X., Sun, R., Nakhost, H., Dai, H., Eisenschlos, J. M., Arik, S. O., & Pfister, T. (2023). Universal Self-Adaptive Prompting. [https://arxiv.org/abs/2305.14926](https://arxiv.org/abs/2305.14926) [↩](https://learnprompting.org/docs/advanced/ensembling/#user-content-fnref-1)

### Bhuwan Bhatt

Bhuwan Bhatt, a Machine Learning Engineer with over 5 years of industry experience, is passionate about solving complex challenges at the intersection of machine learning and Python programming. Bhuwan has contributed his expertise to leading companies, driving innovation in AI/ML projects. Beyond his professional endeavors, Bhuwan is deeply committed to sharing his knowledge and experiences with others in the field. He firmly believes in continuous improvement, striving to grow by 1% each day in both his technical skills and personal development.

[Edit this page](https://github.com/trigaten/Learn_Prompting/tree/v1.2.3/docs)