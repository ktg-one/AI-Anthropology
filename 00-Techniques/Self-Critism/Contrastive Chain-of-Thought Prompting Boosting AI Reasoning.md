---
title: "Contrastive Chain-of-Thought Prompting: Boosting AI Reasoning"
source: https://learnprompting.org/docs/advanced/thought_generation/contrastive_cot
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Discover how Contrastive CoT improves reasoning by using both correct and incorrect examples to refine AI model accuracy, enhancing problem-solving skills.
tags:
  - clippings
feature: thumbnails/external/3ca7c7191658e81a91376a8203fdb348.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on October 1, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/thought_generation/#Valeriia%20Kuka-bio)

![Contrastive Chain-of-Thought in action](https://learnprompting.org/docs/assets/advanced/advanced_covers/contrastive_cot_cover.svg)

Overview of Contrastive Chain-of-Thought (CoT) Prompting

Takeaways

- **Learning from Negative Examples**: Contrastive Chain-of-Thought (CoT) enhances LLM reasoning by incorporating both positive and negative examples
- **Prompt Structure**: Contrastive CoT prompts include a question, correct/incorrect answers, and the query.
- **Generating Examples**: Automatically create contrastive examples by shuffling key entities from correct answers.

### Information and Links

| Technique | Institution | Date of Publication | Paper | Code |
| --- | --- | --- | --- | --- |
| Contrastive Chain-of-Thought (CoT) Prompting | DAMO Academy, Alibaba Group; Singapore University of Technology and Design; Nanyang Technological University, Singapore | Nov 2023 | [Contrastive Chain-of-Thought Prompting](https://arxiv.org/abs/2311.09277) | [DAMO-NLP-SG/contrastive-cot](https://github.com/DAMO-NLP-SG/contrastive-cot) |

## What is Contrastive Chain-of-Thought (CoT) Prompting?

[Chain-of-Thought (CoT) Prompting](https://learnprompting.org/docs/intermediate/chain_of_thought)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/thought_generation/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Jason Wei. (2022). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> improves the accuracy of [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) when solving mathematical and reasoning tasks by compelling the models to think. Adding a simple statement like "Let's think step by step" to the prompt can significantly improve the model's performance. Adding a positive example, a question-answer pair, before the actual question further improves the reasoning of the LLM. Learning from negative examples is not unique to humans and can also be replicated in LLMs. Embedding negative examples with the prompt can help LLMs learn from them and generate better explanations for their answers.

Inspired by human's ability to learn from positive and negative examples, **Contrastive Chain-of-Thought (CoT) Prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/thought_generation/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Yew Ken Chia. (2023). Contrastive Chain-of-Thought Prompting. In arXiv preprint arXiv:1907.11692. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> , employs negative examples along with positive ones to enhance the reasoning capabilities of language models. Making the models aware of what mistakes to avoid via negative examples also makes them more accurate.

## How to Use Contrastive Chain-of-Thought (CoT) Prompting?

The prompt in the Contrastive CoT compromises of the following components:

1. Sample question or example question
2. Correct explanation question in 1
3. Incorrect explanation for question in 1
4. Actual question/query

The example below shows Contrastive Chain-of-Thought prompting in action.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Question : James writes a 3-page letter to 2 different friends twice a week. How many pages does he write a year?

Explanation: He writes each friend 3*2=6 pages a week. So he writes 6*2=12 pages every week. That means he writes 12\*52=624 pages a year.

Wrong Explanation: He writes each friend 12*52=624 pages a week. So he writes 3*2=6 pages every week. That means he writes 6\*2=12 pages a year.

Question: James has 30 teeth. His dentist drills 4 of them and caps 7 more teeth than he drills. What percentage of James' teeth does the dentist fix?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Explanation: The dentist drills 4 teeth, so there are 30 - 4 = 26 teeth left. The dentist caps 7 more teeth than he drills, so he caps 4 + 7 = 11 teeth. Therefore, the dentist fixes a total of 4 + 11 = 15 teeth. To find the percentage of teeth the dentist fixes, we divide the number of teeth fixed by the total number of teeth and multiply by 100: 15/30 × 100 = 50%

## How to Use an Automated Method to Generate Contrastive Examples?

The authors devise an automated method to generate contrastive examples in the paper. It involves the following steps:

1. Curate examples with correct reasoning steps from the existing dataset.
2. Within the example in step 1, use the entity recognition model to identify numbers, equations, or persons.
3. Shuffle the position of the entities extracted from step 2.

![contrastive Chain-of-Thought prompting](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fautomatic-contrastive-example.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Contrastive example generation<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/thought_generation/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Yew Ken Chia. (2023). Contrastive Chain-of-Thought Prompting. In arXiv preprint arXiv:1907.11692.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

The image below shows an instance where a contrastive example is generated using a positive example.

![Contrastive Chain-of-Thought prompting](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fcontrastive-examples.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

From positive example to contrastive example<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/thought_generation/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Yew Ken Chia. (2023). Contrastive Chain-of-Thought Prompting. In arXiv preprint arXiv:1907.11692.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

The example below shows Contrastive CoT in action. Feel free to modify it and test your inputs.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiSmFtZXMgd2VudCBzd2ltbWluZyBvbiBNb25kYXksIFdlZG5lc2RheSwgYW5kIFRodXJzZGF5LCBzbyBoZSB3ZW50IHN3aW1taW5nIGZvciBhIHRvdGFsIG9mIDMgZGF5cyB0aGlzIHdlZWsuIiwicHJvbXB0IjoiUXVlc3Rpb24gOiBKYW1lcyBoYXMgMTAgcmVkIGJhbGxzIGluIGhpcyBiYXNrZXQuIEFteSByZXBsYWNlcyA0IHJlZCBiYWxscyB3aXRoIDcgYmx1ZSBiYWxscy4gSG93IG1hbnkgYmFsbHMgZG9lcyBKYW1lcyBoYXZlIGluIGhpcyBiYXNrZXQ%2FXG5cbkV4cGxhbmF0aW9uOiBJbml0aWFsbHksIEphbWVzIGhhcyAxMCByZWQgYmFsbHMuIEFteSB0YWtlcyA0IG9mIHRob3NlLCBKYW1lcyBoYXMgMTAtNCA9IDYgcmVtYWluaW5nLiBUaGVuLCBzaGUgcHV0cyA3IGJsdWUgYmFsbHMsIEphbWVzIG5vdyBoYXMgNis3PSAxMyBiYWxscyBpbiB0b3RhbC5cblxuV3JvbmcgRXhwbGFuYXRpb246IEluaXRpYWxseSwgSmFtZXMgaGFzIDEwIHJlZCBiYWxscy4gQW15IHRha2VzIDQgb2YgdGhvc2UsIEphbWVzIGhhcyA2Kzc9IDEzIHJlbWFpbmluZy4gVGhlbiwgc2hlIHB1dHMgNyBibHVlIGJhbGxzLCBKYW1lcyBub3cgaGFzIDEwLTQgPSA2IGJhbGxzIGluIHRvdGFsLlxuXG5RdWVzdGlvbjogSmFtZXMgZ29lcyBmb3Igc3VtbWluZyB3aGVuZXZlciBpdCBpcyBzdW5ueSBvdXRzaWRlLiBUaGlzIHdlZWssIGl0IHdhcyBzdW5ueSBvbiBNb25kYXksIFdlZG5lc2RheSwgYW5kIFRodXJzZGF5LiBIb3cgbWFueSBkYXlzIGRpZCBKYW1lcyBnbyBzd2ltbWluZyB0aGlzIHdlZWs%2FIiwibW9kZWwiOiJncHQtMy41LXR1cmJvIn0%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

Tip

The code for [Contrastive Chain-of-Thought](https://learnprompting.org/vocabulary/contrastive_chain-of-thought) (CoT) Prompting is open-sourced and available for further research and implementation at [DAMO-NLP-SG/contrastive-cot](https://github.com/DAMO-NLP-SG/contrastive-cot).

## Conclusion

Learning from negative examples is not unique to humans and can also be replicated in language models. Embedding negative examples with the prompt can help language models learn from them and generate better explanations for their answers.