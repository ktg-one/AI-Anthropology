---
title: Prompt Paraphrasing
source: https://learnprompting.org/docs/advanced/ensembling/prompt_paraphrasing
author:
  - '[["Bhuwan Bhatt"]]'
published:
created: 2025-09-01
description: Prompt Paraphrasing, a technique to create more varied high-quality prompts for the language model of your choice.
tags:
  - clippings
feature: thumbnails/external/76e695d5fa5c355b94b44cf2ee9dd409.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on November 7, 2024

[Bhuwan Bhatt](https://learnprompting.org/docs/advanced/ensembling/#Bhuwan%20Bhatt-bio)

![Overview of Prompt Paraphrasing (@jiang2019howcanweknow)](https://learnprompting.org/docs/assets/prompt_paraphrasing.svg)

Overview of Prompt Paraphrasing<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/ensembling/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Jiang, Z., Xu, F. F., Araki, J., &amp; Neubig, G. (2019). How Can We Know What Language Models Know? <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/1911.12543" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/1911.12543</a></span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

## Introduction

[Large language models (LLMs)](https://learnprompting.org/vocabulary/LLM) are trained on extensive text data, making them a rich source of information. However, the way you phrase a question (or [prompt](https://learnprompting.org/docs/basics/prompt_engineering)) can impact the response accuracy, even if the model "knows" the answer. In some cases, small changes in wording can make a big difference. For example:

- Prompt 1:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Obama is a \_\_

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

good person

- Prompt 2:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Obama is a \_\_ by profession

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

politician

Despite being similar, only the second prompt yields a correct response.

In this document, we'll talk about **Prompt Paraphrasing**, a technique to create more varied high-quality prompts for a specific LLM:

- What is Prompt Paraphrasing?
- How to Use Prompt Paraphrasing
- How to Choose the Best Prompt
- Results of Prompt Paraphrasing
- Limitations of Prompt Paraphrasing

## What is Prompt Paraphrasing?

**Prompt Paraphrasing**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/ensembling/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Jiang, Z., Xu, F. F., Araki, J., &amp; Neubig, G. (2019). How Can We Know What Language Models Know? <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/1911.12543" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/1911.12543</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a technique used to generate multiple high-quality prompts that retrieve more accurate answers from the model. It takes an initial "seed" prompt and creates several semantically similar versions.

For instance, starting with "*x shares a border with y*" might yield:

- "*x has a common border with y*"
- "*x adjoins y*"

Prompt Paraphrasing uses the LLM itself to generate paraphrased prompts. This way, it leverages the language patterns and templates the model has "learned" best during training.

## How to Use Prompt Paraphrasing

A simple paraphrasing method involves back-translation. Here’s how it works:

1. Translate the original prompt into one or more other languages.
2. Translate these versions back into the original language to create prompts that are different in wording but similar in meaning.

### Example

If you want to find the CEO of a company, you may start with an initial prompt having the structure: "Who is the CEO of company\_name?". An example prompt can be: Who is the CEO of Apple?

Then, you can generate multiple prompt candidates using translation. Say, you want to generate 2 different prompt candidates.

### Step 1: Translate to Other Languages

- **Spanish Translation:**

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Convert the following into spanish: Who is the CEO of Apple?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

¿Quién es el CEO de Apple?

- **French Translation:**

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Convert the following into French: Who is the CEO of Apple?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Qui est le PDG d'Apple ?

### Step 2: Back-Translate to English

- **Spanish to English:**

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Convert the following sentence into English: ¿Quién es el CEO de Apple?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Who is the executive head of Apple?

- **French to English:**

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Convert the following sentence into English: Qui est le PDG d'Apple ?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Name the current CEO of Apple.

After paraphrasing, you now have a set of prompts:

- *Who is the CEO of *x*?*
- *Who is the executive head of *x*?*
- *Name the current CEO of *x*.*

## How to Choose the Best Prompt

After generating several prompts, how do you select the best one? There are two primary approaches<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/ensembling/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Jiang, Z., Xu, F. F., Araki, J., &amp; Neubig, G. (2019). How Can We Know What Language Models Know? <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/1911.12543" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/1911.12543</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> :

- Top-1 Prompt Selection: In this approach, prompts are tested on a training set. Each prompt's accuracy is calculated, and the one with the highest accuracy is chosen for inference.
- Ensemble: Here, all candidate prompts are used simultaneously. Responses are combined using techniques like majority voting (for classification tasks) or averaging (for regression tasks) to produce a final answer.

## Results of Prompt Paraphrasing

Studies show that paraphrasing enhances model performance. For example:

- A manual prompt yields 22.8% accuracy with the BERT-base model.
- Paraphrased prompts improve performance across various selections and models.

| Prompt | Model | Top1 | Top3 | Top5 |
| --- | --- | --- | --- | --- |
| Manual | BERT-base | 22.8 | \- | \- |
| Paraphrased | BERT-base | 22.8 | 23.8 | 24.6 |
| Manual | BERT-large | 25.7 | \- | \- |
| Paraphrased | BERT-large | 25.9 | 27.8 | 28.3 |

## Limitations of Prompt Paraphrasing

- **Computational Cost:** Paraphrasing requires multiple model queries, especially when using ensemble methods.
- **Translation Limits:** Back-translation might revert to the original prompt, which doesn’t add variety.

## Conclusion

Large language models contain vast amounts of knowledge, but phrasing matters. By using prompt paraphrasing, you can create prompts that maximize the retrieval of relevant information, improving model responses for specific factual queries.

## Footnotes

1. Jiang, Z., Xu, F. F., Araki, J., & Neubig, G. (2019). How Can We Know What Language Models Know? [https://arxiv.org/abs/1911.12543](https://arxiv.org/abs/1911.12543) [↩](https://learnprompting.org/docs/advanced/ensembling/#user-content-fnref-1) [↩<sup>2</sup>](https://learnprompting.org/docs/advanced/ensembling/#user-content-fnref-1-2) [↩<sup>3</sup>](https://learnprompting.org/docs/advanced/ensembling/#user-content-fnref-1-3)

### Bhuwan Bhatt

Bhuwan Bhatt, a Machine Learning Engineer with over 5 years of industry experience, is passionate about solving complex challenges at the intersection of machine learning and Python programming. Bhuwan has contributed his expertise to leading companies, driving innovation in AI/ML projects. Beyond his professional endeavors, Bhuwan is deeply committed to sharing his knowledge and experiences with others in the field. He firmly believes in continuous improvement, striving to grow by 1% each day in both his technical skills and personal development.

[Edit this page](https://github.com/trigaten/Learn_Prompting/tree/v1.2.3/docs)