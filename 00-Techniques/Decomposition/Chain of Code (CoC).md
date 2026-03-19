---
title: Chain of Code (CoC)
source: https://learnprompting.org/docs/advanced/decomposition/chain-of-code
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Chain of Code (CoC) is a new framework that improves reasoning in large language models (LLMs) by integrating code execution and language model simulation.
tags:
  - clippings
feature: thumbnails/external/3464a9865c579694d92ec3e94f0233ce.png
thumbnail: thumbnails/resized/f97bb824b49d4a8c6e531744edf91861_86cf658e.webp
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 4 minutes

Last updated on March 11, 2025

[Valeriia Kuka](https://learnprompting.org/docs/advanced/decomposition/#Valeriia%20Kuka-bio)

![Chain of Code (CoC)](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fnew_techniques%2Fchain-of-code.png&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Large language models (LLMs) have demonstrated strong abilities in solving complex reasoning tasks like writing programs, answering science questions, and more. Traditional techniques such as [Chain-of-Thought (CoT) prompting](https://learnprompting.org/docs/intermediate/chain_of_thought) allowed to improve LLMs' performance on reasoning tasks by encouraging the model to break down a problem into intermediate reasoning steps using **natural language**.

Chain-of-Thought is based on **semantic reasoning** that involves understanding and processing the meaning of words and sentences. While semantic reasoning works well for tasks that depend on language and context, it can struggle with precise **numerical** or **symbolic operations**.

[Program of Thoughts (PoT)](https://learnprompting.org/docs/advanced/decomposition/program_of_thoughts) takes a step further from CoT and generates code to represent its reasoning steps. The code is then executed by a code interpreter. PoT excels at tasks like arithmetic but struggles with semantic tasks that are hard to encode in code.

**Chain of Code (CoC)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Li, C., Liang, J., Zeng, A., Chen, X., Hausman, K., Sadigh, D., Levine, S., Fei-Fei, L., Xia, F., &amp; Ichter, B. (2024). Chain of Code: Reasoning with a Language Model-Augmented Code Emulator. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2312.04474" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2312.04474</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a framework designed to overcome these limitations by combining the strengths of both **code execution** and **language-based reasoning**.

CoC merges ideas behind CoT and PoT by having the model generate a mix of executable code and "semantic placeholders." When the code interpreter runs the program, it handles precise operations, and for parts that are ambiguous or non-executable, an LM-based simulation module, called an LMulator, uses language-based reasoning to simulate what the output should be based on the context. This dual mechanism combines the precision of code execution with the flexible reasoning of language models.

### Key Differences: CoC vs. Program of Thoughts (PoT)

- **PoT:** The model writes a full program and relies entirely on a code interpreter to run it. It works best when all parts of the task can be explicitly coded.
- **CoC:** CoC extends PoT by interweaving a code interpreter with an LMulator. This allows CoC to handle parts of the problem that are inherently semantic or ambiguous by simulating the execution of non-executable code segments.

## How Is CoC Built and How Does It Work?

CoC follows a **two-step process**:

### **Step 1: Code Generation**

Given a problem, the LM is prompted to generate a program that lays out a step-by-step solution. The generated code is a mix of:

- **Executable components:** Sections that the interpreter can run (e.g., loops, arithmetic operations).
- **Semantic placeholders:** For parts that require semantic judgment or cannot be directly translated into code (such as checking if an item is a fruit or detecting sarcasm), the model inserts functions like `is_fruit()` or `get_country()`.
	- When the interpreter encounters such a function, it cannot execute it. Instead, the **LMulator** steps in—it uses language-based reasoning to simulate what the output should be based on the context.
	- The simulated result is then incorporated into the overall program state, allowing the process to continue seamlessly.

### **Step 2: Code Execution with an LMulator**

CoC runs the code line by line.

For each line:

- If executable, the interpreter updates the program state with precise calculations.
- If not executable, the LMulator simulates the expected output, and the program state is updated accordingly. This interplay enables CoC to handle a wide range of tasks that mix numerical precision with semantic reasoning.

## Example: Counting Fruits

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Problem

---

I have an orange, a violin, two peaches, an apple, a pepper, and three plums. How many fruits do I have?

### Step 1: Code Generation

The model generates the following code:

```
# Define a dictionary of objects with their counts
objects = {"orange": 1, "violin": 1, "peaches": 2, "apple": 1, "pepper": 1, "plum": 3}

# Initialize the fruit counter
num_fruits = 0

# Iterate over each object
for obj in objects:
    # Check if the object is a fruit (this may not be executable directly)
    object_is_fruit = is_fruit(obj)
    if object_is_fruit:
        num_fruits += objects[obj]

# Final answer
answer = num_fruits
```

### Step 2: Code Execution with LMulator

The interpreter sets up the dictionary and initializes `num_fruits` to 0. It correctly processes the loop structure and arithmetic for summing counts.

When the interpreter reaches `is_fruit(obj)`, it cannot execute this function because it requires semantic judgment. Here, the LMulator is invoked:

- For each object, the LMulator simulates the expected outcome based on context. For example:
	- For `"orange"`, `"peaches"`, `"apple"`, and `"plum"`, it returns `True`.
	- For `"violin"` and `"pepper"`, it returns `False`.
- These simulated values are used to update `num_fruits`.

After processing all objects with a mix of execution and simulation, the final computed value of `answer` reflects the correct count of fruits.

Note

Find Chain-of-Code demo and more information about using CoC in [Google Colab](https://colab.research.google.com/github/google-research/google-research/blob/master/code_as_policies/coc_demo.ipynb).

## How CoC Differs from Existing Techniques

| Method | Key Idea | Executes Code? | Handles Non-Executable Steps? | Improvement in Reasoning |
| --- | --- | --- | --- | --- |
| Chain of Thought (CoT) | Uses step-by-step natural language reasoning | No | No | Limited on numeric/symbolic tasks |
| Program of Thoughts (PoT) | Writes and executes code for problem-solving | Yes | No | Effective primarily for arithmetic tasks |
| ScratchPad | Tracks intermediate steps through text-based simulation | No | Yes | Works only in text-based reasoning |
| Chain of Code (CoC) | Combines code execution with LM-based simulation | Yes | Yes | Integrates the best of both approaches |

## Benefits and Applications

- CoC is suitable for tasks that require both detailed computation (such as mathematics) and understanding of language (such as commonsense reasoning).
- The framework is adaptable to various challenges, including numerical calculations, logical operations, and even data processing tasks.
- Improved Accuracy: Experiments have shown that CoC can outperform traditional methods on benchmark datasets, especially in tasks that combine semantic and numeric reasoning.

## Limitations and Future Directions

While Chain of Code offers a powerful approach, it also faces some challenges:

1. Running both a code interpreter and an LMulator can be slower than direct text-based reasoning.
2. Some tasks might still be difficult to simulate accurately with code-based reasoning.
3. Future work could focus on refining how the LM simulates non-executable steps to further boost performance.

## Conclusion

Chain of Code (CoC) offers a new way for language models to tackle complex reasoning tasks by merging code execution with language-based simulation. This hybrid approach allows models to solve problems more precisely by executing parts of a generated program while still reasoning through more abstract, semantic aspects.