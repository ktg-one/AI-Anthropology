---
title: "ARQ: A New Structured Reasoning Approach for LLMs"
source: https://blog.dailydoseofds.com/p/arq-a-new-structured-reasoning-approach?ref=dailydev
author:
  - "[[Avi Chawla]]"
published: 2025-10-21
created: 2025-11-14
description: ...that actually prevents hallucinations (explained visually).
tags:
  - clippings
feature: thumbnails/external/50e14b2f3d3c852beeeecbb9a54bf79a.webp
thumbnail: thumbnails/resized/e8f41c4c3a108cbed68633203ea9d81b_86cf658e.webp
---
### ...that actually prevents hallucinations (explained visually).

### ARQ: Structured Reasoning Approach for LLMs

Researchers have open-sourced a new reasoning approach that actually prevents hallucinations in LLMs.

It beats popular techniques like Chain-of-Thought and has a SOTA success rate of 90.2%.

![](https://substackcdn.com/image/fetch/$s_!l_5u!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffd945544-ffc8-47c0-9a9c-e4fa58d3b2ee_935x233.png)

It’s implemented in the **[Parlant open-source framework](https://github.com/emcie-co/parlant)** to build instruction-following Agents (**[GitHub repo](https://github.com/emcie-co/parlant)**).

Here’s the core problem with current techniques that this new approach solves.

We have enough research to conclude that LLMs often struggle to assess what truly matters in a particular stage of a long, multi-turn conversation.

For instance, when you give Agents a 2,000-word system prompt filled with policies, tone rules, and behavioral dos and don’ts, you expect them to follow it word by word.

But here’s what actually happens:

- They start strong initially.
- Soon, they drift and start hallucinating.
- Shortly after, they forget what was said five turns ago.
- And finally, the LLM that was supposed to “never promise a refund” is happily offering one.

This means they can easily ignore crucial rules (stated initially) halfway through the process.

We expect techniques like Chain-of-Thought will help.

But even with methods like CoT, reasoning remains free-form, i.e., the model “thinks aloud” but it has limited domain-specific control.

That’s the exact problem the new technique, called Attentive Reasoning Queries (ARQs), solves.

![](https://substackcdn.com/image/fetch/$s_!rV8d!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2e31a2fe-4245-4b17-a183-60a873260072_2210x1566.png)

Instead of letting LLMs reason freely, ARQs guide them through explicit, domain-specific questions.

Essentially, each reasoning step is encoded as a targeted query inside a JSON schema.

For example, before making a recommendation or deciding on a tool call, the LLM is prompted to fill structured keys like:

```markup
{
  “current_context”: “Customer asking about refund eligibility”,
  “active_guideline”: “Always verify order before issuing refund”,
  “action_taken_before”: false,
  “requires_tool”: true,
  “next_step”: “Run check_order_status()”
}
```

This type of query does two things:

1. Reinstate critical instructions by keeping the LLM aligned mid-conversation.
2. Facilitate intermediate reasoning, so that the decisions are auditable and verifiable.

![](https://substackcdn.com/image/fetch/$s_!OACf!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0b4ea69d-b0fd-4b7f-b6a4-973c483e9053_1176x663.png)

By the time the LLM generates the final response, it’s already walked through a sequence of \*controlled\* reasoning steps, which did not involve any free text exploration (unlike techniques like CoT or ToT).

Here’s the success rate across 87 test scenarios:

- ARQ → 90.2%
- CoT reasoning → 86.1%
- Direct response generation → 81.5%

This approach is actually implemented in **[Parlant](https://github.com/emcie-co/parlant)**, a recently trending open-source framework to build instruction-following Agents (14k stars).

ARQs are integrated into three key modules:

![](https://substackcdn.com/image/fetch/$s_!l0dx!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa92f426c-46eb-4c07-9403-faeb64e3d94f_1146x509.png)

- Guideline proposer to decide which behavioral rules apply.
- Tool caller to determine what external functions to use.
- Message generator, when it produces the final customer-facing reply.

You can see the full implementation and try it yourself.

But the core insight applies regardless of what tools you use:

When you make reasoning explicit, measurable, and domain-aware, LLMs stop improvising and start reasoning with intention. Free-form thinking sounds powerful, but in high-stakes or multi-turn scenarios, structure always wins.

**[You can find the Parlant GitHub repo here →](https://github.com/emcie-co/parlant)**

Thanks for reading!