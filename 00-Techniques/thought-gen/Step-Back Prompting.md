---
title: Step-Back Prompting
source: https://learnprompting.org/docs/advanced/thought_generation/step_back_prompting
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Step-Back Prompting helps LLMs tackle complex problems by first focusing on high-level concepts, reducing errors.
tags:
  - clippings
feature: thumbnails/external/424669764eb22ac95d49dd0f527d82b7.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 4 minutes

Last updated on October 3, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/thought_generation/#Valeriia%20Kuka-bio)

![Overview of Step-Back Prompting](https://learnprompting.org/docs/assets/advanced/thought_gen_covers/step_back_cover.svg)

Overview of Step-Back Prompting

### Information and Links

| Technique | Institution | Date of Publication | Paper |
| --- | --- | --- | --- |
| Step-Back Prompting | Google DeepMind | Oct 2023 | [Take a Step Back: Evoking Reasoning via Abstraction in Large Language Models](https://arxiv.org/abs/2310.06117) |

## What is Step-Back Prompting?

**Step-Back Prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/thought_generation/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Zheng, H. S., Mishra, S., Chen, X., Cheng, H.-T., Chi, E. H., Le, Q. V., &amp; Zhou, D. (2024). Take a Step Back: Evoking Reasoning via Abstraction in Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2310.06117" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2310.06117</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a technique designed to improve [Large Language Models' (LLMs)](https://learnprompting.org/vocabulary/LLM) ability to solve complex tasks by encouraging them to "step back" and focus on abstract principles before reasoning through details. The method works by prompting the model to first derive **high-level concepts** and **first principles** before tackling specific details. This abstraction helps prevent errors in intermediate steps and leads to more accurate reasoning.

Step-Back Prompting improves performance across reasoning-intensive tasks, such as STEM (science, technology, engineering, math), Knowledge-based QA, and Multi-Hop Reasoning. It has been tested on models like PaLM-2L, GPT-4, and Llama2-70B, showing significant improvements over traditional methods like [Chain-of-Thought (CoT) Prompting](https://learnprompting.org/docs/intermediate/chain_of_thought).

## How Step-Back Prompting Works

The method involves two steps:

1. **Abstraction**: The model is prompted to focus on a higher-level concept or principle related to the question.
2. **Reasoning**: Once the high-level abstraction is retrieved, the model uses it to reason through the specifics of the original question.

For example:

- **Original Question**: "What happens to the pressure of an ideal gas if the temperature is increased by a factor of 2 and the volume is increased by a factor of 8?"
- **Step-Back Abstraction**: "What are the principles involved in this problem?" (Ideal Gas Law)
- **Final Answer**: Using the Ideal Gas Law, the model can calculate the correct answer: the pressure decreases by a factor of 4.

## How Step-Back Prompting Differs from Existing Techniques

1. [Chain-of-Thought (CoT) Prompting](https://learnprompting.org/docs/intermediate/chain_of_thought): CoT prompts the model to solve problems step-by-step in a linear sequence. While this helps break down complex problems, it can lead to mistakes when intermediate steps are faulty. **Step-Back Prompting**, on the other hand, first asks the model to abstract high-level concepts before addressing specifics, reducing errors caused by focusing too soon on details.
2. Take a Deep Breath (TDB) Prompting: TDB prompts models to slow down and carefully process each step, but like CoT, it still works linearly. **Step-Back Prompting** is different because it prompts the model to first generalize the problem and think at a higher level before proceeding.
3. [Decomposition Prompting](https://learnprompting.org/docs/advanced/decomposition/introduction): Decomposition breaks a problem into smaller sub-problems. Step-Back Prompting differs by rephrasing the original question into a more **general** concept, which helps avoid narrow, low-level reasoning errors. It abstracts instead of decomposing.

## How to Use Step-Back Prompting

Consider a question from physics:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Original Question

---

What happens to the pressure of an ideal gas when temperature increases by a factor of 2, and volume increases by a factor of 8?

Let's apply Step-Back Prompting to it by following these steps:

### 1\. **Abstraction Step**

Instead of asking the model to give the answer to the original question, we prompt it with a step-back question. It is a derived question from the original question at a higher level of abstraction.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Step-Back Question

---

What are the fundamental concepts or principles involved in this problem?

Step-Back question is created manually by identifying the core concept behind the question and prompt the model to retrieve relevant facts or principles.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

The Ideal Gas Law: PV = nRT, , where P is the pressure, V is the volume, n is the number of moles, R is the gas constant, and T is the temperature.

### 2\. **Reasoning Step**

After retrieving the principle, guide the model to apply it to solve the original problem.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Reasoning Step

---

Use the Ideal Gas Law: PV = nRT to answer the question: What happens to the pressure of an ideal gas when temperature increases by a factor of 2, and volume increases by a factor of 8?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Apply Ideal gas law to find out the pressure.

If the temperature is increased by a factor of 2, then T becomes 2T. If the volume is increased by a factor of 8, then V becomes 8V.

Substituting these values into the ideal gas law, we get: P(8V) = nR(2T)

Dividing both sides by 8V, we get: P = nR(2T) / 8V

We can see that the pressure has decreased by a factor of 4.

## Results of Step-Back Prompting

**Step-Back Prompting** has demonstrated impressive results across various tasks, including STEM reasoning, knowledge-based question answering, and multi-hop reasoning tasks. Below are performance gains observed with Step-Back Prompting compared to baseline models and other prompting techniques:

| **Task** | **Model** | **Baseline** | **Step-Back Improvement** |
| --- | --- | --- | --- |
| **MMLU (Physics)** | PaLM-2L | 66.4% | +7% |
| **MMLU (Chemistry)** | PaLM-2L | 70.9% | +11% |
| **TimeQA** | PaLM-2L | 41.5% | +27% |
| **MuSiQue** | PaLM-2L | 35.5% | +7% |
| **StrategyQA** | PaLM-2L | 82.8% | +3.6% |

- **Substantial Performance Gains**: Step-Back Prompting outperforms Chain-of-Thought and Take-a-Deep-Breath prompting methods, with improvements ranging from 7% to 27% depending on the task.
- **Error Reduction**: Step-Back Prompting reduces reasoning errors by focusing first on high-level abstractions before diving into specifics.
- **Robustness**: The method is model-agnostic, showing improvements on multiple LLMs (PaLM-2L, GPT-4, and Llama2-70B).

## Conclusion

**Step-Back Prompting** is a powerful technique for improving complex reasoning tasks in Large Language Models by first prompting for abstraction before diving into detailed reasoning. This method has shown significant improvements in performance across various domains, making it a valuable tool for enhancing LLM capabilities.