---
title: "Role Prompting: Guide LLMs with Persona-Based Tasks"
source: https://learnprompting.org/docs/advanced/zero_shot/role_prompting
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-07
description: Master role prompting in AI to enhance style, accuracy, and depth in LLM outputs. Learn best practices, understand limitations, and optimize your language model interactions effectively.
tags:
  - clippings
feature: thumbnails/external/5aa2de717607ccc4b0a8ac6ff5f43d85.svg
---
🟢 This article is rated [easy](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 10 minutes

Last updated on September 27, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/zero_shot/#Valeriia%20Kuka-bio)

![A diagram of role prompting technique](https://learnprompting.org/docs/assets/advanced/advanced_covers/role_prompting_cover.svg)

  

Takeaways

- **Role Prompting** assigns a persona to an [LLM](https://learnprompting.org/vocabulary/LLM), such as "teacher" or "salesperson," to guide the style, tone, and focus of responses.
- **Enhances text clarity and accuracy** by aligning the response with the role, improving task performance in reasoning and explanation.
- **Useful for a wide range of tasks** like writing, reasoning, and dialogue-based applications, and can customize responses to fit specific contexts.
- **Best practices** include using non-intimate roles, gender-neutral terms, and a two-step approach for better results.
- **Limitations**: Role prompting can reinforce stereotypes and depends heavily on the quality of the role representation in the model's training data.

In the Basics Section we already covered [Role Prompting](https://learnprompting.org/docs/basics/roles). If you want you can start there. Now, we'll dive into a more advanced discussion.

## What is Role Prompting?

If you’re interested in prompting, you’ve probably already come across this technique many times when finding prompt templates for different applications. Most of them start with: “I want you to act as …” or “You’re a …”

This act of assigning a role to a [Large Language Model (LLM)](https://learnprompting.org/vocabulary/LLM) you’re prompting is called **role prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Zheng, M., Pei, J., &amp; Jurgens, D. (2023). Is “A Helpful Assistant” the Best Role for Large Language Models? A Systematic Evaluation of Social Roles in System Prompts. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2311.10054" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2311.10054</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> <sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wang, Z. M., Peng, Z., Que, H., Liu, J., Zhou, W., Wu, Y., Guo, H., Gan, R., Ni, Z., Yang, J., Zhang, M., Zhang, Z., Ouyang, W., Xu, K., Huang, S. W., Fu, J., &amp; Peng, J. (2024). RoleLLM: Benchmarking, Eliciting, and Enhancing Role-Playing Abilities of Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2310.00746" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2310.00746</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> or **role-play prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">3</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Kong, A., Zhao, S., Chen, H., Li, Q., Qin, Y., Sun, R., &amp; Zhou, X. (2023). Better Zero-Shot Reasoning with Role-Play Prompting. ArXiv, abs/2308.07702. <a target="_blank" rel="noopener noreferrer" href="https://api.semanticscholar.org/CorpusID:260900230" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://api.semanticscholar.org/CorpusID:260900230</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> or **persona prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">4</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Schmidt, D. C., Spencer-Smith, J., Fu, Q., &amp; White, J. (2023). Cataloging Prompt Patterns to Enhance the Discipline of Prompt Engineering. <a target="_blank" rel="noopener noreferrer" href="https://api.semanticscholar.org/CorpusID:257368147" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://api.semanticscholar.org/CorpusID:257368147</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> <sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">5</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wang, Z., Mao, S., Wu, W., Ge, T., Wei, F., &amp; Ji, H. (2024). Unleashing the Emergent Cognitive Synergy in Large Language Models: A Task-Solving Agent through Multi-Persona Self-Collaboration. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2307.05300" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2307.05300</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> . Here is an example of using role prompting:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

You are a historian. Explain the significance of the Industrial Revolution.

In this prompt, the role is "historian". Other examples of roles include occupational roles like “plumber,” “therapist” or interpersonal “friend,” “mother,” or “supervisor”. You can find other examples of roles in the table<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Zheng, M., Pei, J., &amp; Jurgens, D. (2023). Is “A Helpful Assistant” the Best Role for Large Language Models? A Systematic Evaluation of Social Roles in System Prompts. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2311.10054" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2311.10054</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> below:

| **Category** | **Examples** |
| --- | --- |
| **Family** | mother (mom, mum, mommy), father (dad, papa, daddy), son, daughter, etc. |
| **School** | student, professor, tutor, instructor, etc. |
| **Romantic** | partner, husband, wife, etc. |
| **Work** | coworker, supervisor, colleague, boss |
| **Social** | friend, best friend, stranger, buddy, etc. |
| **AI** | AI language model, Policy Analysis AI, Medical Diagnostic AI, etc. |
| **Occupations** | driver, accountant, banker, dentist, etc. |

## How to Use Role Prompting?

One obvious use case for role prompting is text styling and imitation<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">6</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Reynolds, L., &amp; McDonell, K. (2021). Prompt Programming for Large Language Models: Beyond the Few-Shot Paradigm. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2102.07350" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2102.07350</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> . Interestingly, recent studies<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Zheng, M., Pei, J., &amp; Jurgens, D. (2023). Is “A Helpful Assistant” the Best Role for Large Language Models? A Systematic Evaluation of Social Roles in System Prompts. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2311.10054" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2311.10054</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> <sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">3</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Kong, A., Zhao, S., Chen, H., Li, Q., Qin, Y., Sun, R., &amp; Zhou, X. (2023). Better Zero-Shot Reasoning with Role-Play Prompting. ArXiv, abs/2308.07702. <a target="_blank" rel="noopener noreferrer" href="https://api.semanticscholar.org/CorpusID:260900230" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://api.semanticscholar.org/CorpusID:260900230</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> have shown that role prompting can also enhance the performance of prompted models in tasks such as reasoning.

In the following sections, we'll demonstrate how to leverage role prompting for each of these goals.

### Style Imitation

Here, we make the AI imitate the writing style of a person.

This can be used to change the tone, style, and even the depth of the information presented.

#### Email Drafting

Imagine you need to write an outreach email to a potential marketing partner, and it's your first time doing it.

You go to your favorite LLM for help. Here's what you'll get if you write a simple prompt:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Write a quick outreach email to \[person\] about partnering up.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Subject: Exploring Partnership Opportunities

Hi \[Person's Name\],

I hope this email finds you well. I’m reaching out to explore potential collaboration opportunities between our teams. I believe there’s a strong alignment between our goals and expertise, and I’m confident we could create something impactful together.

I’d love to set up a time to discuss how we can partner up and bring value to both of our organizations.

Looking forward to hearing your thoughts!

Compare this to the result you could get with role prompting:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

You are a salesperson. Write a quick outreach email to \[person\] about partnering up.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Subject: Let's Discuss a Potential Partnership Opportunity

Hi \[Person's Name\],

I’m \[Your Name\] from \[Your Company\], and I wanted to reach out because I see a great opportunity for us to collaborate. Our products/services align well with what you’re doing at \[Their Company\], and I believe that by partnering, we can achieve even greater results together.

I’d love to chat about how we can create value for both of our businesses. Are you available for a quick call sometime this week?

Looking forward to your response.

You can make your communication more business-like and action-driven. This can help the person on the other end see that you get them and can speak their language. You can even customize your prompt based on the recipient's occupation or the individual most competent for the task.

#### Concept Explanation

Picture another example. Your boss mentioned a new concept for you, [API](https://learnprompting.org/vocabulary/api). And you don't have the time to read through explanatory articles. So you ask an LLM.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Quickly explain what an API is.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

An API (Application Programming Interface) is a set of rules and protocols that allows different software applications to communicate with each other. It defines how requests and responses should be formatted, enabling one program to access the features or data of another program without needing to understand its internal workings. APIs are essential for integrating different systems and enabling them to work together, often used for things like retrieving data, accessing services, or interacting with software components.

Sounds good, but can be hard to understand as there are still some unknown concepts like "features of a program" and "program" itself. Let's try role prompting:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

You're a teacher. Quickly explain what an API is.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

An API, or Application Programming Interface, is like a menu in a restaurant. It lists what you can do with a program or service, and how to ask for it. Just like you don't need to know how the kitchen cooks your meal, you don't need to know how the program works inside—just how to ask for what you want using the API. It makes it easy for different apps or websites to talk to each other and share information.

Looks more comprehensive and digestible. Now the LLM also included an analogy with a menu in a restaurant which is very helpful to grasp the key idea of the API.

Researchers also tried out framing prompts as a teacher-student dialogue instead of just telling an LLM to be thorough and simple<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">6</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Reynolds, L., &amp; McDonell, K. (2021). Prompt Programming for Large Language Models: Beyond the Few-Shot Paradigm. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2102.07350" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2102.07350</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> . They found that this approach leads to more stable and consistent outputs from the model.

#### Writing an Entertaining Story

Your toddler likes to read Joanne Rowling and have already read all the [bibliography](https://learnprompting.org/docs/bibliography). You can ask to an LLM imitate Joanne Rowling's style and write a short story. Here's the prompt you can try yourself to compare results.

Simple prompt:

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiIiwicHJvbXB0IjoiV3JpdGUgYSBzaG9ydCBzdG9yeSBmb3IgbXkgdG9kZGxlci4iLCJtb2RlbCI6ImdwdC0zLjUtdHVyYm8ifQ%3D%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

Role prompt:

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiIiwicHJvbXB0IjoiWW91IGFyZSBKb2FubmUgUm93bGluZy4gV3JpdGUgYSBzaG9ydCBzdG9yeSBmb3IgbXkgdG9kZGxlci4iLCJtb2RlbCI6ImdwdC0zLjUtdHVyYm8ifQ%3D%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

### Enhanced LLM Accuracy

Role prompting can be used to improve accuracy on certain problems, like general world knowledge<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Zheng, M., Pei, J., &amp; Jurgens, D. (2023). Is “A Helpful Assistant” the Best Role for Large Language Models? A Systematic Evaluation of Social Roles in System Prompts. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2311.10054" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2311.10054</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> and reasoning<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">3</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Kong, A., Zhao, S., Chen, H., Li, Q., Qin, Y., Sun, R., &amp; Zhou, X. (2023). Better Zero-Shot Reasoning with Role-Play Prompting. ArXiv, abs/2308.07702. <a target="_blank" rel="noopener noreferrer" href="https://api.semanticscholar.org/CorpusID:260900230" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://api.semanticscholar.org/CorpusID:260900230</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> . While this statement is backed by some research, this area has not been studied enough, as we discussed in our article: [Is Role Prompting Effective?](https://learnprompting.org/blog/role_prompting)<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">7</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Schulhoff, S. V. (2024). Is Role Prompting Effective? <a target="_blank" rel="noopener noreferrer" href="https://learnprompting.org/blog/role_prompting" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://learnprompting.org/blog/role_prompting</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> .

Here are a few recommendations for creating role prompts that improve accuracy:

- Use non-intimate interpersonal roles: Non-intimate interpersonal roles yield better results than occupational roles, especially in settings such as schools, social environments, and workplaces.
- Use gender-neutral roles: Gender-neutral terms in prompts generally lead to better performance. Prompts with male roles often outperform those with female roles.
- Use audience or role prompt, don’t use interpersonal prompts:
	- Do: Audience prompt – You are talking to a/an \[role\]
	- Do: Role prompt – You are a/an \[role\]
	- Don’t: Interpersonal prompt – You are talking to your \[role\]
	- Don’t use imaginative constructs: Directly specifying the role or audience is more effective than prompting the model to "Imagine" the role
- Use a two-staged approach<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">3</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Kong, A., Zhao, S., Chen, H., Li, Q., Qin, Y., Sun, R., &amp; Zhou, X. (2023). Better Zero-Shot Reasoning with Role-Play Prompting. ArXiv, abs/2308.07702. <a target="_blank" rel="noopener noreferrer" href="https://api.semanticscholar.org/CorpusID:260900230" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://api.semanticscholar.org/CorpusID:260900230</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> :
	- First, assign a role to the model and add details of this role. Let the LLM write an output.
	- Second, write your question or task for the LLM.

We summarize these best practices in one example with an employee-boss setting and a task to craft an elevator pitch.

Step 1:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

You're an employee who thrives on generating new ideas and always knows how to present them effectively. I'm your boss, who listens to your ideas and decides whether to implement them.

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Great, let's play this out. I'll start by presenting a new idea, and you can provide feedback or decide on the next steps.

Step 2:

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

Craft an elevator pitch about \[your new project idea\].

 

![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### AI Output

---

Elevator Pitch:

Imagine our audience eagerly tuning in every week for a live, interactive session where they can ask experts anything about AI and [machine learning](https://learnprompting.org/vocabulary/Machine_Learning). Our new project, "AI Unplugged," is a weekly live Q&A that will be streamed on LinkedIn and Twitter. It’s more than just content; it’s a conversation. By inviting thought leaders and engaging directly with our community, we’ll establish ourselves as the go-to resource for cutting-edge insights and practical advice in the AI space. This is our chance to turn followers into loyal advocates by making our brand not just a source of information, but a part of their journey in AI.

### Expressing Complex Ideas and Subtle Behaviors

Invoking figures such as Mahatma Gandhi, Ayn Rand, or Eliezer Yudkowksy can subtly imply specific moral criteria without explicitly stating them<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">6</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Reynolds, L., &amp; McDonell, K. (2021). Prompt Programming for Large Language Models: Beyond the Few-Shot Paradigm. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2102.07350" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2102.07350</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> . This could have different applications, here are some of them:

- Educational chatbots offering advice based on the beliefs of figures like Gandhi, guiding students to explore various ethical perspectives.
- Chatbots engaging students in discussions that align with specific philosophical ideologies, helping them deepen their understanding of complex moral frameworks.
- As an opinion writer, you could frame your arguments by invoking principles associated with specific figures.

## Limitations of Role Prompting

How well role prompting works depends on how each role is encoded and represented in the LLM. If the role isn’t well-represented or is misrepresented in the training data, the model might respond inaccurately or inappropriately when prompted with that role.

Another limitation is in the data LLMs are trained on. Since LLMs learn from big datasets that can have biases, role prompting could accidentally reinforce stereotypes or biased behaviors. For example, if a role is often linked to certain traits or behaviors in the training data, the model might repeat those connections, even if they’re wrong or inappropriate.

The research that guides our best practices is limited by the number of roles checked and the specific models used. Keep this in mind as you continue, and be cautious of potential biases or misrepresentations when applying role prompting in your work.

## Conclusion

Role prompting is a powerful technique that guides LLM's behavior by assigning it specific roles, enhancing the style, accuracy, and depth of its outputs. Whether you're aiming for a certain tone, improving clarity, or eliciting complex and nuanced responses, role prompting can be of help. By adhering to best practices and being aware of potential pitfalls, you can fully leverage role prompting, making your interactions with language models more effective and tailored to your specific needs.

## Further Reading

This section highlights some of the latest research papers on role prompting, which propose more sophisticated systems in this area. Each paper warrants a separate review, but if you’re interested, feel free to dive into the further reading.

- "Evaluating Persona Prompting for Question Answering Tasks"<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">8</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Olea, C., Tucker, H., Phelan, J., Pattison, C., Zhang, S., Lieb, M., Schmidt, D., &amp; White, J. (2024). Evaluating Persona Prompting for Question Answering Tasks. Security, Privacy and Trust Management. <a target="_blank" rel="noopener noreferrer" href="https://api.semanticscholar.org/CorpusID:270819947" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://api.semanticscholar.org/CorpusID:270819947</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> proposes different strategies for composing prompts with role prompting and investigates how different persona styles influence the performance of LLMs, particularly in handling questions with varying levels of "openness." This "openness" refers to the number of correct answers and the various ways those answers can be expressed. The paper also proposes methods for auto-generating roles and introduces a roundtable setting where several agents each take on one role.
- "Role-Play Zero-Shot Prompting with Large Language Models for Open-Domain Human-Machine Conversation"<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">9</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Njifenjou, A., Sucal, V., Jabaian, B., &amp; Lefèvre, F. (2024). Role-Play Zero-Shot Prompting with Large Language Models for Open-Domain Human-Machine Conversation. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2406.18460" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2406.18460</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> proposes a general [prompt structure](https://learnprompting.org/docs/basics/prompt_structure) for role prompting consisting of system [instructions](https://learnprompting.org/docs/basics/instructions), situational context, response instructions, and conversation history, which can be tailored to different conversational tasks. The method allows LLMs to adopt roles that enhance their conversational abilities, such as empathy and engagement, effectively improving open-domain conversations in various languages, especially in French.
- "Large Language Models are Diverse Role-Players for Summarization Evaluation"<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">10</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wu, N., Gong, M., Shou, L., Liang, S., &amp; Jiang, D. (2023). Large Language Models are Diverse Role-Players for Summarization Evaluation. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2303.15078" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2303.15078</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> introduces a new framework called DRPE (Diverse Role-Player Evaluation) that utilizes role prompting to assess text summarization quality. It leverages LLMs to simulate various role-players, both static (objective) and dynamic (subjective), to evaluate summaries across multiple subjective dimensions such as coherence, grammar, and interestingness. This method outperforms traditional metrics like BLEU/ROUGE by better aligning with human evaluations.
- "Character is Destiny: Can Large Language Models Simulate Persona-Driven Decisions in Role-Playing?"<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">11</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Xu, R., Wang, X., Chen, J., Yuan, S., Yuan, X., Liang, J., Chen, Z., Dong, X., &amp; Xiao, Y. (2024). Character is Destiny: Can Large Language Models Simulate Persona-Driven Decisions in Role-Playing? <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2404.12138" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2404.12138</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> The paper explores the ability of LLMs to role-play and simulate persona-driven decision-making in complex scenarios, such as those found in novels. The authors introduce the NEXTDECISIONPREDICTION task and create the LIFECHOICE dataset, which includes key decision points from 1,401 characters in 395 books. The paper finds that while LLMs show promise in predicting decisions based on personas, there is room for improvement.
- "Persona is a Double-edged Sword: Enhancing the Zero-Shot Reasoning by [Ensembling](https://learnprompting.org/docs/reliability/ensembling) the Role-playing and Neutral Prompts"<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">12</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Kim, J., Yang, N., &amp; Jung, K. (2024). Persona is a Double-edged Sword: Enhancing the Zero-shot Reasoning by Ensembling the Role-playing and Neutral Prompts. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2408.08631" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2408.08631</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> explores how role-playing personas can both help and hinder reasoning in LLMs. It proposes a framework called "Jekyll & Hyde" that combines results from both persona-based and neutral prompts to enhance the robustness of LLMs in reasoning tasks.
- "Self-Prompt Tuning: Enable Autonomous Role-Playing in LLMs"<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">13</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Kong, A., Zhao, S., Chen, H., Li, Q., Qin, Y., Sun, R., Zhou, X., Zhou, J., &amp; Sun, H. (2024). Self-Prompt Tuning: Enable Autonomous Role-Playing in LLMs. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2407.08995" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2407.08995</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> introduces a method called self-prompt tuning, which allows LLMs to generate their own role-play prompts through [fine-tuning](https://learnprompting.org/vocabulary/fine-tuning). By fine-tuning models like Mistral-7B and Llama-2-7B on a newly created LIMA-Role dataset, the models can automatically generate expert role-play prompts for different tasks, leading to improved performance on a range of NLP benchmarks.