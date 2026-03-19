---
title: "Decomposed Prompting (DecomP): Breaking Down Complex Tasks for LLMs"
source: https://learnprompting.org/docs/advanced/decomposition/decomp
author:
  - '[["Bhuwan Bhatt"]]'
published:
created: 2025-09-07
description: Learn how Decomposed Prompting breaks down complex tasks into manageable sub-tasks, enhancing LLM performance. Discover its advantages over Few-Shot prompting.
tags:
  - clippings
feature: thumbnails/external/93351d0059cc4c9f15b1b78aca808ffb.svg
---
Reading Time: 3 minutes

Last updated on September 27, 2024

[Bhuwan Bhatt](https://learnprompting.org/docs/advanced/decomposition/#Bhuwan%20Bhatt-bio)

![decomposer prompt and sub-task handler](https://learnprompting.org/docs/assets/advanced/advanced_covers/Decomposed_Prompting_cover.svg)

Takeaways

- Understand the limitations of [Few-Shot prompting](https://learnprompting.org/vocabulary/few-shot_prompting).
	- Understand the working mechanism and advantages of Decomposed Prompting.

## Introduction

[Few-Shot Prompting](https://learnprompting.org/docs/basics/few_shot) allows [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) to solve problems without explicit [fine-tuning](https://learnprompting.org/vocabulary/fine-tuning). However, this approach struggles as task complexity increases. **Decomposed Prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Tushar Khot. (2023). Decomposed Prompting: A Modular Approach for Solving Complex Tasks. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> or **DecomP** is a modular approach that tackles complex tasks by breaking them into simpler sub-tasks, delegating each sub-task to LLMs or other handlers better suited to solve them.

## How to Use Decomposed Prompting?

First, a decomposer prompt outlines the process of solving a complex task through smaller sub-tasks. Each of these sub-tasks is then handled by specific sub-task handlers. These handlers can:

- Use Decomposed Prompting to further break down the task,
- Use a simple prompt to solve the sub-task, or
- Apply a function to handle the sub-task.

There are three key advantages to this technique:

1. Each sub-task handler can be given richer, more targeted [exemplars](https://learnprompting.org/vocabulary/exemplars), leading to more accurate responses.
2. Complex sub-tasks can be further simplified and solved.
3. Sub-task handlers can be reused across multiple tasks.

### DecomP in Action: Letter Concatenation

Let’s consider an example of Decomposed Prompting in action. Suppose we need to concatenate the first letter of each word in a string, using spaces as separators. This can be achieved by breaking the problem into three sub-tasks:

1. Split the string into a list of words.
2. Extract the first letter from each word.
3. Concatenate the extracted letters, using spaces as separators.

First, the decomposer specifies the sequence of questions and corresponding sub-tasks:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

QC: Concatenate the first letter of every word in "Jack Ryan" using spaces Q1: \[split\] What are the words in "Jack Ryan"? #1: \["Jack". "Ryan"\] Q2: (foreach) \[str\_pos\] What is the first letter of #1? #2: \["J", "R"\] Q3: \[merge\] Concatenate #2 with spaces #3: "J R" Q4: \[EOQ\]

Here, \[EOQ\] indicates the end of the question. Each sub-task is processed by its handler, with the solution from one sub-task passed to the next. For example, the result of Q1 ("Jack", "Ryan") is used as input for Q2 in this case.

In the example, the decomposer relies on two task-specific handlers:

- split: Finds character positions in strings
- str\_pos: Concatenates characters

The Few-Shot prompts for these task-specific handlers might look like this:

- `split`

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Q: What are the words in "Elon Musk Tesla"? A: \["Elon", "Musk", "Tesla"\] Q: What are the letters in "C++"? A: \["C", "+", "+"\] ...

- `str_pos`

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Q: Concatenate \["n", "i", "e"\] A: "nie" Q: Concatenate \["n", "i", "c", "e"\] using spaces A: "n i c e" ...

Once all the sub-tasks are executed, the last answer before \[EOQ\] is returned as the final response.

A more detailed representation of the prompt execution and inference procedure is provided in the example below:

![Inference procedure in Decomposed Prompting](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fdecomp_detailed.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Inference procedure in Decomposed Prompting<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Tushar Khot. (2023). Decomposed Prompting: A Modular Approach for Solving Complex Tasks.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

The decomposer prompt determines the first sub-task to be completed: splitting words in this case. The sub-task is handled by the **split** sub-task handler and the answer generated is appended to the decomposer prompt to get the second sub-task. The process continues until the decomposer prompt produces \[EOQ\]. At this point, there are no more tasks left and the last answer is returned as the solution.

## What Are Decomposed Prompting Results?

- Decomposed Prompting outperforms and generalizes better than [Chain-of-Thought (CoT) Prompting](https://learnprompting.org/docs/intermediate/chain_of_thought) and [Least-to-Most prompting](https://learnprompting.org/docs/intermediate/least_to_most) in exact match (EM) results on $k^{th}$ letter concatenation task, with $k=3$ and using space as delimiter implying sub-task-specific prompts are more effective at teaching hard sub-tasks than a single CoT prompt.

![results for letter concatenation task](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fkth_letter_concatenation_decomp.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Comparision of the model on k-th letter concatenation task<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Tushar Khot. (2023). Decomposed Prompting: A Modular Approach for Solving Complex Tasks.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

- Decomposed Prompting with Chain-of-Thought further increases the ability of the model to generalize to longer sequence lengths.

![results for sequence reversal task](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fsequence_reversal_decomp.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Comparision of the model on sequence reversal task<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Tushar Khot. (2023). Decomposed Prompting: A Modular Approach for Solving Complex Tasks.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

## Conclusion

While few-shot prompting is an effective technique to improve the performance of LLMs, it can easily fail when the task to be performed is more complex than the exemplars fed to the [LLM](https://learnprompting.org/vocabulary/LLM). Decomposed prompting, on the other hand, can enhance the LLM's performance by decomposing the task into sub-tasks and delegating each sub-task to the task-specific handler which can be another LLM, a function, or a trained model.

Find more on [Decomposition Prompting](https://learnprompting.org/docs/advanced/decomposition/introduction) methods.