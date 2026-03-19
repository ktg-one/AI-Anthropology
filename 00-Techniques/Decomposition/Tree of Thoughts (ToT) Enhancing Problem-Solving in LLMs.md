---
title: "Tree of Thoughts (ToT): Enhancing Problem-Solving in LLMs"
source: https://learnprompting.org/docs/advanced/decomposition/tree_of_thoughts
author:
  - '[["Bhuwan Bhatt"]]'
published:
created: 2025-09-07
description: Discover how Tree of Thoughts (ToT) prompting boosts decision-making by exploring multiple reasoning paths, outperforming traditional methods in complex tasks.
tags:
  - clippings
feature: thumbnails/external/eb199fcc4b791fc13fdea97b76df2483.svg
---
Reading Time: 4 minutes

Last updated on September 27, 2024

[Bhuwan Bhatt](https://learnprompting.org/docs/advanced/decomposition/#Bhuwan%20Bhatt-bio)

![Tree of Thoughts illustration](https://learnprompting.org/docs/assets/advanced/advanced_covers/tot_cover.svg)

Takeaways

- **Tree of Thoughts (ToT) prompting** enables models to explore and evaluate multiple reasoning paths, enhancing decision-making and solution accuracy.
- **ToT mimics human problem-solving** by using a tree structure where nodes represent partial solutions, allowing the model to backtrack when necessary.
- **Two key components**: Propose prompts generate possible solutions, and value prompts evaluate and guide the model toward the best path.
- **ToT outperforms other methods** in tasks like math reasoning, creative writing, and puzzles, with higher success rates and more coherent results.
- **Limitations** include increased resource consumption and inefficiency for simpler tasks that don’t require extensive reasoning.

## What is Tree of Thoughts Prompting?

Since their inception, [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) are increasingly becoming popular and getting deployed in a wide range of applications across many different industries. But, a common theme across [LLM](https://learnprompting.org/vocabulary/LLM) inference is that they are still confined to token-level, left-to-right decision-making processes. They still fall short in tasks requiring exploration or making assumptions about the future state, given the present state.

Tree of Thoughts (ToT) prompting<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Shunyu Yao. (2023). Tree of Thoughts: Deliberate Problem Solving with Large Language Models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a framework for LLM inference that allows LLMs to make an informed decision by considering and self-evaluating multiple different reasoning paths that will likely lead to an optimal solution. ToT also empowers the model to backtrack when a path is unlikely to lead to a valid solution. ToT is similar to the [best-first search algorithm](https://en.wikipedia.org/wiki/Best-first_search) in Computer Science.

ToT aims to mimic human's problem-solving approach. Research shows that, given a problem, humans search through a combinatorial problem space - a tree where the nodes represent partial solutions and branches represent operators that modify the nodes. They use heuristics to identify the next branch that guides them closer to the solution. The process continues till the problem concludes.

## How to Use Tree of Thoughts Prompting?

Let's look at how we can implement ToT using two distinct examples:

- Game of 24
- Creative writing

### Game of 24

Game of 24 is a mathematical problem where the goal is to use given four numbers and four basic operators: +, -, /,\*, to obtain 24. At each step, the **propose prompt** generates three possible solutions, and the **value prompt** evaluates each of the generated candidates and decides whether proceeding with the suggested generation is worthwhile. It will be clear once we look at the example below.

**Problem statement:** Using the numbers 4, 9, 10, and 13 and four basic operators +, -, /,\*, generate an expression that evaluates to 24.

1. In the first step, prompt the model to get candidate solutions.
<iframe src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiNCs5ID0gMTMgKGxlZnQ6IDEzLCAxMCwgMTMpXG4xMC00ID0gNiAobGVmdDogNiwgOSwgMTMpXG4xMy05ID0gNCAobGVmdDogNCwgOSwgMTApIiwicHJvbXB0IjoiSW5wdXQ6IDQsIDYsIDgsIDEwXG5Qb3NzaWJsZSBuZXh0IHN0ZXBzOlxuNCs2ID0gMTAgKGxlZnQ6IDEwLCA4LCAxMClcbjgtNCA9IDQgKGxlZnQgNCwgNiwgMTApXG4xMCs0ID0gMTQgKGxlZnQ6IDE0LCA2LCA4KVxuXG5JbnB1dDogNCA5IDEwIDEzXG5Qb3NzaWJsZSBuZXh0IHN0ZXBzOiIsIm1vZGVsIjoiZ3B0LTMuNS10dXJibyJ9" loading="lazy" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>
2. In the second step, prompt the model to evaluate all its generated solution  
	Evaluating 13, 10, 13
<iframe src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiMTAgKyAxMyArIDEzID0gMzYgaW1wb3NzaWJsZSIsInByb21wdCI6IkV2YWx1YXRlIGlmIHRoZSBudW1iZXJzIGNhbiByZWFjaCAyNCAoIHN1cmUvbGlrZWx5L2ltcG9zc2libGUpXG4xMCAxNDogMTArMTQgPSAyNCBzdXJlXG4xMCA3IDI6IDcqMisxMCA9IDI0IHN1cmVcbjExIDExOiAxMSArIDExID0gMjIgaW1wb3NzaWJsZVxuMTMsIDEwLCAxMzoiLCJtb2RlbCI6ImdwdC0zLjUtdHVyYm8ifQ%3D%3D" loading="lazy" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

Evaluating 6, 9, 13

<iframe src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiNiAqICAoMTMtOSkgPSAyNCBzdXJlIiwicHJvbXB0IjoiSW5wdXQ6IDQsIDYsIDgsIDEwXG5Qb3NzaWJsZSBuZXh0IHN0ZXBzOlxuNCs2ID0gMTAgKGxlZnQ6IDEwLCA4LCAxMClcbjgtNCA9IDQgKGxlZnQgNCwgNiwgMTApXG4xMCs0ID0gMTQgKGxlZnQ6IDE0LCA2LCA4KVxuXG5JbnB1dDogNCA5IDEwIDEzXG5Qb3NzaWJsZSBuZXh0IHN0ZXBzOiIsIm1vZGVsIjoiZ3B0LTMuNS10dXJibyJ9" loading="lazy" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

For each generated node using the propose prompt, the value prompt evaluates it. Then, for all the nodes that are likely to reach the solution, expand them using the propose prompt. Use Breadth First Search (BFS) to expand all nodes at one level before moving on to the nodes at the next level. The process is continued until only the number 24 is left in a node.

### Creative Writing

The creative writing task helps evaluate the creative thinking and planning abilities of the LLM.

**Problem statement:** Given four random sentences, generate a passage with four paragraphs that end in the input four sentences respectively.

**Step 1:**  
First, ask the LLM to generate 5 different plans for the passage.

Plan 1

<iframe src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiUGFyYWdyYXBoIDE6IERpc2N1c3MgdGhlIHNpbXBsaWNpdHkgb2YgZG9pbmcgYSBoYW5kc3RhbmQgd2l0aCBjb25maWRlbmNlLlxuXG5QYXJhZ3JhcGggMjogRGVzY3JpYmUgYW4gdW5leHBlY3RlZCBzZW5zYXRpb24gZXhwZXJpZW5jZWQgaW4gc3BhY2UuXG5cblBhcmFncmFwaCAzOiBTaGFyZSBhIGh1bW9yb3VzIGFuZWNkb3RlIGFib3V0IHVzaW5nIHNpZ24gbGFuZ3VhZ2UgdG8gZGV0ZXIgdW53YW50ZWQgYWR2YW5jZXMuXG5cblBhcmFncmFwaCA0OiBSZWZsZWN0IG9uIHRoZSB2YXJ5aW5nIHBlcnNwZWN0aXZlcyB0aGF0IG90aGVycyBoYXZlIG9mIG9uZSdzIGlkZW50aXR5LiIsInByb21wdCI6IldyaXRlIGEgY29oZXJlbnQgcGFzc2FnZSBvZiA0IHNob3J0IHBhcmFncmFwaHMuIFRoZSBlbmQgc2VudGVuY2Ugb2YgZWFjaCBwYXJhZ3JhcGggbXVzdCBiZTogMS4gSXQgaXNuJ3QgZGlmZmljdWx0IHRvIGRvIGEgaGFuZHN0YW5kIGlmIHlvdSBqdXN0IHN0YW5kIG9uIHlvdXIgaGFuZHMuIDIuIEl0IGNhdWdodCBoaW0gb2ZmIGd1YXJkIHRoYXQgc3BhY2Ugc21lbGxlZCBvZiBzZWFyZWQgc3RlYWsuIDMuIFdoZW4gc2hlIGRpZG4ndCBsaWtlIGEgZ3V5IHdobyB3YXMgdHJ5aW5nIHRvIHBpY2sgaGVyIHVwLCBzaGUgc3RhcnRlZCB1c2luZyBzaWduIGxhbmd1YWdlLiA0LlxuRWFjaCBwZXJzb24gd2hvIGtub3dzIHlvdSBoYXMgYSBkaWZmZXJlbnQgcGVyY2VwdGlvbiBvZiB3aG8geW91IGFyZS5cblxuR2VuZXJhdGUgYSBvbmUgbGluZSBwbGFuIG9uIGhvdyB5b3Ugd291bGQgd3JpdGUgdGhlIHBhc3NhZ2UuIiwibW9kZWwiOiJncHQtMy41LXR1cmJvIn0%3D" loading="lazy" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

Plan 2

<iframe src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiSSB3b3VsZCB3cml0ZSBhIHBhc3NhZ2UgZXhwbG9yaW5nIHVuaXF1ZSBhbmQgdW5leHBlY3RlZCBleHBlcmllbmNlcywgc3VjaCBhcyBkb2luZyBhIGhhbmRzdGFuZCwgZXhwZXJpZW5jaW5nIHRoZSBzY2VudCBvZiBzcGFjZSwgdXNpbmcgc2lnbiBsYW5ndWFnZSB0byBkZXRlciB1bndhbnRlZCBhdHRlbnRpb24sIGFuZCB0aGUgdmFyeWluZyBwZXJjZXB0aW9ucyBvdGhlcnMgaGF2ZSBvZiBvdXIgaWRlbnRpdHkuXG5cbkl0IGlzbid0IGRpZmZpY3VsdCB0byBkbyBhIGhhbmRzdGFuZCBpZiB5b3UganVzdCBzdGFuZCBvbiB5b3VyIGhhbmRzLiBBcyBoZSBhdHRlbXB0ZWQgdGhlIGFjcm9iYXRpYyBmZWF0LCBoZSBmb3VuZCBhIHNlbnNlIG9mIGJhbGFuY2UgYW5kIGNvbnRyb2wgaGUgaGFkIG5ldmVyIGV4cGVyaWVuY2VkIGJlZm9yZS5cblxuSXQgY2F1Z2h0IGhpbSBvZmYgZ3VhcmQgdGhhdCBzcGFjZSBzbWVsbGVkIG9mIHNlYXJlZCBzdGVhay4gVGhlIGFzdHJvbmF1dHMgd2VyZSBzdXJwcmlzZWQgYnkgdGhlIHVuZXhwZWN0ZWQgYXJvbWEgdGhhdCBmaWxsZWQgdGhlaXIgc3BhY2VjcmFmdCwgYSByZW1pbmRlciBvZiB0aGUgcmljaG5lc3Mgb2YgRWFydGgncyBjdWlzaW5lLlxuXG5XaGVuIHNoZSBkaWRuJ3QgbGlrZSBhIGd1eSB3aG8gd2FzIHRyeWluZyB0byBwaWNrIGhlciB1cCwgc2hlIHN0YXJ0ZWQgdXNpbmcgc2lnbiBsYW5ndWFnZS4gSGVyIHNpbGVudCBjb21tdW5pY2F0aW9uIHdhcyBhIHBvd2VyZnVsIHRvb2wgaW4gZXhwcmVzc2luZyBoZXIgZGlzaW50ZXJlc3QgYW5kIGFzc2VydGluZyBoZXIgYm91bmRhcmllcy5cblxuRWFjaCBwZXJzb24gd2hvIGtub3dzIHlvdSBoYXMgYSBkaWZmZXJlbnQgcGVyY2VwdGlvbiBvZiB3aG8geW91IGFyZS4gT3VyIGlkZW50aXRpZXMgYXJlIHNoYXBlZCBieSB0aGUgaW50ZXJhY3Rpb25zIHdlIGhhdmUgd2l0aCBvdGhlcnMsIGVhY2ggcGVyc29uIGhvbGRpbmcgYSB1bmlxdWUgcGVyc3BlY3RpdmUgb24gb3VyIHRydWUgc2VsdmVzLiIsInByb21wdCI6IldyaXRlIGEgY29oZXJlbnQgcGFzc2FnZSBvZiA0IHNob3J0IHBhcmFncmFwaHMuIFRoZSBlbmQgc2VudGVuY2Ugb2YgZWFjaCBwYXJhZ3JhcGggbXVzdCBiZTogMS4gSXQgaXNuJ3QgZGlmZmljdWx0IHRvIGRvIGEgaGFuZHN0YW5kIGlmIHlvdSBqdXN0IHN0YW5kIG9uIHlvdXIgaGFuZHMuIDIuIEl0IGNhdWdodCBoaW0gb2ZmIGd1YXJkIHRoYXQgc3BhY2Ugc21lbGxlZCBvZiBzZWFyZWQgc3RlYWsuIDMuIFdoZW4gc2hlIGRpZG4ndCBsaWtlIGEgZ3V5IHdobyB3YXMgdHJ5aW5nIHRvIHBpY2sgaGVyIHVwLCBzaGUgc3RhcnRlZCB1c2luZyBzaWduIGxhbmd1YWdlLiA0LlxuRWFjaCBwZXJzb24gd2hvIGtub3dzIHlvdSBoYXMgYSBkaWZmZXJlbnQgcGVyY2VwdGlvbiBvZiB3aG8geW91IGFyZS5cblxuR2VuZXJhdGUgYSBvbmUgbGluZSBwbGFuIG9uIGhvdyB5b3Ugd291bGQgd3JpdGUgdGhlIHBhc3NhZ2UuIiwibW9kZWwiOiJncHQtMy41LXR1cmJvIn0%3D" loading="lazy" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>**Step 2:**

Present all 5 plans to the LLM and ask it to choose the best one. A simple [Zero-Shot](https://learnprompting.org/docs/basics/few_shot) voting prompt, "analyze choices below, then conclude which is most promising for the instruction," is used.

Repeat this step 5 times and choose the plan (say Plan 1) that gains the maximum votes.

**Step 3**  
Use the chosen plan to generate the passage.

The image below illustrates the use of ToT for creative writing tasks.

![Tree of Thoughts framework for creative writing](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Ftot_creative_writing.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

ToT for creative writing<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Shunyu Yao. (2023). Tree of Thoughts: Deliberate Problem Solving with Large Language Models.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

## What Are Tree of Thoughts Prompting Results?

- In the "Game of 24" task, a mathematical reasoning problem, ToT with b = 1(retaining the best 1 candidate at each step) is comparable to [Chain-of-Thought (CoT) Prompting](https://learnprompting.org/docs/intermediate/chain_of_thought), and ToT with b = 5 beats CoT by a huge margin of 25%.

| Method | Success |
| --- | --- |
| IO (best of 100) | 33% |
| CoT (best of 100) | 49% |
| ToT (ours) (b=5) | 74% |

- In creative writing, ToT generates more coherent passages compared to passages generated using [Input-Output (IO)](https://learnprompting.org/vocabulary/input-output_prompting) prompting and CoT prompting<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Jason Wei. (2022). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> .

![Coherency test scores for ToT and other techniques](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Ftot_coherency_score.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

ToT coherency score for creative writing task<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Shunyu Yao. (2023). Tree of Thoughts: Deliberate Problem Solving with Large Language Models.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

- In crossword puzzles, ToT significantly outperforms IO and CoT techniques in word level success rate and also wins 20% of the games compared to the 1% win rate of CoT.

| Method | Success Rate(%) |  |  |
| --- | --- | --- | --- |
|  | **Letter** | **Word** | **Game** |
| IO | 38.7 | 14 | 0 |
| CoT | 40.6 | 15.6 | 1 |
| ToT | **78** | **60** | **20** |

## Limitations of Tree of Thoughts Prompting

- Although the ToT framework can help LLMs solve problems that require planning and decision-making, it may not be the most efficient [prompting technique](https://learnprompting.org/vocabulary/prompting_technique) for common NLP (Natural Language Processing) tasks as they are too easy for models like GPT-4.
- ToT is a resource (cost, number of requests, etc.) intensive framework.

![Cost Comparision of ToT with IO and CoT in the Game of 24 task](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Ftot_cost.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Cost analysis of the Game of 24<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Shunyu Yao. (2023). Tree of Thoughts: Deliberate Problem Solving with Large Language Models.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

## Conclusion

Tree of Thoughts (ToT) is a practical framework for intellectually demanding tasks that require some planning and look-ahead. However, implementing ToT is demanding in terms of resources consumed and effort required. Consequently, it is wise to use it to solve only those tasks that cannot be solved using techniques like IO prompting and CoT prompting.

Find more on [Decomposition Prompting](https://learnprompting.org/docs/advanced/decomposition/introduction) methods.