---
title: "Prompt Ensembling: DiVeRSe and AMA for Accurate LLM Results"
source: https://learnprompting.org/docs/reliability/ensembling
author:
  - '[["Sander Schulhoff"]]'
published:
created: 2025-09-07
description: Discover how prompt ensembling methods like DiVeRSe and AMA improve LLM accuracy by using multiple prompts and advanced answer aggregation techniques.
tags:
  - clippings
feature: thumbnails/external/5cb20613b8cdd7ec698b1d5c0507f87b.webp
thumbnail: thumbnails/resized/e8d7734abadd4ba2f18560cf9f103d04_86cf658e.webp
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 7 minutes

Last updated on August 7, 2024

[Sander Schulhoff](https://learnprompting.org/docs/reliability/#Sander%20Schulhoff-bio)

Takeaways

- **Definition of Prompt Ensembling**: Prompt ensembling involves generating multiple prompts for the same question and analyzing the responses to identify the most accurate answer.
- **Approach Differences**: Techniques vary in how they diversify prompts and select responses:
	- **DiVeRSe** modifies the subset of exemplars preceding the question.
	- **AMA** alters the phrasing of the question itself.
	- Response selection strategies in both methods are complex and not covered here.

## What is Prompt Ensembling?

**Prompt ensembling** is the concept of using multiple different prompts to try to answer the same question. There are many different approaches to this.

## DiVeRSe

DiVeRSe<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/reliability/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Li, Y., Lin, Z., Zhang, S., Fu, Q., Chen, B., Lou, J.-G., &amp; Chen, W. (2022). On the Advance of Making Language Models Better Reasoners. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> ("**Di**verse **Ve**rifier on **R**easoning **S**t**e**ps") is a method that improves the reliability of answers in a threefold manner. It does this by

1. using multiple prompts to generate diverse completions,
2. using a verifier to distinguish good answers from bad answers, and
3. using a verifier to check the correctness of reasoning steps.

![diverse](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Freliability%2Fdiverse.webp&w=1920&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

DiVeRSe (Li et al.)

### Diverse Prompts

DiVeRSe uses 5 different prompts a given input. To construct each prompt, they randomly sample a few exemplars from the training set. Here is an example of one such Few-Shot prompt (k=2), with exemplars taken from the [GSM8K benchmark](https://raw.githubusercontent.com/openai/grade-school-math/master/grade_school_math/data/train.jsonl)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/reliability/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Cobbe, K., Kosaraju, V., Bavarian, M., Chen, M., Jun, H., Kaiser, L., Plappert, M., Tworek, J., Hilton, J., Nakano, R., Hesse, C., &amp; Schulman, J. (2021). Training Verifiers to Solve Math Word Problems. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> . In practice, DiVeRSe uses 5 exemplars in prompts for this benchmark.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Q: Natalia sold clips to 48 of her friends in April, and then she sold half as many clips in May. How many clips did Natalia sell altogether in April and May? A: Natalia sold 48/2 = 24 clips in May. Natalia sold 48+24 = 72 clips altogether in April and May.

#### 72

Q: Weng earns $12 an hour for babysitting. Yesterday, she just did 50 minutes of babysitting. How much did she earn? A: Weng earns 12/60 = $0.2 per minute. Working 50 minutes, she earned 0.2 x 50 = $10.

#### 10

Q: Betty is saving money for a new wallet which costs $100. Betty has only half of the money she needs. Her parents decided to give her $15 for that purpose, and her grandparents twice as much as her parents. How much more money does Betty need to buy the wallet? A:

After generating 5 different prompts like above, DiVeRSe samples 20 reasoning paths for each (temperature = 0.5). Here are a few example completions of the above prompt. Note that the answers are not always correct.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Betty has 0.5\*100 = $50. Then she gets 15 more = $65. Then she gets 2\*15 = $90. She needs 100-90 = $10 more.

#### 10

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

A: Betty has 0.5\*100 = $500. Then she gets 15 more = $650. Then she gets 2\*15 = $900. She needs 100-90 = $1000 more.

#### 1000

At this point, DiVeRSe has generated 100 different completions.

### Voting Verifier

Now, we could just take the majority answer, as Self-Consistency<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/reliability/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">3</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Mitchell, E., Noh, J. J., Li, S., Armstrong, W. S., Agarwal, A., Liu, P., Finn, C., &amp; Manning, C. D. (2022). Enhancing Self-Consistency and Performance of Pre-Trained Language Models through Natural Language Inference. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> does.

However, DiVeRSe proposes a much more complicated method, which they call a *voting verifier*.

At test time, using the voting verifier is a two-step process. First, the verifier (a neural network) assigns a 0-1 score to each completion based on how likely it is to be correct. Then, the 'voting' component sums all of the scores over different answers and yields the final answer.

#### Example

Here is a small example. Say we have the following completions for the prompt:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

What is two plus two?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

4

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

two + 2 = 5

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

I think 2+2 = 6

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

two plus two = 4

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

It is 5

The verifier will read each completion and assign a score to it. For example, it might assign the scores: 0.9, 0.1, 0.2, 0.8, 0.3 respectively. Then, the voting component will sum up the scores for each answer.

```
score(4) = 0.9 + 0.8 = 1.7
score(5) = 0.1 + 0.3 = 0.4
score(6) = 0.2
```

The final answer is 4 since it has the highest score.

**But how is the verifier trained?**

The verifier is trained with a slightly complex loss function, which I will not cover it here. Read section 3.3 of the paper for more details<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/reliability/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Li, Y., Lin, Z., Zhang, S., Fu, Q., Chen, B., Lou, J.-G., &amp; Chen, W. (2022). On the Advance of Making Language Models Better Reasoners. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> .

## Ask Me Anything (AMA) Prompting

![AMA Prompting](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Freliability%2FAMA_Prompting.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Ask Me Anything (AMA) prompting<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/reliability/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">4</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Arora, S., Narayan, A., Chen, M. F., Orr, L., Guha, N., Bhatia, K., Chami, I., Sala, F., &amp; Ré, C. (2022). Ask Me Anything: A simple strategy for prompting language models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is another prompt ensembling method with a similar approach to DiVeRSe. However, both its multiple prompt step and its answer aggregation step differ significantly. The core idea of AMA is to use a [LLM](https://learnprompting.org/vocabulary/LLM) to generate multiple prompts, instead of just using different Few-Shot exemplars.

### Multiple Prompts

AMA shows that you can take a question and reformat it in multiple ways to create different prompts. For example, say you are scraping a bunch of websites for information on animals and want to only record ones that live in North America. Let's construct a prompt to determine this.

Given the following passage from Wikipedia:

```
The Kermode bear, sometimes called the spirit bear (Ursus americanus kermodei), is a subspecies of the American black bear and lives in the Central and North Coast regions of British Columbia, Canada.
```

You can format this task into a prompt like so:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Is the following claim True or False given the context?

Context: The Kermode bear, sometimes called the spirit bear (Ursus americanus kermodei), is a subspecies of the American black bear and lives in the Central and North Coast regions of British Columbia, Canada. Claim: This animal lives in North America Answer:

This is a bit of an odd formulation. Why not just use the following simpler prompt?

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Context: The Kermode bear, sometimes called the spirit bear (Ursus americanus kermodei), is a subspecies of the American black bear and lives in the Central and North Coast regions of British Columbia, Canada. Question: Does this animal live in North America?

Well, by formulating the question in this special way, we can generate different prompts. Our first step here will be to take the claim `This animal lives in North America` and reformat it into different questions, which are basically asking the same thing. To do this, we will pass the claim through prompts like those in the below image.

![AMA multiprompting](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Freliability%2FAMA_multiprompting.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

This might output:

1. Was the animal living in North America?
2. Does the animal live in North America?
3. Where does the animal live?

The idea behind this is to create different *views* of the task. We then apply each to the given context like so:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Context: The Kermode bear, sometimes called the spirit bear (Ursus americanus kermodei), is a subspecies of the American black bear and lives in the Central and North Coast regions of British Columbia, Canada. Question: Was the animal living in North America?

Then, we can generate answers for each:

1. `Yes it was`
2. `Yes it does`
3. `North America`

These are *intermediate* answers. We need to map them to task labels (e.g. Yes or No).

We can do this by passing the intermediate answers through a prompt like the following:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Select the correct category.

"Categories":

\- Yes, North America - No, not North America

"Yes it was" fits the category:

Now we can get our output answers.

1. `Yes, North America`
2. `Yes, North America`
3. `Yes, North America`

Here, they all agree, so we can just take the first answer. However, if they disagreed, we could use the AMA aggregation step to get a final answer.

### Answer Aggregation

AMA uses a very complicated strategy for aggregating answers (more so than DiVeRSe) instead of simply taking the majority answer. To understand why the majority answer may be a poor choice, consider two of the questions we generated before:

1. Was the animal living in North America?
2. Does the animal live in North America?

They are extremely similar, so will likely generate the same result. Since the questions are so similar, they will effectively bias the end result. To deal with this, AMA relies on weak supervision and complex mathematics to estimate dependencies between different prompts it creates, and then uses this to weight them appropriately.

So, for the three questions we generated, it might assign weights of 25%, 25%, and 50%, since the first two are so similar.

Although AMA's aggregation strategy is powerful, it is so complicated that I will not cover it here. Read section 3.4 of the paper for more details<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/reliability/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">4</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Arora, S., Narayan, A., Chen, M. F., Orr, L., Guha, N., Bhatia, K., Chami, I., Sala, F., &amp; Ré, C. (2022). Ask Me Anything: A simple strategy for prompting language models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> .

### Results

- With this prompting strategy, AMA can use GPT-J-6B<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/reliability/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">5</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wang, B., &amp; Komatsuzaki, A. (2021). GPT-J-6B: A 6 Billion Parameter Autoregressive Language Model. <a target="_blank" rel="noopener noreferrer" href="https://github.com/kingoflolz/mesh-transformer-jax." style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://github.com/kingoflolz/mesh-transformer-jax.</a> <a target="_blank" rel="noopener noreferrer" href="https://github.com/kingoflolz/mesh-transformer-jax" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://github.com/kingoflolz/mesh-transformer-jax</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> to outperform GPT-3.
- AMA is better on questions where given context contains the answer.

## Conclusion

Prompt ensembling methods are very powerful. They can be used to improve the performance of any model and can be used to improve the performance of a model on a specific task.

In practice, majority voting should be your go-to strategy.

## FAQ

### What do prompt ensembling methods do?

Prompt ensembling methods help reduce bias in an LLM output distribution by combining the outputs of multiple different prompts to improve the reliability of the response.

### What are some different prompt ensembling methods?

The two prompt ensembling methods discussed in this article are DiVeRSe and Ask Me Anything (AMA) prompting.

### What is the difference between DiVeRSe and AMA?

DiVeRSe and AMA differ in both their formation of multiple prompts and in their strategies of answer aggregation. First, while DiVeRSe requires user input of Few-Shot examples as multiple prompt inputs, AMA automates the creation of various prompts by tasking the LLM to come up with variations of the input question. In terms of answer aggregation, DiVeRSe uses a voting verifier to score completions from the multiple prompts, while AMA calculates a weighted aggregation of the responses in order to further reduce bias in the end result.