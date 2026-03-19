---
title: "Bootstrap Qmdre"
version: "v1.0"
status: "ACTIVE"
model: "Multi-model"
tags: ["framework", "chain-of-thought", "perplexity", "qmdr", "active"]
created: "2025-11-22"
updated: "2025-11-22"
creator: "ktg"
category: "framework"
description: "Prompt for AI agent system"
---

🟢 Aligned Chain-of-Thought (AlignedCoT)
🟢
This article is rated easy
Reading Time: 4 minutes
Last updated on October 17, 2024
Valeriia Kuka

What is AlignedCoT?
AlignedCoT (Aligned Chain-of-Thought)1
Yang, Z., Huang, Y., Xiong, J., Feng, L., Liang, X., Wang, Y., & Tang, J. (2024). AlignedCoT: Prompting Large Language Models via Native-Speaking Demonstrations. https://arxiv.org/abs/2311.13538

 is a technique designed to create demonstrations for Chain-of-Thought (CoT) prompting. The idea behind AlignedCoT is to guide large language models (LLMs) to use their own “native style” of thought, instead of relying on human-crafted prompts that may not fully align with the LLM's learned behaviors.

This method addresses the challenge that LLMs often perform better when following their own learned habits rather than imitating human-written prompts.

How Does AlignedCoT Differ from Existing Techniques?
Unlike traditional CoT methods, which rely heavily on human-created few-shot examples or static dataset samples, AlignedCoT allows the model to generate its reasoning steps in its own native language style.

How Does AlignedCoT Work?
AlignedCoT is built around a 3-step process that helps LLMs perform complex reasoning tasks in a more structured, error-free manner:

Probing: Query the LLM with a Zero-Shot Chain-of-Thought prompt (“Let’s think step by step”) to let it generate its own reasoning process, free from human-crafted formats.

Refining: Any errors in the initial CoT generation are corrected by having the model iterate and fix mistakes, making the thought process more logical and consistent.

Formatting: The final step unifies the presentation and structure of the LLM’s reasoning so that each CoT is clear, error-free, and consistently formatted.

How to Use AlignedCoT
AlignedCoT can be used to improve reasoning tasks like mathematical problem solving and commonsense reasoning.

You don’t need to manually apply these steps yourself. You can simply use the ready-made AlignedCoT demonstrations created by the authors. These demonstrations are designed to optimize the model’s performance using native-style reasoning.

Here’s a template for using AlignedCoT prompts:

 Copy
Astronaut
Template for using AlignedCoT
Q1: [Question 1] A1: [Solution from AlignedCoT authors]

Q2: [Question 2] A2: [Solution from AlignedCoT authors]

Q3: [Your question] A3:

Let’s think step by step:

You can find a collection of AlignedCoT prompts on the official AlignedCoT GitHub.

Here's an example with AlignedCoT demonstrations:

 Copy
Astronaut
Prompt
[Question]: Jason had 20 lollipops. He gave Denny some lollipops. Now Jason has 12 lollipops. How many lollipops did Jason give to Denny?

[Solution]:

Let’s think step by step.

First, Jason had 20 lollipops. Then he gave some to Denny and now he has 12 lollipops.

So, to find out how many lollipops Jason gave to Denny, we need to subtract the number of lollipops Jason has now from the number he had at the beginning. So, 20 - 12 = 8.

Therefore, Jason gave 8 lollipops to Denny.

Answer: 8.

[Question]: There are 15 trees in the grove. Grove workers will plant trees in the grove today. After they are done, there will be 21 trees. How many trees did the grove workers plant today?

[Solution]:

Let’s think step by step.

First, we know that there were originally 15 trees in the grove.

Then, the grove workers planted some trees.

After they finished, there were 21 trees in total.

So, to find out how many trees they planted, we subtract the original number of trees from the final number of trees.

That is, 21 - 15 = 6.

So, the grove workers planted 6 trees today.

Answer: 6.

[Question]: [Your question] [Solution]:

Let’s think step by step:

Results of AlignedCoT
Experiments show that AlignedCoT improves reasoning accuracy across a range of tasks. Below is a summary of the performance improvements for GPT-3.5-turbo and GPT-4 models using AlignedCoT compared to other prompting methods:

Model	Prompt	GSM8K	AQUA	SVAMP	AddSub	SingleEQ	Penguins	Average
GPT-3.5-turbo	CoT w/o AlignedCoT	77.1	54.7	82.8	93.1	96.0	78.1	80.3
GPT-3.5-turbo	CoT w/ AlignedCoT	78.7	57.1	84.8	94.9	97.6	87.7	83.5
GPT-4	CoT w/o AlignedCoT	93.1	72.8	94.1	96.6	N/A	89.2	89.2
GPT-4	CoT w/ AlignedCoT	94.4	75.6	94.8	98.6	N/A	90.9	90.9
Performance Boost: AlignedCoT shows consistent performance improvements across multiple reasoning benchmarks, averaging +3.2% on GPT-3.5 and +1.7% on GPT-4.
Error Detection: It also significantly enhances the LLM’s ability to detect logical errors, with GPT-4 achieving a 78.9% accuracy in identifying incorrect problem setups.
Broad Applicability: AlignedCoT can be combined with other prompting techniques (e.g., self-consistency, Auto-CoT) to further boost performance in reasoning-heavy tasks.