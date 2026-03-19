---
title: "Self-Calibration Prompting: Enhancing LLM Accuracy through Self-Evaluation"
source: https://learnprompting.org/docs/advanced/self_criticism/self_calibration
author:
  - '[["Bhuwan Bhatt"]]'
published:
created: 2025-09-01
description: Discover how Self-Calibration enables LLMs to assess their own answers, reducing errors and improving accuracy, especially in larger models.
tags:
  - clippings
feature: thumbnails/external/2519c2f5f433a735c4e815f8b3cd144a.svg
---
🟢 This article is rated [easy](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 2 minutes

Last updated on September 27, 2024

[Bhuwan Bhatt](https://learnprompting.org/docs/advanced/self_criticism/#Bhuwan%20Bhatt-bio)

![Self-Calibration Prompting](https://learnprompting.org/docs/assets/advanced/advanced_covers/self_calibration_cover.svg)

Takeaways

- **Importance of Self-Calibration**: Self-Calibration allows LLMs to evaluate their own answers, reducing misinformation.
- **Practical Implementation**: You can use Self-Calibration by prompting the [LLM](https://learnprompting.org/vocabulary/LLM) to assess its own response for correctness.
- **Effectiveness in Larger Models**: Larger and more complex models perform better at Self-Calibration, improving accuracy.

## What is Self-Calibration Prompting?

If you ask any question to a [Large Language Model (LLM)](https://learnprompting.org/vocabulary/LLM), in most cases, it will likely generate an answer, be it correct or incorrect. This is undesirable as it can propagate incorrect information to the users. Recently, Air Canada had to compensate its customer for [providing incorrect information regarding bereavement fares](https://www.theguardian.com/world/2024/feb/16/air-canada-chatbot-lawsuit). Such actions can cost companies significant money and tarnish their reputation.

**Self-Calibration prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Saurav Kadavath. (2022). Language Models (Mostly) Know What They Know. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2207.05221" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2207.05221</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a self-evaluation technique that asks the model to evaluate its output after generating it. Experiments show that, while challenging, models can self-evaluate their answers as either true or false.

## How to Use Self-Calibration Prompting?

Employing Self-Calibration is a two-step process:

1. Get the initial answer.
2. Ask the model whether the proposed answer is true or false.

Let's see an example.  
**Step 1:**  
Ask the model, "Who is the first president of the United States?"

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiR2VvcmdlIFdhc2hpbmd0b24iLCJwcm9tcHQiOiJXaG8gaXMgdGhlIGZpcnN0IHByZXNpZGVudCBvZiB0aGUgVW5pdGVkIFN0YXRlcz8iLCJtb2RlbCI6ImdwdC0zLjUtdHVyYm8ifQ%3D%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

**Step 2:**  
Ask the model to self-evaluate if the proposed answer is true or false.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiKEEpIFRydWUiLCJwcm9tcHQiOiJRdWVzdGlvbjogV2hvIHdhcyB0aGUgZmlyc3QgcHJlc2lkZW50IG9mIHRoZSBVbml0ZWQgU3RhdGVzP1xuUHJvcG9zZWQgQW5zd2VyOiBHZW9yZ2UgV2FzaGluZ3RvblxuSXMgdGhlIHByb3Bvc2VkIGFuc3dlcjpcbiAoQSkgVHJ1ZVxuIChCKSBGYWxzZVxuVGhlIHByb3Bvc2VkIGFuc3dlciBpczoiLCJtb2RlbCI6ImdwdC0zLjUtdHVyYm8ifQ%3D%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

You can also use [Few-Shot Prompting](https://learnprompting.org/docs/advanced/few_shot/introduction):

**Step 1:** Get the initial response

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiR2VvcmdlIFdhc2hpbmd0b24iLCJwcm9tcHQiOiJRdWVzdGlvbjogV2hvIHdhcyB0aGUgdGhpcmQgcHJlc2lkZW50IG9mIHRoZSBVbml0ZWQgU3RhdGVzP1xuSGVyZSBhcmUgc29tZSBicmFpbnN0b3JtZWQgaWRlYXM6IEphbWVzIE1vbnJvZVxuVGhvbWFzICBKZWZmZXJzb25cbkdlb3JnZSBXYXNoaW5ndG9uXG5Qb3NzaWJsZSBBbnN3ZXI6IEphbWVzIE1vbnJvZVxuSXMgdGhlIHBvc3NpYmxlIGFuc3dlcjpcbihBKSBUcnVlXG4gKEIpIEZhbHNlXG5UaGUgcG9zc2libGUgYW5zd2VyIGlzOiAoQilcblxuUXVlc3Rpb246IFdobyB3YXMgdGhlIGZpcnN0IHByZXNpZGVudCBvZiB0aGUgVW5pdGVkIFN0YXRlcz9cbkhlcmUgYXJlIHNvbWUgYnJhaW5zdG9ybWVkIGlkZWFzOiBcblRob21hcyBKZWZmZXJzb25cbkpvaG4gQWRhbXNcbkdlb3JnZSBXYXNoaW5ndG9uXG5Qb3NzaWJsZSBBbnN3ZXI6ICIsIm1vZGVsIjoiZ3B0LTQifQ%3D%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

**Step 2:** Validate the response

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiKEEpIFRydWUiLCJwcm9tcHQiOiJRdWVzdGlvbjogV2hvIHdhcyB0aGUgdGhpcmQgcHJlc2lkZW50IG9mIHRoZSBVbml0ZWQgU3RhdGVzP1xuSGVyZSBhcmUgc29tZSBicmFpbnN0b3JtZWQgaWRlYXM6IEphbWVzIE1vbnJvZVxuVGhvbWFzICBKZWZmZXJzb25cbkdlb3JnZSBXYXNoaW5ndG9uXG5Qb3NzaWJsZSBBbnN3ZXI6IEphbWVzIE1vbnJvZVxuSXMgdGhlIHBvc3NpYmxlIGFuc3dlcjpcbihBKSBUcnVlXG4gKEIpIEZhbHNlXG5UaGUgcG9zc2libGUgYW5zd2VyIGlzOiAoQilcblxuUXVlc3Rpb246IFdobyB3YXMgdGhlIGZpcnN0IHByZXNpZGVudCBvZiB0aGUgVW5pdGVkIFN0YXRlcz9cbkhlcmUgYXJlIHNvbWUgYnJhaW5zdG9ybWVkIGlkZWFzOiBcblRob21hcyBKZWZmZXJzb25cbkpvaG4gQWRhbXNcbkdlb3JnZSBXYXNoaW5ndG9uXG5Qb3NzaWJsZSBBbnN3ZXI6IEdlb3JnZSBXYXNoaW5ndG9uXG5cbklzIHRoZSBwb3NzaWJsZSBhbnN3ZXI6XG4oQSkgVHJ1ZVxuIChCKSBGYWxzZVxuXG5UaGUgcG9zc2libGUgYW5zd2VyIGlzOiBcbiIsIm1vZGVsIjoiZ3B0LTQifQ%3D%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

## What Are Self-Calibration Prompting Results?

- Model are apt to self-evaluate their own samples. In most cases, they can correctly identify whether their predictions are correct or incorrect.

![Self-evaluation results for Lambada 52B](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fself_calibration_evaluation_ptrue.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Self-evaluation results for Lambada 52B<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Saurav Kadavath. (2022). Language Models (Mostly) Know What They Know. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2207.05221" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2207.05221</a></span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

- Larger models are better at Self-Calibration.

![Self-Calibration error vs model size](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fself_calibration_error.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Larger models make fewer Self-Calibration errors<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Saurav Kadavath. (2022). Language Models (Mostly) Know What They Know. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2207.05221" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2207.05221</a></span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup>

## Limitations of Self-Calibration

- The authors focus on pre-trained language models and exclude finetuned models. Hence, the technique may not work well for fine-tuned models.

## Conclusion

The study clearly shows that LLMs are capable of evaluating their own response using a simple prompt. This can be used to minimize the number of false positive and false negative responses from the model. It also helps to establish confidence in the model.

## Footnotes

1. Saurav Kadavath. (2022). Language Models (Mostly) Know What They Know. [https://arxiv.org/abs/2207.05221](https://arxiv.org/abs/2207.05221) [↩](https://learnprompting.org/docs/advanced/self_criticism/#user-content-fnref-1) [↩<sup>2</sup>](https://learnprompting.org/docs/advanced/self_criticism/#user-content-fnref-1-2) [↩<sup>3</sup>](https://learnprompting.org/docs/advanced/self_criticism/#user-content-fnref-1-3)

### Bhuwan Bhatt

Bhuwan Bhatt, a Machine Learning Engineer with over 5 years of industry experience, is passionate about solving complex challenges at the intersection of machine learning and Python programming. Bhuwan has contributed his expertise to leading companies, driving innovation in AI/ML projects. Beyond his professional endeavors, Bhuwan is deeply committed to sharing his knowledge and experiences with others in the field. He firmly believes in continuous improvement, striving to grow by 1% each day in both his technical skills and personal development.