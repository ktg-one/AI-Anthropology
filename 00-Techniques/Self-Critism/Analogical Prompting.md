---
title: Analogical Prompting
source: https://learnprompting.org/docs/advanced/thought_generation/analogical_prompting
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Analogical Prompting empowers LLMs to learn by analogy, generating relevant examples to solve complex tasks.
tags:
  - clippings
feature: thumbnails/external/f810903ffa6f23990bf8600130905d31.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on October 3, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/thought_generation/#Valeriia%20Kuka-bio)

![Overview of Analogical Prompting](https://learnprompting.org/docs/assets/advanced/thought_gen_covers/analogical_prompt_cover.svg)

Overview of Analogical Prompting

### Information and Links

| Technique | Institution | Date of Publication | Paper |
| --- | --- | --- | --- |
| Analogical Prompting | Google DeepMind, Stanford University | Oct 2023 | [Large Language Models as Analogical Reasoners](https://arxiv.org/abs/2310.01714) |

## What is Analogical Prompting?

**Analogical Prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/thought_generation/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Yasunaga, M., Chen, X., Li, Y., Pasupat, P., Leskovec, J., Liang, P., Chi, E. H., &amp; Zhou, D. (2024). Large Language Models as Analogical Reasoners. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2310.01714" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2310.01714</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a new approach that enhances the reasoning process of [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) by drawing inspiration from human analogical reasoning. Inspired by our ability to draw connections between past experiences and current challenges, analogical prompting encourages LLMs to self-generate relevant examples before tackling new problems.

For example, if you're asked to solve a complex math problem, you might think of similar problems you’ve solved before and apply that knowledge. Similarly, analogical prompting instructs LLMs to recall or generate examples and solutions that resemble the current task. The LLM then uses these examples to better solve the original problem.

## How Does Analogical Prompting Work?

1. **Problem Statement**: The LLM is presented with a problem.
2. **Generate Exemplars**: It generates relevant problems and their solutions as [exemplars](https://learnprompting.org/vocabulary/exemplars).
3. **Solve Original Problem**: The LLM uses these exemplars to solve the initial problem.

This method not only removes the need for manually labeled examples but also tailors the exemplars to the specific problem, making it more adaptive.

## How Does Analogical Prompting Differ from Existing Techniques?

Analogical Prompting builds upon and improves earlier prompting techniques such as:

- [Zero-Shot Chain-of-Thought (CoT)](https://learnprompting.org/docs/intermediate/zero_shot_cot): LLMs are guided to "think step by step," but this guidance may be too generic for complex tasks. Analogical prompting generates demonstrations and does this automatically.
- [Chain-of-Thought (CoT)](https://learnprompting.org/docs/intermediate/chain_of_thought): LLMs are given labeled examples to mimic reasoning processes, but acquiring these labeled examples is labor-intensive. The generated examples through Analogical Prompting are customized for each problem, which improves adaptability compared to the fixed exemplars in [Few-Shot](https://learnprompting.org/docs/advanced/few_shot/introduction) CoT.

## How to Use Analogical Prompting

Analogical Prompting can be implemented with a specific instruction template in the LLM's input. Here's a general template you can follow:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Template

---

\[Insert problem here\]

Instruction: Relevant problems: Solve the initial problem:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Sample Prompt

---

Your task is to tackle mathematical problems. When presented with a math problem, recall relevant problems as examples. Afterward, proceed to solve the initial problem.

\[Insert problem here\]

Instruction: Relevant problems: Recall examples of math problems that are relevant to the initial problem. Your problems should be distinct from each other and from the initial problem (e.g., involving different numbers and names).

For each problem: After "Q: ", describe the problem After "A: ", explain the solution.

Solve the initial problem:

### Example:

If the problem is to calculate the area of a square given its vertices, the model first generates a similar problem with a known side length, solves it, and then applies this reasoning to the original problem.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Q: What is the area of the square with the four vertices at (-2, 2), (2, -2), (-2, -6), and (-6, -2)?

Recall relevant problems: Solve the initial problem:

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

# Relevant exemplars:

Q: What is the area of the square with a side length of 5? A: The area of a square is found by squaring the length of its side. So, the area of this square is 5^2 = 25. …

# Solve the initial problem:

To find the area of the square, we need to find the side length. The length is … \\sqrt-8 = \\sqrt32. So, the area of the square is (\\sqrt32)^2 = 32.

## Results of Analogical Prompting

Analogical prompting has been tested across various tasks including math problem-solving and code generation. The results show that it consistently outperforms both Zero-Shot and Few-Shot CoT methods.

### Performance Comparison on GSM8K (Math Dataset)

| Method | Accuracy (GSM8K) |
| --- | --- |
| Zero-Shot | 75.0% |
| Few-Shot CoT | 76.7% |
| **Analogical Prompting** | **77.8%** |

Analogical prompting particularly shines in complex tasks that require reasoning across multiple steps, such as solving competitive programming challenges or advanced math problems.

## Conclusion

Analogical prompting allows LLMs to generate their own reasoning examples tailored to each problem, offering a flexible and powerful method to guide reasoning without the need for labeled data. This approach improves performance on reasoning tasks and opens new possibilities for solving more complex problems where fixed examples are impractical or unavailable.