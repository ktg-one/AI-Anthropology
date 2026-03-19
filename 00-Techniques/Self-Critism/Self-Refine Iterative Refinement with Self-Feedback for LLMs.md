---
title: "Self-Refine: Iterative Refinement with Self-Feedback for LLMs"
source: https://learnprompting.org/docs/advanced/self_criticism/self_refine
author:
  - '[["Bhuwan Bhatt"]]'
published:
created: 2025-09-07
description: Learn how Self-Refine enables LLMs to iteratively enhance their outputs by using feedback, improving performance in tasks like code optimization and sentiment analysis.
tags:
  - clippings
feature: thumbnails/external/c7da2efad25ae32e9efec82fd1b79e5d.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on September 27, 2024

[Bhuwan Bhatt](https://learnprompting.org/docs/advanced/self_criticism/#Bhuwan%20Bhatt-bio)

![Self-Refine Prompting](https://learnprompting.org/docs/assets/advanced/advanced_covers/self_refine_cover.svg)

Takeaways

- **Refining through feedback**: Self-Refine enhances Large Language Model outputs by iteratively improving initial results based on model feedback.
- **Practical application**: It is a simple three-step process: generate output, get feedback, and refine the answer, repeating until the output is satisfactory.
- **Performance boost**: Self-Refine significantly improves performance on tasks such as code optimization and [sentiment](https://learnprompting.org/vocabulary/Sentiment_Analysis) analysis, especially for larger models.

## What is Self-Refine Prompting?

[Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) can solve a wide variety of tasks. Still, they can often fall short in addressing intricate requirements: tasks involving multiple different objectives or tasks involving hard-to-define goals. The initial output from the [LLM](https://learnprompting.org/vocabulary/LLM) in such cases involves some inaccuracies and false ideas.

When given a problem, humans come up with an initial draft and then refine iteratively to improve it based on self-provided feedback. For instance, when writing an email for a work colleague, you may first write a direct request such as "Send me the data ASAP". This may look like an okay email to send to friends, but with your work colleague, you may feel the need to be formal. Based on this self-provided feedback, you may re-phrase the email to: "Hi Ashley, could you please send me the data at your earliest convenience?"

Inspired by humans' ability to refine the solution, **Self-Refine prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Aman Madaan. (2023). Self-Refine: Iterative Refinement with Self-Feedback. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2303.17651" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2303.17651</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> aims to improve the initial outputs from LLMs through iterative feedback and refinement. It is a 3 step approach involving:

1. Initial output: Prompt the model to get the initial output.
2. Feedback: Pass the prompt and initial output back to the model to get the feedback.
3. Refinement: Pass the feedback back to the model to get the refined output.

It is an iterative process and continues till the model output meets the stopping criteria.

## How to Use Self-Refine Prompting?

**Step 1:** Prompt the model to get the output.  
Let's prompt the model to generate Python code to find the greatest number among three given numbers.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiZGVmIGZpbmRfZ3JlYXRlc3QobnVtMSwgbnVtMiwgbnVtMyk6XG4gICAgaWYgbnVtMSA%2BPSBudW0yIGFuZCBudW0xID49IG51bTM6XG4gICAgICAgIHJldHVybiBudW0xXG4gICAgZWxpZiBudW0yID49IG51bTEgYW5kIG51bTIgPj0gbnVtMzpcbiAgICAgICAgcmV0dXJuIG51bTJcbiAgICBlbHNlOlxuICAgICAgICByZXR1cm4gbnVtM1xuIiwicHJvbXB0IjoiR2VuZXJhdGUgYSBweXRob24gZnVuY3Rpb24gdGhhdCBmaW5kcyB0aGUgZ3JlYXRlc3QgYW1vbmcgMyBudW1iZXJzLiIsIm1vZGVsIjoiZ3B0LTMuNS10dXJibyJ9" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

**Step 2:** Get feedback Send the output back to the same model to get feedback. If the code cannot be improved anymore, ask the model to say so which is the stopping criteria.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiVGhlIGNvZGUgaXMgc2ltcGxlIGFuZCBlYXN5IHRvIHVuZGVyc3RhbmQuIEdvb2Qgam9iIG9uIHRoYXQhIFxuT25lIHdheSB0byBzbGlnaHRseSBpbXByb3ZlIGl0cyByZWFkYWJpbGl0eSBpcyBieSBhZGRpbmcgY29tbWVudHMgdG8gZXhwbGFpbiB3aGF0IHRoZSBjb2RlIGlzIGRvaW5nLiBcbkFub3RoZXIgaW1wcm92ZW1lbnQgY291bGQgYmUgdG8gdXBkYXRlIHRoZSBsYXN0IGBlbGlmYCBzdGF0ZW1lbnQgdG8gYGVsaWYgbnVtMyA%2BPSBudW0xIGFuZCBudW0zID49IG51bTI6YCBmb3IgY29uc2lzdGVuY3kuIiwicHJvbXB0IjoiSSB3aWxsIGdpdmUgeW91IGEgcHl0aG9uIGZ1bmN0aW9uLCB5b3VyIGpvYiBpcyB0byBnaXZlIGVhc3kgdG8gZm9sbG93IGZlZWRiYWNrcyBvbiBpbXByb3ZpbmcgaXRzIHJlYWRhYmlsaXR5LCBxdWFsaXR5LCBhbmQgcnVudGltZSBvZiB0aGUgY29kZS4gSWYgdGhlcmUgYXJlIG5vIGltcHJvdmVtZW50cyB0byBtYWtlLCBzYXkgc28uXG5IZXJlIGlzIHRoZSBjb2RlOlxuXG5cbmRlZiBmaW5kX2dyZWF0ZXN0KG51bTEsIG51bTIsIG51bTMpOlxuICAgIGlmIG51bTEgPj0gbnVtMiBhbmQgbnVtMSA%2BPSBudW0zOlxuICAgICAgICByZXR1cm4gbnVtMVxuICAgIGVsaWYgbnVtMiA%2BPSBudW0xIGFuZCBudW0yID49bnVtMzpcbiAgICAgICAgcmV0dXJuIG51bTJcbiAgICBlbHNlOlxuICAgICAgICByZXR1cm4gbnVtMyIsIm1vZGVsIjoiZ3B0LTMuNS10dXJibyJ9" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

**Step 3:** Implement feedback Prompt the LLM to use its feedback and improve the existing code.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiIyBJbXByb3ZlZCBjb2RlIHdpdGggY29tbWVudHMgYW5kIGNvbnNpc3RlbnQgY29tcGFyaXNvbiBpbiB0aGUgbGFzdCBlbGlmIHN0YXRlbWVudFxuZGVmIGZpbmRfZ3JlYXRlc3QobnVtMSwgbnVtMiwgbnVtMyk6XG4gICAgIyBDaGVjayBpZiBudW0xIGlzIHRoZSBncmVhdGVzdFxuICAgIGlmIG51bTEgPj0gbnVtMiBhbmQgbnVtMSA%2BPSBudW0zOlxuICAgICAgICByZXR1cm4gbnVtMVxuICAgICMgQ2hlY2sgaWYgbnVtMiBpcyB0aGUgZ3JlYXRlc3RcbiAgICBlbGlmIG51bTIgPj0gbnVtMSBhbmQgbnVtMiA%2BPSBudW0zOlxuICAgICAgICByZXR1cm4gbnVtMlxuICAgICMgSWYgbmVpdGhlciBudW0xIG5vciBudW0yIGlzIHRoZSBncmVhdGVzdCwgdGhlbiBudW0zIG11c3QgYmUgdGhlIGdyZWF0ZXN0XG4gICAgZWxpZiBudW0zID49IG51bTEgYW5kIG51bTMgPj0gbnVtMjpcbiAgICAgICAgcmV0dXJuIG51bTMiLCJwcm9tcHQiOiJCYXNlZCBvbiB0aGUgZmVlZGJhY2sgaW1wcm92ZSB0aGUgY29kZSBiZWxvdzpcbkhlcmUgaXMgdGhlIGNvZGU6XG5cblxuZGVmIGZpbmRfZ3JlYXRlc3QobnVtMSwgbnVtMiwgbnVtMyk6XG4gICAgaWYgbnVtMSA%2BPSBudW0yIGFuZCBudW0xID49IG51bTM6XG4gICAgICAgIHJldHVybiBudW0xXG4gICAgZWxpZiBudW0yID49IG51bTEgYW5kIG51bTIgPj1udW0zOlxuICAgICAgICByZXR1cm4gbnVtMlxuICAgIGVsc2U6XG4gICAgICAgIHJldHVybiBudW0zXG5cbkZlZWRiYWNrOlxuVGhlIGNvZGUgaXMgc2ltcGxlIGFuZCBlYXN5IHRvIHVuZGVyc3RhbmQuIEdvb2Qgam9iIG9uIHRoYXQhIFxuT25lIHdheSB0byBzbGlnaHRseSBpbXByb3ZlIGl0cyByZWFkYWJpbGl0eSBpcyBieSBhZGRpbmcgY29tbWVudHMgdG8gZXhwbGFpbiB3aGF0IHRoZSBjb2RlIGlzIGRvaW5nLiBcbkFub3RoZXIgaW1wcm92ZW1lbnQgY291bGQgYmUgdG8gdXBkYXRlIHRoZSBsYXN0IGBlbGlmYCBzdGF0ZW1lbnQgdG8gYGVsaWYgbnVtMyA%2BPSBudW0xIGFuZCBudW0zID49IG51bTI6YCBmb3IgY29uc2lzdGVuY3kuIiwibW9kZWwiOiJncHQtMy41LXR1cmJvIn0%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

**Step 4:** Ask for more feedback.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiVGhlIGNvZGUgaXMgZWFzeSB0byByZWFkIGFuZCB1bmRlcnN0YW5kLiBUaGVyZSBhcmUgbm8gbW9yZSBpbXByb3ZlbWVudHMgdG8gbWFrZS4iLCJwcm9tcHQiOiJJIHdpbGwgZ2l2ZSB5b3UgYSBweXRob24gZnVuY3Rpb24sIHlvdXIgam9iIGlzIHRvIGdpdmUgZWFzeSB0byBmb2xsb3cgZmVlZGJhY2tzIG9uIGltcHJvdmluZyBpdHMgcmVhZGFiaWxpdHksIHF1YWxpdHksIGFuZCBydW50aW1lIG9mIHRoZSBjb2RlLiBJZiB0aGVyZSBhcmUgbm8gaW1wcm92ZW1lbnRzIHRvIG1ha2UsIHNheSBzby5cbkhlcmUgaXMgdGhlIGNvZGU6XG5cbmRlZiBmaW5kX2dyZWF0ZXN0KG51bTEsIG51bTIsIG51bTMpOlxuICAgICMgQ2hlY2sgaWYgbnVtMSBpcyB0aGUgZ3JlYXRlc3RcbiAgICBpZiBudW0xID49IG51bTIgYW5kIG51bTEgPj0gbnVtMzpcbiAgICAgICAgcmV0dXJuIG51bTFcbiAgICAjIENoZWNrIGlmIG51bTIgaXMgdGhlIGdyZWF0ZXN0XG4gICAgZWxpZiBudW0yID49IG51bTEgYW5kIG51bTIgPj0gbnVtMzpcbiAgICAgICAgcmV0dXJuIG51bTJcbiAgICAjIElmIG5laXRoZXIgbnVtMSBub3IgbnVtMiBpcyB0aGUgZ3JlYXRlc3QsIHRoZW4gbnVtMyBtdXN0IGJlIHRoZSBncmVhdGVzdFxuICAgIGVsaWYgbnVtMyA%2BPSBudW0xIGFuZCBudW0zID49IG51bTI6XG4gICAgICAgIHJldHVybiBudW0zIiwibW9kZWwiOiJncHQtMy41LXR1cmJvIn0%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

Since no more improvements are necessary, we stop the iteration.

## What Are Self-Refine Prompting Results?

Employing Self-Refine boosts the model performance and outperforms the previous state-of-the-art across all tasks. Some notable results include:

- GPT-4's performance increases by 8.7 units for code optimization when augmented using Self-Refine.
- Self-Refine improves the performance in code readability by at least 13.9 units.
- Self-Refine improves the performance in sentiment reversal tasks by at least 21.6 units.

![](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fself_refine_results.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Self-Refine results on various tasks using the latest models from OpenAI<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Aman Madaan. (2023). Self-Refine: Iterative Refinement with Self-Feedback. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2303.17651" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2303.17651</a></span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

## Limitations of Self-Refine Prompting

While Self-Refine shows remarkable performance gain across a variety of tasks, there are a few limitations to this approach:

- The base model needs to be capable of following [instructions](https://learnprompting.org/docs/basics/instructions) provided by the users. So, primitive LMs may not be able to benefit from this approach.
- The results are based on tests performed using the dataset in English.
- Bad actors can use the technique to steer the model into generating toxic or harmful text.

## Conclusion

Self-refine enables LLMs to iteratively refine their own output without the need for labeled data, training, or a separate language model. The technique is simple and can be used across a wide variety of tasks including, but not limited to, code optimization, code readability, math reasoning, acronym generation, etc.