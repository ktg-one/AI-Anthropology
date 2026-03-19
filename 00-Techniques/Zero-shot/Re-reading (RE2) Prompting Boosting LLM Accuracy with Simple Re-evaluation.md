---
title: "Re-reading (RE2) Prompting: Boosting LLM Accuracy with Simple Re-evaluation"
source: https://learnprompting.org/docs/advanced/zero_shot/re_reading
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Discover how Re-reading (RE2) enhances LLM reasoning by prompting models to re-evaluate inputs. Learn to apply RE2 for improved accuracy in arithmetic, commonsense, and symbolic tasks.
tags:
  - clippings
feature: thumbnails/external/8b2dfb85062c93918d773768a59bfaba.svg
---
🟢 This article is rated [easy](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 9 minutes

Last updated on September 27, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/zero_shot/#Valeriia%20Kuka-bio)

![A diagram of Re-reading (RE2) technique](https://learnprompting.org/docs/assets/advanced/advanced_covers/re_reading_cover.svg)

Takeaways

- **Re-reading (RE2)** is a technique that improves [LLM](https://learnprompting.org/vocabulary/LLM) performance by prompting the model to re-read the question, reducing errors from missed details.
- **RE2 is versatile** and can be applied to arithmetic, commonsense, and symbolic reasoning tasks, enhancing reasoning across diverse applications.
- **Simple yet effective**: Despite its simplicity, RE2 consistently enhances reasoning and can be combined with techniques like Chain-of-Thought (CoT) for further improvement.
- **Limitations include** increased computational cost, inefficacy in addressing deep logical errors, and potential redundancy in simpler tasks.
- **RE2's strength** lies in its ability to refine answers for complex, detail-oriented problems, making LLMs more reliable.

## What is Re-reading (RE2)?

Sometimes [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) just fail to notice important details in our prompt and this leads to incorrect results.

**Re-reading (RE2)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Xu, X., Tao, C., Shen, T., Xu, C., Xu, H., Long, G., &amp; guang Jian-Lou. (2024). Re-Reading Improves Reasoning in Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2309.06275" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2309.06275</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a technique that aims to solve this problem by asking an LLM to re-read the prompt.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### RE2 Prompting

---

Q: {Input Query} Read the question again: {Input Query}

While being so simple, RE2 is a general end effective technique that consistently enhances the reasoning performance of LLMs through just a rereading strategy. Furthermore, RE2 is compatible and can be combined with most thought-eliciting prompting methods, including [Chain-of-Thought (CoT)](https://learnprompting.org/docs/intermediate/chain_of_thought).

## How to Use Re-reading (RE2)?

Re-reading can enhance an LLM's reasoning capabilities in several areas, including:

- Arithmetic reasoning: solving math problems
- Commonsense reasoning: drawing on common-sense knowledge
- Symbolic reasoning: applying logical inference to symbols to generate new knowledge

Let’s explore specific use cases of these capabilities and see how Re-reading works in practice with some examples.

Caution

Before reading about the use cases, please keep in mind that LLMs still have limitations — they can make things up and make errors. Use them as assistants, not as a complete replacement for your work. Rely on them at your discretion.

### Arithmetic Reasoning

Imagine you build an educational tool or just want to help your kid to understand math. LLMs can help learn and practice math, providing step-by-step explanations, and offering personalized feedback.

To improve these capabilities, you can use Re-reading. Here's an example of a math problem:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### RE2 Prompting

---

Q: Hally and her friends organized a high school reunion. To cover the cost of a late-night party that they planned for at the reunion, each attendee had to pay 100 dollars. After the party, Hally and her friends realized that the total expenses were 500 dollars less than the total contributions. If there were 50 people at the party, how much money was used to pay for the party expenses?

Read the question again: Hally and her friends organized a high school reunion. To cover the cost of a late-night party that they planned for at the reunion, each attendee had to pay $100. After the party, Hally and her friends realized that the total expenses were $500 less than the total contributions. If there were 50 people at the party, how much money was used to pay for the party expenses?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Let's break this down:

Each attendee paid 100 dollars. There were 50 attendees.

The total contributions from all attendees were:

Total contributions = 50 × 100 = 5000 dollars

According to the problem, the total expenses were $500 less than the total contributions. So, the total expenses were:

Total expenses = 5000 − 500 = 4500 dollars

Therefore, 4,500 dollars was used to pay for the party expenses.

### Commonsense Reasoning

LLMs' commonsense reasoning can be used in many applications, here are some of them:

- Customer support automation: LLMs can enhance AI-driven chatbots by handling queries that require a basic understanding of common sense, such as recognizing customer concerns and providing relevant solutions.
- Content generation: LLMs can generate content that aligns with human expectations and societal norms.
- Safety and error detection: In AI-driven systems, commonsense reasoning can be used to flag illogical or potentially harmful [instructions](https://learnprompting.org/docs/basics/instructions).

#### Customer Support Chatbot

Imagine you ordered a new laptop last week, but it still hasn’t arrived. The tracking number says it was delivered yesterday, yet you never received it. So, you reach out to the company’s support chatbot:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Simple Prompting

---

I ordered a new laptop last week, but it hasn’t arrived yet. The tracking number says it was delivered yesterday, but I never received it. Can you help me figure out what happened?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

It looks like your order was delivered yesterday according to the tracking information. Please check with your neighbors or any safe locations where the package might have been left.

This response missed the critical detail that you did not actually receive the package despite the tracking status. You can make use of the RE2 prompting technique:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### RE2 Prompting

---

Q: "I ordered a new laptop last week, but it hasn’t arrived yet. The tracking number says it was delivered yesterday, but I never received it. Can you help me figure out what happened?"

Read the question again: "I ordered a new laptop last week, but it hasn’t arrived yet. The tracking number says it was delivered yesterday, but I never received it. Can you help me figure out what happened?"

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

I see that your tracking information shows the package as delivered, but you did not receive it. I’ll check if there was an error in the delivery process or if the package might have been left in an incorrect location.

In the meantime, I recommend contacting our delivery service directly to report the issue. I will also initiate an investigation to ensure the package is found or a replacement is sent as soon as possible.

This response more effectively addresses your concern and takes the necessary steps to resolve the issue.

### Symbolic Reasoning

Symbolic reasoning capabilities of LLMs can be used in various use cases, here are some of them:

- Contract analysis: An LLM is used to analyze legal contracts to ensure they comply with regulatory standards and do not contain conflicting clauses.
- Automated code review: An LLM is employed to review code for logical errors, security vulnerabilities, and adherence to coding standards.
- Medical diagnosis support: An LLM assists in diagnosing patients by interpreting medical symbols (symptoms, test results) and inferring possible conditions based on logical rules.

## How to Combine Re-reading (RE2) with Chain-of-Thought (CoT) Prompting?

Chain-of-Thought (CoT) prompting<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., Chi, E., Le, Q., &amp; Zhou, D. (2023). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2201.11903" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2201.11903</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a powerful [prompting technique](https://learnprompting.org/vocabulary/prompting_technique). When combined with Re-reading (RE2), it can give even more improved results<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Xu, X., Tao, C., Shen, T., Xu, C., Xu, H., Long, G., &amp; guang Jian-Lou. (2024). Re-Reading Improves Reasoning in Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2309.06275" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2309.06275</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> .

Here's a template of the prompt combining Chain-of-Though (CoT) prompting with Re-reading (RE2):

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### RE2 + CoT

---

Q: {question}

Read the question again: {question}

#Answer format instruction#

A: Let’s think step by step.

### Arithmetic Reasoning Example

Here's how you can combine CoT with RE2 to receive better results with math word problems<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Xu, X., Tao, C., Shen, T., Xu, C., Xu, H., Long, G., &amp; guang Jian-Lou. (2024). Re-Reading Improves Reasoning in Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2309.06275" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2309.06275</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> .

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Just CoT

---

Q: Every day, Wendi feeds each of her chickens three cups of mixed chicken feed, containing seeds, mealworms and vegetables to help keep them healthy. She gives the chickens their feed in three separate meals. In the morning, she gives her flock of chickens 15 cups of feed. In the afternoon, she gives her chickens another 25 cups of feed. How many cups of feed does she need to give her chickens in the final meal of the day if the size of Wendi’s flock is 20 chickens?

Your final answer should be a single numerical number, in the form answer, at the end of your response.

Let’s think step by step.

The correct answer should be 20, but the model gives another answer:

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

First, let’s calculate how much feed Wendi gives her chickens in the morning.

She has 20 chickens, and she gives each chicken 3 cups of feed, so in total, she gives them 20 x 3 = 60 cups of feed in the morning.

Next, let’s calculate how much feed Wendi gives her chickens in the afternoon.

Again, she has 20 chickens, and she gives each chicken 3 cups of feed, so in total, she gives them 20 x 3 = 60 cups of feed in the afternoon.

To find out how much feed she needs to give her chickens in the final meal of the day, we need to subtract the total feed given in the morning and afternoon from the total feed needed for the day.

The total feed needed for the day for 20 chickens is 20 x 3 x 3 = 180 cups of feed.

So, the feed needed in the final meal of the day is 180 - 60 - 60 = 60 cups of feed.

Therefore, Wendi needs to give her chickens 60 cups of feed in the final meal of the day.

Answer: 60

Let's try to combine Chain-of-Though (CoT) with Re-reading (RE2):

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### RE2 + CoT

---

Q: Every day, Wendi feeds each of her chickens three cups of mixed chicken feed, containing seeds, mealworms and vegetables to help keep them healthy. She gives the chickens their feed in three separate meals. In the morning, she gives her flock of chickens 15 cups of feed. In the afternoon, she gives her chickens another 25 cups of feed. How many cups of feed does she need to give her chickens in the final meal of the day if the size of Wendi’s flock is 20 chickens?

Read the question again: Every day, Wendi feeds each of her chickens three cups of mixed chicken feed, containing seeds, mealworms and vegetables to help keep them healthy. She gives the chickens their feed in three separate meals. In the morning, she gives her flock of chickens 15 cups of feed. In the afternoon, she gives her chickens another 25 cups of feed. How many cups of feed does she need to give her chickens in the final meal of the day if the size of Wendi’s flock is 20 chickens?

Your final answer should be a single numerical number, in the form answer, at the end of your response.

Let’s think step by step.

Now, the answer is right:

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

First, we need to determine the total amount of feed Wendi gives her chickens in the morning and afternoon.

In the morning, she gives 15 cups of feed, and in the afternoon, she gives another 25 cups. So, the total amount of feed given in the morning and afternoon is 15 + 25 = 40 cups.

Next, we need to determine the total amount of feed needed for Wendi’s flock of 20 chickens. Since each chicken requires 3 cups of feed, we multiply 3 by 20 to get 60 cups.

Finally, we subtract the total amount of feed given in the morning and afternoon from the total amount needed. 60 - 40 = 20

Therefore, Wendi needs to give her chickens 20 cups of feed in the final meal of the day.

Answer: 20

### Limitations of Re-reading (RE2)

Some potential limitations of RE2 include:

- **Re-reading doesn't always help:** Continuously Re-reading the same prompt may not necessarily improve reasoning.
- **Increased computational cost:** Re-reading and processing the same prompt multiple times can increase computational cost and response time.
- **Misapplication in simple tasks:** For simpler tasks that don’t require extensive reasoning, using RE2 might introduce unnecessary complexity.
- **Limited effectiveness for deep logical errors:** RE2 may not effectively address deeper logical errors or gaps in the model’s understanding of complex concepts. If the model lacks the necessary domain knowledge or logical framework, Re-reading might not lead to the correct answer.

## Conclusion

Re-reading (RE2) is a simple yet powerful technique that enhances the reasoning capabilities of Large Language Models (LLMs) by encouraging them to re-evaluate the prompt. This method can improve the accuracy and reliability of the model's responses, especially in complex tasks like arithmetic, commonsense, and symbolic reasoning. By combining RE2 with other techniques, such as Chain-of-Thought (CoT), users can further boost the performance of LLMs.