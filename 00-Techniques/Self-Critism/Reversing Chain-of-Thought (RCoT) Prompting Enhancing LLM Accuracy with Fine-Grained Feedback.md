---
title: "Reversing Chain-of-Thought (RCoT) Prompting: Enhancing LLM Accuracy with Fine-Grained Feedback"
source: https://learnprompting.org/docs/advanced/self_criticism/rcot
author:
  - '[["Bhuwan Bhatt"]]'
published:
created: 2025-09-07
description: Learn how Reversing Chain-of-Thought (RCoT) improves LLM performance by detecting inconsistencies, identifying hallucinations, and refining reasoning through feedback.
tags:
  - clippings
feature: thumbnails/external/f4366b1dc0619a8ff3684f8730325c9f.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 4 minutes

Last updated on September 27, 2024

[Bhuwan Bhatt](https://learnprompting.org/docs/advanced/self_criticism/#Bhuwan%20Bhatt-bio)

![Illustration of Reversing Chain-of-Thought](https://learnprompting.org/docs/assets/advanced/advanced_covers/reversing_cot_cover.svg)

Takeaways

- **Fine-grained feedback**: Reversing Chain-of-Thought (RCoT) detects and eliminates factual inconsistencies in [LLM](https://learnprompting.org/vocabulary/LLM) reasoning by using detailed feedback.
- **Condition checking**: RCoT identifies hallucinated or overlooked conditions through problem reconstruction and comparison.
- **Effective for complex tasks**: RCoT's performance is more impactful on challenging problems, improving accuracy significantly.

## What is Reversing Chain-of-Thought (RCoT) Prompting?

[Chain-of-Thought (CoT) Prompting](https://learnprompting.org/docs/intermediate/chain_of_thought)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Jason Wei. (2022). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> helps to improve the accuracy of [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) on arithmetic reasoning tasks by forcing the model to think step by step before answering the question. However, LLMs still struggle to maintain factual consistency during reasoning and seem to overlook conditions, misinterpret the original questions, and may hallucinate. This is especially true when the original question contains multiple conditions. The example below shows an instance where ChatGPT overlooks the condition that the provided date in the question is tomorrow's date.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Today's meeting is rescheduled to 11 am tomorrow, 10/16/1924. What is the date one year ago from today?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

The current date is 10/16/1924. To find the date one year ago from today, you would subtract one year from the current year, which would be 1923. The correct answer is 10/16/1923. ❌

**Reversing Chain-of-Thought (RCoT) prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Tianci Xue. (2023). RCOT: Detecting and Rectifying Factual Inconsistency in Reasoning by Reversing Chain-of-Thought. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> aims to enhance LLMs' reasoning abilities by detecting and rectifying condition [hallucinations](https://learnprompting.org/vocabulary/hallucination). RCoT employs a 3 step process to detect and rectify hallucinations:

1. RCoT uses the original incorrect solution to construct a new problem (say Q').
2. RCoT conducts a fine-grained comparison between the original problem (Q) and reconstructed problem (Q') and detects hallucinations, overlookings, and question misinterpretation.
3. RCoT provides the detected shortcomings to the LLM in the form of feedback and guides it to the correct output.

## How to Use Reversing Chain-of-Thought?

Let's use RCoT to solve a math word problem. The dialog below shows the question and initial LLM response:

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiVG8gY2FsY3VsYXRlIGhvdyBtYW55IHN0YWNrcyBMYW5hIGNvdWxkIG1ha2Ugd2l0aCA3MiBleHRyYSBuaWNrZWxzLCB3ZSBuZWVkIHRvIGRpdmlkZSB0aGUgdG90YWwgbnVtYmVyIG9mIG5pY2tlbHMgYnkgdGhlIG51bWJlciBvZiBuaWNrZWxzIGluIGVhY2ggc3RhY2suIFNpbmNlIHRoZXJlIGFyZSA1IG5pY2tlbHMgaW4gZWFjaCBzdGFjaywgNzIgZXh0cmEgbmlja2VscyBpcyBlcXVhbCB0byA3Mi81ID0gMTQuNCBzdGFja3MuIEhvd2V2ZXIsIExhbmEgY2Fubm90IGhhdmUgYSBmcmFjdGlvbiBvZiBhIHN0YWNrLCBzbyB3ZSBuZWVkIHRvIHJvdW5kIGRvd24gdG8gdGhlIG5lYXJlc3Qgd2hvbGUgbnVtYmVyLiBUaGVyZWZvcmUsIExhbmEgY291bGQgbWFrZSAxNCBzdGFja3Mgd2l0aCB0aGUgNzIgZXh0cmEgbmlja2Vscy4gVGhlcmVmb3JlLCB0aGUgZmluYWwgYW5zd2VyIGlzIDE0LiIsInByb21wdCI6IlF1ZXN0aW9uczogTGFuYSBoYWQgNzIgZXh0cmEgbmlja2Vscy4gSWYgc2hlIHB1dCB0aGVtIGludG8gc3RhY2tzIHdpdGggOCBpbiBlYWNoIHN0YWNrLCBob3cgbWFueSBzdGFja3MgY291bGQgc2hlIG1ha2U%2FXG5cbkFuc3dlcjogTGV0J3MgdGhpbmsgc3RlcCBieSBzdGVwLiIsIm1vZGVsIjoiZ3B0LTQifQ%3D%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

**Step 1:** Problem Reconstruction  
Reconstruct the problem by providing the question and initial response to the LLM.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiUXVlc3Rpb246IExhbmEgZm91bmQgYSBqYXIgY29udGFpbmluZyA3MiBuaWNrZWxzLiBTaGUgZGVjaWRlZCB0byBzdGFjayB0aGVtIHdpdGggZWFjaCBzdGFjayBjb250YWluaW5nIDUgbmlja2Vscy4gSG93IG1hbnkgZnVsbCBzdGFja3Mgb2Ygbmlja2VscyBjb3VsZCBzaGUgbWFrZT8iLCJwcm9tcHQiOiJHaXZlIHRoZSBjb25jcmV0ZSBwcm9tcHQgKHByb2JsZW0pIHRoYXQgY2FuIGdlbmVyYXRlIHRoaXMgYW5zd2VyLiBUaGUgcHJvYmxlbSBzaG91bGQgY29udGFpbiBhbGwgYmFzaWMgYW5kIG5lY2Vzc2FyeSBpbmZvcm1hdGlvbiBhbmQgY29ycmVzcG9uZCB0byB0aGUgYW5zd2VyLiBUaGUgcHJvYmxlbSBjYW4gb25seSBhc2sgZm9yIG9uZSByZXN1bHQuXG5RdWVzdGlvbjogTGFuYSBoYWQgNzIgZXh0cmEgbmlja2Vscy4gSWYgc2hlIHB1dCB0aGVtIGludG8gc3RhY2tzIHdpdGggOCBpbiBlYWNoIHN0YWNrLCBob3cgbWFueSBzdGFja3MgY291bGQgc2hlIG1ha2U%2FXG5cbkFuc3dlcjogTGV0J3MgdGhpbmsgc3RlcCBieSBzdGVwLiBUbyBjYWxjdWxhdGUgaG93IG1hbnkgc3RhY2tzIExhbmEgY291bGQgbWFrZSB3aXRoIDcyIGV4dHJhIG5pY2tlbHMsIHdlIG5lZWQgdG8gZGl2aWRlIHRoZSB0b3RhbCBudW1iZXIgb2Ygbmlja2VscyBieSB0aGUgbnVtYmVyIG9mIG5pY2tlbHMgaW4gZWFjaCBzdGFjay4gU2luY2UgdGhlcmUgYXJlIDUgbmlja2VscyBpbiBlYWNoIHN0YWNrLCA3MiBleHRyYSBuaWNrZWxzIGlzIGVxdWFsIHRvIDcyLzUgPSAxNC40IHN0YWNrcy4gSG93ZXZlciwgTGFuYSBjYW5ub3QgaGF2ZSBhIGZyYWN0aW9uIG9mIGEgc3RhY2ssIHNvIHdlIG5lZWQgdG8gcm91bmQgZG93biB0byB0aGUgbmVhcmVzdCB3aG9sZSBudW1iZXIuIFRoZXJlZm9yZSwgTGFuYSBjb3VsZCBtYWtlIDE0IHN0YWNrcyB3aXRoIHRoZSA3MiBleHRyYSBuaWNrZWxzLiBUaGVyZWZvcmUsIHRoZSBmaW5hbCBhbnN3ZXIgaXMgMTQuIiwibW9kZWwiOiJncHQtNCJ9" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

As you can see, the reconstructed problem has different facts than the ones stated in the original problem:

**Step 2 (i):** Problem Decomposition  
Now, let's decompose both problems into a list of conditions and facts stated in the problem.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiT3JpZ2luYWwgUHJvYmxlbSBDb25kaXRpb25zOlxuMS4gTGFuYSBoYXMgNzIgZXh0cmEgbmlja2Vscy5cbjIuIFNoZSBzdGFja3MgdGhlIG5pY2tlbHMgd2l0aCA4IGluIGVhY2ggc3RhY2suXG5cblJlY29uc3RydWN0ZWQgUHJvYmxlbSBDb25kaXRpb25zOlxuMS4gTGFuYSBmb3VuZCBhIGphciBjb250YWluaW5nIDcyIG5pY2tlbHMuXG4yLiBTaGUgc3RhY2tzIHRoZSBuaWNrZWxzIHdpdGggNSBpbiBlYWNoIHN0YWNrLiIsInByb21wdCI6IlBsZWFzZSBsaXN0IHRoZSBjb25kaXRpb25zIG9mIHRoZSBvcmlnaW5hbCBwcm9ibGVtIGFuZCByZWNvbnN0cnVjdGVkIHByb2JsZW0uIFRoZXJlIG1heSBiZSBtdWx0aXBsZSBjb25kaXRpb25zLlxuT3JpZ2luYWwgUHJvYmxlbTpcbkxhbmEgaGFkIDcyIGV4dHJhIG5pY2tlbHMuIElmIHNoZSBwdXQgdGhlbSBpbnRvIHN0YWNrcyB3aXRoIDggaW4gZWFjaCBzdGFjaywgaG93IG1hbnkgc3RhY2tzIGNvdWxkIHNoZSBtYWtlP1xuXG5SZWNvbnN0cmN0ZWQgUHJvYmxlbTpcbkxhbmEgZm91bmQgYSBqYXIgY29udGFpbmluZyA3MiBuaWNrZWxzLiBTaGUgZGVjaWRlZCB0byBzdGFjayB0aGVtIHdpdGggZWFjaCBzdGFjayBjb250YWluaW5nIDUgbmlja2Vscy4gSG93IG1hbnkgZnVsbCBzdGFja3Mgb2Ygbmlja2VscyBjb3VsZCBzaGUgbWFrZT8iLCJtb2RlbCI6ImdwdC0zLjUtdHVyYm8ifQ%3D%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

**Step 2 (ii):** Condition Comparison  
Detect hallucinated and overlooked conditions from the condition list.

- overlooked condition:
<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiTm8sIHRoZSBjYW5kaWRhdGUgY29uZGl0aW9uIGNhbm5vdCBiZSBkZWR1Y2VkIGZyb20gdGhlIGNvbmRpdGlvbiBsaXN0LiBUaGUgY29uZGl0aW9uIGxpc3Qgc3BlY2lmaWVzIHRoYXQgTGFuYSBzdGFja3MgdGhlIG5pY2tlbHMgd2l0aCA1IGluIGVhY2ggc3RhY2ssIHdoaWNoIGNvbnRyYWRpY3RzIHRoZSBjYW5kaWRhdGUgY29uZGl0aW9uIHRoYXQgc3VnZ2VzdHMgc2hlIHN0YWNrcyB0aGUgbmlja2VscyB3aXRoIDggaW4gZWFjaCBzdGFjay4gVGhlc2UgYXJlIHR3byBzZXBhcmF0ZSBzY2VuYXJpb3MgYW5kIG9uZSBjYW5ub3QgYmUgaW5mZXJyZWQgZnJvbSB0aGUgb3RoZXIuIiwicHJvbXB0IjoiR2l2ZW4gYSBjYW5kaWRhdGUgY29uZGl0aW9uOiBcIlNoZSBzdGFja3MgdGhlIG5pY2tlbHMgd2l0aCA4IGluIGVhY2ggc3RhY2suXCJcbkhlcmUgaXMgYSBjb25kaXRpb24gbGlzdDpcIjEuIExhbmEgZm91bmQgYSBqYXIgY29udGFpbmluZyA3MiBuaWNrZWxzLiAyLiBTaGUgc3RhY2tzIHRoZSBuaWNrZWxzIHdpdGggNSBpbiBlYWNoIHN0YWNrLlwiXG5Gcm9tIGEgbWF0aGVtYXRpY2FsIHBvaW50IG9mIHZpZXcsIGNhbiB0aGlzIGNhbmRpZGF0ZSBjb25kaXRpb24gYmUgZGVkdWNlZCBmcm9tIHRoZSBjb25kaXRpb24gbGlzdD8gUGxlYXNlIGlsbHVzdHJhdGUgeW91ciByZWFzb24gYW5kIGFuc3dlciBcInllc1wiIG9yIFwibm9cIi4iLCJtb2RlbCI6ImdwdC0zLjUtdHVyYm8ifQ%3D%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>
- hallucinated condition
<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiTm8sIHRoaXMgY2FuZGlkYXRlIGNvbmRpdGlvbiBjYW5ub3QgYmUgZGVkdWNlZCBmcm9tIHRoZSBjb25kaXRpb24gbGlzdC4gVGhlIGNvbmRpdGlvbiBsaXN0IHNwZWNpZmllcyB0aGF0IHNoZSBzdGFja3MgdGhlIG5pY2tlbHMgd2l0aCA4IGluIGVhY2ggc3RhY2ssIHdoaWNoIGlzIGRpZmZlcmVudCBmcm9tIHRoZSBjYW5kaWRhdGUgY29uZGl0aW9uIHRoYXQgc3VnZ2VzdHMgc2hlIHdhbnRzIHRvIHN0YWNrIHRoZW0gaW4gcGlsZXMgb2YgNS4gVGhlc2UgYXJlIHR3byBkaWZmZXJlbnQsIHVucmVsYXRlZCBjb25kaXRpb25zLiIsInByb21wdCI6IkdpdmVuIGEgY2FuZGlkYXRlIGNvbmRpdGlvbjogXCJTaGUgc3RhY2tzIHRoZSBuaWNrZWxzIHdpdGggNSBpbiBlYWNoIHN0YWNrLlwiXG5IZXJlIGlzIGEgY29uZGl0aW9uIGxpc3Q6XCIxOiBMYW5hIGhhZCA3MiBleHRyYSBuaWNrZWxzLiAyLiBTaGUgc3RhY2tzIHRoZSBuaWNrZWxzIHdpdGggOCBpbiBlYWNoIHN0YWNrLlwiXG5Gcm9tIGEgbWF0aGVtYXRpY2FsIHBvaW50IG9mIHZpZXcsIGNhbiB0aGlzIGNhbmRpZGF0ZSBjb25kaXRpb24gYmUgZGVkdWNlZCBmcm9tIHRoZSBjb25kaXRpb24gbGlzdD8gUGxlYXNlIGlsbHVzdHJhdGUgeW91ciByZWFzb24gYW5kIGFuc3dlciBcInllc1wiIG9yIFwibm9cIi4iLCJtb2RlbCI6ImdwdC0zLjUtdHVyYm8ifQ%3D%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

**Step 2 (iii):** Question comparison  
Compare the questions to check if the LLM can detect the difference in facts within the questions.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiTm8sIHRoZXNlIHByb2JsZW1zIGFyZSBub3QgYXNraW5nIHRoZSBzYW1lIHRoaW5nIGluIHRoZSBlbmQuIFxuXG5JbiB0aGUgZmlyc3QgcHJvYmxlbSwgTGFuYSBpcyBzdGFja2luZyBoZXIgNzIgbmlja2VscyBpbnRvIHN0YWNrcyBvZiA4LiBUaGlzIHJlcXVpcmVzIHVzIHRvIGRpdmlkZSA3MiBieSA4IHRvIGZpbmQgdGhlIG51bWJlciBvZiBzdGFja3MsIHdoaWNoIGlzIDkgc3RhY2tzLiBcblxuSW4gY29udHJhc3QsIHRoZSBzZWNvbmQgcHJvYmxlbSBhc2tzIGhvdyBtYW55IHN0YWNrcyBMYW5hIGNvdWxkIG1ha2UgaWYgc2hlIHN0YWNrcyBoZXIgNzIgbmlja2VscyBpbnRvIHN0YWNrcyBvZiA1LiBXZSBuZWVkIHRvIGRpdmlkZSA3MiBieSA1IGluIHRoaXMgY2FzZSwgcmVzdWx0aW5nIGluIDE0IGZ1bGwgc3RhY2tzIGFuZCAyIG5pY2tlbHMgbGVmdCBvdmVyLiBcblxuVGhlcmVmb3JlLCB0aGUgdHdvIHByb2JsZW1zIGFyZSBhc2tpbmcgZm9yIGRpZmZlcmVudCByZXN1bHRzIGJlY2F1c2UgdGhlIG51bWJlciBvZiBuaWNrZWxzIGluIGVhY2ggc3RhY2sgaXMgZGlmZmVyZW50LiIsInByb21wdCI6IlExOiBMYW5hIGhhZCA3MiBleHRyYSBuaWNrZWxzLiBJZiBzaGUgcHV0IHRoZW0gaW50byBzdGFja3Mgd2l0aCA4IGluIGVhY2ggc3RhY2ssIGhvdyBtYW55IHN0YWNrcyBjb3VsZCBzaGUgbWFrZT9cblEyOiBMYW5hIGZvdW5kIGEgamFyIGNvbnRhaW5pbmcgNzIgbmlja2Vscy4gU2hlIGRlY2lkZWQgdG8gc3RhY2sgdGhlbSB3aXRoIGVhY2ggc3RhY2sgY29udGFpbmluZyA1IG5pY2tlbHMuIEhvdyBtYW55IGZ1bGwgc3RhY2tzIG9mIG5pY2tlbHMgY291bGQgc2hlIG1ha2U%2FXG5JbnN0cnVjdGlvbjogRnJvbSBhIG1hdGhlbWF0aWNhbCBwb2ludCBvZiB2aWV3LCBhcmUgdGhlc2UgcHJvYmxlbXMgYXNraW5nIHRoZSBzYW1lIHRoaW5nIGluIHRoZSBlbmQ%2FIFBsZWFzZSBpbGx1c3RyYXRlIHlvdXIgcmVhc29uIGFuZCBhbnN3ZXIgXCJ5ZXNcIiBvciBcIm5vXCIuIiwibW9kZWwiOiJncHQtMy41LXR1cmJvIn0%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

**Step 3:** Fine-grained feedback and revision  
Collect all factual inconsistencies, provide feedback to the LLM, and instruct it to revise its solution.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiVG8gc29sdmUgdGhpcyBwcm9ibGVtLCBMYW5hIG5lZWRzIHRvIGRpdmlkZSB0aGUgdG90YWwgbnVtYmVyIG9mIG5pY2tlbHMgYnkgdGhlIG51bWJlciBvZiBuaWNrZWxzIGluIGVhY2ggc3RhY2suIFNvLCA3MiBuaWNrZWxzIGRpdmlkZWQgYnkgOCBuaWNrZWxzIHBlciBzdGFjayBlcXVhbHMgOSBzdGFja3MuIFRoZXJlZm9yZSwgTGFuYSBjb3VsZCBtYWtlIDkgc3RhY2tzIHdpdGggaGVyIGV4dHJhIG5pY2tlbHMuIiwicHJvbXB0IjoiUXVlc3Rpb246IExhbmEgaGFkIDcyIGV4dHJhIG5pY2tlbHMuIElmIHNoZSBwdXQgdGhlbSBpbnRvIHN0YWNrcyB3aXRoIDggaW4gZWFjaCBzdGFjaywgaG93IG1hbnkgc3RhY2tzIGNvdWxkIHNoZSBtYWtlP1xuXG5JbnN0cnVjdGlvbjogIFxuSGVyZSBhcmUgdGhlIG1pc3Rha2VzIGFuZCByZWFzb25zIGluIHlvdXIgYW5zd2VyIHRvIHRoZSBwcm9ibGVtLiAgXG5Zb3UgaGF2ZSBpZ25vcmVkIHNvbWUgcmVhbCBjb25kaXRpb25zOlxuMTogU2hlIHN0YWNrcyB0aGUgbmlja2VscyB3aXRoIDggaW4gZWFjaCBzdGFjay5cbllvdSBzaG91bGQgY29uc2lkZXIgYWxsIHJlYWwgY29uZGl0aW9ucyBpbiB0aGUgcHJvYmxlbS5cbkhlcmUgYXJlIGRldGFpbGVkIHJlYXNvbnM6XG5ObywgdGhlIGNhbmRpZGF0ZSBjb25kaXRpb24gY2Fubm90IGJlIGRlZHVjZWQgZnJvbSB0aGUgY29uZGl0aW9uIGxpc3QuIFRoZSBjb25kaXRpb24gbGlzdCBzcGVjaWZpZXMgdGhhdCBMYW5hIHN0YWNrcyB0aGUgbmlja2VscyB3aXRoIDUgaW4gZWFjaCBzdGFjaywgd2hpY2ggY29udHJhZGljdHMgdGhlIGNhbmRpZGF0ZSBjb25kaXRpb24gdGhhdCBzdWdnZXN0cyBzaGUgc3RhY2tzIHRoZSBuaWNrZWxzIHdpdGggOCBpbiBlYWNoIHN0YWNrLiBUaGVzZSBhcmUgdHdvIHNlcGFyYXRlIHNjZW5hcmlvcyBhbmQgb25lIGNhbm5vdCBiZSBpbmZlcnJlZCBmcm9tIHRoZSBvdGhlci5cblxuWW91IHVzZSBzb21lIHdyb25nIGNhbmRpZGF0ZSBjb25kaXRpb25zOlxuMTogU2hlIHN0YWNrcyB0aGUgbmlja2VscyB3aXRoIDUgaW4gZWFjaCBzdGFjay5cblRoZXkgYWxsIGNhbiBub3QgYmUgZGVkdWNlZCBmcm9tIHRoZSB0cnVlIGNvbmRpdGlvbiBsaXN0LlxuWW91IHNob3VsZCBjb25zaWRlciBhbGwgcmVhbCBjb25kaXRpb25zIGluIHRoZSBwcm9ibGVtLlxuSGVyZSBhcmUgZGV0YWlsZWQgcmVhc29uczpcblRoZSBjb25kaXRpb24gbGlzdCBzcGVjaWZpZXMgdGhhdCBzaGUgc3RhY2tzIHRoZSBuaWNrZWxzIHdpdGggOCBpbiBlYWNoIHN0YWNrLCB3aGljaCBpcyBkaWZmZXJlbnQgZnJvbSB0aGUgY2FuZGlkYXRlIGNvbmRpdGlvbiB0aGF0IHN1Z2dlc3RzIHNoZSB3YW50cyB0byBzdGFjayB0aGVtIGluIHBpbGVzIG9mIDUuIFRoZXNlIGFyZSB0d28gZGlmZmVyZW50LCB1bnJlbGF0ZWQgY29uZGl0aW9ucy5cblxuUmV2aXNlZCBTb2x1dGlvbjoiLCJtb2RlbCI6ImdwdC00In0%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

## What Are Reversing Chain-of-Thought Results?

- RCoT consistently outperforms standard CoT and the double-check (asks LLMs to check their answers but does not point out whether the answer is correct) methods in the Zero-Shot setting.

![Zero-Shot results](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Frcot_zero_shot_results.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

RCoT Zero-Shot results<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Tianci Xue. (2023). RCOT: Detecting and Rectifying Factual Inconsistency in Reasoning by Reversing Chain-of-Thought.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

- The performance gain after employing RCoT is greater in challenging tasks than in easier tasks. For instance, ChatGPT's performance improves by 4.1% on AQuA and by 5.0% on the Date dataset. AQuA dataset contains diverse problems, and the Date dataset requires multi-hop reasoning and common sense date knowledge, making them complex compared to other datasets.
- On simpler datasets like the SVAMP dataset, which contains problems that usually only need one-step calculation, the performance improves but is less apparent. ChatGPT's performance improves by 2.8% in the SVAMP dataset.
- The result of employing RCoT with a Few-Shot setting is similar to the result obtained after employing RCoT using a Zero-Shot setting.
- RCoT can effectively detect overlooking and misinterpretation errors but struggles to detect hallucination errors.

![RCoT's effectiveness in detecting errors](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Frcot_error_detection_ability.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

RCoT's effectiveness in detecting errors.<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Tianci Xue. (2023). RCOT: Detecting and Rectifying Factual Inconsistency in Reasoning by Reversing Chain-of-Thought.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

## Limitations of Reversing Chain-of-Thought

Some limitations of RCoT include:

- RCoT cannot detect all possible reasoning errors. For instance, RCoT struggles to detect computational errors.
- There is a significant difference between RCoT-generated feedback and human-generated feedback.
- RCoT involves multiple conversations with the LLM. This may consume additional resources (hardware, money, etc) and can also slow down the inference speed.

## Conclusion

RCoT improves the reasoning abilities of LLMs by enabling them to detect and rectify factual inconsistencies in their generated solution. RCoT detects factual inconsistencies by fine-grained comparison between the original question and the reconstructed question using the original incorrect answer. It then reports the detected inconsistencies to the LLM through fine-grained feedback and guides the LLM to the correct solution.