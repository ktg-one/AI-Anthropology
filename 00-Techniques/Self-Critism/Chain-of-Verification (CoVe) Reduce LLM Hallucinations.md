---
title: "Chain-of-Verification (CoVe): Reduce LLM Hallucinations"
source: https://learnprompting.org/docs/advanced/self_criticism/chain_of_verification
author:
  - '[["Bhuwan Bhatt"]]'
published:
created: 2025-09-07
description: Discover how Chain-of-Verification (CoVe) reduces hallucinations in LLMs by verifying facts step-by-step, improving accuracy over Zero-Shot and CoT methods.
tags:
  - clippings
feature: thumbnails/external/0b2e0ccf30bf6a26be9563929ad2e761.svg
---
🟢 This article is rated [easy](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 4 minutes

Last updated on September 27, 2024

[Bhuwan Bhatt](https://learnprompting.org/docs/advanced/self_criticism/#Bhuwan%20Bhatt-bio)

![CoVe illustration](https://learnprompting.org/docs/assets/advanced/advanced_covers/cove_cover.svg)

Takeaways

- **Reduces hallucinations**: CoVe minimizes factual errors in [Large Language Models' (LLMs)](https://learnprompting.org/vocabulary/LLM) responses by using verification questions.
- **Improved accuracy**: CoVe outperforms Zero-Shot, Few-Shot, and Chain-of-Thought (CoT) methods in generating accurate responses.
- **Four-step process**: It involves baseline response, verification planning, answering verification questions, and refining the final output.
- **Limitations**: CoVe reduces but doesn't fully eliminate hallucinations, especially in reasoning steps.

## What is CoVe Prompting?

Often, [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) generate responses that look plausible but are incorrect. This is referred to as [hallucination](https://learnprompting.org/vocabulary/hallucination) in [LLM](https://learnprompting.org/vocabulary/LLM) and is an unresolved issue. [Hallucinations](https://learnprompting.org/vocabulary/hallucination) are more apparent for lesser-known facts or facts that appear less frequently in the training corpus and when generating long-form texts (multiple sentences and paragraphs). For reasoning tasks, [Chain-of-Thought (CoT)](https://learnprompting.org/docs/intermediate/chain_of_thought)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Jason Wei. (2022). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> improves the quality of response by encouraging the model to generate its thoughts before producing the final response. **Chain-of-Verification (CoVe)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Shehzaad Dhuliawala. (2023). Chain-of-Verification Reduces Hallucination in Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2309.11495" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2309.11495</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> follows a similar approach and uses verification questions to improve the quality of response.

Chain-of-Verification (CoVe) prompting is a self-critique technique that improves upon the initial response from the LLM by first planning the verification questions to check its work and then systematically answering those questions to produce a refined response. The answers to these verification questions are usually short and easy compared to the initial answer. The initial answer is improved by providing verification questions and answers to the LLM as feedback.

Here is an example employing CoVe to refine the original answer:

- Query

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Name some politicians who were born in NY, New York.

- Baseline Response

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Here are some politicians who were born in NY, New York: Hillary Clinton - former secretary of state and former Democratic presidential nominee Donald Trump - former president of the United States Michael Bloomberg - former Mayor of New York City and former Democratic presidential candidate ...

- Plan verifications

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Where was Hillary Clinton born? Where was Donald Trump born? Where was Michael Bloomberg born? ...

- Execute verifications

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Hillary Clinton was born in Chicago, Illinois, United States on October 26, 1947. Donald Trump was born on June 14, 1946, in Queens, New York City, New York, United States Michael Bloomberg was born on February 14, 1942, in Boston, Massachusetts, United States. ...

- Final verified response

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Here are some politicians who were born in NY, New York: Donald Trump - former president of the United States Alexandria Ocasio-Cortez - Democratic member of the U.S. House of Representatives ...

As seen in the example above, the individual verification questions are answered more accurately than in the original long-form answer.

## How to Use CoVe Prompting?

Answer generation using CoVe is a 4-step process:

1. Baseline response generation  
	In this step, you prompt the model to generate a draft of the answer. The answer may not be factually correct.
2. Planning verifications  
	In this step, you generate a list of verification questions using the query and initial response.
3. Verification execution  
	This step prompts the LLM to generate a response for each of the verification questions.
4. Final response generation  
	In this step, you incorporate the answer from the previous step and generate a final response.

Let's go through an example to understand the process better.

Let's say we want to find the names of politicians born in New York City (NYC).

**Step 1:** Baseline response generation  
Prompt the model to get the list of politicians born in NYC.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiMS4gTWljaGFlbCBCbG9vbWJlcmdcbjIuIERvbmFsZCBUcnVtcFxuMy4gRnJhbmtsaW4gRC4gUm9vc2V2ZWx0XG40LiBSdWR5IEdpdWxpYW5pXG41LiBUaGVvZG9yZSBSb29zZXZlbHRcbjYuIEVkIEtvY2hcbjcuIEtpcnN0ZW4gR2lsbGlicmFuZFxuOC4gQ2h1Y2sgU2NodW1lclxuOS4gQmlsbCBkZSBCbGFzaW9cbjEwLiBKb2huIExpbmRzYXkiLCJwcm9tcHQiOiJMaXN0IGFsbCBwb2xpdGljaWFucyBib3JuIGluIE5ZQy4iLCJtb2RlbCI6ImdwdC0zLjUtdHVyYm8ifQ%3D%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

**Step 2:** Planning verifications  
Generate a list of verification questions to verify the model's answer.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiV2FzIE1pY2hhZWwgQmxvb21iZXJnIGJvcm4gaW4gTmV3IFlvcmsgQ2l0eT9cbldhcyBEb25hbGQgVHJ1bXAgYm9ybiBpbiBOZXcgWW9yayBDaXR5P1xuV2FzIEZyYW5rbGluIEQuIFJvb3NldmVsdCBib3JuIGluIE5ldyBZb3JrIENpdHk%2FXG5XYXMgUnVkeSBHaXVsaWFuaSBib3JuIGluIE5ldyBZb3JrIENpdHk%2FXG5XYXMgVGhlb2RvcmUgUm9vc2V2ZWx0IGJvcm4gaW4gTmV3IFlvcmsgQ2l0eT9cbldhcyBFZCBLb2NoIGJvcm4gaW4gTmV3IFlvcmsgQ2l0eT9cbldhcyBLaXJzdGVuIEdpbGxpYnJhbmQgYm9ybiBpbiBOZXcgWW9yayBDaXR5P1xuV2FzIENodWNrIFNjaHVtZXIgYm9ybiBpbiBOZXcgWW9yayBDaXR5P1xuV2FzIEJpbGwgZGUgQmxhc2lvIGJvcm4gaW4gTmV3IFlvcmsgQ2l0eT9cbldhcyBKb2huIExpbmRzYXkgYm9ybiBpbiBOZXcgWW9yayBDaXR5PyIsInByb21wdCI6Ikxpc3QgYWxsIHBvbGl0aWNpYW5zIGJvcm4gaW4gTllDLlxuMS4gTWljaGFlbCBCbG9vbWJlcmdcbjIuIERvbmFsZCBUcnVtcFxuMy4gRnJhbmtsaW4gRC4gUm9vc2V2ZWx0XG40LiBSdWR5IEdpdWxpYW5pXG41LiBUaGVvZG9yZSBSb29zZXZlbHRcbjYuIEVkIEtvY2hcbjcuIEtpcnN0ZW4gR2lsbGlicmFuZFxuOC4gQ2h1Y2sgU2NodW1lclxuOS4gQmlsbCBkZSBCbGFzaW9cbjEwLiBKb2huIExpbmRzYXlcblxuR2VuZXJhdGUgc2hvcnQgdmVyaWZpY2F0aW9uIHF1ZXN0aW9uIHRvIHZlcmlmeSB3aGV0aGVyIGVhY2ggcG9saXRpY2lhbiB3YXMgYm9ybiBpbiBOWUMgb3Igbm90LiIsIm1vZGVsIjoiZ3B0LTMuNS10dXJibyJ9" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

**Step 3:** Verification execution  
Get answers for each of the verification questions.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiV2FzIE1pY2hhZWwgQmxvb21iZXJnIGJvcm4gaW4gTmV3IFlvcmsgQ2l0eT8gTm8uXG5XYXMgRG9uYWxkIFRydW1wIGJvcm4gaW4gTmV3IFlvcmsgQ2l0eT8gWWVzLlxuV2FzIEZyYW5rbGluIEQuIFJvb3NldmVsdCBib3JuIGluIE5ldyBZb3JrIENpdHk%2FIE5vLlxuV2FzIFJ1ZHkgR2l1bGlhbmkgYm9ybiBpbiBOZXcgWW9yayBDaXR5PyBZZXMuXG5XYXMgVGhlb2RvcmUgUm9vc2V2ZWx0IGJvcm4gaW4gTmV3IFlvcmsgQ2l0eT8gTm8uXG5XYXMgRWQgS29jaCBib3JuIGluIE5ldyBZb3JrIENpdHk%2FIE5vLlxuV2FzIEtpcnN0ZW4gR2lsbGlicmFuZCBib3JuIGluIE5ldyBZb3JrIENpdHk%2FIE5vLlxuV2FzIENodWNrIFNjaHVtZXIgYm9ybiBpbiBOZXcgWW9yayBDaXR5PyBZZXMuXG5XYXMgQmlsbCBkZSBCbGFzaW8gYm9ybiBpbiBOZXcgWW9yayBDaXR5PyBOby5cbldhcyBKb2huIExpbmRzYXkgYm9ybiBpbiBOZXcgWW9yayBDaXR5PyBZZXMuIiwicHJvbXB0IjoiQW5zd2VyIGVhY2ggb2YgdGhlIGZvbGxvd2luZyAoYW5zd2VyIGltbWVkaWF0ZWx5IGFmdGVyIHRoZSBxdWVzdGlvbiBtYXJrKSA6ICAgXG5XYXMgTWljaGFlbCBCbG9vbWJlcmcgYm9ybiBpbiBOZXcgWW9yayBDaXR5P1xuV2FzIERvbmFsZCBUcnVtcCBib3JuIGluIE5ldyBZb3JrIENpdHk%2FXG5XYXMgRnJhbmtsaW4gRC4gUm9vc2V2ZWx0IGJvcm4gaW4gTmV3IFlvcmsgQ2l0eT9cbldhcyBSdWR5IEdpdWxpYW5pIGJvcm4gaW4gTmV3IFlvcmsgQ2l0eT9cbldhcyBUaGVvZG9yZSBSb29zZXZlbHQgYm9ybiBpbiBOZXcgWW9yayBDaXR5P1xuV2FzIEVkIEtvY2ggYm9ybiBpbiBOZXcgWW9yayBDaXR5P1xuV2FzIEtpcnN0ZW4gR2lsbGlicmFuZCBib3JuIGluIE5ldyBZb3JrIENpdHk%2FXG5XYXMgQ2h1Y2sgU2NodW1lciBib3JuIGluIE5ldyBZb3JrIENpdHk%2FXG5XYXMgQmlsbCBkZSBCbGFzaW8gYm9ybiBpbiBOZXcgWW9yayBDaXR5P1xuV2FzIEpvaG4gTGluZHNheSBib3JuIGluIE5ldyBZb3JrIENpdHk%2FIiwibW9kZWwiOiJncHQtMy41LXR1cmJvIn0%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

**Step 4:** Final response generation  
Use the answer from the previous step to refine the original answer.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiTGlzdCBvZiBwb2xpdGljaWFucyBib3JuIGluIE5ZQzpcbjEuIERvbmFsZCBUcnVtcFxuMi4gUnVkeSBHaXVsaWFuaVxuMy4gQ2h1Y2sgU2NodW1lclxuNC4gSm9obiBMaW5kc2F5IiwicHJvbXB0IjoiTGlzdCBhbGwgcG9saXRpY2lhbnMgYm9ybiBpbiBOWUMuXG4xLiBNaWNoYWVsIEJsb29tYmVyZ1xuMi4gRG9uYWxkIFRydW1wXG4zLiBGcmFua2xpbiBELiBSb29zZXZlbHRcbjQuIFJ1ZHkgR2l1bGlhbmlcbjUuIFRoZW9kb3JlIFJvb3NldmVsdFxuNi4gRWQgS29jaFxuNy4gS2lyc3RlbiBHaWxsaWJyYW5kXG44LiBDaHVjayBTY2h1bWVyXG45LiBCaWxsIGRlIEJsYXNpb1xuMTAuIEpvaG4gTGluZHNheVxuXG5Vc2UgdGhlIHZlcmlmaWNhdGlvbiBxdWVzdGlvbiBhbmQgYW5zd2VycyBiZWxvdyBhbmQgcmVzcG9uZCB3aXRoIHRoZSByZXZpc2VkIGxpc3Q6XG5XYXMgTWljaGFlbCBCbG9vbWJlcmcgYm9ybiBpbiBOZXcgWW9yayBDaXR5PyBOby5cbldhcyBEb25hbGQgVHJ1bXAgYm9ybiBpbiBOZXcgWW9yayBDaXR5PyBZZXMuXG5XYXMgRnJhbmtsaW4gRC4gUm9vc2V2ZWx0IGJvcm4gaW4gTmV3IFlvcmsgQ2l0eT8gTm8uXG5XYXMgUnVkeSBHaXVsaWFuaSBib3JuIGluIE5ldyBZb3JrIENpdHk%2FIFllcy5cbldhcyBUaGVvZG9yZSBSb29zZXZlbHQgYm9ybiBpbiBOZXcgWW9yayBDaXR5PyBOby5cbldhcyBFZCBLb2NoIGJvcm4gaW4gTmV3IFlvcmsgQ2l0eT8gTm8uXG5XYXMgS2lyc3RlbiBHaWxsaWJyYW5kIGJvcm4gaW4gTmV3IFlvcmsgQ2l0eT8gTm8uXG5XYXMgQ2h1Y2sgU2NodW1lciBib3JuIGluIE5ldyBZb3JrIENpdHk%2FIFllcy5cbldhcyBCaWxsIGRlIEJsYXNpbyBib3JuIGluIE5ldyBZb3JrIENpdHk%2FIE5vLlxuV2FzIEpvaG4gTGluZHNheSBib3JuIGluIE5ldyBZb3JrIENpdHk%2FIFllcy5cbiIsIm1vZGVsIjoiZ3B0LTMuNS10dXJibyJ9" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

As expected, the final refined response from the LLM only consists of those individuals who were born in NYC, as revealed by the answers to the verification questions in step 3.

Please note that unlike the examples above, the original paper uses [Few-Shot Prompting](https://learnprompting.org/docs/advanced/few_shot/introduction) to execute the entire process.

## What Are CoVe Prompting Results?

Experiments using CoVe for list-based and long-form generation show that:

- CoVe performs significantly better than [Zero-Shot](https://learnprompting.org/docs/advanced/zero_shot/introduction), Few-Shot, and CoT. Hallucinations are reduced after employing CoVe.

![precision vs hallucinations](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2FCoVe_results.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Test Precision and average number of positive and negative (hallucination)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Shehzaad Dhuliawala. (2023). Chain-of-Verification Reduces Hallucination in Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2309.11495" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2309.11495</a></span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

- CoVe improves performance on closed book QA. Employing CoVe improves the F1 score by 23% (from 0.39 to 0.48).

![cove vs Zero-Shot and Few-Shot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2FCoVe_closed_book.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

CoVe's performance against Zero-Shot and Few-Shot in closed book MultiSpanQ<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Shehzaad Dhuliawala. (2023). Chain-of-Verification Reduces Hallucination in Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2309.11495" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2309.11495</a></span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

- On long-form content generation, CoVe-based Llama outperforms InstructGPT, ChatGPT and PerplexityAI.

![CoVe vs other LLMs trained with Zero-Shot, Few-Shot, and CoT](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2FCoVe_outperforms_chatgpt.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

CoVe against InstructGPT, ChatGPT and PerplexityAI<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Shehzaad Dhuliawala. (2023). Chain-of-Verification Reduces Hallucination in Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2309.11495" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2309.11495</a></span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

## Limitations of CoVe Prompting

- CoVe reduces the hallucinations in the generated response but doesn't remove them completely.
- The paper reduces hallucinations in the form of directly stated factual inaccuracies. The paper doesn't gauge the effectiveness of CoVe in reducing other forms of hallucinations, such as incorrect reasoning steps.
- The CoVe approach relies on the LLM for finding its own inaccuracies. If the model cannot find its own inaccuracies, it won't benefit from CoVe.

## Conclusion

Hallucinations are common in LLM responses, especially when the generated response is a long passage comprising multiple sentences. Such hallucinations degrade the quality of the generated response. CoVe is a simple and effective technique to reduce the hallucinations from an LLM response without any training or [fine-tuning](https://learnprompting.org/vocabulary/fine-tuning). However, the paper doesn't study the effectiveness of CoVe in reducing hallucinations other than factual inaccuracies.

## Footnotes