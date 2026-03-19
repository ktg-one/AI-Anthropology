---
title: "Self-Verification Prompting: Enhancing LLM Accuracy in Reasoning Tasks"
source: https://learnprompting.org/docs/advanced/self_criticism/self_verification
author:
  - '[["Bhuwan Bhatt"]]'
published:
created: 2025-09-07
description: Learn how Self-Verification improves LLM accuracy by validating conclusions, correcting errors in reasoning, and enhancing performance without extra data.
tags:
  - clippings
feature: thumbnails/external/0df379eca1db72b7551f028c1356a71c.svg
---
◆ This article is rated [hard](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 4 minutes

Last updated on September 27, 2024

[Bhuwan Bhatt](https://learnprompting.org/docs/advanced/self_criticism/#Bhuwan%20Bhatt-bio)

![Self-Verification process](https://learnprompting.org/docs/assets/advanced/advanced_covers/self_verif_cover.svg)

Takeaways

- **Error Correction**: Self-Verification helps LLMs fix mistakes in multi-step reasoning by verifying conclusions against the original context.
- **Dual Process**: It involves generating multiple answers and verifying them by checking if conclusions match the initial conditions.
- **Improved Performance**: Self-Verification boosts accuracy in reasoning tasks, including commonsense reasoning, and enhances high-performing models like InstructGPT.

## What is Self-Verification Prompting?

[Chain-of-Thought (CoT) Prompting](https://learnprompting.org/docs/intermediate/chain_of_thought)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Jason Wei. (2022). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> helps [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) simulate the human thinking process and construct intermediate reasoning steps before writing the conclusion when solving complex tasks. But when solving complex tasks requiring multiple reasoning steps, a small mistake in the early steps can propagate to other steps and produce a wrong answer. CoT lacks an error correction mechanism. Some methods<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Shen, J., Yin, Y., Li, L., Shang, L., Jiang, X., Zhang, M., &amp; Liu, Q. (2021). Generate &amp; Rank: A Multi-task Framework for Math Word Problems. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2109.03034" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2109.03034</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> mitigate this issue by training a separate verifier to evaluate the accuracy of generated response, but, training requires a ton of human-labeled task-specific data as well as computing resources.

Humans can self-verify their answers by using the conclusion to predict the original condition provided in the question. If the original condition in the question can be derived from the conclusion, the obtained answer is correct. **Self-Verification Prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">3</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Yixuan Weng. (2022). Large Language Models are Better Reasoners with Self-Verification. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2212.09561" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2212.09561</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> mimics this human behavior and evaluates the correctness of the generated response by using the generated response to predict the conditions in the original context.

The Self-Verification process consists of two steps:

- Forward reasoning: The [LLM](https://learnprompting.org/vocabulary/LLM) generates candidate answers with [CoT prompting](https://learnprompting.org/vocabulary/CoT_Prompting). The LLM performs sampling decoding to generate multiple candidate answers.
- Backward verification: Each candidate answer obtained from the LLM in the previous step are verified and the answer that gets the most votes or correctly predicts the condition given the conclusion more frequently is the final answer.

## How to Use Self-Verification Prompting?

Let's use Self-Verification prompting to generate an answer for the following question:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Jackie has 10 apples. Adam has 8 apples. How many more apples does Jackie have than Adam?

### Forward Reasoning

- Generate sample answers using [Few-Shot Chain-of-Thought](https://learnprompting.org/docs/intermediate/chain_of_thought) and [sampling decoding](https://www.ibm.com/docs/en/watsonx/saas?topic=lab-model-parameters-prompting). You can change the temperature value, top k, or top p variable to get a variety of answers.

| Parameter | Supported values | Use |
| --- | --- | --- |
| Temperature | Floating-point number in the range 0.0 (same as greedy decoding) to 2.0 (maximum creativity) | Higher values lead to greater variability |
| Top K | Integer in the range 1 to 100 | Higher values lead to greater variability |
| Top P | Floating-point number in the range 0.0 to 1.0 | Unless you change the value, this setting is not used |

Answer A1:

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiU2luY2UgSmFja2llIGhhcyAxMCBhcHBsZXMgYW5kIEFkYW0gaGFzIDggYXBwbGVzLCBpbiB0b3RhbCwgSmFja2llIGhhcyAxMCs4PTE4IG1vcmUgYXBwbGVzIHRoYW4gQWRhbSwgc28gdGhlIGFuc3dlciBpcyAxOC4iLCJwcm9tcHQiOiJROiBUaGVyZSBhcmUgMTUgdHJlZXMgaW4gdGhlIGdyb3ZlLiBHcm92ZSB3b3JrZXJzIHdpbGwgcGxhbnQgdHJlZXMgaW4gdGhlIGdyb3ZlIHRvZGF5LiBBZnRlciB0aGV5IGFyZSBkb25lLCB0aGVyZSB3aWxsIGJlIDIxIHRyZWVzLiBIb3cgbWFueSB0cmVlcyBkaWQgdGhlIGdyb3ZlIHdvcmtlcnMgcGxhbnQgdG9kYXk%2FXG5BOiBUaGVyZSBhcmUgMTUgdHJlZXMgb3JpZ2luYWxseS4gVGhlbiB0aGVyZSB3ZXJlIDIxIHRyZWVzIGFmdGVyIHNvbWUgbW9yZSB3ZXJlIHBsYW50ZWQuIFNvIHRoZXJlXG5tdXN0IGhhdmUgYmVlbiAyMSAtIDE1ID0gNi4gVGhlIGFuc3dlciBpcyA2LlxuXG5ROkphY2tpZSBoYXMgMTAgYXBwbGVzLiBBZGFtIGhhcyA4IGFwcGxlcy4gSG93IG1hbnkgbW9yZSBhcHBsZXMgZG9lcyBKYWNraWUgaGF2ZSB0aGFuIEFkYW0%2FXG5BOiIsIm1vZGVsIjoiZ3B0LTMuNS10dXJibyJ9" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

Answer A2:

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiSmFja2llIGhhcyAxMCBhcHBsZXMsIHNvIEphY2tpZSBoYXMgMTAtOD0yIG1vcmUgYXBwbGVzIHRoYW4gQWRhbSwgYW5kIHRoZSBhbnN3ZXIgaXMgMiIsInByb21wdCI6IlE6IFRoZXJlIGFyZSAxNSB0cmVlcyBpbiB0aGUgZ3JvdmUuIEdyb3ZlIHdvcmtlcnMgd2lsbCBwbGFudCB0cmVlcyBpbiB0aGUgZ3JvdmUgdG9kYXkuIEFmdGVyIHRoZXkgYXJlIGRvbmUsIHRoZXJlIHdpbGwgYmUgMjEgdHJlZXMuIEhvdyBtYW55IHRyZWVzIGRpZCB0aGUgZ3JvdmUgd29ya2VycyBwbGFudCB0b2RheT9cbkE6IFRoZXJlIGFyZSAxNSB0cmVlcyBvcmlnaW5hbGx5LiBUaGVuIHRoZXJlIHdlcmUgMjEgdHJlZXMgYWZ0ZXIgc29tZSBtb3JlIHdlcmUgcGxhbnRlZC4gU28gdGhlcmVcbm11c3QgaGF2ZSBiZWVuIDIxIC0gMTUgPSA2LiBUaGUgYW5zd2VyIGlzIDYuXG5cblE6SmFja2llIGhhcyAxMCBhcHBsZXMuIEFkYW0gaGFzIDggYXBwbGVzLiBIb3cgbWFueSBtb3JlIGFwcGxlcyBkb2VzIEphY2tpZSBoYXZlIHRoYW4gQWRhbT9cbkE6IiwibW9kZWwiOiJncHQtMy41LXR1cmJvIn0%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

### Backward Verification

This step consists of multiple sub-steps. Let's go through each of them:

#### Rewritten Candidate Conclusion

Rewrite the original question with the candidate's answer in a declarative form. You can use the following [prompt template](https://learnprompting.org/vocabulary/prompt_template):

> Please change the questions and answers into complete declarative sentences \[q\] The answer is \[y\].

Declarative form for Answer A1:

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiSmFja2llIGhhcyAxMCBhcHBsZXMgYW5kIEFkYW0gaGFzIDggYXBwbGVzLCBzbyBKYWNraWUgaGFzIDE4IG1vcmUgYXBwbGVzIHRoYW4gQWRhbS4iLCJwcm9tcHQiOiJQbGVhc2UgY2hhbmdlIHRoZSBxdWVzdGlvbnMgYW5kIGFuc3dlcnMgaW50byBjb21wbGV0ZSBkZWNsYXJhdGl2ZSBzZW50ZW5jZXMgW0phY2tpZSBoYXMgMTAgYXBwbGVzLiBBZGFtIGhhcyA4IGFwcGxlcy5Ib3cgbWFueSBtb3JlIGFwcGxlcyBkb2VzIEphY2tpZSBoYXZlIHRoYW4gQWRhbT9dIFRoZSBhbnN3ZXIgaXMgW1NpbmNlIEphY2tpZSBoYXMgMTAgYXBwbGVzIGFuZCBBZGFtIGhhcyA4IGFwcGxlcywgaW4gdG90YWwsIEphY2tpZSBoYXMgMTArOD0xOCBtb3JlIGFwcGxlcyB0aGFuIEFkYW0sIHNvIHRoZSBhbnN3ZXIgaXMgMTguXSIsIm1vZGVsIjoiZ3B0LTMuNS10dXJibyJ9" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

Declarative form for Answer A2:

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiSmFja2llIGhhcyAxMCBhcHBsZXMuIEFkYW0gaGFzIDggYXBwbGVzLiBKYWNraWUgaGFzIDIgbW9yZSBhcHBsZXMgdGhhbiBBZGFtLiIsInByb21wdCI6IlBsZWFzZSBjaGFuZ2UgdGhlIHF1ZXN0aW9ucyBhbmQgYW5zd2VycyBpbnRvIGNvbXBsZXRlIGRlY2xhcmF0aXZlIHNlbnRlbmNlcyBbSmFja2llIGhhcyAxMCBhcHBsZXMuIEFkYW0gaGFzIDggYXBwbGVzLkhvdyBtYW55IG1vcmUgYXBwbGVzIGRvZXMgSmFja2llIGhhdmUgdGhhbiBBZGFtP10gVGhlIGFuc3dlciBpcyBbSmFja2llIGhhcyAxMCBhcHBsZXMsIHNvIEphY2tpZSBoYXMgMTAtOD0yIG1vcmUgYXBwbGVzIHRoYW4gQWRhbSwgYW5kIHRoZSBhbnN3ZXIgaXMgMl0iLCJtb2RlbCI6ImdwdC0zLjUtdHVyYm8ifQ%3D%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

#### Rewritten Condition/ Condition Masking

- Mask one of the conditions in the declarative and prepare new questions for the LLM. The new questions can be either true-false questions or questions asking the LLM to predict the masked value. Sample questions from the above declarative form:
	- Jackie has X apples, and Adam has 8 apples, so Jackie has 18 more apples than Adam. What is the value of X?
	- Jackie has X apples. Adam has 8 apples. Jackie has 2 more apples than Adam. What is the value of X?
- True-false questions are suitable for non-arithmetic tasks. We won't be using them in our demonstration, but they can be of the form:
	- Adam has 8 apples, so Jackie has 18 more apples than Adam. Jackie has a total of 10 apples. Is it correct(True or False)?
	- Adam has 8 apples. Jackie has 2 more apples than Adam. Jackie has a total of 10 apples. Is it correct(True or False)?

#### Verification

- Finally, pass the re-written conditions to the LLM and predict the masked value (or true/false). For each rewritten condition, repeat the process P (say 5) times and increment the score of the respective condition when the LLM predicts the condition correctly.
- The answer corresponding to the condition with maximum votes is the final answer.
<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiSWYgSmFja2llIGhhcyAxOCBtb3JlIGFwcGxlcyB0aGFuIEFkYW0gYW5kIEFkYW0gaGFzIDggYXBwbGVzLCB0aGVuIEphY2tpZSBtdXN0IGhhdmUgOCArIDE4ID0gMjYgYXBwbGVzLlxuXG5UaGVyZWZvcmUsIHRoZSB2YWx1ZSBvZiBYIGlzIDI2IGFwcGxlcy4iLCJwcm9tcHQiOiJKYWNraWUgaGFzIFggYXBwbGVzIGFuZCBBZGFtIGhhcyA4IGFwcGxlcywgc28gSmFja2llIGhhcyAxOCBtb3JlIGFwcGxlcyB0aGFuIEFkYW0uIFdoYXQgaXMgdGhlIHZhbHVlIG9mIFg%2FIiwibW9kZWwiOiJncHQtMy41LXR1cmJvIn0%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe><iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiSWYgSmFja2llIGhhcyAyIG1vcmUgYXBwbGVzIHRoYW4gQWRhbSB3aG8gaGFzIDggYXBwbGVzLCB0aGVuIEphY2tpZSBoYXMgOCArIDIgPSAxMCBhcHBsZXMuXG5UaGVyZWZvcmUsIHRoZSB2YWx1ZSBvZiBYIGlzIDEwLiIsInByb21wdCI6IkphY2tpZSBoYXMgWCBhcHBsZXMuIEFkYW0gaGFzIDggYXBwbGVzLiBKYWNraWUgaGFzIDIgbW9yZSBhcHBsZXMgdGhhbiBBZGFtLldoYXQgaXMgdGhlIHZhbHVlIG9mIFg%2FIiwibW9kZWwiOiJncHQtMy41LXR1cmJvIn0%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

Here, the later condition correctly predicts the value of X more often, and hence, the answer that corresponds to this rewritten condition, i.e., "A2: Jackie has 10 apples, so Jackie has 10-8=2 more apples than Adam, and the answer is 2." is the correct answer.

## What Are Self-Verification Prompting Results?

- Self-Verification improves the performance of prior methods in all datasets. It also achieves the new state-of-the-art (SOTA) performance in 6 of the 8 datasets.
- Even high-performing forward reasoning models like InstructGPT improve by an average of 2.33% when using Self-Verification implying models with strong forward reasoning capabilities also benefit from the Self-Verification mechanism.
- Self-Verification technique can effectively improve the accuracy of commonsense reasoning models.

![verification stage improves accuracy](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fself_verification_commonsense_reasoning_effectiveness.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Impact of the verification stage in accuracy<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">3</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Yixuan Weng. (2022). Large Language Models are Better Reasoners with Self-Verification. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2212.09561" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2212.09561</a></span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

## Limitations of Self-Verification Prompting

- The effectiveness of Self-Verification relies on the ability of the model to generate the correct answer as one of the candidate answers. As such, smaller language models may not benefit from this technique.
- The method requires generating multiple candidate inference chains. This increases the computational cost for inference.

## Conclusion

Just like humans, LLMs are capable of self-verifying their own answers without relying on an external trained model for answer verification. Self-verification improves the accuracy and reliability of LLMs in reasoning tasks without the need for separate models trained on human-labeled data.