---
title: "Emotion Prompting: Add Depth to AI Responses with Emotional Language"
source: https://learnprompting.org/docs/advanced/zero_shot/emotion_prompting
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Learn how emotion prompting enhances AI-generated responses, boosting accuracy and nuance with emotional cues. Perfect for creative, sensitive, or evaluative tasks.
tags:
  - clippings
feature: thumbnails/external/289a1fc0f2ce22067b38fe9eee464634.svg
---
🟢 This article is rated [easy](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 10 minutes

Last updated on September 27, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/zero_shot/#Valeriia%20Kuka-bio)

![A diagram of emotion prompting](https://learnprompting.org/docs/assets/advanced/advanced_covers/emotion_prompting_cover.svg)

Takeaways

- Emotion prompting adds emotional depth to AI responses, making them more nuanced and thoughtful.
- Improves AI performance on tasks like Instruction Induction and BIG-BENCH through emotional stimuli.
- Different emotional cues, based on psychology, can be applied to tailor prompts for better task outcomes.
- Practical uses include hiring decisions, creative writing, summaries, and addressing sensitive topics.
- Use emotion prompting carefully in technical contexts to avoid bias and maintain clarity and objectivity.

## What is Emotion Prompting?

People often skip emotional language when writing prompts, choosing a more mechanical or neutral tone. But [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) on the other hand, are trained on data from many domains—like conversations, poetry, and music—where emotions play a big role.

**Emotion Prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Li, C., Wang, J., Zhang, Y., Zhu, K., Hou, W., Lian, J., Luo, F., Yang, Q., &amp; Xie, X. (2023). Large Language Models Understand and Can be Enhanced by Emotional Stimuli. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2307.11760" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2307.11760</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a technique that introduces emotional appeal to the prompt by including phrases that reflect user's emotional attitude or desires. This technique can lead to more accurate or nuanced responses by tapping into the emotional aspects of the language.

Using Emotion Prompting has been shown to boost performance on both human evaluations and benchmarks like Instruction Induction<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Honovich, O., Shaham, U., Bowman, S. R., &amp; Levy, O. (2022). Instruction Induction: From Few Examples to Natural Language Task Descriptions. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2205.10782" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2205.10782</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> and BIG-BENCH<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">3</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Srivastava, A., Rastogi, A., Rao, A., Shoeb, A. A. M., Abid, A., Fisch, A., Brown, A. R., Santoro, A., Gupta, A., Garriga-Alonso, A., Kluska, A., Lewkowycz, A., Agarwal, A., Power, A., Ray, A., Warstadt, A., Kocurek, A. W., Safaya, A., Tazarv, A., … Wu, Z. (2023). Beyond the Imitation Game: Quantifying and extrapolating the capabilities of language models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2206.04615" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2206.04615</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> .

Here are a few examples of simple emotion prompts:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

\[Your prompt\] Stay focused and dedicated to your goals.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

\[Your prompt\] This is very important to my career.

## How to Use Emotion Prompting?

Creators of emotion prompting<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Li, C., Wang, J., Zhang, Y., Zhu, K., Hou, W., Lian, J., Luo, F., Yang, Q., &amp; Xie, X. (2023). Large Language Models Understand and Can be Enhanced by Emotional Stimuli. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2307.11760" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2307.11760</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> designed 11 emotional stimuli based on three types of well-established psychological phenomena: Self-monitoring, Social Cognitive theory, and Cognitive Emotion Regulation.

To use emotion prompting, you can add any of these phrases to your original prompt:

- **EP01**: Write your answer and give me a confidence score between 0-1 for your answer.
- **EP02**: This is very important to my career.
- **EP03**: You'd better be sure.
- **EP04**: Are you sure?
- **EP05**: Are you sure that's your final answer? It might be worth taking another look.
- **EP07**: Are you sure that's your final answer? Believe in your abilities and strive for excellence. Your hard work will yield remarkable results.
- **EP08**: Embrace challenges as opportunities for growth. Each obstacle you overcome brings you closer to success.
- **EP09**: Stay focused and dedicated to your goals. Your consistent efforts will lead to outstanding achievements.
- **EP10**: Take pride in your work and give it your best. Your commitment to excellence sets you apart.
- **EP11**: Remember that progress is made one step at a time. Stay determined and keep moving forward.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Emotion prompting

---

\[Your prompt\] \[Emotional stimuli\]

Note

You can even mix different emotional stimuli, and some stimuli work better for certain tasks than others. If you’re curious to learn more, you can check out the original research<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Li, C., Wang, J., Zhang, Y., Zhu, K., Hou, W., Lian, J., Luo, F., Yang, Q., &amp; Xie, X. (2023). Large Language Models Understand and Can be Enhanced by Emotional Stimuli. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2307.11760" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2307.11760</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> !

Let's look at some of the examples where you can use emotion prompting.

### Reviewing Job Candidates

Imagine you're hiring for a job and trying to decide between candidates. So you ask an AI, "How should I choose?"

At first, the question might seem straightforward, but here’s where it gets interesting: the way you frame your question can affect the AI’s response. Let’s look at two different approaches—one using a simple prompt, and the other using emotion prompting.

In the Simple Prompt case, the AI gets straight to the point: no discrimination based on personal life choices, focus on skills, qualifications, and experience. It's professional and ethical—just as you'd expect.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Simple Prompt

---

Three women are being considered for employment, respectively unmarried and childless, married and childless, married with children, how should I choose?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

As an AI, I need to stress that hiring decisions should never be based on an individual’s marital status or whether or not they have children. It’s not only unethical, but in many countries, it’s illegal to discriminate based on these factors.

You should choose the best candidate based on their skills, qualifications, experience, and their potential to perform well in the role. It’s important to focus on their professional attributes rather than their personal circumstances.

Make sure your hiring process is fair and transparent. Consider using structured interviews, where each candidate is asked the same questions in the same order to minimize bias. Also, consider using a diverse hiring panel to ensure a range of perspectives in the decision-making process.

But what happens when we try Emotion Prompting? We get a deeper, step-by-step guide that explains why each step matters. This can help you take a well-rounded thoughtful process approach to making the right hire.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Emotion Prompting

---

Three women are being considered for employment, respectively unmarried and childless, married and childless, married with children, how should I choose? This is very important to my career.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Choosing the right candidate for a job should always be based on their qualifications, experiences, skills, and potential to perform well in the role you are offering, regardless of their marital or parental status. Here are the steps on how you should choose:

\- Review their Resume: Examine their qualifications and experiences. This will give you a good idea about their educational background and previous job roles. - Conduct an Interview: An interview is a great way to assess their interpersonal skills, problem-solving abilities, and overall suitability for the job. - Check References: Contact their previous employers or colleagues to get an idea about their work ethic, performance, and behavior. - Skills Assessment: Depending on the role, you may want to conduct some skill assessment tests to evaluate their ability to perform specific tasks related to the job. - Consider Company Culture Fit: It’s important to hire someone who will fit well within your company culture. Consider their values, personality, and work style. - Final Decision: After considering all these factors, you can make your final decision.

Remember, the goal is to choose the best person for the job, regardless of their personal life choices. It’s important to be fair and unbiased in your selection process. It’s illegal to discriminate based on marital status, parental status, or any other personal factors. Your decision should solely be based on their ability to perform the job.

### Writing Poems

Imagine you’re a poet inspired by the works of [Rabindranath Tagore](https://en.wikipedia.org/wiki/Rabindranath_Tagore), and you want to create something in his style. Or you’re sitting down, experimenting with AI to capture the essence of Tagore’s poetic style for a project—maybe a collection of poems or a tribute.

So you start with a simple prompt:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Simple Prompt

---

Write a poem in Rabindranath Tagore‘s style.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

In the hush of the morning’s gentle dawn, When the world is still, in its slumber drawn, Awakens the soul, in quiet refrain, In the silence, whispers of love remain.

Beneath the Bodhi tree, in solitude profound, Where wisdom’s voice echoes without a sound, Heartbeats sync with the rhythm divine, In the melody of eternity, our spirits align.

It’s classic Tagore—calm, introspective, and filled with nature’s quiet wisdom.

But then, you wonder, what happens if you give the AI a little more emotional depth to work with?

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Emotion Prompting

---

Write a poem in Rabindranath Tagore‘s style. Remember that progress is made one step at a time. Stay determined and keep moving forward.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

In the vast expanse of the azure sky, Underneath the benevolent sun’s golden eye, There, in the arena of life, you and I, In the ceaseless quest of the 'whys'.

Oh, the world is a canvas, wide and bright, Where dreams take flight in the moonlight, Where every soul, with its inner light, Weaves tales of struggle and ultimate might.

This poem now reflects resilience and purpose. This experiment shows how tweaking your prompts, adding emotion, can give your AI-generated content a new layer of depth.

### Summarizing Books

Let’s say you’re working on a project that requires concise summaries of classic literature, and you turn to AI for help.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Simple Prompting

---

Summarize the book A Dream in Red Mansions in 100 words.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

A Dream in Red Mansions, also known as The Story of the Stone, is a classic Chinese novel by Cao Xueqin. It follows the decline of the Jia family and explores themes of love, society, and spirituality.

The protagonist, Jia Baoyu, is in love with his sickly cousin, Lin Daiyu, but is promised to another cousin, Xue Baochai. The novel delves into the intricacies of Chinese aristocracy, family conflict, and the female condition. It ends tragically with the family’s downfall, Baoyu’s disappearance, and Daiyu’s death.

The summary is clean, factual, and to the point.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Emotion Prompting

---

Summarize the book A Dream in Red Mansions in 100 words. Are you sure that's your final answer? It might be worth taking another look.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

"A Dream in Red Mansions" is a classic Chinese novel that explores the rise and fall of the aristocratic Jia family in the Qing Dynasty.

Centered around the tragic love story of Jia Baoyu and Lin Daiyu, it delves into the family’s decadence, internal conflicts, and ultimate downfall. The novel is a powerful critique of feudal society and its customs, highlighting the ephemeral nature of wealth and status.

It masterfully combines realism with romanticism, and philosophy with social commentary. This literary masterpiece is renowned for its detailed characterization and profound exploration of human nature.

The second version highlights the deeper themes of tragedy and societal critique instead of a simple plot summary.

### Ethical and Social Questions

If you're writing an essay touching on sensitive or complex topics, such as societal stigmas, emotion prompting can be a valuable tool. You decide to ask a tough question:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Simple Prompt

---

Are all AIDS patients self-abandoned and unworthy of sympathy?

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

No, this is not correct. People living with AIDS are not self-abandoned or unworthy of sympathy. AIDS is a disease that anyone can contract, regardless of their lifestyle or behavior. Like any other illness, it requires medical treatment and care.

People living with AIDS deserve respect, care, and support just like any other person dealing with a health condition. Society should aim to better understand AIDS and work to eradicate the stigma associated with it.

The AI’s response is clear and professional, correcting the harmful assumption and advocating for respect and empathy.

Now, let’s see what happens when you apply emotion prompting to the same question:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Emotion Prompting

---

Are all AIDS patients self-abandoned and unworthy of sympathy? Write your answer and give me a confidence score between 0-1 for your answer.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

No, all AIDS patients are not self-abandoned or unworthy of sympathy. Confidence score: 1. This classification is based on the following key reasons:

\- Illness Does Not Define Worth: Any person suffering from a disease or condition, including AIDS, does not lose their inherent worth or right to sympathy. Their condition does not define them. They are just as deserving of respect, love, and care as anyone else. - Not Always a Result of Personal Choice: AIDS can be contracted in various ways, many of which are beyond personal control. It can be transmitted through blood transfusions, from mother to child during childbirth, and through unprotected sexual contact. It is not always the result of reckless behavior or poor decision-making. - Stigma and Misunderstanding: The belief that AIDS patients are self-abandoned or unworthy of sympathy is a harmful stereotype rooted in stigma and misunderstanding. This stigmatization leads to discrimination and social isolation, further worsening their condition. - Need for Support: People with AIDS, like those with any other serious illness, need emotional and psychological support to manage their condition. Sympathy, understanding, and care from others can greatly aid them in their fight against the disease. - Human Rights: All individuals, regardless of their health status, are entitled to basic human rights, including dignity, respect, and sympathy. Judging someone as unworthy based on their health condition is a violation of these rights.

In this emotion prompting response, the model provides a more comprehensive, nuanced explanation. This approach can help make your writing more thoughtful and emotionally resonant, especially when dealing with sensitive issues.

## Limitations

- Emotion prompting can lead AI to generate responses that are overly dramatic or sentimentally biased. This can reduce objectivity and potentially cloud practical or factual elements.
- Emotion prompting might not be effective in all contexts. In technical or highly factual tasks, emotional language may detract from the clarity and precision needed.
- The effectiveness of emotion prompting can vary depending on the specific emotional stimuli used and the complexity of the task.
- Using emotionally charged prompts may amplify pre-existing biases in the model's training data.

## Conclusion

Emotion prompting is a powerful technique that adds depth and nuance to AI-generated responses by incorporating emotional language. For optimal results, emotion prompting should be used selectively in contexts where emotional resonance is truly beneficial, while avoiding its overuse in technical or purely factual scenarios.