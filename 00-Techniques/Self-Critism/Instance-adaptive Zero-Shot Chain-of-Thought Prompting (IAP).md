---
title: Instance-adaptive Zero-Shot Chain-of-Thought Prompting (IAP)
source: https://learnprompting.org/docs/new_techniques/instance_adaptive_zero_shot_chain_of_thought
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-08
description: Explore Instance-adaptive Zero-Shot CoT Prompting, a technique to improve LLM reasoning accuracy by selecting prompts per question.
tags:
  - clippings
feature: thumbnails/external/8565511681c5e9e1093a2bd4c5527be4.svg
---
◆ This article is rated [hard](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on March 10, 2025

[Valeriia Kuka](https://learnprompting.org/docs/new_techniques/#Valeriia%20Kuka-bio)

Takeaways

- **IAP Overview**: Instance-adaptive Zero-shot [CoT Prompting](https://learnprompting.org/vocabulary/CoT_Prompting) (IAP) enhances reasoning in large language models (LLMs) by tailoring prompts to individual questions, improving the accuracy of zero-shot reasoning.
- **Methodology**: IAP selects prompts based on saliency scores that analyze how well a prompt facilitates information flow between the question, prompt, and rationale, using strategies like Sequential Substitution (IAP-ss) and Majority Vote (IAP-mv).
- **Performance Gains**: IAP consistently outperformed traditional task-level prompting in various reasoning tasks, showing significant accuracy improvements, particularly in complex multi-step problems.

![Overview of Instance-adaptive Zero-Shot Chain-of-Thought Prompting (IAP)](https://learnprompting.org/docs/assets/advanced/new_docs_oct3/instance_zero_shot_cot_cover.svg)

Overview of Instance-adaptive Zero-Shot Chain-of-Thought Prompting (IAP)

## What is Instance-adaptive Zero-Shot CoT Prompting?

**Instance-adaptive Zero-Shot Chain-of-Thought (CoT) Prompting (IAP)** is a strategy designed to improve reasoning performance in [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) by selecting the most effective prompt on a per-instance basis. Unlike traditional approaches that use a single prompt for all questions in a task (task-level prompting), IAP tailors prompts to each individual question, enhancing the accuracy and effectiveness of **Zero-Shot CoT reasoning**.

### How It Works:

1. **Prompt Selection Based on Information Flow**: IAP analyzes how well a prompt helps the LLM aggregate information from the question to the prompt and from the question and prompt to the reasoning steps (rationale). By using **saliency scores**, the model can identify which prompts are better at transferring the necessary information to get the correct answer.
2. **Adaptive Mechanism**: IAP employs two strategies for prompt selection:
	- **Sequential Substitution (IAP-ss)**: This method evaluates each prompt sequentially, stopping when a good prompt is found for the instance.
	- **Majority Vote (IAP-mv)**: This method evaluates all candidate prompts and selects the answer based on the highest-scoring prompts.
3. **Saliency Score Calculation**: Saliency scores measure the importance of each token's contribution to the reasoning. IAP computes saliency scores for three key interactions:
	- **Question-to-Prompt**: How well the prompt reflects the question.
	- **Question-to-Rationale**: How much information from the question contributes directly to the reasoning.
	- **Prompt-to-Rationale**: How well the prompt influences the reasoning process.

## How IAP Differs from Existing Techniques

- **Task-Level vs. Instance-Level**: Previous methods like Plan-and-Solve or OPPR aim to find the best prompt for an entire task. IAP, however, selects the best prompt for each individual question, making it more flexible and accurate.
- **Saliency-Based Approach**: While task-level methods focus on crafting optimal prompts for general use, IAP uses saliency score analysis to dynamically select prompts that better suit the specific information flow of each instance.
- **Improved Long-Range Reasoning**: IAP's ability to adapt to individual questions makes it especially effective in tasks that require complex, multi-step reasoning.

## How to Use IAP

IAP is particularly useful for reasoning tasks such as math problems, logic puzzles, and commonsense reasoning. To implement it, you would:

1. **Prepare Prompts**: Collect a set of diverse prompts with different reasoning styles, such as "Let’s think step by step" or "Don’t think. Just feel."
2. **Analyze Information Flow**: Use saliency score analysis to evaluate how well each prompt helps the LLM handle the question at hand.
3. **Select or Combine Prompts**: Depending on the strategy (IAP-ss or IAP-mv), either sequentially test prompts or aggregate results to find the best reasoning path.

## Results of IAP

IAP was tested on various reasoning tasks, including math (GSM8K, SVAMP), logic (Causal Judgment), and commonsense reasoning (CommonsenseQA, MMLU), using multiple LLMs such as LLaMA-3, Qwen, and LLaMA-2. It consistently outperformed task-level prompting approaches like OPPR and Self-discover, achieving significant accuracy improvements across different models and datasets.

### Key Results:

| **Dataset** | **Task** | **Accuracy (Best Prompt)** | **IAP-mv Accuracy** | **Improvement** |
| --- | --- | --- | --- | --- |
| GSM8K | Math Reasoning | 64.52% | 66.34% | +1.82% |
| SVAMP | Math Reasoning | 73.67% | 77.33% | +3.66% |
| Causal Judge | Logic Reasoning | 18.18% | 29.95% | +11.77% |
| CSQA | Commonsense Reasoning | 64.95% | 68.39% | +3.44% |

These results highlight that IAP significantly boosts accuracy, particularly in tasks involving complex reasoning and multi-step problem-solving.

## Conclusion

Instance-adaptive Zero-shot Chain-of-Thought Prompting (IAP) offers a dynamic, saliency-based approach to prompt selection for reasoning tasks. By tailoring prompts to each question rather than applying a one-size-fits-all solution, IAP improves LLM performance across math, logic, and commonsense reasoning tasks. Its ability to adaptively enhance the information flow between the question, prompt, and rationale makes it a powerful tool for zero-shot reasoning with LLMs.