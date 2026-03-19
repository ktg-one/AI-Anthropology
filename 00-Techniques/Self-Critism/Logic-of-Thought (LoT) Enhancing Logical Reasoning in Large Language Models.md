---
title: "Logic-of-Thought (LoT): Enhancing Logical Reasoning in Large Language Models"
source: https://learnprompting.org/docs/new_techniques/logic_of_thought
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-08
description: Explore Logic-of-Thought (LoT), a technique to improve LLM logical reasoning by injecting formal logic into prompts.
tags:
  - clippings
feature: thumbnails/external/9a5e37e2a344f40f2d3ffe7cfbf7fbec.svg
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 5 minutes

Last updated on March 10, 2025

[Valeriia Kuka](https://learnprompting.org/docs/new_techniques/#Valeriia%20Kuka-bio)

Takeaways

- **LoT Enhances Reasoning**: Logic-of-Thought (LoT) boosts logical reasoning in large language models (LLMs) by incorporating formal logic, resulting in greater accuracy.
- **Three-Phase Process**: LoT employs a method of extracting logical propositions, extending them with formal rules, and translating them into natural language, enhancing reasoning capabilities.
- **Performance Gains**: LoT achieves significant improvements in logical reasoning tasks, outperforming methods like Chain-of-Thought (CoT) and Tree-of-Thoughts (ToT) with more precise responses.

![Overview of Logic-of-Thought (LoT) Prompting](https://learnprompting.org/docs/assets/advanced/new_docs_oct3/logic_of_thought_cover.svg)

Overview of Logic-of-Thought (LoT) Prompting

## What is Logic-of-Thought (LoT)?

**Logic-of-Thought (LoT)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/new_techniques/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Liu, T., Xu, W., Huang, W., Wang, X., Wang, J., Yang, H., &amp; Li, J. (2024). Logic-of-Thought: Injecting Logic into Contexts for Full Reasoning in Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2409.17539" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2409.17539</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a novel technique designed to improve the logical reasoning abilities of [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM). While LLMs are highly effective across many tasks, they struggle with complex logical reasoning, especially when using traditional methods like [Chain-of-Thought (CoT)](https://learnprompting.org/docs/intermediate/chain_of_thought).

LoT addresses these challenges by injecting formal propositional logic into prompts, guiding LLMs through more accurate reasoning processes. It adds logical information to input prompts, avoiding the information loss that often occurs when LLMs attempt symbolic reasoning.

### How does LoT work?

LoT operates in three phases to augment input prompts with logical reasoning:

1. **Logic Extraction**: LoT uses LLMs to extract logical propositions and relationships from the input. It identifies key conditional or logical connections between elements of the context.
2. **Logic Extension**: Logical expressions extracted from the first phase are expanded using formal logic rules (e.g., Transitive Law, Contraposition Law). This ensures that logical deductions are complete and align with human intuition.
3. **Logic Translation**: The expanded logical expressions are translated back into natural language. This augmented information is then combined with the original input, enhancing the prompt and helping the LLM to reason more accurately.

For example, if the input contains statements about a person reading a book, LoT might extract logical propositions such as "If a person reads a book, they become smarter" and ensure this information is added to the LLM's reasoning process.

## How LoT differs from existing techniques

LoT improves on existing methods like **Chain-of-Thought (CoT)**, **[Self-Consistency (SC)](https://learnprompting.org/docs/intermediate/self_consistency)**, and **[Tree-of-Thoughts (ToT)](https://learnprompting.org/docs/advanced/decomposition/tree_of_thoughts)** by ensuring that logical information is systematically extracted and applied. Here's how it compares:

- **Chain-of-Thought (CoT)**: CoT adds intermediate reasoning steps but sometimes generates unfaithful conclusions. LoT addresses this by grounding reasoning steps in formal logic, reducing errors.
- **Neuro-symbolic approaches**: Methods like **LINC** or **SatLM** combine LLMs with symbolic reasoning tools. However, these methods can lose information when converting problems into logical expressions. LoT avoids this by directly augmenting prompts without relying on external tools.
- **Tree-of-Thoughts (ToT)**: ToT explores multiple branches of reasoning, but LoT can further enhance this process by ensuring logical coherence within those branches.

## Benefits and Applications

LoT is particularly useful for tasks requiring robust logical reasoning, such as solving puzzles, legal reasoning, or question-answering on standardized tests. It can be applied in scenarios where logical consistency is crucial, and it performs well even in tasks with complex reasoning layers.

## How to use LoT

Here’s an example process using LoT:

### Phase 1. Logic Extraction Prompt

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Please use uppercase English letters such as A, B, C, etc. to identify all possible propositions. Do not include negative tones such as "not" in the propositions. For example, if the sentence is "It is not bored," you should use "A: bored" to represent it.

Next, for each proposition, use the symbol to represent its negative form. For example, the negative form of proposition A can be expressed as A.

Now, please carefully analyze the context and find causal relationship between propositions seriously. A causal expression is only established when the context directly supports this relationship. Use arrows (→) to indicate causal relationships, for example, "If A, then B", "B if A" and "A causes B" etc. can be represented as A → B.

Finally, output propositions and causal expressions.

\[You input\]

### Phase 2. Logic Extention

Logical expressions extracted from the first phase are expanded using formal logic rules (e.g., Transitive Law, Contraposition Law). This ensures that logical deductions are complete and align with human intuition.

### Phase 3. Logic Translation Prompt

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

\[Output from Phase 2\]

Please use the provided propositions to translate each expression into a complete sentence.

¬A represents the negation of proposition A, the arrow (→) represents the causal relationship, and A → B represents if A, then B.

Only output the sentences in a paragraph!

## Results of LoT

LoT has been tested across several logical reasoning datasets, showing significant improvements over baseline methods like CoT and ToT. The following table summarizes the performance gains when LoT is combined with other prompting methods:

| **Dataset** | **CoT** | **LoT + CoT** | **SC(5)** | **LoT + SC(5)** | **ToT** | **LoT + ToT** |
| --- | --- | --- | --- | --- | --- | --- |
| ReClor | 52.17 | +4.35 | 56.52 | +2.18 | 58.70 | +2.17 |
| LogiQA | 34.00 | +2.50 | 36.60 | +1.40 | 34.50 | +5.00 |
| RuleTaker | 60.70 | +0.90 | 59.00 | +1.00 | 65.50 | +0.00 |
| ProofWriter | 58.80 | +2.70 | 57.50 | +2.50 | 61.50 | +6.00 |
| FOLIO | 78.00 | +0.00 | 76.00 | +2.60 | 80.00 | +0.00 |

- **ReClor Dataset**: LoT improves Chain-of-Thought performance by +4.35% and boosts Self-Consistency by +2.18%.
- **LogiQA Dataset**: LoT boosts performance by +2.50% over CoT and +1.40% over SC.
- **ProofWriter Dataset**: LoT shows the highest gains on this dataset, improving ToT by +6%.

## Conclusion

Logic-of-Thought (LoT) is a powerful approach for injecting formal logic into large language models, enhancing their ability to handle complex reasoning tasks. By systematically extracting, extending, and translating logical information into natural language, LoT augments existing methods like CoT and ToT, improving accuracy and reducing errors in logical reasoning tasks. This technique is particularly valuable for applications requiring precise logical deductions, such as legal reasoning or standardized test question-answering.