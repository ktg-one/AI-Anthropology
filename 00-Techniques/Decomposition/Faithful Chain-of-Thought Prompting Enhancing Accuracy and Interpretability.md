---
title: "Faithful Chain-of-Thought Prompting: Enhancing Accuracy and Interpretability"
source: https://learnprompting.org/docs/advanced/decomposition/faithful_cot
author:
  - '[["Bhuwan Bhatt"]]'
published:
created: 2025-09-07
description: Learn how Faithful Chain-of-Thought (CoT) reasoning improves model accuracy and interpretability by ensuring final answers align with the presented reasoning process.
tags:
  - clippings
feature: thumbnails/external/2fc0ecca0d60e6a82eb6ebeb890b85c1.svg
---
Reading Time: 5 minutes

Last updated on September 27, 2024

[Bhuwan Bhatt](https://learnprompting.org/docs/advanced/decomposition/#Bhuwan%20Bhatt-bio)

![Flowchart showing the procedure of Faithful Chain-of-Thought (CoT) Reasoning](https://learnprompting.org/docs/assets/advanced/advanced_covers/faithful_cot_cover.svg)

Takeaways

- **Chain-of-Thought (CoT) reasoning** improves accuracy but may not reflect the actual process behind the final answer.
- **Faithful CoT** ensures the final answer comes directly from the reasoning chain, improving trust and [interpretability](https://learnprompting.org/vocabulary/interpretability).
- It uses two steps: **translation** (breaking down the query) and **problem solving** (executing the reasoning chain).
- **Faithful CoT outperforms other methods** in most datasets and is robust to exemplar choice.
- **Limitations** include the unclear translation stage and minimal impact of natural language comments on accuracy.

## What is Faithful Chain-of-Thought Reasoning?

Instructing [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) to express their reasoning before answering, known as [Chain-of-Thought (CoT) Prompting](https://learnprompting.org/docs/intermediate/chain_of_thought)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Jason Wei. (2022). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> , can improve response quality and accuracy. By breaking down the reasoning step-by-step, the model is guided toward more thoughtful and precise outcomes. However, research shows that models don’t always follow the reasoning they present when reaching their final answer.

In other words, these models can be **“unfaithful”** to their own logic. The reasoning provided doesn’t always reflect the actual process behind the conclusion. This raises concerns about interpretability, as it becomes harder for users to trust or verify the model’s decision-making. While the model may show its reasoning, it might not match how it actually arrived at the answer.

Here's an example where the final answer is unrelated to the reasoning chain produced by the LM:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Q: John plans to sell all his toys and use the money to buy video games. He has 13 lego sets and he sells them for $15 each. He ends up buying 8 videogames for $20 each and has $5 left. How many lego sets does he still have?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

A: He started with 13 lego sets. He sold them for $15 each. So he must have gotten 13 \* $15 = $195 from selling them. He used this money to buy 8 video games for $20 each. This means he spent 8 \* $20 = $160 on the video games. He had $5 left, so in total he must have had $195 + $5 = $200. The answer is 0. ❌

**Faithful Chain-of-Thought (CoT) Reasoning**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Qing Lyu. (2023). Faithful Chain-of-Thought Reasoning. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a reasoning framework designed to generate trustworthy reasoning chains by ensuring that the final answers are directly derived from the reasoning process. It involves two key stages:

- **Step 1. Translation**: The LLM converts the natural language (NL) query into a reasoning chain, which combines both natural language and symbolic language (SL). The NL component breaks down the complex problem into simpler, independent subproblems, each addressed using a task-specific SL; such as Python, Datalog, [Planning Domain Definition Language (PDDL)](https://learnprompting.org/vocabulary/pddl), etc.
- **Step 2. Problem Solving**: The generated reasoning chain is then executed using a deterministic solver, like a Python interpreter or PDDL planner, to produce the final answer. Since the reasoning chain is actually executed to derive the answer, it provides a faithful explanation of the process, making this approach far more interpretable than standard Chain-of-Thought methods. An added benefit of this transparency is improved correctness.

## How to Use Faithful Chain-of-Thought Reasoning?

The example below demonstrates how you can use Faithful CoT to solve the following math word problem:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Daniel has 17 apples. Rosy gives Daniel 5 oranges and in return Daniel gives her 3 apples. How many apples does Daniel have now?

### Step 1. Translation

First, translate the problem into a reasoning chain containing natural language (NL) and symbolic language (SL). You can employ a [Few-Shot Prompting](https://learnprompting.org/docs/basics/few_shot) approach to do so. In the example below, we translate the query into a reasoning chain that consists of natural language comments and Python code.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiIyAxLiBIb3cgbWFueSBhcHBsZXMgZG9lcyBEYW5pZWwgaGF2ZSBpbiB0aGUgYmVnaW5uaW5nPyAoaW5kZXBlbmRlbnQsIHN1cHBvcnQ6IFtcIkRhbmllbCBoYXMgMTcgYXBwbGVzXCJdKVxubl9hcHBsZXNfYmVnaW4gPSAxN1xuIyAyLiBIb3cgbWFueSBhcHBsZXMgZG9lcyBEYW5pZWwgZ2l2ZSB0byBSb3N5PyAoaW5kZXBlbmRlbnQsIHN1cHBvcnQ6IFtcIkRhbmllbCBnaXZlcyBoZXIgMyBhcHBsZXNcIl0pXG5uX2FwcGxlc19naXZlbiA9IDNcbiMgMy4gRmluYWwgYW5zd2VyOiBIb3cgbWFueSBhcHBsZXMgZG9lcyBEYW5pZWwgaGF2ZSBub3c%2FIChkZXBlbmRzIG9uIDEsIDIpXG5uX2FwcGxlc19maW5hbCA9IG5fYXBwbGVzX2JlZ2luIC0gbl9hcHBsZXNfZ2l2ZW5cblxubl9hcHBsZXNfZmluYWwiLCJwcm9tcHQiOiJJZiB0aGVyZSBhcmUgMyBjYXJzIGluIHRoZSBwYXJraW5nIGxvdCBhbmQgMiBtb3JlIGNhcnMgYXJyaXZlLCBob3cgbWFueSBjYXJzIGFyZSBpbiB0aGUgcGFya2luZyBsb3Q%2FXG5cbiMgTGV0J3Mgd3JpdGUgYSBweXRob24gcHJvZ3JhbSB0byBjb21wdXRlIHRoZSBudW1iZXIgb2YgY2FycyBpbiB0aGUgcGFya2luZyBsb3RcblxuIyAxLiBIb3cgbWFueSBjYXJzIGFyZSB0aGVyZSBpbiB0aGUgYmVnaW5uaW5nPyAoaW5kZXBlbmRlbnQsIHN1cHBvcnQ6IFtcInRoZXJlIGFyZSAzIGNhcnMgaW4gdGhlIHBhcmtpbmcgbG90XCJdKVxubl9jYXJzX2JlZ2luID0gM1xuIyAyLiBIb3cgbWFueSBjYXJzIGFycml2ZT8gKGluZGVwZW5kZW50LCBzdXBwb3J0OiBbXCIyIG1vcmUgY2FycyBhcnJpdmVcIl0pIFxubl9jYXJzX2Fycml2ZSA9IDJcbiMgMy4gRmluYWwgYW5zd2VyOiBIb3cgbWFueSBjYXJzIGFyZSBpbiB0aGUgcGFya2luZyBsb3Q%2FIChkZXBlbmRzIG9uIDEsIDIpIFxubl9jYXJzX3RvdGFsID0gbl9jYXJzX2JlZ2luICsgbl9jYXJzX2Fycml2ZVxuXG5uX2NhcnNfdG90YWxcblxuRGFuaWVsIGhhcyAxNyBhcHBsZXMgLiBSb3N5IGdpdmVzIERhbmllbCA1IG9yYW5nZXMgYW5kIGluIHJldHVybiBEYW5pZWwgZ2l2ZXMgaGVyIDMgYXBwbGVzLiBIb3cgbWFueSBhcHBsZXMgZG9lcyBEYW5pZWwgaGF2ZSBub3c%2FXG5cbiMgTGV0J3Mgd3JpdGUgYSBweXRob24gcHJvZ3JhbSB0byBjb21wdXRlIHRoZSBudW1iZXIgb2YgcmVtYWluaW5nIGFwcGxlcyB3aXRoIERhbmllbC4iLCJtb2RlbCI6ImdwdC00In0%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

In the example, we see that the natural language component of the reasoning chain consists of three types of information:

- **Subquestions:** The LLM breaks down the original question into simpler sub-questions that are easy to answer. Example: *How many apples does Daniel have in the beginning?*
- **Dependency Graph:** The NL components specify whether each subquestion can be answered independently or relies on answers from prior subquestions. Example: *(depends on 1, 2)*.
- **Rationales:** Each subquestion is followed by the rationale to support the answer. Example: *support: \["Daniel has 17 apples"\]*.

### Step 2. Problem Solving

In this step, the generated symbolic language code is executed to obtain the final answer. Since the output is a Python code, we use a Python interpreter to execute the code and get the final result: `14`. You can verify the answer by executing it on the [online Python interpreter](https://www.online-python.com/).

```
# 1. How many apples does Daniel have in the beginning? (independent, support: ["Daniel has 17 apples"])
n_apples_begin = 17
# 2. How many apples does Daniel give to Rosy? (independent, support: ["Daniel gives her 3 apples"])
n_apples_given = 3
# 3. Final answer: How many apples does Daniel have now? (depends on 1, 2)
n_apples_final = n_apples_begin - n_apples_given

n_apples_final

### OUTPUT
------
>>> 14
```

## What Are the Faithful Chain-of-Thought Reasoning Results?

- With [greedy decoding](https://learnprompting.org/vocabulary/greedy_decoding), Faithful CoT outperforms all other techniques in 8 of 10 datasets. Results are similar with self-consistency decoding: Faithful CoT outperforms other techniques in 7 of 10 datasets.

![Faithful CoT vs CoT and LtM](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Ffaithful_cot_results.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Comparison of Faithful CoT with CoT and [Least-to-Most Prompting (LtM)](https://learnprompting.org/docs/intermediate/least_to_most)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Qing Lyu. (2023). Faithful Chain-of-Thought Reasoning.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

- In most datasets, human annotators agree with the reasoning chain produced by Faithful CoT.

![Plausibility of reasoning chain produced by Faithful CoT](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Ffaithful_cot_reasoning_chain_compared.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Human evaluation results of reasoning chain produced by Faithful CoT<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Qing Lyu. (2023). Faithful Chain-of-Thought Reasoning.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

- Faithful CoT is robust to the choice of [exemplars](https://learnprompting.org/vocabulary/exemplars). When exemplars are randomly chosen from the dataset, the mean accuracy fluctuates very slightly (-1.5 to +1.2), suggesting that the performance of Faithful CoT is minimally influenced by the choice of exemplars.

## Limitations of Faithful Chain-of-Thought Reasoning

- While it is easy to see that the problem-solving stage is faithful, the final answer is a result of directly executing the steps in the reasoning chain. The translation stage is still opaque: it is not interpretable how the LLM generates a reasoning chain from the question.
- The NL comments in the reasoning chain make it easy to understand the reasoning for the end user, but, empirical results show that NL comments do not make a big difference in terms of performance.

![Effect of different components in accuracy](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Ffaithful_cot_ablation_result.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Impact of different NL components in the accuracy<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Qing Lyu. (2023). Faithful Chain-of-Thought Reasoning.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

From the image, it is clear that except in the **CLUTRR** dataset, removing the natural language component (No NL) doesn't result in any significant accuracy drop compared to the full prompt.

## Conclusion

Faithful CoT guarantees a faithful reasoning chain for the generated final answer by decomposing the answer generation into two distinct stages: translation and problem solving. Additionally, empirical results from the [ablation](https://learnprompting.org/vocabulary/ablation) study suggest that the framework is robust to the choice of exemplars, and improving the model's interpretability doesn't come at the expense of overall performance.

Find more on [Decomposition Prompting](https://learnprompting.org/docs/advanced/decomposition/introduction) methods.