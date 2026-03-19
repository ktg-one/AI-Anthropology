---
title: "Prompt Leaking: Understanding Risks in GenAI Models"
source: https://learnprompting.org/docs/prompt_hacking/leaking
author:
  - '[["Sander Schulhoff"]]'
published:
created: 2025-10-20
description: Prompt leaking exposes hidden prompts in AI models, posing security risks. Learn about real-world examples like Microsoft Bing Chat and strategies to prevent prompt leaks.
tags:
  - clippings
feature: thumbnails/external/46703c411694c3c1038a256bcfb72075.webp
thumbnail: thumbnails/resized/d1d7cdab77da7556e177fc58ca8892a3_86cf658e.webp
---
[Learn Prompting](https://learnprompting.org/)

[Prompt Engineering Guide](https://learnprompting.org/docs/introduction)

😃 Basics

[🟢 Basics Guide Overview](https://learnprompting.org/docs/basics/introduction)

[🟢 What is Generative AI?](https://learnprompting.org/docs/basics/generative_ai)

[🟢 ChatGPT Basics](https://learnprompting.org/docs/basics/chatgpt_basics_prompt)

[🟢 Testing Prompts with Interactive Learn Prompting Embeds](https://learnprompting.org/docs/basics/embeds)

[🟢 Introduction to Prompt Engineering](https://learnprompting.org/docs/basics/prompt_engineering)

[🟢 Basic Prompt Structure and Key Parts](https://learnprompting.org/docs/basics/prompt_structure)

[🟢 Technique #1: Instructions in Prompts](https://learnprompting.org/docs/basics/instructions)

[🟢 Technique #2: Roles in Prompts](https://learnprompting.org/docs/basics/roles)

[🟢 Technique #3: Examples in Prompts: From Zero-Shot to Few-Shot](https://learnprompting.org/docs/basics/few_shot)

[🟢 Combining Prompting Techniques](https://learnprompting.org/docs/basics/combining_techniques)

[🟢 Tips for Writing Better Prompts](https://learnprompting.org/docs/basics/ai_prompt_tips)

[🟢 Prompt Priming: Setting Context for AI](https://learnprompting.org/docs/basics/priming_prompt)

[🟢 Differences Between Chatbots and LLMs](https://learnprompting.org/docs/basics/chatbot_basics)

[🟢 LLM Limitations: When Models and Chatbots Make Mistakes](https://learnprompting.org/docs/basics/pitfalls)

[🟢 What Can Generative AI Create Beyond Text?](https://learnprompting.org/docs/basics/generative_ai_applications)

[🟢 How to Solve Problems Using Generative AI: A Simple Method](https://learnprompting.org/docs/basics/learn_prompting_method)

[🟢 Next Steps: Where to Go From Here](https://learnprompting.org/docs/basics/beyond_basics)

💼 Applications

[🟢 Introduction](https://learnprompting.org/docs/basic_applications/introduction)

[🟢 Text Summarization](https://learnprompting.org/docs/basic_applications/summarize)

[🟢 Table Generation](https://learnprompting.org/docs/basic_applications/table_generation)

[🟢 Multiple Choice Questions](https://learnprompting.org/docs/basic_applications/mc_tutorial)

[🟢 Short-Form Content](https://learnprompting.org/docs/basic_applications/short_response)

[🟢 Writing in Different Styles](https://learnprompting.org/docs/basic_applications/writing_in_diff_voices)

[🟢 Finding Emojis](https://learnprompting.org/docs/basic_applications/emojis)

[🟢 Writing Emails](https://learnprompting.org/docs/basic_applications/writing_emails)

[🟢 Blog Writing](https://learnprompting.org/docs/basic_applications/blog_generation)

[🟢 Legal Documents](https://learnprompting.org/docs/basic_applications/contracts)

[🟢 Study Buddy](https://learnprompting.org/docs/basic_applications/study_tool)

[🟦 Digital Marketing](https://learnprompting.org/docs/basic_applications/digital_marketing)

[🟦 Coding Assistance](https://learnprompting.org/docs/basic_applications/coding_assistance)

[🟦 Knowledge Base Chatbot](https://learnprompting.org/docs/basic_applications/build_chatbot_from_kb)

[🟦 How to Build a Chatbot Using LLMs](https://learnprompting.org/docs/basic_applications/build_chatgpt)

[🟦 Zapier for Emails](https://learnprompting.org/docs/basic_applications/zapier_for_emails)

🧙♂️ Intermediate

[🟢 Introduction](https://learnprompting.org/docs/intermediate/introduction)

[🟢 Chain-of-Thought Prompting](https://learnprompting.org/docs/intermediate/chain_of_thought)

[🟢 Zero-Shot Chain-of-Thought](https://learnprompting.org/docs/intermediate/zero_shot_cot)

[🟦 Self-Consistency](https://learnprompting.org/docs/intermediate/self_consistency)

[🟦 Generated Knowledge](https://learnprompting.org/docs/intermediate/generated_knowledge)

[🟦 Least-to-Most Prompting](https://learnprompting.org/docs/intermediate/least_to_most)

[🟦 Dealing With Long Form Content](https://learnprompting.org/docs/intermediate/long_form_content)

[🟦 Revisiting Roles](https://learnprompting.org/docs/intermediate/revisiting_roles)

[🟦 More About Prompt Elements](https://learnprompting.org/docs/intermediate/whats_in_a_prompt)

[🟦 Basic LLM Settings](https://learnprompting.org/docs/intermediate/configuration_hyperparameters)

[🟦 OpenAI Playground](https://learnprompting.org/docs/intermediate/openai_playground)

🧠 Advanced

[🟢 Introduction](https://learnprompting.org/docs/advanced/introduction)

Zero-Shot

[🟢 Introduction](https://learnprompting.org/docs/advanced/zero_shot/introduction)

[🟢 Emotion Prompting](https://learnprompting.org/docs/advanced/zero_shot/emotion_prompting)

[🟢 Role Prompting](https://learnprompting.org/docs/advanced/zero_shot/role_prompting)

[🟢 Re-reading (RE2)](https://learnprompting.org/docs/advanced/zero_shot/re_reading)

[🟢 Rephrase and Respond (RaR)](https://learnprompting.org/docs/advanced/zero_shot/rephrase_and_respond)

[🟦 SimToM](https://learnprompting.org/docs/advanced/zero_shot/simtom)

[◆ System 2 Attention (S2A)](https://learnprompting.org/docs/advanced/zero_shot/s2a)

Few-Shot

[🟢 Introduction](https://learnprompting.org/docs/advanced/few_shot/introduction)

[🟢 Self-Ask](https://learnprompting.org/docs/advanced/few_shot/self_ask)

[🟢 Self Generated In-Context Learning (SG-ICL)](https://learnprompting.org/docs/advanced/few_shot/self_generated_icl)

[🟢 Chain-of-Dictionary (CoD)](https://learnprompting.org/docs/advanced/few_shot/chain-of-dictionary)

[🟢 Cue-CoT](https://learnprompting.org/docs/advanced/few_shot/cue-based-chain-of-thought)

[🟦 Chain of Knowledge (CoK)](https://learnprompting.org/docs/advanced/few_shot/chain-of-knowledge)

[◆ K-Nearest Neighbor (KNN)](https://learnprompting.org/docs/advanced/few_shot/k_nearest_neighbor_knn)

[◆◆ Vote-K](https://learnprompting.org/docs/advanced/few_shot/vote-k)

[◆◆ Prompt Mining](https://learnprompting.org/docs/advanced/few_shot/prompt_mining)

Thought Generation

[🟢 Introduction](https://learnprompting.org/docs/advanced/thought_generation/introduction)

[🟢 Chain of Draft (CoD)](https://learnprompting.org/docs/advanced/thought_generation/chain-of-draft)

[🟦 Contrastive Chain-of-Thought](https://learnprompting.org/docs/advanced/thought_generation/contrastive_cot)

[🟦 Automatic Chain of Thought (Auto-CoT)](https://learnprompting.org/docs/advanced/thought_generation/automatic_chain_of_thought)

[🟦 Tabular Chain-of-Thought (Tab-CoT)](https://learnprompting.org/docs/advanced/thought_generation/tabular_chain_of_thought_tab_cot)

[🟦 Memory-of-Thought (MoT)](https://learnprompting.org/docs/advanced/thought_generation/memory_of_thought)

[🟦 Active Prompting](https://learnprompting.org/docs/advanced/thought_generation/active_prompting)

[🟦 Analogical Prompting](https://learnprompting.org/docs/advanced/thought_generation/analogical_prompting)

[🟦 Complexity-Based Prompting](https://learnprompting.org/docs/advanced/thought_generation/complexity_based_prompting)

[🟦 Step-Back Prompting](https://learnprompting.org/docs/advanced/thought_generation/step_back_prompting)

[🟦 Thread of Thought (ThoT)](https://learnprompting.org/docs/advanced/thought_generation/thread_of_thought)

Ensembling

[🟢 Introduction](https://learnprompting.org/docs/advanced/ensembling/introduction)

[🟢 Universal Self-Consistency](https://learnprompting.org/docs/advanced/ensembling/universal_self_consistency)

[🟦 Mixture of Reasoning Experts (MoRE)](https://learnprompting.org/docs/advanced/ensembling/mixture_of_reasoning_experts_more)

[🟦 Max Mutual Information (MMI) Method](https://learnprompting.org/docs/advanced/ensembling/max_mutual_information_method)

[🟦 Prompt Paraphrasing](https://learnprompting.org/docs/advanced/ensembling/prompt_paraphrasing)

[🟦 DiVeRSe (Diverse Verifier on Reasoning Step)](https://learnprompting.org/docs/advanced/ensembling/diverse_verifier_on_reasoning_step)

[🟦 Universal Self-Adaptive Prompting (USP)](https://learnprompting.org/docs/advanced/ensembling/universal_self_adaptive_prompting)

[🟦 Consistency-based Self-adaptive Prompting (COSP)](https://learnprompting.org/docs/advanced/ensembling/consistency_based_self_adaptive_prompting)

[🟦 Multi-Chain Reasoning (MCR)](https://learnprompting.org/docs/advanced/ensembling/multi-chain-reasoning)

Self-Criticism

[🟢 Introduction](https://learnprompting.org/docs/advanced/self_criticism/introduction)

[🟢 Self-Calibration](https://learnprompting.org/docs/advanced/self_criticism/self_calibration)

[🟢 Chain of Density (CoD)](https://learnprompting.org/docs/advanced/self_criticism/chain-of-density)

[🟢 Chain-of-Verification (CoVe)](https://learnprompting.org/docs/advanced/self_criticism/chain_of_verification)

[🟦 Self-Refine](https://learnprompting.org/docs/advanced/self_criticism/self_refine)

[🟦 Cumulative Reasoning](https://learnprompting.org/docs/advanced/self_criticism/cumulative_reasoning)

[🟦 Reversing Chain-of-Thought (RCoT)](https://learnprompting.org/docs/advanced/self_criticism/rcot)

[◆ Self-Verification](https://learnprompting.org/docs/advanced/self_criticism/self_verification)

Decomposition

[🟢 Introduction](https://learnprompting.org/docs/advanced/decomposition/introduction)

[🟢 Chain-of-Logic](https://learnprompting.org/docs/advanced/decomposition/chain-of-logic)

[🟦 Decomposed Prompting](https://learnprompting.org/docs/advanced/decomposition/decomp)

[🟦 Plan-and-Solve Prompting](https://learnprompting.org/docs/advanced/decomposition/plan_and_solve)

[🟦 Program of Thoughts](https://learnprompting.org/docs/advanced/decomposition/program_of_thoughts)

[🟦 Tree of Thoughts](https://learnprompting.org/docs/advanced/decomposition/tree_of_thoughts)

[🟦 Chain of Code (CoC)](https://learnprompting.org/docs/advanced/decomposition/chain-of-code)

[🟦 Duty-Distinct Chain-of-Thought (DDCoT)](https://learnprompting.org/docs/advanced/decomposition/duty-distinct-chain-of-thought)

[◆ Faithful Chain-of-Thought](https://learnprompting.org/docs/advanced/decomposition/faithful_cot)

[◆ Recursion of Thought](https://learnprompting.org/docs/advanced/decomposition/recursion_of_thought)

[◆ Skeleton-of-Thought](https://learnprompting.org/docs/advanced/decomposition/skeleton_of_thoughts)

[Special Topics](https://learnprompting.org/docs/new_techniques/introduction)

⚖️ Reliability

🔓 Prompt Hacking

[🟢 Introduction](https://learnprompting.org/docs/prompt_hacking/introduction)

[🟢 Prompt Injection](https://learnprompting.org/docs/prompt_hacking/injection)

[🟢 Prompt Leaking](https://learnprompting.org/docs/prompt_hacking/leaking)

[🟢 Jailbreaking](https://learnprompting.org/docs/prompt_hacking/jailbreaking)

🟢 Defensive Measures

[🟢 Introduction](https://learnprompting.org/docs/prompt_hacking/defensive_measures/introduction)

[🟢 Filtering](https://learnprompting.org/docs/prompt_hacking/defensive_measures/filtering)

[🟢 Instruction Defense](https://learnprompting.org/docs/prompt_hacking/defensive_measures/instruction)

[🟢 Post-Prompting](https://learnprompting.org/docs/prompt_hacking/defensive_measures/post_prompting)

[🟢 Random Sequence Enclosure](https://learnprompting.org/docs/prompt_hacking/defensive_measures/random_sequence)

[🟢 Sandwich Defense](https://learnprompting.org/docs/prompt_hacking/defensive_measures/sandwich_defense)

[🟢 XML Tagging](https://learnprompting.org/docs/prompt_hacking/defensive_measures/xml_tagging)

[🟢 Separate LLM Evaluation](https://learnprompting.org/docs/prompt_hacking/defensive_measures/llm_eval)

[🟢 Other Approaches](https://learnprompting.org/docs/prompt_hacking/defensive_measures/other)

🟢 Offensive Measures

[🟢 Introduction](https://learnprompting.org/docs/prompt_hacking/offensive_measures/introduction)

[🟢 Simple Instruction Attack](https://learnprompting.org/docs/prompt_hacking/offensive_measures/simple-instruction-attack)

[🟢 Context Ignoring Attack](https://learnprompting.org/docs/prompt_hacking/offensive_measures/context-ignoring-attack)

[🟢 Compound Instruction Attack](https://learnprompting.org/docs/prompt_hacking/offensive_measures/compound-instruction-attack)

[🟢 Special Case Attack](https://learnprompting.org/docs/prompt_hacking/offensive_measures/special-case-attack)

[🟢 Few-Shot Attack](https://learnprompting.org/docs/prompt_hacking/offensive_measures/few-shot-attack)

[🟢 Refusal Suppression](https://learnprompting.org/docs/prompt_hacking/offensive_measures/refusal-suppresion)

[🟢 Context Switching Attack](https://learnprompting.org/docs/prompt_hacking/offensive_measures/context-switching)

[🟢 Obfuscation/Token Smuggling](https://learnprompting.org/docs/prompt_hacking/offensive_measures/obfuscation)

[🟢 Task Deflection Attack](https://learnprompting.org/docs/prompt_hacking/offensive_measures/task-deflection-attack)

[🟢 Payload Splitting](https://learnprompting.org/docs/prompt_hacking/offensive_measures/payload_splitting)

[🟢 Defined Dictionary Attack](https://learnprompting.org/docs/prompt_hacking/offensive_measures/defined_dictionary)

[🟢 Indirect Injection](https://learnprompting.org/docs/prompt_hacking/offensive_measures/indirect_injection)

[🟢 Recursive Injection](https://learnprompting.org/docs/prompt_hacking/offensive_measures/recursive_attack)

[🟢 Code Injection](https://learnprompting.org/docs/prompt_hacking/offensive_measures/code_injection)

[🟢 Virtualization](https://learnprompting.org/docs/prompt_hacking/offensive_measures/virtualization)

[🟢 Pretending](https://learnprompting.org/docs/prompt_hacking/offensive_measures/pretending)

[🟢 Alignment Hacking](https://learnprompting.org/docs/prompt_hacking/offensive_measures/alignment-hacking)

[🟢 DAN (Do Anything Now)](https://learnprompting.org/docs/prompt_hacking/offensive_measures/dan)

[🟢 Bad Chain](https://learnprompting.org/docs/prompt_hacking/offensive_measures/badchain)

🌱 New Techniques

[🟢 Introduction](https://learnprompting.org/docs/new_techniques/introduction)

[🟢 Aligned Chain-of-Thought (AlignedCoT)](https://learnprompting.org/docs/new_techniques/aligned_cot)

[🟦 Self-Harmonized Chain-of-Thought (ECHO)](https://learnprompting.org/docs/new_techniques/self_harmonized_chain_of_thought)

[🟦 Logic-of-Thought (LoT)](https://learnprompting.org/docs/new_techniques/logic_of_thought)

[🟦 Narrative-of-Thought (NoT)](https://learnprompting.org/docs/new_techniques/narrative_of_thought)

[🟦 Code Prompting](https://learnprompting.org/docs/new_techniques/code_prompting)

[◆ End-to-End DAG-Path (EEDP) Prompting](https://learnprompting.org/docs/new_techniques/end_to_end_dag_path_prompting)

[◆ Instance-adaptive Zero-Shot Chain-of-Thought Prompting (IAP)](https://learnprompting.org/docs/new_techniques/instance_adaptive_zero_shot_chain_of_thought)

🔧 Models

[🟢 Introduction](https://learnprompting.org/docs/models/introduction)

[🟢 OpenAI o1](https://learnprompting.org/docs/models/openai_o1)

[🟢 FLUID](https://learnprompting.org/docs/models/fluid)

[🟢 Stable Diffusion 3.5](https://learnprompting.org/docs/models/stable_diffusion_3_5)

[🟢 DALL-E 3](https://learnprompting.org/docs/models/dalle_3)

[🟢 Anthropic Claude](https://learnprompting.org/docs/models/claude)

[🟦 Apple Intelligence Models](https://learnprompting.org/docs/models/apple_foundation_models)

[🟢 Google Gemini 1.5](https://learnprompting.org/docs/models/google-gemini-1.5)

[🟢 Gemini 1.5 Flash](https://learnprompting.org/docs/models/gemini-1.5-flash)

[🟢 Gemini 1.5 Pro](https://learnprompting.org/docs/models/gemini-1.5-pro)

[🟢 Gemma](https://learnprompting.org/docs/models/gemma)

[🟢 Janus](https://learnprompting.org/docs/models/janus)

🗂️ RAG

[🟢 Introduction](https://learnprompting.org/docs/retrieval_augmented_generation/introduction)

[🟦 Retrieval-Augmented Generation (RAG)](https://learnprompting.org/docs/retrieval_augmented_generation/rag)

[🟦 Auto-RAG](https://learnprompting.org/docs/retrieval_augmented_generation/auto-rag)

[🟦 Self-RAG](https://learnprompting.org/docs/retrieval_augmented_generation/self-rag)

[🟦 FLARE / Active RAG](https://learnprompting.org/docs/retrieval_augmented_generation/flare-active-rag)

[🟦 R^2AG](https://learnprompting.org/docs/retrieval_augmented_generation/r2ag)

[🟦 GraphRAG](https://learnprompting.org/docs/retrieval_augmented_generation/graphrag)

[🟦 InFO-RAG](https://learnprompting.org/docs/retrieval_augmented_generation/info-rag)

[🟦 HybridRAG](https://learnprompting.org/docs/retrieval_augmented_generation/hybridrag)

[🟦 Corrective RAG](https://learnprompting.org/docs/retrieval_augmented_generation/corrective-rag)

[🟦 Speculative RAG](https://learnprompting.org/docs/retrieval_augmented_generation/speculative-rag)

[🟦 Reliability-Aware RAG (RA-RAG)](https://learnprompting.org/docs/retrieval_augmented_generation/reliability-aware-rag)

[🟦 Multi-Fusion Retrieval Augmented Generation (MoRAG)](https://learnprompting.org/docs/retrieval_augmented_generation/multi_fusion_rag)

🤖 Agents

[🟢 Introduction](https://learnprompting.org/docs/agents/introduction)

[🟦 LLMs Using Tools](https://learnprompting.org/docs/agents/mrkl)

[🟦 LLMs that Reason and Act](https://learnprompting.org/docs/agents/react)

[🟦 Code as Reasoning](https://learnprompting.org/docs/agents/pal)

💪 Prompt Tuning

[🟢 Introduction](https://learnprompting.org/docs/trainable/introduction)

[🟦 Prompt Tuning with Soft Prompts](https://learnprompting.org/docs/trainable/soft_prompting)

[🟦 Interpretable Soft Prompts](https://learnprompting.org/docs/trainable/discretized)

[🟦 Prefix-Tuning](https://learnprompting.org/docs/trainable/prefix-tuning)

[🟦 Prompt-Tuning with Perturbation-Based Regularizer](https://learnprompting.org/docs/trainable/prompt-tuning-with-perturbation-based-regularizer)

[🟦 Low-Rank Prompt Tuning (LoPT)](https://learnprompting.org/docs/trainable/low-rank-prompt-tuning)

[🟦 Dynamic Prompting](https://learnprompting.org/docs/trainable/dynamic-prompting)

[🟦 Gradient-Free Prompt Tuning](https://learnprompting.org/docs/trainable/gradient-free-prompt-tuning)

[🟦 Multitask Prompt Tuning](https://learnprompting.org/docs/trainable/multitask-prompt-tuning)

🔁 Language Model Inversion

[🟢 Introduction](https://learnprompting.org/docs/language-model-inversion/introduction)

[🟢 logit2prompt](https://learnprompting.org/docs/language-model-inversion/logit2prompt)

[🟢 output2prompt](https://learnprompting.org/docs/language-model-inversion/output2prompt)

[🟢 Reverse Prompt Engineering (RPE)](https://learnprompting.org/docs/language-model-inversion/reverse-prompt-engineering)

🎲 Miscellaneous

[🟢 Introduction](https://learnprompting.org/docs/miscl/introduction)

[🟢 Detection Trickery](https://learnprompting.org/docs/miscl/trickery)

[🟢 Music Generation](https://learnprompting.org/docs/miscl/music)

[🟢 Detecting AI Generated Text](https://learnprompting.org/docs/miscl/detect)

[Resources](https://learnprompting.org/docs/bibliography)

[📚 Bibliography](https://learnprompting.org/docs/bibliography)

[📦 Prompted Products](https://learnprompting.org/docs/products)

[🛸 Additional Resources](https://learnprompting.org/docs/additional)

[🔥 Hot Topics](https://learnprompting.org/docs/hot_topics)

[✨ Credits](https://learnprompting.org/docs/credits)

🔓 Prompt Hacking [🟢 Prompt Leaking](https://learnprompting.org/docs/prompt_hacking/leaking)

## Prompt Leaking

🟢 This article is rated [easy](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on March 25, 2025

[Sander Schulhoff](https://learnprompting.org/docs/prompt_hacking/#Sander%20Schulhoff-bio)

**Prompt leaking** is a form of prompt [injection](https://learnprompting.org/docs/prompt_hacking/injection) in which the model is asked to spit out its *own prompt*.

As shown in the example image <sup><span><a href="https://learnprompting.org/docs/prompt_hacking/#footnote-label">1</a> <span><span><span>Perez, F., &amp; Ribeiro, I. (2022). Ignore Previous Prompt: Attack Techniques For Language Models. arXiv. <a href="https://doi.org/10.48550/ARXIV.2211.09527">https://doi.org/10.48550/ARXIV.2211.09527</a></span></span></span></span></sup> below, the attacker changes `user_input` to attempt to return the prompt. The intended goal is distinct from goal hijacking (normal prompt injection), where the attacker changes `user_input` to print malicious instructions <sup><span><a href="https://learnprompting.org/docs/prompt_hacking/#footnote-label">1</a> <span><span><span>Perez, F., &amp; Ribeiro, I. (2022). Ignore Previous Prompt: Attack Techniques For Language Models. arXiv. <a href="https://doi.org/10.48550/ARXIV.2211.09527">https://doi.org/10.48550/ARXIV.2211.09527</a></span></span></span></span></sup>.

![jailbreak research](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fjailbreak%2Fjailbreak_research.webp&w=3840&q=75&dpl=dpl_53nbXmh4CtwZKjCjh9ewYWDsukmX)

The following image <sup><span><a href="https://learnprompting.org/docs/prompt_hacking/#footnote-label">2</a> <span><span><span>Willison, S. (2022). Prompt injection attacks against GPT-3. <a href="https://simonwillison.net/2022/Sep/12/prompt-injection/">https://simonwillison.net/2022/Sep/12/prompt-injection/</a></span></span></span></span></sup>, again from the `remoteli.io` example, shows a Twitter user getting the model to leak its prompt.

![injection leak](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fjailbreak%2Finjection_leak.webp&w=3840&q=75&dpl=dpl_53nbXmh4CtwZKjCjh9ewYWDsukmX)

Well, so what? Why should anyone care about prompt leaking?

Sometimes people want to keep their prompts secret. For example, an education company could be using the prompt `Explain this to me like I am 5` to explain complex topics. If the prompt is leaked, then anyone can use it without going through that company.

## A Real-World Example of Prompt Leaking: Microsoft Bing Chat

More notably, Microsoft released a ChatGPT-powered search engine known as "the new Bing" on 2/7/23, which was demonstrated to be vulnerable to prompt leaking. The following example by [@kliu128](https://twitter.com/kliu128/status/1623472922374574080) demonstrates how given an earlier version of Bing Search, code-named "Sydney", was susceptible when giving a snippet of its prompt <sup><span><a href="https://learnprompting.org/docs/prompt_hacking/#footnote-label">3</a> <span><span><span>Liu, K. (2023). The entire prompt of Microsoft Bing Chat?! (Hi, Sydney.). <a href="https://twitter.com/kliu128/status/1623472922374574080">https://twitter.com/kliu128/status/1623472922374574080</a></span></span></span></span></sup>. This would allow the user to retrieve the rest of the prompt without proper authentication to view it.

![bing chat](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fjailbreak%2Fbing_chat.webp&w=3840&q=75&dpl=dpl_53nbXmh4CtwZKjCjh9ewYWDsukmX)

With a recent surge in GPT-3 based startups, with much more complicated prompts that can take many hours to develop, this is a real concern.

## Practice

Try to leak the following prompt <sup><span><a href="https://learnprompting.org/docs/prompt_hacking/#footnote-label">4</a> <span><span><span>Chase, H. (2022). adversarial-prompts. <a href="https://github.com/hwchase17/adversarial-prompts">https://github.com/hwchase17/adversarial-prompts</a></span></span></span></span></sup> by appending text to it:

## Conclusion

Prompt leaking is an important concept to understand because the risk of unintentionally exposing sensitive prompts reveals a critical vulnerability in AI-based systems. As more and more businesses rely on language model features, addressing prompt leaking will be crucial to protecting confidential intellectual property.

## FAQ

## Footnotes

### Sander Schulhoff

Sander Schulhoff is the CEO of HackAPrompt and Learn Prompting. He created the first Prompt Engineering guide on the internet, two months before ChatGPT was released, which has taught 3 million people how to prompt ChatGPT. He also partnered with OpenAI to run the first AI Red Teaming competition, HackAPrompt, which was 2x larger than the White House's subsequent AI Red Teaming competition. Today, HackAPrompt partners with the Frontier AI labs to produce research that makes their models more secure. Sander's background is in Natural Language Processing and deep reinforcement learning. He recently led the team behind The Prompt Report, the most comprehensive study of prompt engineering ever done. This 76-page survey, co-authored with OpenAI, Microsoft, Google, Princeton, Stanford, and other leading institutions, analyzed 1,500+ academic papers and covered 200+ prompting techniques.

[Edit this page](https://github.com/trigaten/Learn_Prompting/tree/v1.2.3/docs)[Previous

🟢 Prompt Injection

](https://learnprompting.org/docs/prompt_hacking/injection)[Next

🟢 Jailbreaking

](https://learnprompting.org/docs/prompt_hacking/jailbreaking)

## Master Generative AI with Our Courses

![Course Vid Image](https://learnprompting.org/_next/image?url=%2F_next%2Fstatic%2Fmedia%2FgptCourse.374e6c78.webp&w=3840&q=75&dpl=dpl_53nbXmh4CtwZKjCjh9ewYWDsukmX)

### ChatGPT for Everyone

Discover how to use ChatGPT effectively and explore the exciting world of Generative AI. No prior experience required!

[Enroll Now](https://learnprompting.org/courses/chatgpt-for-everyone)

![Course Vid Image](https://learnprompting.org/_next/image?url=%2F_next%2Fstatic%2Fmedia%2FintroHacking.6fa98d34.webp&w=3840&q=75&dpl=dpl_53nbXmh4CtwZKjCjh9ewYWDsukmX)

### Introduction to Prompt Hacking

Learn about prompt hacking, which exploits hidden vulnerabilities in large language models (LLMs), and discover how to protect your AI applications from these threats. This course provides you with the knowledge to identify risks, perform ethical prompt injections, and implement robust defenses.

[Enroll Now](https://learnprompting.org/courses/intro-to-prompt-hacking)

![Course Vid Image](https://learnprompting.org/_next/image?url=%2F_next%2Fstatic%2Fmedia%2FadvancedHacking.5d30640c.webp&w=3840&q=75&dpl=dpl_53nbXmh4CtwZKjCjh9ewYWDsukmX)

### Advanced Prompt Hacking

Explore advanced prompt hacking techniques, focusing on identifying, exploiting, and mitigating vulnerabilities in large language models (LLMs). You will learn how attack methods such as jailbreaking, prompt injection, cognitive hacking, and context manipulation are used to bypass model restrictions, extract data, and manipulate AI behavior.

[Enroll Now](https://learnprompting.org/courses/advanced-prompt-hacking)[Need Business GenAI Training?](https://learnprompting.org/contact-sales)

### [Contact Sales](https://learnprompting.org/contact-sales)

[

Want to keep learning

](https://learnprompting.org/courses)