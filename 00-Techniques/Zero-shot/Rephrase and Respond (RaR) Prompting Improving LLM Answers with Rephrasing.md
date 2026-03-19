---
title: "Rephrase and Respond (RaR) Prompting: Improving LLM Answers with Rephrasing"
source: https://learnprompting.org/docs/advanced/zero_shot/rephrase_and_respond
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Improve LLM performance with Rephrase and Respond (RaR). Learn how rephrasing questions before answering refines accuracy for complex tasks. Discover key benefits and examples.
tags:
  - clippings
feature: thumbnails/external/c946dd4a9fd4fb0a790d23f3865e7d5f.svg
---
🟢 This article is rated [easy](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 7 minutes

Last updated on September 27, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/zero_shot/#Valeriia%20Kuka-bio)

![A diagram of Rephrase and Respond (RaR)](https://learnprompting.org/docs/assets/advanced/advanced_covers/rephrase_and_respond_cover.svg)

Takeaways

- **Rephrase and Respond (RaR)** improves [LLM](https://learnprompting.org/vocabulary/LLM) accuracy by asking the model to rephrase a question before answering.
- **Works for various tasks** like question-answering and symbolic reasoning, refining ambiguous queries for better responses.
- **Easy to implement**: Just add "Rephrase and expand the question, and respond" to prompts for clearer answers.
- **Two-step option**: Rephrasing and responding can be split into separate phases for enhanced results.
- **Limitations**: RaR may over-complicate simple questions or alter the original intent, leading to irrelevant answers.

## What is Rephrase and Respond (RaR)?

[Prompt Engineering](https://learnprompting.org/docs/basics/prompt_engineering) consists of applying specific techniques when constructing a prompt with a goal to improve the quality of the response provided by [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM).

The creators of **Rephrase and Respond (RaR)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Deng, Y., Zhang, W., Chen, Z., &amp; Gu, Q. (2024). Rephrase and Respond: Let Large Language Models Ask Better Questions for Themselves. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2311.04205" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2311.04205</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> took this concept a step further. Instead of searching for a perfect prompt formula, they asked, "What if we let the model rephrase the question itself and then answer it?"

They focused on question-answering tasks and proposed the idea of incorporating a rephrasing request directly into the prompt. This can be as simple as adding one sentence: "Rephrase and expand the question, and respond."

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

{Your question}

Rephrase and expand the question, and respond.

It's a concise and effective technique that can be combined with other techniques and has demonstrated improvements on multiple benchmarks.

### Example

Let's take an example question<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Allen-Zhu, Z., &amp; Li, Y. (2024). Physics of Language Models: Part 3.2, Knowledge Manipulation. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2309.14402" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2309.14402</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> where we ask a model to answer whether a known person is born in an even/odd month. The ambiguity for the model here lies in the definition of the "even" and "odd" month:

- Does "odd" mean "strange"? Then, February can be considered odd because of an irregular number of days.
- Does "even/odd" month refer to a month with an even/odd number of days?
- How can "even/odd" be applied to the calendar? The concept of even and odd applies to integers, not to calendar months or dates.

Here's an example:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Simple prompt

---

Was Ludwig van Beethoven born in an even month?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

No, Ludwig van Beethoven was born on December 17, 1770. Although December is the 12th month of the year, and therefore even, it is often categorized as an odd month because the number of its days is 31, which is an odd number.

Let's try to ask the model to rephrase:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Rephrase and Respond prompting

---

Was Ludwig van Beethoven born in an even month?

Rephrase and expand the question, and respond.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Rephrased Question: Was Ludwig van Beethoven born during a month with an even number, and if so, which month was it?

Response: Ludwig van Beethoven was born on December 17, 1770. December is the twelfth month of the year, which is an even number. Thus, Beethoven was indeed born in an even month.

Now, it answers correctly.

## How to Use Rephrase and Respond (RaR)?

Apart from adding "Rephrase and expand the question, and respond" to the prompt, you can use many other variations for asking a model to rephrase the question:

- Reword and elaborate on the inquiry, then provide an answer.
- Reframe the question with additional context and detail, then provide an answer.
- Modify the original question for clarity and detail, then offer an answer.
- Restate and elaborate on the inquiry before proceeding with a response.

All models can benefit from rephrasing questions, with more advanced models expected to gain a larger improvement.

### Example, Coin Flip

In this example<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">3</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., Chi, E., Le, Q., &amp; Zhou, D. (2023). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2201.11903" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2201.11903</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> , we provide the model with an initial position of the coin and describe the subsequent actions of people who either flipped or did not flip the coin. Then, we ask the model to provide an answer "Yes" or "No" to the question "Is the coin still heads up?."

Let's compare the two results that we get from a simple prompt and a Rephrase and Respond (RaR) prompt. In this example, the correct answer is "Yes, the coin still heads up."

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Simple prompt

---

A coin is heads up. Aluino flips the coin. Arthor flips the coin. Is the coin still heads up? Flip means reverse. Answer the Yes or No question.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

No.

This is incorrect. Let's try to ask the model to rephrase:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Rephrase and Respond prompting

---

A coin is heads up. Aluino flips the coin. Arthor flips the coin. Is the coin still heads up? Flip means reverse.

Rephrase and expand the question, and respond.

Answer the Yes or No question.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

The coin started out being heads up. Then, Aluino flipped the coin, reversing its side. After that, Arthor also flipped the coin, reversing its side again. Is the coin facing heads up now? Considering the action of flipping the coin means to reverse its side, after two flips, the coin would indeed be back in its original position. So, yes, the coin is still heads up.

Correct!

## How to Use Two-Step Rephrase and Respond (RaR)?

Another way to use Rephrase and Respond is a two-step procedure, separating the rephasing step from the responding step in RaR:

- Step 1, a rephrasing LLM: Given the original {question}, we ask a rephrasing LLM to generate a self-rephrased query called {rephrased\_question}:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Step 1, a rephrasing LLM

---

{question}

Given the above question, rephrase and expand it to help you do better answering. Maintain all information in the original question.

- Step 2, a responding LLM: We prompt a responding LLM with both the original {question} and the {rephrased\_question}:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Step 2, a responding LLM

---

{question}

{rephrased\_question}

Interestingly, we can use the same LLM for both steps or different LLMs for each. One of the potential ways to use this is to let stronger LLMs rephrase for weaker LLMs to respond for better results.

## How to Combine Rephrase and Respond (RaR) with Few-Shot Chain-of-Thought (CoT) Prompting?

Although [Few-Shot Chain-of-Thought (CoT)](https://learnprompting.org/docs/intermediate/chain_of_thought)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">3</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., Chi, E., Le, Q., &amp; Zhou, D. (2023). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2201.11903" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2201.11903</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is not included into the [Zero-Shot prompting techniques](https://learnprompting.org/docs/advanced/zero_shot/introduction) that we study here, it has been the most effective CoT technique for its usage of Few-Shot examples.

That's why we think it's important to mention that Rephrase and Respond (RaR) can be combined with a Few-Shot Chain-of-Thought (CoT) to achieve even better results.

To combine these techniques, again, just add this phrase to the end of the prompt: "Given the above question, rephrase and expand it to help you do better answering. Maintain all information in the original question."

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### RaR + Few-Shot CoT

---

Q: {question 1}

A: {example of the correct answer 1}

Q: {question 2}

A: {example of the correct answer 2}

...

Q: {question n}

Given the above question, rephrase and expand it to help you do better answering. Maintain all information in the original question.

### Example, Letter Concatenation Task

In this example, the task centers on symbolic reasoning. We ask the LLM to concatenate the final letters of a given list of names. Here's how you can combine RaR and CoT for this task:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### RaR + One-Shot CoT

---

Q: Take the last letters of the words in "Elon Musk" and concatenate them.

A: The last letter of "Elon" is "n". The last letter of "Musk" is "k". Concatenating them is "nk". The answer is nk.

Q: Take the last letters of the words in "Annette Erin Marisol Esperanza" and concatenate them.

Given the above question, rephrase and expand it to help you do better answering. Maintain all information in the original question.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Rephrased and Expanded Question:

To find the concatenated result of the last letters of each word in the phrase "Annette Erin Marisol Esperanza," follow these steps:

Identify the last letter of each word in the phrase. Concatenate these last letters in the order of the words.

So for the phrase "Annette Erin Marisol Esperanza":

The last letter of "Annette" is "e". The last letter of "Erin" is "n". The last letter of "Marisol" is "l". The last letter of "Esperanza" is "a".

Concatenate these last letters to get the final result. The answer is "enla".

## Limitations of Rephrase and Respond (RaR)

Rephrase and Respond (RaR) is a compelling [prompt engineering technique](https://learnprompting.org/vocabulary/prompt_engineering_technique), but it does come with some limitations.

Here are a few potential drawbacks:

- While rephrasing can help clarify ambiguous questions, it can also make straightforward queries unnecessarily complex.
- The success of RaR hinges on the model's ability to rephrase questions accurately. If the rephrasing misses the mark, the response may not be as effective.
- Rephrasing can sometimes inadvertently alter the original question's intent or focus, leading to a response that doesn’t fully address the user's needs.

## Conclusion

RaR is a valuable tool for improving LLM outputs for question-answering tasks, especially when carefully implemented alongside other prompt strategies. By leveraging RaR, you can achieve clearer and more accurate responses.