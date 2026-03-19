---
title: Active Prompting
source: https://learnprompting.org/docs/advanced/thought_generation/active_prompting
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Enhance LLM performance with Active Prompting. Discover how uncertainty-based question selection and CoT annotations improve reasoning and accuracy.
tags:
  - clippings
feature: thumbnails/external/f4d46e3b14af3d1d88a0a16e4926cf7a.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 6 minutes

Last updated on October 3, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/thought_generation/#Valeriia%20Kuka-bio)

![Overview of Active Prompting](https://learnprompting.org/docs/assets/advanced/thought_gen_covers/active_prompt_cover.svg)

Overview of Active Prompting

### Information and Links

| Technique | Institution | Date of Publication | Paper | Code |
| --- | --- | --- | --- | --- |
| Active Prompting | The Hong Kong University of Science and Technology, University of Toronto, The University of Hong Kong, University of Illinois Urbana-Champaign | Feb 2023 | [Active Prompting with Chain-of-Thought for Large Language Models (LLMs)](https://arxiv.org/abs/2302.12246) | [shizhediao/active-prompt](https://github.com/shizhediao/active-prompt) |

## What is Active Prompting?

**Active Prompting** (or **Active-Prompt**)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/thought_generation/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Diao, S., Wang, P., Lin, Y., Pan, R., Liu, X., &amp; Zhang, T. (2024). Active Prompting with Chain-of-Thought for Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2302.12246" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2302.12246</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a technique for improving [Chain-of-Thought (CoT)](https://learnprompting.org/docs/intermediate/chain_of_thought) prompting performance by selectively human-annotating [exemplars](https://learnprompting.org/vocabulary/exemplars) where the model shows the most uncertainty. This approach helps maximize the efficiency of human annotation efforts by focusing only on the most challenging questions for the model.

Active Prompting consists of four main steps:

1. Uncertainty Estimation:
- It prompts the model several times ($k$) with unlabeled questions using Chain-of-Thought Prompting with a few human-written chains-of-thought or [Zero-Shot Chain-of-Thought (CoT)](https://learnprompting.org/docs/intermediate/zero_shot_cot) prompting without human-written chains-of-thought to generate possible answers with intermediate steps for a set of unlabeled questions.
	- It calculates the uncertainty $u$ based on $k$ answers via a selected uncertainty metric.
2. Selection: The questions with the highest uncertainty are selected for human annotation.
3. Annotation: The selected questions from step 2 are manually annotated by humans to provide more accurate answers.
4. Inference: The newly annotated exemplars are used to improve the model’s performance in answering future questions.

Active Prompting saves significant human resources by reducing the need to annotate all training data. It outperforms other techniques such as [Automatic Chain-of-Thought](https://learnprompting.org/docs/advanced/thought_generation/auto_cot) prompting, Random Chain-of-Thought prompting, and [Self-Consistency](https://learnprompting.org/docs/intermediate/self_consistency) on a range of reasoning tasks. Active Prompting research<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/thought_generation/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Diao, S., Wang, P., Lin, Y., Pan, R., Liu, X., &amp; Zhang, T. (2024). Active Prompting with Chain-of-Thought for Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2302.12246" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2302.12246</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is the first to show the benefits of selective question annotation in CoT prompting for solving complex reasoning tasks.

## How to Use Active Prompting?

Let’s break down the Active Prompting process with an example. Assume you have a pool of $n$ unlabeled questions.

### Step 1. Uncertainty Estimation

First, you prompt the model multiple times ($k$) for each unlabeled question using:

- A number of annotated examplars if you want to use CoT option
- "Think step-by-step" if you want to use Zero-Shot CoT option

Let’s say you choose the CoT option. You provide exemplars (Q1 and Q2), then ask your pool question (Q3). Repeat this process $k$ times for each question.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompting k times with CoT option

---

Q1: Josh and Anna were both born on August 17th, but in different years. To consolidate celebrations they also got married on August 17 when Josh turned 22. If today they’re celebrating 30 years of marriage and their combined age is exactly 5 times what Josh’s age was when they married, how old was Anna when they got married?

A1: Let’s think step by step. To calculate how old was Anna when they got married, we have to know their combined age, Josh’s age after 30 years, and Anna’s age after 30 years from their marriage. Since their combined age is 5 times Josh’s age when he got married, their combined age is 5 \* 22 = 110 years. Josh must be 30 years older than his age when they got married, so he is 22 + 30 = 52 years old now. Therefore, Anna’s current age will be 110 - 52 = 58 years. If they married 30 years ago, Anna must have been 58 - 30 = 28 years old when they married The answer is 28.

Q2: John buys a chair. He then buys a table that is 3 times the price of the chair. Then, he buys a couch that is 5 times the price of the table. If John paid $380 for all these items, what is the price of the couch?

A2: Let’s think step by step. To calculate the price of the couch, we need to know the price of the chair, the price of the table, and the relation between the chair, table, couch, and total money paid. Let x be the price of the chair, 3 \* x be the price of the table, and 5 \* (3 \* x) = 15 \* x be the price of the couch. The relationship between the chair, table, couch, and the total price paid is x + 3 \* x + 15 \* x = $380, which is 19 \* x = 380, and x=20. The price of the couch is 15 \* x, which is 15 \* 20 = $300. The answer is 300.

Q3: John has 5 apples, and he gives 2 to Mary. How many apples does John have left?

As a result you will get $k$ answers for each of your $n$ questions.

Next, you need to measure the uncertainty of the model for each question based on the $k$ answers it generates for a given question.

To do that, you select the uncertainty metric. An example metric could be **disagreement**:

You use the disagreement among $k$ generated answers for a given question from the pool. The disagreement calculates the unique answers in the predictions.

- You count the number of unique answers generated for a question, $h$
- Calculate the disagreement by dividing $uncertainty = h/k$

### Step 2. Selection

Then, you select the questions with the highest uncertainty based on the metric. For simplicity, let's review just one example question from the set of the most uncertain questions.

Imagine you take disagreement as an useartainty metric. You prompt the model $k$ times and find that the below question consistently yields different LLM's outputs meaning the model is uncertain in the answer:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

John has 5 apples, and he gives 2 to Mary.

How many apples does John have left?

This is just one example while in reality there can be many of them.

### Step 3. Annotation

You manually annotate the selected question to provide a clear, correct answer:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Annotated Question

---

Q: John has 5 apples, and he gives 2 to Mary. How many apples does John have left?

A: John starts with 5 apples. He gives away 2 apples. Therefore, he has 5 - 2 = 3 apples left.

### Step 4. Inference

This annotated question becomes an example for the model.

Tip

The code for Active Prompting is open-sourced and available for further research and implementation at [shizhediao/active-prompt](https://github.com/shizhediao/active-prompt).

## What are the Experimental Results for Active Prompting?

Active Prompting has demonstrated superior performance across several benchmarks, including arithmetic, commonsense, and symbolic reasoning tasks. It consistently outperforms traditional CoT and other baseline techniques, highlighting its effectiveness in enhancing LLM capabilities.

- **Self-Consistency**: Active-Prompt outperforms self-consistency across most tasks. Active-Prompt shows a 7.2% improvement over SC on arithmetic reasoning tasks. For commonsense and symbolic reasoning, Active-Prompt consistently outperforms SC across all tasks.
- **Chain-of-Thought**: Compared to CoT, Active-Prompt demonstrates significant improvements. For instance, Active-Prompt scores 83.4% on GSM8K, compared to 63.1% by CoT. Across other datasets (e.g., ASDiv, SVAMP, AQUA), Active-Prompt outperforms CoT by margins ranging from 1.0% to 15.4%, showing the robustness of the active selection method.
- **Random Chain-of-Thought**: Active-Prompt also shows consistent improvements over Random-CoT, with higher average performance across the datasets.
- **Automatic Chain-of-Thought**: Though Auto-CoT produces decent results, particularly with code-davinci-002, Active-Prompt surpasses it in every task.

## Limitations of Active Prompting

Despite its advantages, Active Prompting has some limitations:

- **Human Annotation Required**: Some level of human involvement is needed to annotate the most uncertain questions.
- **Choosing the right uncertainty metric matters**: The way we measure uncertainty can impact performance, so we need to pick the right one based on the task at hand.

## Conclusion

Active prompting really enhances how well Large Language Models solve complex reasoning problems. By focusing on the questions the model is most uncertain about, we make the annotation process efficient and tailor it to boost the model's learning.