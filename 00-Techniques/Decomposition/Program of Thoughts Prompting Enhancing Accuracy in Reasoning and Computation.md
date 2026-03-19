---
title: "Program of Thoughts Prompting: Enhancing Accuracy in Reasoning and Computation"
source: https://learnprompting.org/docs/advanced/decomposition/program_of_thoughts
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Learn how Program of Thoughts (PoT) prompting separates reasoning from computation to solve complex numerical reasoning tasks.
tags:
  - clippings
feature: thumbnails/external/a58ad98036e9614be3eb0f100b6fedfa.svg
---
Reading Time: 4 minutes

Last updated on October 1, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/decomposition/#Valeriia%20Kuka-bio)

![Few-Shot and Zero-Shot Program of Thoughts Prompting](https://learnprompting.org/docs/assets/advanced/advanced_covers/Program_of_Thoughts_Prompting_cover.svg)

Takeaways

- **Program of Thoughts (PoT) Prompting** separates reasoning from computation by delegating calculations to external interpreters like Python, reducing computational errors.
- **PoT vs. Chain-of-Thought (CoT)**: Unlike CoT, which merges reasoning and computation, PoT improves accuracy by using structured programs for complex tasks.
- **Tasks best suited for PoT**: PoT excels in math word problems, financial reasoning, and cases where exact computation is required.
- **Limitations** include the potential risks of executing generated code and reduced effectiveness on datasets with diverse question types like AQuA.

## What is Program of Thoughts Prompting?

In [Chain-of-Thought (CoT) Prompting](https://learnprompting.org/docs/intermediate/chain_of_thought)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Jason Wei. (2022). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> , Large Language Models ([LLMs](https://learnprompting.org/vocabulary/LLM)) perform both reasoning and computations. The LLM generates mathematical expressions as a reasoning step and then solves it to get the final answer. However, LLMs are not the ideal candidate for solving mathematical expressions for three reasons:

- LLMs are prone to computational errors.
- LLMs are incapable of solving complex mathematical expressions involving polynomial equations, differential equations, etc.
- LLMs are highly inefficient at expressing iteration.

**Program of Thoughts (PoT) prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wenhu Chen. (2022). Program of Thoughts Prompting: Disentangling Computation from Reasoning for Numerical Reasoning Tasks. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a **prompting technique that separates reasoning from computation**. To be specific, PoT delegates computation steps to an external language interpreter. For instance, the LLM can express the reasoning steps as a Python program, which can be delegated to a Python interpreter to get an accurate response.

The example input and output pair generated by employing [CoT prompting](https://learnprompting.org/vocabulary/CoT_Prompting) and PoT prompting below illustrate how PoT differs from CoT.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Question: In Fibonacci sequence, it follows the rule that each number is equal to the sum of the preceding two numbers. Assuming the first two numbers are 0 and 1, what is the 50th number in Fibonacci sequence?

- A sample response generated using CoT prompting:

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

The first number is 0, the second number is 1, therefore, the third number is 0+1=1. The fourth number is 1+1=2. The fifth number is 1+2=3. The sixth number is 2+3=5. The seventh number is 3+5=8. The eighth number is 5+8=13. ..... (Skip 1000 tokens) The 50th number is 32,432,268,459.

- A sample response generated using PoT prompting:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Question: In Fibonacci sequence, it follows the rule that each number is equal to the sum of the preceding two numbers. Assuming the first two numbers are 0 and 1, what is the 50th number in Fibonacci sequence?

\# Python code, return ans

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

length\_of\_fibonacci\_sequence = 50 fibonacci\_sequence = np.zeros(length\_of\_fibonacci\_sequence) fibonacci\_sequence\[0\] = 0 fibonacci\_ sequence\[1\] = 1 for i in range(3, length\_of\_fibonacci\_sequence): fibonacci\_sequence = fibonacci\_sequence\[i-1\] + fibonacci\_sequence\[i-2\] ans = fibonacci\_sequence\[-1\]

It is clear that while CoT prompting generates natural language output, PoT prompting yields a Python program, which is executed in the Python interpreter to get the final response.

## How to Use Program of Thoughts Prompting?

We can use PoT in either [Zero-Shot or Few-Shot Prompting](https://learnprompting.org/docs/basics/few_shot) settings. In Zero-Shot PoT, the prompt doesn't include any [exemplar](https://learnprompting.org/vocabulary/exemplars).

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiZGVmIHNvbHZlcigpOlxuICAgIHNlYXR0bGVfc2hlZXAgPSAyMFxuICAgIGNoYXJsZXN0b25fc2hlZXAgPSBzZWF0dGxlX3NoZWVwICogNFxuICAgIHRvdWxvdXNlX3NoZWVwID0gY2hhcmxlc3Rvbl9zaGVlcCAqIDJcbiAgICBcbiAgICB0b3RhbF9zaGVlcCA9IHNlYXR0bGVfc2hlZXAgKyBjaGFybGVzdG9uX3NoZWVwICsgdG91bG91c2Vfc2hlZXBcbiAgICBcbiAgICByZXR1cm4gdG90YWxfc2hlZXBcblxuIyBOb3cgbGV0J3MgY2FsbCB0aGUgc29sdmVyIGZ1bmN0aW9uIGFuZCBwcmludCB0aGUgcmVzdWx0XG5wcmludChzb2x2ZXIoKSkiLCJwcm9tcHQiOiIjIFF1ZXN0aW9uOiBUb3Vsb3VzZSBoYXMgdHdpY2UgYXMgbWFueSBzaGVlcCBhcyBDaGFybGVzdG9uLlxuQ2hhcmxlc3RvbiBoYXMgNCB0aW1lcyBhcyBtYW55IHNoZWVwIGFzIFNlYXR0bGUuIEhvdyBtYW55IHNoZWVwIGRvIFRvdWxvdXNlLCBDaGFybGVzdG9uLCBhbmQgU2VhdHRsZSBoYXZlIHRvZ2V0aGVyIGlmXG5TZWF0dGxlIGhhcyAyMCBzaGVlcD9cbiMgQW5zd2VyIHRoaXMgcXVlc3Rpb24gYnkgaW1wbGVtZW50aW5nIGEgc29sdmVyIGZ1bmN0aW9uLlxuZGVmIHNvbHZlcjpcbiMgTGV0J3Mgd3JpdGUgYSBQeXRob24gcHJvZ3JhbSBzdGVwIGJ5IHN0ZXAsIGFuZCB0aGVuIHJldHVyblxudGhlIGFuc3dlclxuIyBGaXJzdGx5LCB3ZSBuZWVkIGRlZmluZSB0aGUgZm9sbG93aW5nIHZhcmlhYmxlOiIsIm1vZGVsIjoiZ3B0LTMuNS10dXJibyJ9" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

The prompt generates a Python program as the output, which the Python interpreter executes to get the final output, i.e., 260.

```
def solver():
    seattle_sheep = 20
    charleston_sheep = seattle_sheep * 4
    toulouse_sheep = charleston_sheep * 2
    
    total_sheep = seattle_sheep + charleston_sheep + toulouse_sheep
    
    return total_sheep

# Now let's call the solver function and print the result
print(solver())

### OUTPUT
----
>>> 260
```

As expected, a Few-Shot PoT prompt requires exemplars demonstrating how to solve the problem. Like Zero-Shot, the output is a program that we separately execute using an interpreter to get the final output.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiY29zdF9vZl9vcmlnaW5hbF9ob3VzZSA9IDgwMDAwXG5pbmNyZWFzZV9yYXRlID0gMTUwIC8gMTAwXG52YWx1ZV9vZl9ob3VzZSA9ICgxICsgaW5jcmVhc2VfcmF0ZSkgKiBjb3N0X29mX29yaWdpbmFsX2hvdXNlXG5jb3N0X29mX3JlcGFpciA9IDUwMDAwXG5hbnMgPSB2YWx1ZV9vZl9ob3VzZSAtIGNvc3Rfb2ZfcmVwYWlyIC0gY29zdF9vZl9vcmlnaW5hbF9ob3VzZSIsInByb21wdCI6IlF1ZXN0aW9uOiBKYW5ldOKAmXMgZHVja3MgbGF5IDE2IGVnZ3MgcGVyIGRheS4gU2hlIGVhdHMgdGhyZWUgZm9yIGJyZWFrZmFzdCBldmVyeSBtb3JuaW5nIGFuZCBiYWtlcyBtdWZmaW5zIGZvciBoZXIgZnJpZW5kcyBldmVyeSBkYXkgd2l0aCBmb3VyLiBTaGUgc2VsbHMgdGhlIHJlbWFpbmRlciBhdCB0aGUgZmFybWVycycgbWFya2V0IGRhaWx5IGZvciAkMiBwZXIgZnJlc2ggZHVjayBlZ2cuIEhvdyBtdWNoIGluIGRvbGxhcnMgZG9lcyBzaGUgbWFrZSBldmVyeSBkYXkgYXQgdGhlIGZhcm1lcnMnIG1hcmtldD9cbiMgUHl0aG9uIGNvZGUsIHJldHVybiBhbnNcbnRvdGFsX2VnZ3MgPSAxNlxuZWF0ZW5fZWdncyA9IDNcbmJha2VkX2VnZ3MgPSA0XG5zb2xkX2VnZ3MgPSB0b3RhbF9lZ2dzIC0gZWF0ZW5fZWdncyAtIGJha2VkX2VnZ3MgZG9sbGFyc19wZXJfZWdnID0gMlxuYW5zID0gc29sZF9lZ2dzICogZG9sbGFyc19wZXJfZWdnXG5cblF1ZXN0aW9uOiBBIHJvYmUgdGFrZXMgMiBib2x0cyBvZiBibHVlIGZpYmVyIGFuZCBoYWxmIHRoYXQgbXVjaCB3aGl0ZSBmaWJlci4gSG93IG1hbnkgYm9sdHMgaW4gdG90YWwgZG9lcyBpdCB0YWtlPyBcbiMgUHl0aG9uIGNvZGUsIHJldHVybiBhbnNcbmJvbHRzX29mX2JsdWVfZmliZXIgPSAyXG5ib2x0c19vZl93aGl0ZV9maWJlciA9IG51bV9vZl9ibHVlX2ZpYmVyIC8gMlxuYW5zID0gYm9sdHNfb2ZfYmx1ZV9maWJlciArIGJvbHRzX29mX3doaXRlX2ZpYmVyXG5cblF1ZXN0aW9uOiBKb3NoIGRlY2lkZXMgdG8gdHJ5IGZsaXBwaW5nIGEgaG91c2UuIEhlIGJ1eXMgYSBob3VzZSBmb3IgJDgwLDAwMCBhbmQgdGhlbiBwdXRzIGluICQ1MCwwMDAgaW4gcmVwYWlycy4gVGhpcyBpbmNyZWFzZWQgdGhlIHZhbHVlIG9mIHRoZSBob3VzZSBieSAxNTAlLiBIb3cgbXVjaCBwcm9maXQgZGlkIGhlIG1ha2U%2FXG4jIFB5dGhvbiBjb2RlLCByZXR1cm4gYW5zIiwibW9kZWwiOiJncHQtMy41LXR1cmJvIn0%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>
```
cost_of_original_house = 80000
increase_rate = 150 / 100
value_of_house = (1 + increase_rate) * cost_of_original_house
cost_of_repair = 50000
ans = value_of_house - cost_of_repair - cost_of_original_house
print(ans)
### OUTPUT
----
>>> 70000.0
```

### PoT as an Intermediate Step

For problems requiring additional reasoning, PoT can also be utilized as an intermediate step to tackle the computation part. The code generated by PoT can be executed to get the intermediate result, which is then substituted with the original question to get the final answer using [Chain-of-Thought Prompting](https://learnprompting.org/docs/intermediate/chain_of_thought).

![using Program-as-Thought as an intermediate step](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fpot_as_intermediate.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

PoT as an intermediate step<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wenhu Chen. (2022). Program of Thoughts Prompting: Disentangling Computation from Reasoning for Numerical Reasoning Tasks.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

## What Are Program of Thoughts Prompting Results?

- Zero-Shot PoT outperforms [Zero-Shot Chain-of-Thought](https://learnprompting.org/docs/intermediate/zero_shot_cot) across all math word problems (MWP) datasets by a significant margin.

![results of PoT](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fzero_shot_pot_and_cot_results.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Comparasion of Zero-Shot PoT with similar techniques across MWP datasets<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wenhu Chen. (2022). Program of Thoughts Prompting: Disentangling Computation from Reasoning for Numerical Reasoning Tasks.</span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

- On financial datasets, Few-Shot PoT + [Self-Consistency (SC)](https://learnprompting.org/docs/intermediate/self_consistency) decoding outperforms Few-Shot CoT + SC by roughly 20% on FinQA/ConvFinQA and 7% on TATQA. On MWP datasets, Few-Shot PoT + Self-Consistency (SC) decoding wins by a small margin of roughly 2-6%.

| Model | GSM8K | AQuA | SVAMP | TabWMP | FinQA | ConvFin | TATQA |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Codex CoT-SC | 78.0 | 52.0 | 86.8 | 75.4 | 44.4 | 47.9 | 63.2 |
| PoT-SC-Codex | 80.0 | 58.6 | 89.1 | 81.8 | **68.1** | **67.3** | **70.2** |

## Limitations of Program of Thoughts Prompting

There are two major limitations to PoT prompting:

- PoT requires the execution of generated code. If the code is malicious and contains snippets like `import os; os.rmdir()`, it could harm the machine running the snippets. Code snippets could also be exploited to run SQL [injection](https://learnprompting.org/docs/prompt_hacking/injection), which could either delete data or leak confidential data.
- For datasets like AQuA, which contain a complex and wide variety of questions, PoT's performance suffers. The reason behind this could be that the exemplars cannot cover the diversity of questions in the dataset.

## Conclusion

Program-of-Thought (PoT) separates computation from reasoning by having the LLM express reasoning as structured programs rather than natural language, improving accuracy for tasks that can be represented as code, like math or accounting. However, PoT is limited to such problems and carries the risk of executing malicious code from user prompts.

Find more on [Decomposition Prompting](https://learnprompting.org/docs/advanced/decomposition/introduction) methods.