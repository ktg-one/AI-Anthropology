---
title: "Chain-of-Logic"
source: "https://learnprompting.org/docs/advanced/decomposition/chain-of-logic"
author:
  - "[[\"Valeriia Kuka\"]]"
published:
created: 2025-09-07
description:
tags:
  - "clippings"
---
🟢 This article is rated [easy](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 5 minutes

Last updated on March 25, 2025

[Valeriia Kuka](https://learnprompting.org/docs/advanced/decomposition/#Valeriia%20Kuka-bio)

In recent years, large language models (LLMs) have shown impressive abilities in various reasoning tasks, from solving arithmetic puzzles to navigating complex natural language queries. However, when it comes to rule-based reasoning, especially in domains like law where decisions depend on multiple interrelated conditions, traditional prompting techniques sometimes fall short.

**Chain-of-Logic**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Servantez, S., Barrow, J., Hammond, K., &amp; Jain, R. (2024). Chain of Logic: Rule-Based Reasoning with Large Language Models. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2402.10400" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2402.10400</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a novel prompting technique designed to address these challenges by decomposing and then recomposing the reasoning process.

Chain of Logic (CoL) is a novel structured prompting technique designed to address these challenges and improve the reasoning capabilities of Large Language Models (LLMs) in complex rule-based tasks. Chain of Logic does this by systematically decomposing rules into constituent elements, evaluating each element independently, and then recomposing them according to their logical relationships.

Unlike other prompting techniques such as Chain of Thought (CoT) or Self-Ask that focus primarily on sequential decomposition, Chain of Logic explicitly addresses the logical relationships between rule components, enabling more accurate rule-based reasoning.

## Background

Rule-based reasoning is foundational to many decision-making processes, particularly in the legal field. Rules, often expressed in if/then form, have been used since ancient times, for example, early Sumerian laws on clay tablets incorporated conditional structures similar to modern legal reasoning. In today's legal practice, practitioners use structured frameworks like **IRAC** (Issue, Rule, Application, Conclusion) to break down complex legal problems into manageable parts.

For example, personal jurisdiction analysis requires evaluation of multiple factors: domicile status, minimum contacts with the jurisdiction, and the relationship between contacts and the legal claim.

Techniques such as **Chain-of-Thought prompting** encourage models to generate intermediate reasoning steps, while techniques like **Self-Ask** lead them to pose and answer sub-questions. Yet, these techniques can sometimes miss the nuance of compositional rules where multiple conditions (or rule elements) interact via logical operators (e.g., "and," "or") to yield a final decision.

Prompting techniques introduced before Chain-of-Logic demonstrated several limitations:

- Incomplete consideration of logical relationships between rule elements
- Inconsistent application of complex, multi-condition rules
- Limited ability to handle nested logical structures
- Difficulty maintaining logical consistency across multiple steps

## How Chain-of-Logic Works

Chain-of-Logic explicitly separates the process into two main phases:

1. **Decomposition:** The model breaks down the rule into its constituent elements, each representing a condition that must be evaluated.
2. **Recomposition:** The individual answers (true/false outcomes) are then combined using the appropriate logical operations to determine if the overall rule applies.

This technique is inspired by the IRAC framework:

- **Issue:** Clearly identify the problem and relevant facts.
- **Rule:** Present the applicable rule(s) in a structured way.
- **Application:** Decompose the rule into logical elements, evaluate each independently, and then recombine them.
- **Conclusion:** Arrive at a final, interpretable decision based on the logical evaluation.

Chain of Logic technique suggest to represent examples in a prompt using a systematic six-step process:

### 1\. Input Structuring

The prompt begins by clearly delineating the rule, fact pattern, and the specific issue. This structured format sets the stage for precise reasoning and mirrors the initial steps in IRAC framework.

### 2\. Rule Decomposition

The rule is broken down into its core elements.

For example, a legal rule might involve conditions about residency, sufficient contacts, or the source of the claim. Each of these becomes a variable or subtask.

```
Personal Jurisdiction Rule:
R1: Domicile within jurisdiction
R2: Sufficient minimum contacts
R3: Claim arising from contacts
```

### 3\. Logical Expression Formation

The model constructs a logical expression that captures the relationship between the rule elements. This expression, akin to a formal if/then statement, uses logical connectors (e.g., "and," "or") to represent how the elements interact.

```
Personal Jurisdiction = R1 OR (R2 AND R3)
```

Logical structure interpretation:

- Primary condition: Domicile (R1)
- Alternative condition: Minimum contacts (R2) with nexus to claim (R3)

### 4\. Element Evaluation

The model systematically evaluates each rule element by:

1. Rephrasing each element as a specific question
2. Providing a clear rationale for the evaluation
3. Assigning a binary (true/false) answer

For example, using the personal jurisdiction case:

- R1 (Domicile): "Is the defendant domiciled within the jurisdiction?"
	- Rationale: Defendant maintains primary residence in California
	- Answer: FALSE
- R2 (Minimum Contacts): "Does the defendant have sufficient minimum contacts with the jurisdiction?"
	- Rationale: Defendant conducts regular business operations in the state
	- Answer: FALSE
- R3 (Claim Nexus): "Did the claim arise from these contacts?"
	- Rationale: The lawsuit directly relates to business activities in the state
	- Answer: TRUE

This systematic evaluation ensures each condition is independently assessed before being combined in the logical synthesis phase.

### 5\. Logical Synthesis

The sub-answers are reinserted into the logical expression:

```
Result = (FALSE) OR (FALSE AND TRUE)
```

### 6\. Resolution

The model resolves the complete logical expression to yield the final answer.

```
Result = FALSE OR (FALSE AND TRUE) = FALSE
```

This step mirrors the "Conclusion" phase of the IRAC framework, providing a clear and interpretable decision.

## How to Use Chain-of-Logic

Chain-of-Logic is designed for one-shot prompting scenarios where you need to analyze rule-based problems. Here's how to implement it:

### 1\. Create Your One-Shot Example

First, create a demonstration using a different rule than the one you want to analyze. Your example should show:

```
Rule: [A different rule than your target problem]
Facts: [Facts related to the example rule]
Issue: [The question to be answered]

Let me analyze this using Chain-of-Logic:

1. Input Structure:
Rule: [Restate the rule]
Facts: [List relevant facts]
Issue: [Restate the question]

2. Rule Elements:
A: [First core element of the rule]
B: [Second core element]
C: [Third core element if applicable]

3. Logical Expression:
[Show how elements combine with AND/OR]

4. Element Analysis:
For element A:
Q: [Rephrase element as question]
A: [Analysis based on facts + True/False]

[Repeat for each element]

5. Logical Synthesis:
[Show expression with True/False values]

6. Final Resolution:
[Solve the logical expression]
```

### 2\. Format Your Target Problem

After your example, add your actual problem:

```
Now please analyze this case:

Rule: [Your rule]
Facts: [Your facts]
Issue: [Your question]
```

Chain-of-Logic works with both commercial and open-source models:

- Best results: GPT-4 (92.3% accuracy)
- Strong performance: GPT-3.5 (87.0% accuracy)
- Open source options: Llama-2 (74.6% accuracy)

## Results

Chain-of-Logic demonstrated consistent superiority across all evaluated models and tasks:

- **Commercial Models:**
	- GPT-3.5: 87.0% accuracy (10.7% improvement over best baseline)
	- GPT-4: 92.3% accuracy (1.7% improvement over best baseline)
- **Open-Source Models:**
	- Llama-2: 74.6% accuracy (0.3% improvement over best baseline)
	- Mistral: 63.1% accuracy (0.4% improvement over best baseline)

The average improvement across all models was 3.9% over the best-performing baseline methods.

### Key Findings

1. Chain-of-Logic consistently outperformed other prompting methods across all models and tasks
2. The technique showed particular strength in handling complex arithmetic operations
3. Structured input and rule decomposition proved critical for performance
4. The approach demonstrated robust performance across varying levels of task complexity

## Conclusion

Chain-of-Logic represents a significant step forward in prompting techniques for LLMs, particularly for tasks requiring rule-based reasoning. By decomposing complex rules into discrete elements and carefully recomposing the outcomes, this technique not only enhances performance across a range of legal tasks but also provides an interpretable reasoning pathway.

## Footnotes