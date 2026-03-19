---
title: "SimToM Prompting: Enhancing Theory of Mind in LLMs with Perspective-Taking"
source: https://learnprompting.org/docs/advanced/zero_shot/simtom
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Discover how SimToM improves LLMs' Theory of Mind abilities through perspective-taking and question-answering. Boost understanding of human thoughts and actions.
tags:
  - clippings
feature: thumbnails/external/b36f0fdd32105f2c8a0947c28aef6bfa.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 4 minutes

Last updated on September 27, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/zero_shot/#Valeriia%20Kuka-bio)

![A diagram of SimToM](https://learnprompting.org/docs/assets/advanced/advanced_covers/simtom_cover.svg)

Takeaways

- **SimToM** enhances LLMs' ability to understand and predict human thoughts and actions using a two-stage process: **Perspective-Taking** and **Question-Answering.**
- In **Stage 1**, the model identifies which events a character is aware of, and in **Stage 2**, it answers questions from that character’s perspective.
- **SimToM** outperforms traditional prompting techniques like Zero-Shot and Chain-of-Thought in tasks requiring Theory of Mind (ToM).
- **Limitations** include its varied usefulness depending on the LLM's existing abilities and the model size (not tested on models smaller than 7B parameters).

## What is SimToM?

How can you suggest the thoughts, desires, and intentions to others, predict or explain their actions just by observing their behavior? This is a human ability called Theory of Mind (ToM). While it seems pretty easy for us, this process is hard to be transfered to or emulated by even some of the most capable [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM).

**SimToM**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wilf, A., Lee, S. S., Liang, P. P., &amp; Morency, L.-P. (2023). Think Twice: Perspective-Taking Improves Large Language Models’ Theory-of-Mind Capabilities. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2311.10227" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2311.10227</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a two-stage [prompting technique](https://learnprompting.org/vocabulary/prompting_technique) that tries to solve this problem by implementing Simulation Theory perspective to prompting. The Simulation Theory suggests that what people perceive as reality is actually a simulated world, possibly a computer simulation, where humans themselves are constructs.

To make it more concrete, here's how SimToM works:

- **Stage 1, Perspective-Taking**: SimToM filters context based on what the character in question knows
- **Stage 2, Question-Answering**: SimToM answers a question about this character's mental state

SimToM can help eliminate the effect of irrelevant information in the prompt. Without needing additional training and requiring only minimal prompt-tuning, it improves LLMs' reasoning abilities in complex situations evolving a story and several people perspectives. It outperforms baseline [Zero-Shot Prompting](https://learnprompting.org/docs/advanced/zero_shot/introduction) and [Chain-of-Thought Promting](https://learnprompting.org/docs/intermediate/chain_of_thought) on Theory-of-Mind (ToM) benchmarks.

## How to Use SimToM?

Here's the template for both stages:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Stage 1, Perspective-Taking

---

The following is a sequence of events: {story}

Which events does {character\_name} know about?

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Stage 2, Question-Answering

---

{story from character\_name’s perspective}

Answer the following question: {question}

### Example Situation

Let's see how it works on the example from the coffee shop<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Gandhi, K., Fränken, J.-P., Gerstenberg, T., &amp; Goodman, N. D. (2023). Understanding Social Reasoning in Language Models with Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2306.15448" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2306.15448</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> .

First, let's prompt a model only with the story description and a question about it:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Simple prompt

---

Noor is working as a barista at a busy coffee shop. Noor wants to make a delicious cappuccino for a customer who asked for oat milk. Noor grabs a milk pitcher and fills it with oat milk. Noor believes that the milk pitcher contains oatmilk. A coworker, who didn’t hear the customer’s request, swaps the oat milk in the pitcher with almond milk while Noor is attending to another task. Noor sees her coworker swapping the milk.

Does Noor believe the milk pitcher contains oat milk or almond milk?

The correct answer is "almond milk," but the model doesn't state that explicitly:

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Noor believes that the milk pitcher contains oat milk. She had filled the pitcher with oat milk and saw her coworker swap it out, so she would be aware that the pitcher now contains a different type of milk.

Now, let's try the SimToM prompting technique.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Stage 1, Perspective-Taking

---

The following is a sequence of events: Noor is working as a barista at a busy coffee shop. Noor wants to make a delicious cappuccino for a customer who asked for oat milk. Noor grabs a milk pitcher and fills it with oat milk. Noor believes that the milk pitcher contains oatmilk. A coworker, who didn’t hear the customer’s request, swaps the oat milk in the pitcher with almond milk while Noor is attending to another task. Noor sees her coworker swapping the milk.

Which events does Noor know about?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Noor is aware of all the events in the scenario. She knows that she filled the pitcher with oat milk and also saw her coworker swap it with almond milk.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Stage 2, Question-Answering

---

A story from Noor's perspective

Answer the following question: Does Noor believe the milk pitcher contains oat milk or almond milk?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

As I, Noor, was preparing a fresh cappuccino for a customer who requested oat milk, I carefully filled up a milk pitcher with the creamy oat milk. Life in a busy coffee shop is fast-paced, and while I was momentarily attending to another task, my eagle eyes spotted my coworker replacing the oat milk with almond milk. I knew right then that the pitcher no longer held the precious oat milk, but instead was poured with a different kind of milk. So, to answer your question, I believe that the milk pitcher now contains almond milk, not oat milk as I had originally prepared.

With SimToM, the model correctly replies to the question.

Note

In the original SimToM paper<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wilf, A., Lee, S. S., Liang, P. P., &amp; Morency, L.-P. (2023). Think Twice: Perspective-Taking Improves Large Language Models’ Theory-of-Mind Capabilities. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2311.10227" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2311.10227</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> , the authors offer some model-specific prompts. Feel free to check it out if you're interested.

## Limitations of SimToM

SimToM's usefulness may vary based on the model you're using. There are three options for that:

- The model is already good at Theory of Mind (ToM)-related questions and SimToM is not needed anymore
- The model doesn't provide correct answers, but SimToM doesn't help neither
- The model doesn't provide correct answers and SimToM helps with that

The technique was primarily tested on datasets that require “hiding” parts of the original story when answering the question from an agent’s perspective. At the same time, such reasoning may require imputing unseen information instead.

SimToM wasn't tested on smaller language models with less than 7B parameters.

## Conclusion

SimToM is a step forward in the emulation of Theory of Mind (ToM) by large language models. It can be used to develop more sophisticated interactions between humans and machines for settings like personalized assistants, learning assistants, more empathetic interfaces, etc.