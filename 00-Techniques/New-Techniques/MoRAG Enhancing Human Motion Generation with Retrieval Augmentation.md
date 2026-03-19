---
title: "MoRAG: Enhancing Human Motion Generation with Retrieval Augmentation"
source: https://learnprompting.org/docs/retrieval_augmented_generation/multi_fusion_rag
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-08
description: Discover MoRAG, a retrieval-augmented framework for generating diverse, realistic human motions from text. Perfect for animation, VR, and gaming.
tags:
  - clippings
feature: thumbnails/external/74dcbab5f29df1bc87df64ad68d39fdd.jpg
thumbnail: thumbnails/resized/88b0f126a0a70a73acfb2756df55f1b9_86cf658e.webp
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 2 minutes

Last updated on March 2, 2025

[Valeriia Kuka](https://learnprompting.org/docs/retrieval_augmented_generation/#Valeriia%20Kuka-bio)

![Multi-Fusion Retrieval Augmented Generation (MoRAG) Illustration](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fretrieval_augmented_generation%2Fmorag_main.webp&w=1920&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Traditional models often struggle with generating realistic motion for complex or unfamiliar prompts, but MoRAG solves this by retrieving motion sequences for specific body parts, then fusing them into a cohesive full-body sequence. **MoRAG (Multi-Fusion Retrieval Augmented Generation)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/retrieval_augmented_generation/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Shashank, K. S., Maheshwari, S., &amp; Sarvadevabhatla, R. K. (2024). MoRAG – Multi-Fusion Retrieval Augmented Generation for Human Motion. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2409.12140" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2409.12140</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a framework designed to improve text-based human motion generation by enhancing motion diffusion models with a [retrieval-augmented](https://learnprompting.org/docs/retrieval_augmented_generation/rag) approach.

MoRAG breaks down prompts into motion sequences specific to body parts (like the torso, hands, and legs), and retrieves motions tailored to each part. These parts are then combined to generate a realistic, diverse motion sequence from natural language descriptions.

### Example

If a user inputs:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

A person doing yoga.

MoRAG retrieves specific motions for the torso, arms, and legs from its database, and combines them to generate a realistic yoga pose sequence.

## How to Use MoRAG

MoRAG enhances motion generation by combining retrieval-based techniques with diffusion models. The process involves:

1. **Input**: A prompt (e.g., "A person dancing with raised hands").
2. **Part-Specific Retrieval**: The system breaks down the motion into body parts (e.g., torso, hands, legs) and retrieves relevant motions from a motion database.
3. **Fusion**: These part-specific motions are fused into a complete motion sequence.
4. **Generation**: The fused motion is used as additional guidance in the motion diffusion model to create diverse, high-quality sequences.

![Multi-Fusion Retrieval Augmented Generation (MoRAG) overview diagram](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fretrieval_augmented_generation%2Fmorag_overview.webp&w=1920&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

## Benefits of MoRAG

- Better generalization to unseen text descriptions.
- Increased diversity in generated motions.
- Higher alignment between text and motion.

MoRAG can be used in animation, virtual reality, and gaming for generating complex, realistic human motions from simple text descriptions.

Note

To explore MoRAG further, check out the [code and models](https://motion-rag.github.io/) released by the authors.