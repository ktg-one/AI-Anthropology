---
title: Duty-Distinct Chain-of-Thought (DDCoT)
source: https://learnprompting.org/docs/advanced/decomposition/duty-distinct-chain-of-thought
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Learn how to use Duty-Distinct Chain-of-Thought (DDCoT) to improve multimodal reasoning in large language models (LLMs).
tags:
  - clippings
feature: thumbnails/external/5de24f6b17105b6ecdcb56bec84e49c5.jpg
thumbnail: thumbnails/resized/51258d65c0a62dfdf028932f67f38555_86cf658e.webp
---
🧠 AdvancedDecomposition[🟦 Duty-Distinct Chain-of-Thought (DDCoT)](https://learnprompting.org/docs/advanced/decomposition/duty-distinct-chain-of-thought)

# 🟦 Duty-Distinct Chain-of-Thought (DDCoT)

🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 6 minutes

Last updated on March 25, 2025

[Valeriia Kuka](https://learnprompting.org/docs/advanced/decomposition/#Valeriia%20Kuka-bio)

**DDCoT (Duty-Distinct Chain-of-Thought Prompting)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Zheng, G., Yang, B., Tang, J., Zhou, H.-Y., &amp; Yang, S. (2023). DDCoT: Duty-Distinct Chain-of-Thought Prompting for Multimodal Reasoning in Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2310.16436" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2310.16436</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a novel prompting technique designed to improve multimodal reasoning in large language models (LLMs). It addresses the challenges of integrating textual and visual information by **breaking down reasoning into distinct responsibilities**, reasoning (handled by LLMs) and recognition (handled by visual models). This structured approach reduces **hallucinations** and enhances **explainability, generalizability, and zero-shot learning performance** across a variety of multimodal tasks.

## Key Insights Behind DDCoT

DDCoT is built on two fundamental insights derived from extensive analysis of multimodal reasoning challenges:

1. **"Keep critical thinking"** - Maintaining a healthy dose of skepticism by explicitly indicating uncertainty in the reasoning process helps improve correctness. This is implemented through a negative-space design that explicitly marks questions requiring visual information as "uncertain," reducing the tendency of LLMs to hallucinate answers.
2. **"Let everyone do their jobs"** - Dividing labor between LLMs (reasoning) and visual models (recognition) allows each to focus on what they do best. This division of responsibilities prevents language hallucinations that often occur when LLMs try to process interleaved multimodal inputs directly.

## How It Works

DDCoT implements a sequential three-stage process to handle multimodal reasoning tasks:

1. **Breaking Down Reasoning into Sub-questions**
	- Instead of directly solving multimodal problems, the LLM first generates **sub-questions** that separate reasoning from visual recognition.
	- This decomposition is performed in a single stage using prompts like "please think step-by-step and deconstruct the question down to necessary sub-questions."
	- For example, given an image and a question about it, the model will first ask:
		- What objects are in the image?
		- What are the characteristics of those objects?
		- What relationships exist between the objects?
		- What knowledge is relevant to these objects?
2. **Negative-space prompting to identify uncertainty**
	- The model explicitly labels questions that **cannot** be answered without visual input as *"Uncertain."*
	- The prompt includes instructions such as "Assume that you do not have any information about the picture, try to answer the sub-question and formulate the corresponding sub-answer as 'Uncertain' if the sub-question cannot be determined."
	- This "negative-space prompting" explicitly acknowledges the limits of text-only knowledge and prevents the model from hallucinating visual details.
	- Experimental results show this reduces factual errors by 25.3% compared to naive prompting.
3. **Visual recognition to answer uncertain sub-questions**
	- A **visual question answering (VQA) model** processes only the sub-questions marked as uncertain.
	- This focused approach leverages off-the-shelf models like BLIP-2 to extract precise visual information for each uncertain sub-question.
	- Example Output:
		- **Sub-question:** What food items are in the image?
		- **VQA Response:** Oranges.
		- **Sub-question:** What nutrients are commonly found in those foods?
		- **LLM Response:** Vitamin C.
4. **Joint reasoning integration**
	- The LLM combines its **linguistic reasoning** with the **visual recognition results** to generate **accurate, explainable rationales.**
	- The integration prompt includes instructions like "note that the supplementary information given may not always be valid" and "select valid information to form the rationale."
	- This critical approach enables the LLM to filter, validate, and even rectify supplementary knowledge for more reliable answers.
	- Example Rationale:  
		"Oranges are known to be a good source of Vitamin C. Therefore, the nutrient mainly provided by the foods in the image is **Vitamin C.**"

## Challenges Addressed by DDCoT

Previous multimodal CoT methods faced significant challenges, all of which DDCoT effectively addresses:

1. **Labor-intensive annotation**: Creating training data with rationales was time-consuming and costly. DDCoT eliminates this need by generating high-quality rationales in a zero-shot manner.
2. **Limited flexibility**: Existing methods were effective either in zero-shot or fine-tuning scenarios, but not both. MM-CoT rationales work well for fine-tuning but fail in zero-shot settings, while GPT-3-generated rationales don't enhance fine-tuning models. DDCoT's rationales work effectively in both contexts.
3. **Poor generalizability**: Previous approaches struggled with novel, unseen reasoning paths. When tested on out-of-distribution problems (training on two domains and testing on a third), DDCoT outperforms MM-CoT by 15.5%, 9.6%, and 12.2% across different domain combinations.
4. **Insufficient explainability**: The interpretability of generated rationales was limited. In human evaluations, DDCoT scored significantly higher in relevance (92% vs. 70.83%), correctness (86.38% vs. 67.99%), and explainability (83.26% vs. 58.73%) compared to MM-CoT.
5. **Hallucination problems**: Interleaved multimodal information exacerbated language hallucinations. DDCoT's negative-space prompting reduces hallucination rates by 28.1% compared to naive prompting with visual information.

## How to Use DDCoT

1. Fill in the Placeholders:

Replace the following placeholders with your task-specific information:

- {context}: A text description or any additional context for the question.
- {has\_image}: A Boolean indicator (e.g., “True” or “False”) specifying if there is an image.
- {question}: The main question you want the model to answer.
- {option}: The list of answer options.
2. Input the template to the LLM:

Use the exact system instruction provided by the authors. For example, the template begins with:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

System: You are a helpful, highly intelligent guided assistant. You will do your best to guide humans in choosing the right answer to the question. Note that insufficient information to answer questions is common, because you do not have any information about the picture. The final answer should be one of the options.

  

User: Given the context, questions and options, please think step-by-step about the preliminary knowledge to answer the question, deconstruct the question as completely as possible down to necessary sub-questions based on context, questions and options. Then with the aim of helping humans answer the original question, try to answer the sub-questions. The expected answering form is as follows:

  

Sub-questions:

  
1. {sub-question 1}
2. {sub-question 2} ...
  

Sub-answers:

  
1. {sub-answer 1} or 'Uncertain'
2. {sub-answer 2} or 'Uncertain'
  

...

  

Answer: {One of the options} or 'Uncertain'

  

For a question, assume that you do not have any information about the picture, but try to answer the sub-questions and prioritize whether your general knowledge can answer it, and then consider whether the context can help. If sub-questions can be answered, then answer in as short a sentence as possible. If sub-questions cannot be determined without information in images, please formulate corresponding sub-answer into "Uncertain".

  

Only use "Uncertain" as an answer if it appears in the sub-answers. All answers are expected as concise as possible.

  

Here is an attempt:

  

Context: {context}

  

Has An Image: {has\_image}

  

Question: {question}

  

Options: {option}

3. A **visual question answering (VQA) model** processes only the sub-questions marked as uncertain.
4. The LLM combines its **linguistic reasoning** with the **visual recognition results** to generate **accurate, explainable rationales** using the following prompt:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

System: You are a helpful, highly intelligent teacher. You will not only do your best to guide humans to the correct answer, but you will also give the rationales as a reference.

  

User: Given the context, questions, options, supplementary information, think step by step and answer the questions. Please note that we need not only the answer, but more importantly the rationales of getting the answer. The expected answering form is as follows:

  

Rationale: {rationale}

  

Answers: {one of the options}

  

Please note that the supplementary information given may not always be valid. Please select valid information to form the rationale and choose the relatively correct option as your answer.

  

Here is an attempt:

  

Context: {context}

  

Has An Image: {has\_image}

  

Question: {question}

  

Options: {option}

  

Supplementary information: {supplementary\_information}

## Conclusion

DDCoT represents a **significant advancement in multimodal reasoning** by introducing a structured approach that separates reasoning and recognition responsibilities. Through **negative-space prompting and duty-distinct design**, it effectively addresses the hallucination problems that plague multimodal systems while significantly improving performance across zero-shot and fine-tuning scenarios.

The key innovation lies in its ability to generate high-quality rationales without manual annotation, which enhance both zero-shot prompting and fine-tuning learning. DDCoT makes AI models more **accurate, generalizable, and explainable** in tasks requiring both textual and visual reasoning, bringing us closer to human-like multimodal understanding.