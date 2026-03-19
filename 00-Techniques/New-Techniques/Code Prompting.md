---
title: Code Prompting
source: https://learnprompting.org/docs/new_techniques/code_prompting
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-08
description: Discover Code Prompting, a technique to improve LLM conditional reasoning by transforming NL tasks into code.
tags:
  - clippings
feature: thumbnails/external/201ec07dd92313d383a946cbc517b2c4.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on March 10, 2025

[Valeriia Kuka](https://learnprompting.org/docs/new_techniques/#Valeriia%20Kuka-bio)

Takeaways

- **Code Prompting Overview**: Code prompting enhances reasoning in large language models (LLMs) by transforming natural language tasks into structured code representations with conditional logic, which improves accuracy in conditional reasoning.
- **Performance Gains**: This approach significantly boosts performance on conditional reasoning tasks across various models and datasets, proving to be more efficient with fewer training examples and improving variable tracking.

![Overview of Code Prompting](https://learnprompting.org/docs/assets/advanced/new_docs_oct3/code_prompting_cover.svg)

Overview of Code Prompting

## What is Code Prompting?

**Code prompting** is a novel technique that enhances reasoning abilities in **text+code** [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) by transforming **natural language (NL) tasks** into **code representations**. Instead of executing the code, the model uses it as a structured input format to reason and generate answers. This approach aims to improve conditional reasoning, where conclusions depend on specific conditions or logical steps like determining eligibility for a visa or loan based on given rules.

## How Code Prompting Works

1. **Problem Conversion**: Natural language problems are transformed into a code-like structure, with conditional logic and variables, while preserving the original text as comments.
2. **Prompting**: The LLM receives the generated code, interprets the structure, and produces answers in **natural language**.

### Example

A question like "Can a widow claim benefits?" is transformed into a code representation, with variables for key terms (e.g., "widow") and conditional logic for eligibility. The LLM uses this structured format to track variables and conditions effectively, improving its reasoning accuracy.

## How to Use Code Prompting

Code prompting can be applied to any reasoning task requiring logical steps or condition-based conclusions. Below is a template for how the code transformation might look:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Template for Code Prompting

---

You are a helpful assistant. Your task is to process a pseudo-code that describes a question and a document. You need to reason using that document and the comments to return the answers. Answers must be a short span of the document. You have to extract the span from the code comments. Do not write anything else. I will give you some examples first.

Q1: \[Question 1\] A1: \[Solution using preudo-code\]

Q2: \[Question 2\] A2: \[Solution using preudo-code\]

Q3: \[Your question\] A3:

Answers must be a short span of the document. You have to extract the span from the code comments. Do not write anything else.

Let’s think step by step:

Tip

You can find original prompts and their implementations on [GitGub](https://github.com/UKPLab/arxiv2024-conditional-reasoning-llms).

## Results of Code Prompting

The performance of code prompting was evaluated on **three datasets** that require conditional reasoning:

- **ConditionalQA (CondQA)**: Scenario-based reasoning
- **BoardgameQA (BGQA)**: Rule-based logic for board games
- **ShARC**: Conversational question-answering

| **Model** | **CondQA (F1)** | **ShARC (F1)** | **BGQA-3 (F1)** | **Avg. Gain (F1)** |
| --- | --- | --- | --- | --- |
| GPT-3.5 | +22.52% | +8.42% | +18.52% | **+8.53%** |
| Mixtral | +7.75% | +4.22% | +14.57% | **+4.23%** |
| Mistral | +16.78% | +2.74% | +5.93% | **+2.74%** |

Code prompts significantly outperformed text-based prompts across all models and datasets, showing the highest gains on reasoning-intensive tasks like BGQA.

- **Sample efficiency**: Code prompts are **more efficient**, performing better with fewer training examples. For example, code prompts with only **one demonstration** outperformed text prompts with **three demonstrations**.
- **Improved variable tracking**: Code formatting helps LLMs track variables and conditions more effectively, leading to fewer errors in reasoning, particularly for multi-step logical tasks.

## Conclusion

Code prompting is an effective strategy for eliciting **conditional reasoning abilities** in text+code LLMs, enhancing their performance on logical tasks by providing structured inputs. This method not only improves accuracy but also **reduces the need for extensive demonstrations**, making it a valuable tool for improving reasoning in AI applications.