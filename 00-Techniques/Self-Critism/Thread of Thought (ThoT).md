---
title: Thread of Thought (ThoT)
source: https://learnprompting.org/docs/advanced/thought_generation/thread_of_thought
author:
  - '[["Bhuwan Bhatt"]]'
published:
created: 2025-09-07
description: Thread of Thought (ThoT) prompting simplifies chaotic contexts for LLMs, enhancing focus and accuracy.
tags:
  - clippings
feature: thumbnails/external/fb45f2f58f427250fbb9968b13a21c14.webp
thumbnail: thumbnails/resized/752bf8afe72be49579a91890af5152ab_86cf658e.webp
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 6 minutes

Last updated on November 22, 2024

[Bhuwan Bhatt](https://learnprompting.org/docs/advanced/thought_generation/#Bhuwan%20Bhatt-bio)

![Overview of Thread of Thought (ThoT)](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fthought_gen_covers%2Fthot_cover.webp&w=1920&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Overview of Thread of Thought (ThoT)

### Information and Links

| Technique | Institution | Date of Publication | Paper |
| --- | --- | --- | --- |
| Thread of Thought (ThoT) | University of Macau, Microsoft Corporation, University of Technology Sydney | November 2023 | [Thread of Thought Unraveling Chaotic Contexts](https://arxiv.org/abs/2311.08734) |

## Introduction

[Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) have achieved a remarkable performance in natural language understanding and generation. They are used for a variety of tasks such as translation, summarization, question answering, etc. As LLMs become more capable, their applications grow increasingly diverse and complex.

In advanced applications like [Retrieval-Augmented Generation (RAG)](https://learnprompting.org/docs/retrieval_augmented_generation/introduction), users often input vast texts containing tens of thousands of tokens. This data may vary widely in relevance and connectivity, with some details critical to the query and others irrelevant. Such scenarios exemplify **"Chaotic Contexts"**—more challenging than mere "long contexts," which involve a large token count but lack the same degree of informational disarray.

## Challenges in Handling Chaotic Contexts

Current techniques for managing chaotic contexts include:

- **Retrieval-Augmentation with Long Context Extensions:** Combining extended model contexts with retrieval mechanisms.
- **Prompt Streamlining:** Reducing irrelevant or redundant information within the input.

However, both approaches often require fine-tuning or retraining, demanding labeled data and substantial computational resources.

## Introducing Thread of Thought Prompting

Thread of Thought (ThoT) prompting<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/thought_generation/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Zhou, Y., Geng, X., Shen, T., Tao, C., Long, G., Lou, J.-G., &amp; Shen, J. (2023). Thread of Thought Unraveling Chaotic Contexts. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2311.08734" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2311.08734</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> offers an alternative that eliminates the need for fine-tuning. Instead, it methodically segments and analyzes extended contexts, extracting relevant details to address specific queries. Much like how humans sift through large volumes of information by isolating key points, ThoT helps LLMs handle complex inputs efficiently.

In short, ThoT prompting helps LLMs to methodically process, summarize, and analyze extended contexts in manageable parts, resulting in more accurate responses in tasks such as multi-turn conversations and complex question answering.

## Key Features of ThoT Prompting

1. **Guided Step-by-Step Processing:** ThoT prompts the model to "walk through" chaotic contexts, analyzing and summarizing each part progressively.
2. **Selective Attention:** By breaking down information into smaller segments, ThoT helps the model ignore irrelevant details and focus on pertinent information.
3. **Two-Tiered Prompting System:** This system involves a first pass for analysis and a second pass for summarizing and deriving conclusions, enhancing the model's ability to synthesize complex information.

For example, if the model is asked about the founding place of "Reclam" from multiple retrieved passages, ThoT helps the model sift through each passage in stages, retaining only the relevant details about "Reclam" and its founding location.

## How to Use ThoT Prompting

ThoT prompting uses a simple and effective two-step process. As discussed previously, it doesn't require any fine-tuning or re-training and can easily be used with a variety of existing language models. Let's briefly discuss the two steps involved in the process:

### Step 1: Initiating the Reasoning

The goal of this step is to provide the "chaotic" context, followed by the question and a trigger to elicit a response from the LLM. The prompt template for this step looks like this:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Template for initiating the reasoning

---

CHAOTIC CONTEXT HERE

Q: QUERY HERE

TRIGGER SENTENCE HERE

A:

#### Example in Action

Now, let's look at a concrete example. Say, given multiple sources of information regarding Reclam, you want to know where Reclam was founded. Your input to the model will look like:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

As a content reviewer, I provide multiple retrieved passages about this question; you need to answer the question. retrieved Passage 1 is: to introduce book vending machines, … retrieved Passage 2 is: of the Carlsbad Decrees, it quickly … retrieved Passage 3 is: It is at "Kreuzstrae 12", opposite … retrieved Passage 4 is: house in Leipzig remained there, … retrieved Passage 5 is: Delcam Delcam is a supplier of … retrieved Passage 6 is: inhabitants are called recreinos. … retrieved Passage 7 is: 'politically unreliable' writers like … retrieved Passage 8 is: Recheio Recheio is the biggest … retrieved Passage 9 is: via the Internet, large volumes of … retrieved Passage 10 is: without needing to pay any royalties, …

Q: Where was Reclam founded? Walk me through this context in manageable parts step by step, summarizing and analyzing as we go.

A:

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

According to retrieved Passage 2, Anton Philipp Reclam founded his own publishing … In retrieved Passage 4, it is mentioned that the Reclam publishing house in Leipzig … Finally, in retrieved Passage 7, it is stated that after the partition of Germany … Therefore, Reclam was originally founded in Leipzig, Germany, and later moved its main office to Stuttgart.

Notice the trigger sentence "Walk me through this context in manageable parts step by step, summarizing and analyzing as we go". The trigger sentence guides LLM to navigate chaotic context by asking it to summarize and analyze the information as it goes thorough the input context.

### Step 2: Refining the Conclusion

The goal of the second step is to extract the conclusion using the response of the LLM in the previous step. The prompt template for this step looks like this:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Template for initiating the reasoning

---

CHAOTIC CONTEXT HERE

Q: QUERY HERE

TRIGGER SENTENCE HERE

A: ANSWER FROM LLM HERE

Therefore, the answer is:

#### Example in Action

Let's use the template to extract the final answer from the LLM.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

As a content reviewer, I provide multiple retrieved passages about this question; you need to answer the question. retrieved Passage 1 is: to introduce book vending machines, … retrieved Passage 2 is: of the Carlsbad Decrees, it quickly … retrieved Passage 3 is: It is at "Kreuzstrae 12", opposite … retrieved Passage 4 is: house in Leipzig remained there, … retrieved Passage 5 is: Delcam Delcam is a supplier of … retrieved Passage 6 is: inhabitants are called recreinos. … retrieved Passage 7 is: 'politically unreliable' writers like … retrieved Passage 8 is: Recheio Recheio is the biggest … retrieved Passage 9 is: via the Internet, large volumes of … retrieved Passage 10 is: without needing to pay any royalties, …

Q: Where was Reclam founded? Walk me through this context in manageable parts step by step, summarizing and analyzing as we go.

A: According to retrieved Passage 2, Anton Philipp Reclam founded his own publishing … In retrieved Passage 4, it is mentioned that the Reclam publishing house in Leipzig … Finally, in retrieved Passage 7, it is stated that after the partition of Germany … Therefore, Reclam was originally founded in Leipzig, Germany, and later moved its main office to Stuttgart.

Therefore, the answer is:

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Reclam was originally founded in Leipzig

## How ThoT Differs from Existing Techniques

ThoT stands apart from traditional approaches:

- **Enhanced Focus vs. Chain-of-Thought (CoT)**: While CoT improves reasoning, it falters in chaotic contexts. ThoT's segmentation approach ensures no key details are overlooked.
- **Plug-and-Play Simplicity**: ThoT works with pre-trained models without the need for additional training, making it cost-effective and easy to implement.
- **Adaptability**: ThoT excels across tasks like retrieval-augmented generation, multi-turn dialogues, and summarizing unstructured data.

### Applications and Benefits of Thread of Thought

ThoT is useful in scenarios where complex or unrelated information must be processed for relevant insights:

- **Question Answering with Distractors:** Handling retrieval-augmented generation tasks with distracting passages.
- **Multi-Turn Dialogues:** Supporting coherent responses by tracking conversation history.
- **Chaotic Data Summarization:** Summarizing unstructured, long-form content like legal or research documents.

## What are ThoT Prompting Results?

ThoT was evaluated on two chaotic context scenarios: retrieval-augmented generation (RAG) and multi-turn conversation response. Two datasets: PopQA and EntityQ were used to evaluate the performance on the RAG task and the MTCR dataset was used to assess multi-turn conversation response.

In all datasets, ThoT significantly outperformed traditional methods. Here are some key results:

| Dataset | Method | Model | Accuracy Improvement |
| --- | --- | --- | --- |
| PopQA | ThoT Prompting | GPT-3.5-turbo | +16% over CoT |
| EntityQ | ThoT Prompting | GPT-3.5-turbo | +8.5% over CoT |
| MTCR | ThoT Prompting | GPT-3.5-turbo | +14.8% over CoT |

## Conclusion

Thread of Thought (ThoT) prompting introduces a new way for language models to tackle complex, chaotic contexts by breaking down information into segments, analyzing each, and synthesizing relevant insights. This approach not only enhances accuracy but also integrates smoothly with existing models, making it an efficient and versatile tool for applications in retrieval-augmented generation and other challenging tasks requiring nuanced comprehension.