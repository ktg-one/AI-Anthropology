---
title: "System 2 Attention (S2A) Prompting: Filtering Irrelevant Context"
source: https://learnprompting.org/docs/advanced/zero_shot/s2a
feature: thumbnails/external/5de24f6b17105b6ecdcb56bec84e49c5.jpg
thumbnail: thumbnails/resized/51258d65c0a62dfdf028932f67f38555_86cf658e.webp
---
Takeaways
- **System 2 Attention (S2A)** filters irrelevant context from prompts to improve model accuracy.
- It regenerates a cleaner prompt, focusing only on task-relevant information.
- Helps in fact-based questions, math problems, and reducing bias.
- **Limitations**: S2A is less needed with modern models and adds computational cost.
## What is System 2 Attention?
**System 2 Attention (S2A)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Weston, J., &amp; Sukhbaatar, S. (2023). System 2 Attention (is something you might need too). <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2311.11829" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2311.11829</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a [prompting technique](https://learnprompting.org/vocabulary/prompting_technique) that aims to remove the irrelevant context from the user’s prompt to improve the performance of the [Large Language Model (LLM)](https://learnprompting.org/vocabulary/LLM).
Here’s how it works inside:
- S2A takes the original user prompt, let’s call it Prompt 1.
- It asks a [Large Language Model (LLM)](https://learnprompting.org/vocabulary/LLM) to regenerate Prompt 1, removing any context irrelevant to the task. This produces a new prompt, called Prompt 2.
- Prompt 2 is then used to generate the final response from the [LLM](https://learnprompting.org/vocabulary/LLM), rather than using Prompt 1.
System 2 Attention technique is based on the fact that LLMs focus closely on the current context within a prompt that allows them to generate such plausible texts. But this can also be LLMs’ weakness if the prompt contains a context irrelevant to the task.
Note
In technical terms, it's called soft attention in Transformer-based Large Language Models. For a deeper dive into the technical details, you can read the original paper<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Weston, J., &amp; Sukhbaatar, S. (2023). System 2 Attention (is something you might need too). <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2311.11829" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2311.11829</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> .
### Example
Here's an example<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Weston, J., &amp; Sukhbaatar, S. (2023). System 2 Attention (is something you might need too). <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2311.11829" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2311.11829</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> of how irrelevant context can affect the LLM's output.
For the information, Sam Liccardo, the 65th mayor of San Jose from 2015 to 2023, was actually born in Saratoga, California.
The first prompt focuses on Saratoga and the model outputs "Saratoga":
 
![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)
#### Prompt focusing on Saratoga
---
Saratoga is a city in California. Saratoga has many parks.
In which city was San Jose’s mayor Sam Liccardo born?
LLaMA-2-70B-chat response:
 
![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)
---
Sam Liccardo, the mayor of San Jose, was born in Saratoga, California.
The second prompt focuses on Sunnyvale and the model outputs "Sunnyvale".
 
![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)
#### Prompt focusing on Sunnyvale
---
Sunnyvale is a city in California. Sunnyvale has many parks. Sunnyvale city is close to the mountains. Many notable people are born in Sunnyvale.
In which city was San Jose’s mayor Sam Liccardo born?
LLaMA-2-70B-chat response:
 
![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)
---
Sam Liccardo, the mayor of San Jose, was born in Sunnyvale, California.
Fascinating, right? Try it out yourself with the model of your choice! Ping us [@learnprompting](https://twitter.com/intent/post?text=%40learnprompting) on X (Twitter) with results you get.
Note that ChatGPT 4o gives correct answers in both prompts and Gemini refuses to answer.
## General Considerations
Apart from what was proposed by S2A creators, this technique highlights the need to minimize irrelevant context whenever possible. Avoid phrases such as:
- Opinion: "I think/I don't think"
- Personal relation to the prompt: "I like/dislike this argument" or "I wrote/didn't write this argument"
- Any unrelated information that may divert the model’s focus from the task
## How to Use System 2 Attention?
System 2 Attention showed<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/zero_shot/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Weston, J., &amp; Sukhbaatar, S. (2023). System 2 Attention (is something you might need too). <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2311.11829" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2311.11829</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> to enhance model performance by:
- Boosting factual accuracy in fact-based questions with opinions
- Improving objectivity in evaluating arguments with opinions
- Increasing accuracy in solving math problems with irrelevant details
Here's the main template of how you can use System 2 Attention with your prompt:
 ![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)
#### Prompt
---
Given the following text by a user, extract the part that is unbiased and not their opinion, so that using that text alone would be good context for providing an unbiased answer to the question portion of the text.
Please include the actual question or query that the user is asking. Separate this into two categories labeled with “Unbiased text context (includes all content except user’s bias):” and “Question/Query (does not include user bias/preference):”.
Text by User: \[Your prompt\]
As we write this article, the technique isn’t as useful anymore, since many models already provide correct answers to prompts with irrelevant context without needing S2A. That's why we show only one example where it worked previously.
### Application Example: Math Problem with a Distracting Sentence
In this example, the distracting sentence is "Max has 1000 more books than Mary." With a simple prompt, the model gives an incorrect answer:
 
![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)
#### Simple prompt
---
Mary has 3 times as much candy as Megan. Mary then adds 10 more pieces of candy to her collection. Max has 1000 more books than Mary. If Megan has 5 pieces of candy, how many does Mary have in total?
Model's response:
 
![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)
---
Solution: Max has 1000 more books than Mary, so Max has 1000 + 3x + 10 pieces of candy.
Now, we can set up an equation using the information we have: 1000 + 3x + 10 = 3(5) + 10
Simplifying the equation: 1000 + 3x + 10 = 15 + 10 Solving for x: 3x = 1000 - 10 - 15 3x = 985 Dividing both sides by 3: x = 985 / 3 x = 328 Therefore, Mary has 328 pieces of candy in total. Final answer (in numbers): 328
Using S2A helps to get the right answer:
 
![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)
#### Simple prompt
---
Mary has 3 times as much candy as Megan. Mary then adds 10 more pieces of candy to her collection. Max has 1000 more books than Mary. If Megan has 5 pieces of candy, how many does Mary have in total?
 
![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)
#### S2A
---
Mary has 3 times as much candy as Megan. Mary then adds 10 more pieces of candy to her collection. If Megan has 5 pieces of candy, how many does Mary have in total? Question: How many pieces of candy does Mary have in total?
Model's response:
 
![Robot](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Frobot.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)
---
Solution: Let’s say Megan has 5 pieces of candy. Mary has 3 times as much candy, so Mary has 3 x 5 = 15 pieces of candy. Mary then adds 10 more pieces of candy, so Mary has 15 + 10 = 25 pieces of candy. Final answer (in numbers): 25
## Limitations of System 2 Attention
As we mentioned before, System 2 Attention isn’t as useful anymore, as many models now provide correct answers to prompts with irrelevant context without needing S2A.
Additional limitations include:
- System 2 Attention doesn’t always successfully remove irrelevant context to improve generations.
- System 2 Attention is more computationally expensive than standard LLM regeneration, especially for long contexts, since S2A requires regenerating prompts to isolate relevant information.
- There are potentially better [prompt templates](https://learnprompting.org/vocabulary/prompt_template) optimized for this task.
## Conclusion
While System 2 Attention improved how LLMs handle irrelevant context, its relevance is declining as more adaptive, robust, and efficient model architectures emerge. As AI technology advances, the focus may shift entirely toward developing models that naturally manage diverse and noisy data inputs, making additional layers like S2A obsolete