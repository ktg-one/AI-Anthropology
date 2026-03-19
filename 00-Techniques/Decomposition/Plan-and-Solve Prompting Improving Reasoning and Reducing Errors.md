---
title: "Plan-and-Solve Prompting: Improving Reasoning and Reducing Errors"
source: https://learnprompting.org/docs/advanced/decomposition/plan_and_solve
author:
  - '[["Bhuwan Bhatt"]]'
published:
created: 2025-09-07
description: Discover Plan-and-Solve Prompting, a technique to enhance Large Language Models' accuracy by reducing missing steps and calculation errors. Learn how PS+ prompting works.
tags:
  - clippings
feature: thumbnails/external/1912767a2674be6c1d98d8edfbb00b71.svg
---
Reading Time: 5 minutes

Last updated on September 27, 2024

[Bhuwan Bhatt](https://learnprompting.org/docs/advanced/decomposition/#Bhuwan%20Bhatt-bio)

![demonstration of plan-and-solve prompting technique](https://learnprompting.org/docs/assets/advanced/advanced_covers/plan_and_solve_cover.svg)

Takeaways

- **Plan-and-Solve (PS) Prompting** addresses missing step errors in Zero-Shot Chain-of-Thought (CoT) reasoning by introducing a planning stage before solving.
- **PS+ prompting** extends PS prompting to reduce calculation errors, ensuring better accuracy in reasoning tasks.
- **How it works**: PS prompting asks the model to plan before solving, while PS+ emphasizes careful calculation and intermediate results.
- **PS+ outperforms** Zero-Shot Chain-of-Thought (CoT) on symbolic reasoning, common sense, and math reasoning datasets.
- **Limitations** include sensitivity to prompt wording and its inability to fully resolve semantic misunderstanding errors.

## What is Plan-and-Solve Prompting?

[Zero-Shot Chain-of-Thought (CoT) Prompting](https://learnprompting.org/docs/intermediate/zero_shot_cot)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Jason Wei. (2022). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> improves the reasoning and accuracy of [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) by enabling them to generate intermediate reasoning steps before predicting the final answer. While this improves the performance in multi-step reasoning tasks, the experiments show that Zero-Shot CoT has three pitfalls:

- Calculation errors
- Missing Step errors
- Semantic misunderstanding

![percentage of calculation, step missing, and semantic errors made by Zero-Shot CoT](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fps_prompt_zero_cot_error_analysis.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Categorization of errors made by Zero-Shot CoT<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Lei Wang. (2023). Plan-and-Solve Prompting: Improving Zero-Shot Chain-of-Thought Reasoning by Large Language Models.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

**Plan-and-Solve (PS) prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Lei Wang. (2023). Plan-and-Solve Prompting: Improving Zero-Shot Chain-of-Thought Reasoning by Large Language Models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> aims to solve the issue of missing step errors in [Zero-Shot CoT](https://learnprompting.org/docs/intermediate/zero_shot_cot) Prompting. To achieve its goal, PS prompting replaces the phrase "Let's think step by step" used in Zero-Shot CoT with "Let's first understand the problem and devise a plan to solve the problem. Then, let's carry out the plan and solve the problem step by step". The example below shows the difference between Zero-Shot CoT and PS prompting.

- **Zero-Shot CoT Prompting**

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Q: In a dance class of 20 students, 20% enrolled in contemporary dance, 25% of the remaining enrolled in jazz dance, and the rest enrolled in hip-hop dance. What percentage of the entire students enrolled in hip-hop dance? A: Let's think step by step.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

First, 20% of the class enrolled in contemporary dance, so that means that 80% of the class is left.

Next, 25% of the remaining 80% enrolled in jazz dance, so that means that 25% of the original class enrolled in jazz dance. That leaves 55% of the original class.

Finally, the rest of the class (55%) enrolled in hip-hop dance. So, 55% of the entire class enrolled in hip-hop dance.

- **Plan-and-Solve (PS) Prompting**

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Q: In a dance class of 20 students, 20% enrolled in contemporary dance, 25% of the remaining enrolled in jazz dance, and the rest enrolled in hip-hop dance. What percentage of the entire students enrolled in hip-hop dance?

A: Let's first understand the problem and devise a plan to solve the problem. Then, let's carry out the plan and solve the problem step by step.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Plan: Step 1: Calculate the total number of students who enrolled: in contemporary and jazz dance. Step 2: Calculate the total number of students who enrolled in hip-hop dance. Step 3: Calculate the percentage of students who enrolled: in hip-hop dance.

Solution: Step 1: 20% of 20 students is 4 students. 25% of the remaining 16 students is 4 students. So, a total of 8 students enrolled in contemporary and jazz dance. Step 2: The remaining 12 students enrolled in hip-hop dance. Step 3: The percentage of students who enrolled in hip-hop dance is 12/20 = 60%.

From the example, it is clear that for complex problems, the reasoning steps generated using the Zero-Shot CoT prompt: "Let's think step by step" may still yield incorrect reasoning steps. Asking the [LLM](https://learnprompting.org/vocabulary/LLM) first to devise the plan and then carry it out - PS prompting - can help minimize the missing steps errors.

It is important to note that the Zero-Shot prompt in PS prompting can be anything as long as it satisfies the following conditions:

- It triggers the LLM to determine subtasks and accomplish the subtasks.
- It guides the LLM to pay more attention to calculation and intermediate results to ensure a correct response

## How to Use Plan-and-Solve Prompting?

Implementing PS prompting is a two-step process. It includes:

- inference, and
- answer extraction

### Step 1: Inference

Feed the prompt to the LLM in the first step; this generates the reasoning step and the answer.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiR2l2ZW46XG5Ub3RhbCBudW1iZXIgb2Ygc3R1ZGVudHMgPSAyMFxuXG4xLiBDYWxjdWxhdGUgdGhlIG51bWJlciBvZiBzdHVkZW50cyBlbnJvbGxlZCBpbiBjb250ZW1wb3JhcnkgZGFuY2U6XG4yMCUgb2YgMjAgPSAwLjIwICogMjAgPSA0IHN0dWRlbnRzXG5cbjIuIENhbGN1bGF0ZSB0aGUgbnVtYmVyIG9mIHN0dWRlbnRzIHJlbWFpbmluZzpcblRvdGFsIHN0dWRlbnRzIC0gc3R1ZGVudHMgaW4gY29udGVtcG9yYXJ5IGRhbmNlID0gMjAgLSA0ID0gMTYgc3R1ZGVudHNcblxuMy4gQ2FsY3VsYXRlIHRoZSBudW1iZXIgb2Ygc3R1ZGVudHMgZW5yb2xsZWQgaW4gamF6eiBkYW5jZTpcbjI1JSBvZiAxNiA9IDAuMjUgKiAxNiA9IDQgc3R1ZGVudHNcblxuNC4gQ2FsY3VsYXRlIHRoZSBudW1iZXIgb2Ygc3R1ZGVudHMgZW5yb2xsZWQgaW4gaGlwLWhvcCBkYW5jZTpcblJlbWFpbmluZyBzdHVkZW50cyA9IFRvdGFsIHN0dWRlbnRzIC0gKHN0dWRlbnRzIGluIGNvbnRlbXBvcmFyeSBkYW5jZSArIHN0dWRlbnRzIGluIGphenogZGFuY2UpXG5SZW1haW5pbmcgc3R1ZGVudHMgPSAyMCAtICg0ICsgNCkgPSAxMiBzdHVkZW50c1xuXG41LiBDYWxjdWxhdGUgdGhlIHBlcmNlbnRhZ2Ugb2Ygc3R1ZGVudHMgZW5yb2xsZWQgaW4gaGlwLWhvcCBkYW5jZTpcblBlcmNlbnRhZ2Ugb2Ygc3R1ZGVudHMgaW4gaGlwLWhvcCBkYW5jZSA9IChOdW1iZXIgb2Ygc3R1ZGVudHMgaW4gaGlwLWhvcCBkYW5jZSAvIFRvdGFsIG51bWJlciBvZiBzdHVkZW50cykgKiAxMDBcblBlcmNlbnRhZ2Ugb2Ygc3R1ZGVudHMgaW4gaGlwLWhvcCBkYW5jZSA9ICgxMiAvIDIwKSAqIDEwMCA9IDAuNjAgKiAxMDAgPSA2MCVcblxuVGhlcmVmb3JlLCA2MCUgb2YgdGhlIGVudGlyZSBzdHVkZW50cyBlbnJvbGxlZCBpbiBoaXAtaG9wIGRhbmNlLiIsInByb21wdCI6IlE6IEluIGEgZGFuY2UgY2xhc3Mgb2YgMjAgc3R1ZGVudHMsIDIwJSBlbnJvbGxlZCBpbiBjb250ZW1wb3JhcnkgZGFuY2UsIDI1JSBvZiB0aGUgcmVtYWluaW5nIGVucm9sbGVkIGluIGphenogZGFuY2UsIGFuZCB0aGUgcmVzdCBlbnJvbGxlZCBpbiBoaXAtaG9wIGRhbmNlLiBXaGF0IHBlcmNlbnRhZ2Ugb2YgdGhlIGVudGlyZSBzdHVkZW50cyBlbnJvbGxlZCBpbiBoaXAtaG9wIGRhbmNlP1xuQTogTGV0J3MgZmlyc3QgdW5kZXJzdGFuZCB0aGVcbnByb2JsZW0gYW5kIGRldmlzZSBhIHBsYW4gdG8gc29sdmUgdGhlIHByb2JsZW0uXG5UaGVuLCBsZXQncyBjYXJyeSBvdXQgdGhlIHBsYW4gYW5kIHNvbHZlIHRoZSBwcm9ibGVtIHN0ZXAgYnkgc3RlcC4iLCJtb2RlbCI6ImdwdC0zLjUtdHVyYm8ifQ%3D%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

### Step 2: Answer Extraction

Next, pass the initial prompt and the generated answer to the LLM to extract the final answer. To extract the answer, you can append a phrase like *"Therefore, the answer (arabic numerals) is"* at the end of the prompt.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiNjAlLiIsInByb21wdCI6IlE6IEluIGEgZGFuY2UgY2xhc3Mgb2YgMjAgc3R1ZGVudHMsIDIwJSBlbnJvbGxlZCBpbiBjb250ZW1wb3JhcnkgZGFuY2UsIDI1JSBvZiB0aGUgcmVtYWluaW5nIGVucm9sbGVkIGluIGphenogZGFuY2UsIGFuZCB0aGUgcmVzdCBlbnJvbGxlZCBpbiBoaXAtaG9wIGRhbmNlLiBXaGF0IHBlcmNlbnRhZ2Ugb2YgdGhlIGVudGlyZSBzdHVkZW50cyBlbnJvbGxlZCBpbiBoaXAtaG9wIGRhbmNlP1xuQTogTGV0J3MgZmlyc3QgdW5kZXJzdGFuZCB0aGVcbnByb2JsZW0gYW5kIGRldmlzZSBhIHBsYW4gdG8gc29sdmUgdGhlIHByb2JsZW0uXG5UaGVuLCBsZXQncyBjYXJyeSBvdXQgdGhlIHBsYW4gYW5kIHNvbHZlIHRoZSBwcm9ibGVtIHN0ZXAgYnkgc3RlcC5cblxuR2l2ZW46XG5Ub3RhbCBudW1iZXIgb2Ygc3R1ZGVudHMgPSAyMFxuXG4xLiBDYWxjdWxhdGUgdGhlIG51bWJlciBvZiBzdHVkZW50cyBlbnJvbGxlZCBpbiBjb250ZW1wb3JhcnkgZGFuY2U6XG4yMCUgb2YgMjAgPSAwLjIwICogMjAgPSA0IHN0dWRlbnRzXG5cbjIuIENhbGN1bGF0ZSB0aGUgbnVtYmVyIG9mIHN0dWRlbnRzIHJlbWFpbmluZzpcblRvdGFsIHN0dWRlbnRzIC0gc3R1ZGVudHMgaW4gY29udGVtcG9yYXJ5IGRhbmNlID0gMjAgLSA0ID0gMTYgc3R1ZGVudHNcblxuMy4gQ2FsY3VsYXRlIHRoZSBudW1iZXIgb2Ygc3R1ZGVudHMgZW5yb2xsZWQgaW4gamF6eiBkYW5jZTpcbjI1JSBvZiAxNiA9IDAuMjUgKiAxNiA9IDQgc3R1ZGVudHNcblxuNC4gQ2FsY3VsYXRlIHRoZSBudW1iZXIgb2Ygc3R1ZGVudHMgZW5yb2xsZWQgaW4gaGlwLWhvcCBkYW5jZTpcblJlbWFpbmluZyBzdHVkZW50cyA9IFRvdGFsIHN0dWRlbnRzIC0gKHN0dWRlbnRzIGluIGNvbnRlbXBvcmFyeSBkYW5jZSArIHN0dWRlbnRzIGluIGphenogZGFuY2UpXG5SZW1haW5pbmcgc3R1ZGVudHMgPSAyMCAtICg0ICsgNCkgPSAxMiBzdHVkZW50c1xuXG41LiBDYWxjdWxhdGUgdGhlIHBlcmNlbnRhZ2Ugb2Ygc3R1ZGVudHMgZW5yb2xsZWQgaW4gaGlwLWhvcCBkYW5jZTpcblBlcmNlbnRhZ2Ugb2Ygc3R1ZGVudHMgaW4gaGlwLWhvcCBkYW5jZSA9IChOdW1iZXIgb2Ygc3R1ZGVudHMgaW4gaGlwLWhvcCBkYW5jZSAvIFRvdGFsIG51bWJlciBvZiBzdHVkZW50cykgKiAxMDBcblBlcmNlbnRhZ2Ugb2Ygc3R1ZGVudHMgaW4gaGlwLWhvcCBkYW5jZSA9ICgxMiAvIDIwKSAqIDEwMCA9IDAuNjAgKiAxMDAgPSA2MCVcblxuVGhlcmVmb3JlLCA2MCUgb2YgdGhlIGVudGlyZSBzdHVkZW50cyBlbnJvbGxlZCBpbiBoaXAtaG9wIGRhbmNlLlxuXG5UaGVyZWZvcmUsIHRoZSBhbnN3ZXIgKGFyYWJpYyBudW1lcmFsKSBpcyIsIm1vZGVsIjoiZ3B0LTMuNS10dXJibyJ9" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

## What is PS+ Prompting?

While PS prompting helps minimize the missing steps error, PS+ prompting, an extension of PS prompting, aims to reduce calculation errors of Zero-Shot CoT along with improving the generated reasoning steps. PS+ prompt extends the PS prompt with additional details instructing the LLM to compute intermediate results and pay more attention to calculation and common sense.

### PS+ Prompting Example

Given a math word problem, *Grace weighs 125 pounds. Alex weighs 2 pounds less than 4 times what Grace weighs. What are their combined weights in pounds?*, let's solve it using both PS and PS+ prompting.

First, let's try with PS prompting:

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiUGxhbjogV2UgY2FuIHVzZSBhbGdlYnJhIHRvIHNvbHZlIHRoaXMgcHJvYmxlbS4gV2UgY2FuIHNldCB1cCBhbiBlcXVhdGlvbiB3aXRoIHRoZSB2YXJpYWJsZSB4IHJlcHJlc2VudGluZyBBbGV4J3Mgd2VpZ2h0IGFuZCBzb2x2ZSBmb3IgWC4gVGhlbiwgd2UgY2FuIGFkZCB0aGUgdHdvIHdlaWdodHMgdG9nZXRoZXIgdG8gZ2V0IHRoZSBjb21iaW5lZCB3ZWlnaHQuIFxuXG5TdGVwIDE6IFNldCB1cCBhbiBlcXVhdGlvbi4gV2Uga25vdyB0aGF0IEFsZXggd2VpZ2hzIDIgcG91bmRzIGxlc3MgdGhhbiA0IHRpbWVzIHdoYXQgR3JhY2Ugd2VpZ2hzLiBXZSBjYW4gcmVwcmVzZW50IHRoaXMgYXM6XG5BbGV4J3Mgd2VpZ2h0ID0gNCAqIEdyYWNlJ3Mgd2VpZ2h0IC0gMlxuXG5TdGVwIDI6IFNvbHZlIGZvciB4LiBXZSBrbm93IHRoYXQgR3JhY2UncyB3ZWlnaHQgaXMgMTI1IHBvdW5kcy4gV2UgY2FuIHN1YnN0aXR1dGUgdGhpcyBpbnRvIHRoZSBlcXVhdGlvbiB0byBzb2x2ZSBmb3IgQWxleCdzIHdlaWdodDpcbkFsZXgncyB3ZWlnaHQgPSA0ICogMTI1IC0gMlxuXG5TdGVwIDM6IENhbGN1bGF0ZSB0aGUgY29tYmluZWQgd2VpZ2h0LiBXZSBjYW4gbm93IGFkZCB0aGUgdHdvIHdlaWdodHMgdG9nZXRoZXIgdG8gZ2V0IHRoZSBjb21iaW5lZCB3ZWlnaHQ6XG5Db21iaW5lZCB3ZWlnaHQgPSAxMjUgKyAoNCAqIDEyNSAtIDIpXG5cblN0ZXAgNDogQW5zd2VyLiBUaGUgY29tYmluZWQgd2VpZ2h0IG9mIEdyYWNlIGFuZCBBbGV4IGlzIDQ5NyBwb3VuZHMuIiwicHJvbXB0IjoiUTogR3JhY2Ugd2VpZ2hzIDEyNSBwb3VuZHMuIEFsZXggd2VpZ2hzIDIgcG91bmRzIGxlc3MgdGhhbiA0IHRpbWVzIHdoYXQgR3JhY2Ugd2VpZ2hzLlxuV2hhdCBhcmUgdGhlaXIgY29tYmluZWQgd2VpZ2h0cyBpbiBwb3VuZHM%2FXG5BOiBMZXQncyBmaXJzdCB1bmRlcnN0YW5kIHRoZVxucHJvYmxlbSBhbmQgZGV2aXNlIGEgcGxhbiB0byBzb2x2ZSB0aGUgcHJvYmxlbS5cblRoZW4sIGxldCdzIGNhcnJ5IG91dCB0aGUgcGxhbiBhbmQgc29sdmUgdGhlIHByb2JsZW0gc3RlcCBieSBzdGVwLiIsIm1vZGVsIjoiZ3B0LTMuNS10dXJibyJ9" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

You can clearly see that PS fails to correctly evaluate the expression *125 + (4 \* 125 - 2)* resulting in an incorrect answer. Now, let's employ PS+ prompting.

- Inference
<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiR3JhY2Ugd2VpZ2hzIDEyNSBwb3VuZHMuXG5cbkxldCB4IGJlIHRoZSBudW1iZXIgb2YgdGltZXMgR3JhY2UncyB3ZWlnaHQuXG5BbGV4IHdlaWdocyA0eCAtIDIgcG91bmRzLlxuXG5HaXZlbiB0aGF0IEFsZXggd2VpZ2hzIDQgdGltZXMgd2hhdCBHcmFjZSB3ZWlnaHMgbWludXMgMiBwb3VuZHMsIHdlIGhhdmU6IDR4IC0gMiA9IEFsZXgncyB3ZWlnaHQuXG5cbk5vdywgd2UgY2FuIHN1YnN0aXR1dGUgR3JhY2UncyB3ZWlnaHQgaW50byB0aGUgZXF1YXRpb246XG40eCAtIDIgPSA0KDEyNSkgLSAyXG40eCAtIDIgPSA0OThcbjR4ID0gNTAwXG54ID0gMTI1XG5cblRoZXJlZm9yZSwgQWxleCB3ZWlnaHM6IDQoMTI1KSAtIDIgPSA0OTggcG91bmRzLlxuXG5UaGVpciBjb21iaW5lZCB3ZWlnaHRzIGFyZTpcbjEyNSAoR3JhY2UpICsgNDk4IChBbGV4KSA9IDYyMyBwb3VuZHMuXG5cbkhlbmNlLCB0aGVpciBjb21iaW5lZCB3ZWlnaHRzIGFyZSA2MjMgcG91bmRzLiIsInByb21wdCI6IlE6IEdyYWNlIHdlaWdocyAxMjUgcG91bmRzLiBBbGV4IHdlaWdocyAyIHBvdW5kcyBsZXNzIHRoYW4gNCB0aW1lcyB3aGF0IEdyYWNlIHdlaWdocy5cbldoYXQgYXJlIHRoZWlyIGNvbWJpbmVkIHdlaWdodHMgaW4gcG91bmRzP1xuQTogTGV0J3MgZmlyc3QgdW5kZXJzdGFuZCB0aGUgcHJvYmxlbSwgZXh0cmFjdCByZWxldmFudCB2YXJpYWJsZXMgYW5kIHRoZWlyIGNvcnJlc3BvbmRpbmcgbnVtZXJhbHMsIGFuZCBkZXZpc2UgYSBwbGFuLiBUaGVuLCBsZXQncyBjYXJyeSBvdXQgdGhlIHBsYW4sIGNhbGN1bGF0ZSBpbnRlcm1lZGlhdGUgcmVzdWx0cyAocGF5IGF0dGVudGlvbiB0byBjYWxjdWxhdGlvbiBhbmQgY29tbW9uIHNlbnNlKSwgc29sdmUgdGhlIHByb2JsZW0gc3RlcCBieSBzdGVwLCBhbmQgc2hvdyB0aGUgYW5zd2VyLiIsIm1vZGVsIjoiZ3B0LTMuNS10dXJibyJ9" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>
- Answer extraction
<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiNjIzIHBvdW5kcy4iLCJwcm9tcHQiOiJROiBHcmFjZSB3ZWlnaHMgMTI1IHBvdW5kcy4gQWxleCB3ZWlnaHMgMiBwb3VuZHMgbGVzcyB0aGFuIDQgdGltZXMgd2hhdCBHcmFjZSB3ZWlnaHMuXG5XaGF0IGFyZSB0aGVpciBjb21iaW5lZCB3ZWlnaHRzIGluIHBvdW5kcz9cbkE6IExldCdzIGZpcnN0IHVuZGVyc3RhbmQgdGhlIHByb2JsZW0sIGV4dHJhY3QgcmVsZXZhbnQgdmFyaWFibGVzIGFuZCB0aGVpciBjb3JyZXNwb25kaW5nIG51bWVyYWxzLCBhbmQgZGV2aXNlIGEgcGxhbi4gVGhlbiwgbGV0J3MgY2Fycnkgb3V0IHRoZSBwbGFuLCBjYWxjdWxhdGUgaW50ZXJtZWRpYXRlIHJlc3VsdHMgKHBheSBhdHRlbnRpb24gdG8gY2FsY3VsYXRpb24gYW5kIGNvbW1vbiBzZW5zZSksIHNvbHZlIHRoZSBwcm9ibGVtIHN0ZXAgYnkgc3RlcCwgYW5kIHNob3cgdGhlIGFuc3dlci5cbkxldCdzIGRlbm90ZTogIFxuLSBHcmFjZSdzIHdlaWdodCBhcyBHID0gMTI1IGxicyAgXG4tIEFsZXgncyB3ZWlnaHQgYXMgQVxuXG5BY2NvcmRpbmcgdG8gdGhlIGdpdmVuIGluZm9ybWF0aW9uLCBBbGV4IHdlaWdocyAyIHBvdW5kcyBsZXNzIHRoYW4gNCB0aW1lcyB3aGF0IEdyYWNlIHdlaWdocy4gV2UgY2FuIHdyaXRlIHRoaXMgYXMgYW4gZXF1YXRpb246ICBcbkEgPSA0RyAtIDIgIFxuQSA9IDQqMTI1IC0gMiAgXG5BID0gNTAwIC0gMiAgXG5BID0gNDk4IGxic1xuXG5Ob3csIHdlIGNhbiBmaW5kIHRoZSBjb21iaW5lZCB3ZWlnaHQgb2YgR3JhY2UgYW5kIEFsZXggYnkgYWRkaW5nIHRoZWlyIHdlaWdodHM6ICBcbkNvbWJpbmVkIHdlaWdodCA9IEdyYWNlJ3Mgd2VpZ2h0ICsgQWxleCdzIHdlaWdodCAgXG5Db21iaW5lZCB3ZWlnaHQgPSAxMjUgKyA0OTggIFxuQ29tYmluZWQgd2VpZ2h0ID0gNjIzIGxic1xuXG5UaGVyZWZvcmUsIHRoZWlyIGNvbWJpbmVkIHdlaWdodHMgaW4gcG91bmRzIGlzIDYyMyBwb3VuZHMuXG5cblRoZXJlZm9yZSB0aGUgYW5zd2VyIGluIGFyYWJpYyBudW1lcmFsIGlzOiIsIm1vZGVsIjoiZ3B0LTMuNS10dXJibyJ9" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

The only difference between PS and PS+ prompting is that in PS+ prompting, the prompt emphasizes the LLM to pay attention to calculation and intermediate steps. As a result, PS+ prompting reduces calculation and the missing steps error.

## What Are Plan-and-Solve Prompting Results?

- PS+ prompting outperforms Zero-Shot CoT in symbolic reasoning datasets like last letters, commonsense reasoning datasets ([CSQA](https://paperswithcode.com/paper/complex-sequential-question-answering-towards), [StrategyQA](https://paperswithcode.com/dataset/strategyqa)), and math reasoning datasets.
- PS+ prompting reduces the missing steps error and semantic understanding error compared to Zero-Shot CoT.

## Limitations of Plan-and-Solve Prompting

There are two major limitations to the PS prompting approach:

- Models like GPT-3 are sensitive to expressions in the prompt hence, designing the prompt to guide LLMs in generating correct reasoning steps takes considerable effort.
- PS prompting addresses calculation and missing-reasoning-step errors but doesn't pacify semantic misunderstanding errors.

## Conclusion

[Plan-and-Solve prompting](https://learnprompting.org/vocabulary/plan-and-solve_prompting) techniques (PS and PS+) help reduce the missing steps error and calculation errors by carefully crafting prompts and making the model think and plan before solving the problem. The approach has proven effective in various tasks: math reasoning, common sense reasoning, and symbolic reasoning. However, the approach heavily relies on the trigger sentence in the prompt. As such, coming up with the best trigger sentence or prompt may prove challenging as it is manual.

Find more on [Decomposition Prompting](https://learnprompting.org/docs/advanced/decomposition/introduction) methods.