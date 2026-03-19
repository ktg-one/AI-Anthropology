---
title: "Program-Aided Language Models (PAL): Code-Driven Problem Solving"
source: https://learnprompting.org/docs/agents/pal
author:
  - '[["Sander Schulhoff"]]'
published:
created: 2025-09-08
description: Discover how PALs solve complex problems by generating code and using programmatic runtimes, contrasting with natural language reasoning in CoT.
tags:
  - clippings
feature: thumbnails/external/a7433c38dee9a8a10b6da78070fe6900.webp
thumbnail: thumbnails/resized/b073c1742e48c38fa83d102032e93e94_86cf658e.webp
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 2 minutes

Last updated on August 7, 2024

[Sander Schulhoff](https://learnprompting.org/docs/agents/#Sander%20Schulhoff-bio)

Takeaways

- **PAL Overview**: Program-Aided Language Models (PAL) enhance problem-solving by generating code to represent intermediate reasoning steps (contrast this with [CoT prompting](https://learnprompting.org/vocabulary/CoT_Prompting), which uses natural language to reason).

## What are Program-aided Language Models (PAL)?

**Program-aided Language Models (PAL)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/agents/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Gao, L., Madaan, A., Zhou, S., Alon, U., Liu, P., Yang, Y., Callan, J., &amp; Neubig, G. (2022). </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> are another example of a [Modular Reasoning, Knowledge, and Language (MRKL) system](https://learnprompting.org/docs/advanced_applications/mrkl). PALs write code to solve a given question and send it to a programmatic runtime to retrieve the result. Unlike [Chain-of-Thought (CoT) prompting](https://learnprompting.org/docs/intermediate/chain_of_thought), which uses natural language for intermediate reasoning, PAL’s intermediate reasoning is done through code.

![pal](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fpal.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

PAL Example (Gao et al.)

One important thing to note is that PAL actually interleaves natural language (NL) and code. In the above image, in blue are natural language reasoning that PAL generates. Although it is not shown in the image, PAL actually generates '#' before each line of NL reasoning, so that they are interpreted as comments by the programmatic runtime.

## Example

Let's look at an example of PAL solving a math question. I use a 3-shot prompt, which is a simplified version of [PAL prompt](https://github.com/reasoning-machines/pal/blob/main/pal/prompt/math_prompts.py).

I will use langchain, a Python package for chaining LLM functionality. First, a few installations are needed:

```
!pip install langchain==0.0.26
!pip install openai
from langchain.llms import OpenAI
import os
os.environ["OPENAI_API_KEY"] = "sk-YOUR_KEY_HERE"
```

Then, we can create an instance of GPT-3 davinci-002 (an API call happens when we use this object):

```
llm = OpenAI(model_name='text-davinci-002', temperature=0)
```

Here is the [Few-Shot](https://learnprompting.org/docs/basics/few_shot) prompt:

```
MATH_PROMPT = '''
Q: There were nine computers in the server room. Five more computers were installed each day, from Monday to Thursday. How many computers are now in the server room?

# solution in Python:
"""There were nine computers in the server room. Five more computers were installed each day, from Monday to Thursday. How many computers are now in the server room?"""
computers_initial = 9
computers_per_day = 5
num_days = 4  # 4 days between Monday and Thursday
computers_added = computers_per_day * num_days
computers_total = computers_initial + computers_added
result = computers_total
return result

Q: Shawn has five toys. For Christmas, he got two toys each from his mom and dad. How many toys does he have now?

# solution in Python:
"""Shawn has five toys. For Christmas, he got two toys each from his mom and dad. How many toys does he have now?"""
toys_initial = 5
mom_toys = 2
dad_toys = 2
total_received = mom_toys + dad_toys
total_toys = toys_initial + total_received
result = total_toys

Q: Jason had 20 lollipops. He gave Denny some lollipops. Now Jason has 12 lollipops. How many lollipops did Jason give to Denny?

# solution in Python:
"""Jason had 20 lollipops. He gave Denny some lollipops. Now Jason has 12 lollipops. How many lollipops did Jason give to Denny?"""
jason_lollipops_initial = 20
jason_lollipops_after = 12
denny_lollipops = jason_lollipops_initial - jason_lollipops_after
result = denny_lollipops

Q: {question}

# solution in Python:
'''
```

Now we can pass the combined prompt to GPT-3:

```
llm_out = llm(MATH_PROMPT.format(question=question))
print(llm_out)
```

The output is:

Emma took a 60-minute plane ride to Seattle. She then took a 2-hour train
ride to Portland, and then a 30-minute bus ride to Vancouver. How long did
it take her to get to Vancouver?

  
  

plane\_ride = 60

  

train\_ride = 2 \* 60 # 2 hours in minutes

  

bus\_ride = 30

  

total\_time = plane\_ride + train\_ride + bus\_ride

  

result = total\_time

Finally, we can pass this code to a Python runtime to get the answer:

```
exec(llm_out)
print(result)
```

The output is **210**, which is correct.

See the Jupyter notebook for this example of [Program-aided Language Models](https://github.com/trigaten/Learn_Prompting/tree/main/docs/code_examples/PAL.ipynb).

## More

Also see [PAL's colab example](https://colab.research.google.com/drive/1u4_RsdI0E79PCMDdcPiJUzYhdnjoXeXc?usp=sharing#scrollTo=Ba0ycacK4i1V).