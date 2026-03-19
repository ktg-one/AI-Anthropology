---
title: "Recursion of Thought Prompting: Solving Complex Tasks Beyond Context Limits"
source: https://learnprompting.org/docs/advanced/decomposition/recursion_of_thought
author:
  - '[["Bhuwan Bhatt"]]'
published:
created: 2025-09-07
description: Learn how Recursion of Thought (RoT) prompting overcomes context length limits by breaking down complex problems into smaller parts, ideal for large-scale tasks.
tags:
  - clippings
feature: thumbnails/external/639a17a926df310cb7bf8aaafe75aa82.svg
---
Reading Time: 3 minutes

Last updated on September 27, 2024

[Bhuwan Bhatt](https://learnprompting.org/docs/advanced/decomposition/#Bhuwan%20Bhatt-bio)

![Recursion of Thought Illustration](https://learnprompting.org/docs/assets/advanced/advanced_covers/recursion_cover.svg)

Takeaways

- **Recursion of Thought (RoT)** overcomes [context length](https://learnprompting.org/vocabulary/context_length) limitations by using a divide-and-conquer strategy, breaking down complex problems into smaller sub-problems.
- **RoT solves large-scale tasks** by processing parts of a problem in separate contexts and then aggregating the results to form the final answer.
- **Training required**: Unlike Chain-of-Thought prompting, RoT requires supervised training before use, making it more resource-intensive.
- **Key applications** include tasks like multi-digit arithmetic and sequence problems that exceed the context window limits of current Large Language Models.
- **Limitations** include the need for prior training and lack of length generalization, meaning models trained with RoT do not automatically adapt to larger problems.

## What is Recursion of Thought Prompting?

One of the major limitations of present-day [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) is that they are limited by their [context length](https://learnprompting.org/vocabulary/context_length). The table below shows the context limit of today's most advanced language models:

| Model Name | Context Window |
| --- | --- |
| gpt-4o | 128,000 tokens |
| gpt-3.5-turbo | 16,385 tokens |
| Gemini 1.0 | 32,000 tokens |

As a result, for complex problems, the context length for [Chain-of-Thought (CoT) prompting](https://learnprompting.org/docs/intermediate/chain_of_thought)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Jason Wei. (2022). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> can grow exponentially and exceed the maximum allowed length.

**Recursion of Thought (RoT) Prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Soochan Lee, G. K. (2023). Recursion of Thought: A Divide-and-Conquer Approach to Multi-Context Reasoning with Language Models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is an inference framework that uses the divide and conquer strategy to divide a problem into multiple sub-problems, solve them in separate contexts, and aggregate the answer from each into a final answer.

## How to Use Recursion of Thought Prompting?

Unlike other methods in this section, you cannot simply prompt the [LLM](https://learnprompting.org/vocabulary/LLM) to use recursive divide and conquer. For the Recursion of Thought to work, you must first train the model using a training dataset. You can train an LLM or any language model, as RoT is a model-agnostic framework.

![decomposer prompt and sub-task handler](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Frot_training_data_sample.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Training Data sample for Recursion of Thought<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Soochan Lee, G. K. (2023). Recursion of Thought: A Divide-and-Conquer Approach to Multi-Context Reasoning with Language Models.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

During inference, RoT utilizes special tokens - `GO`, `THINK`, `STOP` - for recursive context control. As expected, `GO` and `STOP` mark the start and end of a problem sequence. When the model needs to decompose the problem into a simpler version, the subproblem, and solve it, it produces a `THINK` token. It then substitutes the solution to the subproblem back into the problem sequence. The process continues till we get the final solution.

## What Are Recursion of Thought Results?

- The authors train GPT-3 using the RoT framework for 48-digit addition/subtraction and 16-digit multiplication/division. CoT cannot solve those problems due to the context limit of 2048 tokens in GPT-3. Consequently, there is no apples-to-apples comparison. However, GPT-3 trained with RoT achieves near-perfect accuracy in both tasks.
- Results are similar for other problems such as Longest Common Subsequence (LCS), G.2.2 Longest Palindromic Subsequence (LPS), 0-1 knapsack, and Matrix Chain Multiplication (MCM). While CoT cannot solve them beyond a certain complexity, RoT achieves a perfect score.

## Limitations of Recursion of Thought Prompting

There are a few limitations to RoT that make it difficult for people to adopt the framework:

- RoT requires supervised training before you can use it to run inference. This can be a costly and time-consuming procedure.
- RoT is built with a goal to support context length greater than 100K. For common problems, this can be an overkill.
- Unlike humans, RoT is incapable of length generalization. Training on 8-digit multiplication with RoT cannot make a model generalize to 16-digit multiplication.

## Conclusion

For complex problems requiring a large context length, CoT length grows rapidly with increased complexity. Models like GPT-3 cannot accommodate such a huge context length. The RoT framework allows language models with limited context length to solve complex frameworks. However, RoT requires training the model using a labeled dataset before using it for inference. As such, RoT can be a good alternative to expensive and large language models like GPT-4.

Find more on [Decomposition Prompting](https://learnprompting.org/docs/advanced/decomposition/introduction) methods.