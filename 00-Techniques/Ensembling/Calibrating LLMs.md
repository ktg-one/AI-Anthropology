---
title: Calibrating LLMs
source: https://learnprompting.org/docs/reliability/calibration
author:
  - '[["Sander Schulhoff"]]'
published:
created: 2025-09-07
description: This page presents an important next step to reducing biases. Learn more about advanced technical and non-technical methods of calibrating LLMs.
tags:
  - clippings
feature: thumbnails/external/6c0acbcb74fbffe86a00ed99db9b1fba.jpg
thumbnail: thumbnails/resized/b2f719287eaebe8bde04cf37e251cd29_86cf658e.webp
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 5 minutes

Last updated on August 7, 2024

[Sander Schulhoff](https://learnprompting.org/docs/reliability/#Sander%20Schulhoff-bio)

Takeaways

- **LLM Calibration**: Calibrating LLMs involves adjusting their output distributions to reduce biases and ensure more balanced predictions.
- **Example**: In [sentiment analysis](https://learnprompting.org/vocabulary/Sentiment_Analysis), bias can be measured using neutral inputs and countered by applying a transformation which corrects for the measured bias.

## What is Calibrating LLMs?

**Calibrating LLMs**, or more specifically their **output distributions**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/reliability/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Zhao, T. Z., Wallace, E., Feng, S., Klein, D., &amp; Singh, S. (2021). Calibrate Before Use: Improving Few-Shot Performance of Language Models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> , is another way of counteracting some of the biases they exhibit. Let's walk through a quick example: Say we have a [sentiment analysis](https://learnprompting.org/vocabulary/Sentiment_Analysis) task with two possible labels, `Positive` and `Negative`. Consider what happens when the [LLM](https://learnprompting.org/vocabulary/LLM) is prompted with `Input: nothing Sentiment: `. This input doesn't contain any *context* which the LLM can use to make a sentiment prediction, so it is called a **context-free** input.

Since `nothing` is neither a positive nor a negative concept, we would expect the LLM to output a probability of about 0.5 for both `Positive` and `Negative`. However, often (and for this example) that will not be the case.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

p("Positive" | "Input: nothing Sentiment:") = 0.9

p("Negative" | "Input: nothing Sentiment:") = 0.1

Given these label probabilities for a context-free input, we know that the LLM's **output distribution** is likely biased towards the label `Positive`. This may cause the LLM to favor `Positive` for all inputs, even if the input is not actually positive.

If we can somehow **calibrate** the output distribution, such that context-free inputs are assigned a probability of 0.5 for both `Positive` and `Negative`, then we can often remove the bias towards `Positive` and the LLM will be more reliable on both context-free inputs and inputs with context.

## Non-Technical Solution

A non-technical solution to this problem is to simply provide Few-Shot examples where context-free exemplars are effectively assigned a probability of 0.5 for both `Positive` and `Negative`.

For example, we could provide the following Few-Shot examples which show each context-free exemplar being classified as both `Positive` and `Negative`:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Input: I hate this movie. Sentiment: Negative Input: I love this movie. Sentiment: Positive Input: N/A Sentiment: Positive Input: N/A Sentiment: Negative Input: nothing Sentiment: Positive Input: nothing Sentiment: Negative Input: I like eggs. Sentiment:

To my knowledge, this solution has not been explored in the literature, and I am not sure how well it works in practice. However, it is a simple solution that demonstrates what calibration is trying to achieve.

## Technical Solution

Another solution for calibrating LLMs is **contextual calibration**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/reliability/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Zhao, T. Z., Wallace, E., Feng, S., Klein, D., &amp; Singh, S. (2021). Calibrate Before Use: Improving Few-Shot Performance of Language Models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> , where we adjust special calibration parameters, which ensure that context-free inputs (like `Input: nothing Sentiment: `) are assigned a probability of about 0.5 for both labels. Note that in practice this method performs calibration over multiple different context-free inputs (e.g. `Input: N/A Sentiment: `, `Input: [MASK] Sentiment: `). It averages the calibration parameters that work best for each context-free input to find the best calibration parameters for the LLM.

### Example of Contextual Calibration

Let's go through an example of computing the calibration parameters for one context-free input. Note that this example is not reproducible with GPT-3 because it can't be restricted to the labels `Positive` and `Negative`.

Consider again the above example where the LLM assigns the following probabilities to the labels for a context-free input:

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

p("Positive" | "Input: nothing Sentiment:") = 0.9

p("Negative" | "Input: nothing Sentiment:") = 0.1

We want to find some probability distribution q such that:

```
q("Positive" | "Input: nothing Sentiment:") = 0.5

q("Negative" | "Input: nothing Sentiment:") = 0.5
```

We will do so by creating a linear transformation that adjusts (calibrates) the probabilities of $p$.

$\hat q = \text{Softmax}(W\hat p + b)$

This equation takes the original probabilities $\hat p$ and applies the weights $W$ and bias $b$ to them. The weights $W$ and bias $b$ are the calibration parameters, which, when applied to the context-free example's probabilities, will yield $\hat p$ = \[0.5, 0.5\].

#### Computing W and b

We need to somehow compute the weights $W$ and bias $b$. One way to do this is:

$W = \text{diag}(\hat p)^{-1}$

$b = 0$

Although the definition of $W$ may seem a bit strange at first, it is just taking the inverse of each value in $\hat p$ to find a $W$ that will transform the original probabilities $\hat p$ into the calibrated probabilities \[0.5, 0.5\].

Let's verify that this works for the example above:

$\hat p = [0.9, 0.1]$

$W = \text{diag}(\hat p)^{-1} = \text{diag}([0.9, 0.1])^{-1} = \begin{bmatrix} 0.9 & 0 \\ 0 & 0.1 \end{bmatrix}^{-1} = \begin{bmatrix} 1.11 & 0 \\ 0 & 10 \end{bmatrix}$

$\hat q = \text{Softmax}(W\hat p + b) = \text{Softmax}(\begin{bmatrix} 1.11 & 0 \\ 0 & 10 \end{bmatrix}*{[0.9, 0.1]} + 0) = \text{Softmax}([1, 1]) =[0.5, 0.5]$

As mentioned above, we would perform this same process for multiple different context-free inputs, and average the calibration parameters that work best for each context-free input to find the best calibration parameters for the LLM. This means that the final calibration parameters will probably not map any of the context-free inputs to exactly \[0.5, 0.5\].

### Another method

$b$ could also be set to $-\hat p$, and $W$ to the identity matrix. This method performs better on generation rather than classification tasks<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/reliability/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Zhao, T. Z., Wallace, E., Feng, S., Klein, D., &amp; Singh, S. (2021). Calibrate Before Use: Improving Few-Shot Performance of Language Models. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> .

## Conclusion

Our model responses are often predisposed, or biased, towards certain labels. Calibrating LLMs can be used to counteract this bias.