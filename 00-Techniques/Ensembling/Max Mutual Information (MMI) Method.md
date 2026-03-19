---
title: Max Mutual Information (MMI) Method
source: https://learnprompting.org/docs/advanced/ensembling/max_mutual_information_method
author:
  - '[["Andres Caceres"]]'
published:
created: 2025-09-07
description: Learn how to use the max mutual information (MMI) method to select optimal prompt templates.
tags:
  - clippings
feature: thumbnails/external/09c6c29f9a6424c6c8487bc0204c5d1e.failed.png
thumbnail: thumbnails/resized/2a2ac1cb019c2b350cad9dc4215180e6_86cf658e.webp
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on October 26, 2024

[Andres Caceres](https://learnprompting.org/docs/advanced/ensembling/#Andres%20Caceres-bio)

![Max Mutual Information Method Overview](https://learnprompting.org/docs/assets/advanced/maximum_mutual_information_method_cover.svg)

Overview of Max Mutual Information Method

## What is MMI?

**Max Mutual Information Method (MMI)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/ensembling/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Sorensen, T., Robinson, J., Rytting, C., Shaw, A., Rogers, K., Delorey, A., Khalil, M., Fulda, N., &amp; Wingate, D. (2022). An Information-theoretic Approach to Prompt Engineering Without Ground Truth Labels. Proceedings of the 60th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers). <a target="_blank" rel="noopener noreferrer" href="https://doi.org/10.18653/v1/2022.acl-long.60" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://doi.org/10.18653/v1/2022.acl-long.60</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a way to choose the optimal prompt template for your task by using the mutual information score between the template and the output of the model as a metric, and finding whichever template from your list of templates maximizes that metric.

**Mutual information (MI)** is a concept from information theory that quantifies how much information two variables share. In this case, it measures how much a given prompt reveals about the model's output. The intuition is that a prompt with high MI is more likely to produce accurate responses, even if we don’t know the "right" answer ahead of time.

## Benefits and Applications

- **No Need for Labeled Data or Model Access**: The MMI method selects optimal prompt templates without requiring labeled examples or direct access to model parameters.
- **You Can Make Your Own Templates**: Instead of needing a dataset of templates, you can use MMI with templates that you've made to see which is the best out of those.
- **Efficient and Scalable**: MMI can select effective prompts without manual tuning or operations on datasets, making it efficient and easy to scale computationally

## How MMI Works

- **Step 1: Generate Templates**: Generate a set of prompt templates for your task. This can be done manually or by generating them with an LLM.
- **Step 2: Run Sample Inputs**: The model runs a few sample inputs to verify that the prompts generate reasonable outputs.
- **Step 3: Calculate Mutual Information Scores**: Plug in each template into the mutual information algorithm to get a score for each template.
- **Step 4: Choose the Template With Highest Score**: Choose whichever template got the highest mutual information score for your prompt.

## Example Use: Country Capitals

First, you get a list of templates for the task:

1. “What is the capital of \[country\]?”
2. “The capital of \[country\] is:”
3. “I need to know the capital of \[country\].”
4. “Tell me the capital of \[country\].”
5. “\[country\] has a capital city called?”

Second, you input them into the model, generate outputs, and calculate the mutual information scores for each. For example, the following is the calculation of the mutual information scores for the first two templates:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

What is the capital of France?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

The capital of France is Paris.

Mutual information score: 0.85

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

The capital of France is:

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Paris.

Mutual information score: 0.92

The third and last step is to choose whichever prompt gets the highest mutual information score. Let's say the second template had the highest mutual information score (0.92), since the output of the model was very concise and answered the prompt as efficiently as possible.

Now you input the chosen prompt template into the model with your chosen country:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

The capital of Chad is:

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

N'Djamena.

## Conclusion

MMI is a simple and efficient approach to selecting the most effective prompt template for a given task. By using a list of templates and the calculated mutual information score for each, MMI lets you find the template that best aligns the model's responses with your task. This method is also flexible and can be used with very few resources.