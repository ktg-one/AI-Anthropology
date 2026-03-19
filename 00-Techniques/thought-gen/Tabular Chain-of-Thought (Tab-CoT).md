---
title: Tabular Chain-of-Thought (Tab-CoT)
source: https://learnprompting.org/docs/advanced/thought_generation/tabular_chain_of_thought_tab_cot
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Tabular Chain-of-Thought (Tab-CoT) enhances LLM reasoning with structured table, outperforming traditional CoT methods.
tags:
  - clippings
feature: thumbnails/external/117704338a37fca468a4df8e79b32dbc.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 4 minutes

Last updated on October 3, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/thought_generation/#Valeriia%20Kuka-bio)

![Overview of Tabular Chain-of-Thought (Tab-CoT) Prompting](https://learnprompting.org/docs/assets/advanced/thought_gen_covers/tab_cot_cover.svg)

Overview of Tabular Chain-of-Thought (Tab-CoT) Prompting

### Information and Links

| Technique | Institution | Date of Publication | Paper | Code |
| --- | --- | --- | --- | --- |
| Tabular Chain-of-Thought Prompting (Tab-CoT) | StatNLP Research Group, Singapore University of Technology and Design | May 2023 | [Tab-CoT: Zero-Shot Tabular Chain-of-Thought](https://arxiv.org/abs/2305.17812) | [Xalp/Tab-CoT](https://github.com/Xalp/Tab-CoT) |

## What is Tabular Chain-of-Thought Prompting (Tab-CoT)?

**Tabular Chain-of-Thought Prompting (Tab-CoT)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/thought_generation/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Jin, Z., &amp; Lu, W. (2023). Tab-CoT: Zero-shot Tabular Chain of Thought. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2305.17812" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2305.17812</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a novel approach to [Chain-of-Thought (CoT) prompting](https://learnprompting.org/docs/intermediate/chain_of_thought). Tab-CoT suggest to structure the reasoning process in CoT in the form of a table.

Unlike traditional CoT methods that rely on verbose natural language prompts, Tab-CoT leverages the power of tables. This allows [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) to reason in a two-dimensional format, ensuring consistency and facilitating a more organized thought process.

## How Tab-CoT Differs from Existing Techniques

1. **Zero-Shot CoT vs. Tab-CoT**: [Zero-Shot CoT](https://learnprompting.org/docs/intermediate/zero_shot_cot) uses “Let’s think step by step” to guide the LLM through reasoning. However, these methods tend to be verbose and often result in less organized outputs. In contrast, **Tab-CoT** generates concise, structured reasoning steps in a table format. It allows for **2-dimensional reasoning**, enabling the model to check for consistency across both rows and columns.
2. **CoT vs. Tab-CoT**: In [CoT](https://learnprompting.org/docs/intermediate/chain_of_thought), human-engineered reasoning demonstrations are used to guide the model. While this method can yield high performance, it requires significant effort to manually create task-specific examples. Tab-CoT removes this need by automatically generating the reasoning structure in a table, making it more scalable across various tasks without manual intervention.

## How Tab-CoT Works

**Tab-CoT** encourages the LLM to captured its reasoning as a series of steps in a table format.

The table typically has the following columns:

- **Step**: Represents the current reasoning step.
- **Subquestion**: A sub-question the model aims to answer at each step.
- **Process**: The reasoning or calculation performed at that step.
- **Result**: The final answer for that step.

This format breaks down complex problems into manageable steps, enabling the model to "think" in a structured way before generating the final answer.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Problem

---

A chef needs to cook 9 potatoes. He has already cooked 7. If each potato takes 3 minutes to cook, how long will it take him to cook the rest?

**Tab-CoT's Table:**

| Step | Subquestion | Process | Result |
| --- | --- | --- | --- |
| 1 | How many potatoes are left to cook? | 9 - 7 = 2 | 2 |
| 2 | How many minutes will it take? | 2 \* 3 minutes | 6 |

This table allows LLMs to provide a more organized and efficient reasoning process compared to standard CoT, which may involve verbose, unstructured explanations.

## How to Use Tab-CoT

To use **Tab-CoT**, follow these steps:

### Step 1. **Formulating the Table**

The reasoning is structured in a table format with predefined columns that reflect the step-by-step thinking process.

Here's the prompt template:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Table Generation Prompt

---

\[Your Question\]

|step|subquestion|procedure|result|

### Step 2. **Answer Extraction**

Once the table is generated, a final prompt like “The answer is” can be used to extract the result from the completed table. This ensures that the model provides the final answer after performing all reasoning steps.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Answer Extraction Prompt

---

Therefore, the answer is

Tip

The code for Tab-CoT is open-sourced by researchers from StatNLP Research Group, Singapore University of Technology and Design, and available for further research and implementation at [Xalp/Tab-CoT](https://github.com/Xalp/Tab-CoT).

## Results of Tab-CoT

**Tab-CoT** has been evaluated on multiple reasoning tasks, including arithmetic, symbolic, and commonsense reasoning tasks. Below are some key results from experiments comparing **Zero-Shot CoT** and **Tab-CoT**:

| **Task** | **Zero-Shot CoT** | **Tab-CoT** |
| --- | --- | --- |
| **SingleEq** | 78.0% | 81.9% |
| **AddSub** | 69.6% | 70.9% |
| **MultiArith** | 78.7% | 81.2% |
| **GSM8K** | 40.7% | 44.4% |
| **AQUA** | 33.5% | 37.0% |
| **SVAMP** | 62.1% | 60.5% |

- **Efficiency**: Tab-CoT reduces the number of tokens generated while maintaining or improving performance across most tasks.
- **Scalability**: It works well in **Zero-Shot** and **Few-Shot** settings without needing manual design of task-specific examples.
- **Improved Reasoning**: Tab-CoT’s structured table approach captures both vertical (step-wise) and horizontal (cross-step) reasoning, which can result in more accurate final answers.

## Conclusion

**Tab-CoT** presents a significant advancement in CoT prompting methods by introducing a highly structured, tabular approach to reasoning. It offers a concise, scalable, and effective solution for reasoning tasks, outperforming traditional CoT methods in several cases. As LLMs continue to evolve, Tab-CoT's table-based reasoning structure could become a standard for promoting structured reasoning in language models.