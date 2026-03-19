---
title: Mixture-of-Reasoning Experts (MoRE)
source: https://learnprompting.org/docs/advanced/ensembling/mixture_of_reasoning_experts_more
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-01
description: Tackle LLM limitations in question answering with Mixture of Reasoning Experts (MoRE) which leverages specialized experts.
tags:
  - clippings
feature: thumbnails/external/5ee72d4fa2791a35e8454d6380bcf2aa.svg
---
[Learn Prompting](https://learnprompting.org/)

## Mixture of Reasoning Experts (MoRE)

🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on October 3, 2024

[Valeriia Kuka](https://learnprompting.org/docs/advanced/ensembling/#Valeriia%20Kuka-bio)

![Overview of Mixture-of-Reasoning Experts (MoRE) (@si2023gettingmixturelanguagemodel)](https://learnprompting.org/docs/assets/advanced/more_cover.svg)

Overview of Mixture-of-Reasoning Experts (MoRE) <sup><span><a href="https://learnprompting.org/docs/advanced/ensembling/#footnote-label">1</a> <span><span><span>Si, C., Shi, W., Zhao, C., Zettlemoyer, L., &amp; Boyd-Graber, J. (2023). Getting MoRE out of Mixture of Language Model Reasoning Experts. <a href="https://arxiv.org/abs/2305.14628">https://arxiv.org/abs/2305.14628</a></span></span></span></span></sup>

**Mixture of Reasoning Experts (MoRE)** <sup><span><a href="https://learnprompting.org/docs/advanced/ensembling/#footnote-label">1</a> <span><span><span>Si, C., Shi, W., Zhao, C., Zettlemoyer, L., &amp; Boyd-Graber, J. (2023). Getting MoRE out of Mixture of Language Model Reasoning Experts. <a href="https://arxiv.org/abs/2305.14628">https://arxiv.org/abs/2305.14628</a></span></span></span></span></sup> technique is designed to improve the generalization of [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) across different question types in question answering (QA). While LLMs have shown impressive performance, they often struggle when handling questions that require different reasoning skills—such as factual, multihop, mathematical, or commonsense reasoning. MoRE aims to address this challenge by using specialized language models, each trained for a specific reasoning type.

MoRE also introduces a novel approach to selective QA, where the system decides when to abstain from answering if the confidence in its prediction is low. This ensures the system answers accurately when possible and avoids incorrect answers.

MoRE leverages a pool of specialized experts, where each expert is optimized for a distinct reasoning type, such as:

- Factual reasoning (e.g., fact-based questions).
- Multihop reasoning (e.g., questions that require multiple steps of reasoning).
- Mathematical reasoning (e.g., solving math word problems).
- Commonsense reasoning (e.g., questions requiring implicit knowledge).

MoRE uses an **answer selector** to choose the best response based on predictions from the specialized experts. If the system detects that none of the answers are reliable, it can abstain from answering. Another key feature of MoRE is its ability to abstain from answering when it's unsure, improving the system's reliability.

![Overview of experts in Mixture-of-Reasoning Experts (MoRE) (@si2023gettingmixturelanguagemodel)](https://learnprompting.org/docs/assets/advanced/more_2.svg)

Experts in Mixture-of-Reasoning Experts (MoRE) <sup><span><a href="https://learnprompting.org/docs/advanced/ensembling/#footnote-label">1</a> <span><span><span>Si, C., Shi, W., Zhao, C., Zettlemoyer, L., &amp; Boyd-Graber, J. (2023). Getting MoRE out of Mixture of Language Model Reasoning Experts. <a href="https://arxiv.org/abs/2305.14628">https://arxiv.org/abs/2305.14628</a></span></span></span></span></sup>

Each expert in MoRE is designed to handle different reasoning challenges:

- Factual Expert: Uses retrieval-augmented prompting to pull relevant information from external knowledge sources, such as Wikipedia.
- Multihop Expert: Uses Chain-of-Thought (CoT) prompting to break down complex questions into smaller reasoning steps.
- Mathematical Expert: Also relies on CoT prompting, but is fine-tuned to handle numerical and logical computations.
- Commonsense Expert: Uses generated knowledge prompting, appending relevant factoids to answer questions requiring implicit knowledge.

By combining these experts, MoRE ensures higher generalizability compared to single-model approaches.

## Benefits and Applications

MoRE is especially useful in situations requiring robust, interpretable question answering, such as:

- Knowledge retrieval systems: Where factual accuracy is paramount.
- Educational tools: Where questions may span multiple reasoning types (factual, logical, and commonsense).
- Customer support systems: Where users expect reliable answers across diverse domains.

## How to Use MoRE?

![Example of application of Mixture-of-Reasoning Experts (MoRE) (@si2023gettingmixturelanguagemodel)](https://learnprompting.org/docs/assets/advanced/more_1.svg)

Example of application of Mixture-of-Reasoning Experts (MoRE) <sup><span><a href="https://learnprompting.org/docs/advanced/ensembling/#footnote-label">1</a> <span><span><span>Si, C., Shi, W., Zhao, C., Zettlemoyer, L., &amp; Boyd-Graber, J. (2023). Getting MoRE out of Mixture of Language Model Reasoning Experts. <a href="https://arxiv.org/abs/2305.14628">https://arxiv.org/abs/2305.14628</a></span></span></span></span></sup>

Here’s a simplified view of the process:

- Input Question: You ask a question.
- Expert Predictions: Each specialized model generates an answer based on its reasoning expertise.
- Answer Selection: The answer selector chooses the most reliable answer, based on agreement among experts and prediction confidence.
- Selective Answering: If no reliable answer is found, the system abstains.
- **Computational Complexity:** The ensemble of multiple experts increases the system's computational demands, which could be a barrier in resource-limited environments.
- **Model coverage:** The paper focuses on Codex model for experiments. MoRE needs to be tested with other open-souce models.
- **Trade-Offs in not answering:** While abstention from answering improves accuracy, it may also result in unanswered questions that the system could potentially solve, creating a trade-off between coverage and reliability.

## Conclusion

Mixture-of-Reasoning Experts technique offers a novel solution to the challenges of QA by combining specialized models and leveraging inter-expert agreement for both generalizability and selective answering. By specializing models for different reasoning tasks and abstaining when appropriate, MoRE delivers both higher accuracy and better interpretability.

## Footnotes

### Valeriia Kuka

Valeriia Kuka, Head of Content at Learn Prompting, is passionate about making AI and ML accessible. Valeriia previously grew a 60K+ follower AI-focused social media account, earning reposts from Stanford NLP, Amazon Research, Hugging Face, and AI researchers. She has also worked with AI/ML newsletters and global communities with 100K+ members and authored clear and concise explainers and historical articles.

[Edit this page](https://github.com/trigaten/Learn_Prompting/tree/v1.2.3/docs)[Previous

