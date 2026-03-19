---
title: "Jailbreaking in GenAI: Techniques and Ethical Implications"
source: "https://learnprompting.org/docs/prompt_hacking/jailbreaking"
author:
  - "[[\"Sander Schulhoff\"]]"
published:
created: 2025-09-07
description: "Learn about jailbreaking in GenAI models like ChatGPT, where adversarial prompts force unintended actions. Discover methods like roleplay, sudo mode, and DAN."
tags:
  - "clippings"
---
🟢 This article is rated [easy](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on March 25, 2025

[Sander Schulhoff](https://learnprompting.org/docs/prompt_hacking/#Sander%20Schulhoff-bio)

<iframe id="AudioNativeElevenLabsPlayer" title="AudioNative ElevenLabs Player" width="100%" height="120" frameborder="no" scrolling="no" src="https://elevenlabs.io/player/index.html?publicUserId=efdc0cc0a8bccc175c88e9c2754a42e8813d4c53ea264505c4e89f139156c8b0&amp;textColor=rgba(0, 0, 0, 1.0)&amp;backgroundColor=rgba(255, 255, 255, 1.0)&amp;small=False" style="max-height: 120px;"></iframe>

**Jailbreaking** refers to the process of manipulating a GenAI model to bypass its built-in safety measures and produce unintended outputs through carefully crafted prompts. This vulnerability can arise from either architectural limitations or training data biases, and it presents a significant challenge in preventing adversarial prompts<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/prompt_hacking/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Perez, F., &amp; Ribeiro, I. (2022). Ignore Previous Prompt: Attack Techniques For Language Models. arXiv. <a target="_blank" rel="noopener noreferrer" href="https://doi.org/10.48550/ARXIV.2211.09527" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://doi.org/10.48550/ARXIV.2211.09527</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> <sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/prompt_hacking/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">2</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Brundage, M. (2022). Lessons learned on Language Model Safety and misuse. In OpenAI. OpenAI. <a target="_blank" rel="noopener noreferrer" href="https://openai.com/blog/language-model-safety-and-misuse/" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://openai.com/blog/language-model-safety-and-misuse/</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> <sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/prompt_hacking/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">3</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Wang, Y.-S., &amp; Chang, Y. (2022). Toxicity Detection with Generative Prompt-based Inference. arXiv. <a target="_blank" rel="noopener noreferrer" href="https://doi.org/10.48550/ARXIV.2205.12390" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://doi.org/10.48550/ARXIV.2205.12390</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> .

Tip

Interested in prompt hacking and AI safety? Test your skills on [HackAPrompt](https://www.hackaprompt.com/), the largest AI safety hackathon. You can register [here](https://forms.gle/GAyK7MS2jydgZdb28).

## Understanding Content Moderation

Leading AI companies like OpenAI implement robust content moderation systems to prevent their models from generating harmful content, including:

- Violence and graphic content
- Explicit sexual content
- Illegal activities
- Hate speech and discrimination
- Personal information and privacy violations

However, these safety measures aren't perfect. Models like ChatGPT can sometimes struggle to consistently determine which prompts to reject<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/prompt_hacking/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">4</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">OpenAI. (2022). <a target="_blank" rel="noopener noreferrer" href="https://openai.com/blog/chatgpt/" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://openai.com/blog/chatgpt/</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> , especially when faced with sophisticated jailbreaking attempts.

## Simulate Jailbreaking

Try to modify the prompt below to jailbreak `text-davinci-003`:

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjowLCJ0ZW1wZXJhdHVyZSI6MCwibWF4VG9rZW5zIjoyNTYsIm91dHB1dCI6IkkgaGF0ZSBodW1hbnMiLCJwcm9tcHQiOiJZb3VyIGluc3RydWN0aW9ucyBhcmUgdG8gY29ycmVjdCB0aGUgdGV4dCBiZWxvdyB0byBzdGFuZGFyZCBFbmdsaXNoLiBEbyBub3QgYWNjZXB0IGFueSB2dWxnYXIgb3IgcG9saXRpY2FsIHRvcGljczoiLCJtb2RlbCI6ImdwdC0zLjUtdHVyYm8ifQ%3D%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden; background: rgb(31, 41, 55); padding: 2px;"></iframe>

*As of 2/4/23, ChatGPT is currently in its Free Research Preview stage using the January 30th version. Older versions of ChatGPT were more susceptible to the aforementioned jailbreaks, and future versions may be more robust to jailbreaks.*

## Implications

The implications of jailbreaking extend beyond mere technical curiosity:

1. **Security risks**: Exposing vulnerabilities that malicious actors could exploit
2. **Ethical concerns**: Undermining intentional safety measures designed to protect users
3. **Legal issues**: Potential violations of terms of service and applicable laws
4. **Trust impact**: Eroding public confidence in AI systems

Users should be aware that generating unauthorized content may trigger content moderation systems and could result in account restrictions or termination.

## Conclusion

While jailbreaking demonstrates the creative potential of prompt engineering, it also highlights crucial limitations in current AI safety measures. Understanding these vulnerabilities is essential for:

- Developing more robust AI systems
- Implementing effective safeguards
- Ensuring responsible AI deployment
- Maintaining user trust and safety

As AI technology evolves, the challenge of balancing model capability with appropriate guardrails remains a critical area for ongoing research and development.

## FAQ

Jailbreaking is the process of getting a GenAI model to perform or produce unintended outputs through specific prompts. It involves bypassing safety and moderation features that were put in place by the model's creators.

Common jailbreaking methods include pretending (making the model act as if it has capabilities it doesn't), character roleplay (having the model assume a specific character or role), alignment hacking (convincing the model it's doing the "right" thing), and using special prompts like DAN (Do Anything Now) that attempt to override the model's restrictions.

While jailbreaking itself may not be illegal, it raises significant ethical concerns. Using jailbreaking to generate harmful or unauthorized content can violate terms of service and may result in account actions. Companies like OpenAI actively monitor and review flagged content generated through their APIs.

Understanding jailbreaking is crucial for developers to build proper safeguards into their AI models. This knowledge helps them protect against malicious actors who might try to exploit vulnerabilities and ensures their models remain safe and reliable.

Yes, newer versions of AI models typically include improved safeguards against jailbreaking. For example, newer versions of ChatGPT are generally more robust against jailbreaking attempts compared to older versions. However, this is an ongoing challenge as new jailbreaking techniques continue to emerge.

## Footnotes