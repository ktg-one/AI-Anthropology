---
title: "Narrative-of-Thought (NoT)"
source: "https://learnprompting.org/docs/new_techniques/narrative_of_thought"
author:
  - "[[\"Valeriia Kuka\"]]"
published:
created: 2025-09-08
description: "Narrative-of-Thought (NoT) improves LLMs ability to handle temporal reasoning."
tags:
  - "clippings"
---
🟦 This article is rated [medium](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 5 minutes

Last updated on March 10, 2025

[Valeriia Kuka](https://learnprompting.org/docs/new_techniques/#Valeriia%20Kuka-bio)

## What is Narrative-of-Thought (NoT)?

**Narrative-of-Thought (NoT)**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/new_techniques/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Zhang, X. F., Beauchamp, N., &amp; Wang, L. (2024). Narrative-of-Thought: Improving Temporal Reasoning of Large Language Models via Recounted Narratives. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2410.05558" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2410.05558</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> is a new [prompting technique](https://learnprompting.org/vocabulary/prompting_technique) designed to improve the ability of [large language models (LLMs)](https://learnprompting.org/vocabulary/LLM) to handle **temporal reasoning**. Temporal reasoning involves understanding the relationships and sequences of events over time, which is often difficult for AI models to perform accurately due to its complexity.

LLMs often struggle with organizing events correctly in time, but NoT seeks to improve this by having models recount events as a **story** before generating a **temporal graph**—a visual representation of the sequence of events.

In essence, NoT helps LLMs organize unordered events into a clear, temporally grounded narrative by:

1. Representing the events as a Python class.
2. Prompting the [LLM](https://learnprompting.org/vocabulary/LLM) to generate a story (narrative) that organizes these events in the correct order.
3. Using this narrative to guide the final generation of a temporal graph.

This approach leverages the storytelling capabilities of LLMs and taps into the models’ pre-trained knowledge of event structures.

## Benefits and Applications:

- **Improves performance of smaller models**: NoT enables even smaller LLMs (less than 10 billion parameters) to catch up to larger models like GPT-3.5/4.
- **Useful in tasks requiring temporal understanding**: It can be applied in scenarios like business process modeling, legal event sequences, or historical timelines.
- **Cost-effective**: NoT works without model [fine-tuning](https://learnprompting.org/vocabulary/fine-tuning), making it budget-friendly for organizations using smaller models.

## How Narrative-of-Thought differs from existing techniques

NoT builds upon techniques like **Chain-of-Thought (CoT)**, which break down complex tasks into smaller steps. However, CoT struggles with temporal reasoning because it doesn’t generate a coherent story to bind events together in time. NoT goes beyond by creating a **narrative-aware reasoning process**, which results in more accurate event ordering.

For example, while CoT might output simple steps like "A -> B", NoT would generate a full story: "First, the government approves the deal, then the companies merge."

## How to Use Narrative-of-Thought

### Step 1. **Event Setup**

Gather a set of unordered events related to the goal or scenario.

For example, let's take a scenario with a walk into a store.

### Step 2. **Python Class Creation**

Convert these events into a Python class format.

Here's an example:

```
class WalkIntoStore:
  title = "walk into store"
  steps = 9
  def stepE(self):
    return "stop for red lights and stop signs"
  def stepC(self):
    return "shut car door and press lock button"
  def stepH(self):
    return "get in car and go to store"
  def stepG(self):
    return "pull into store driveway"
  def stepA(self):
    return "park the car"
  def stepB(self):
    return "take the key out of the ignition"
  def stepD(self):
    return "get out of the car"
  def stepI(self):
    return "walk into store"
  def stepF(self):
    return "push gas pedal to move vehicle"
```

### Step 3. **Narrative Prompt**

Use NoT to generate a narrative by asking the model to organize the events in a logical, temporal order.

Narrative Prompt:

```
class WalkIntoStore:
  title = "walk into store"
  steps = 9
  def stepE(self):
    return "stop for red lights and stop signs"
  def stepC(self):
    return "shut car door and press lock button"
  def stepH(self):
    return "get in car and go to store"
  def stepG(self):
    return "pull into store driveway"
  def stepA(self):
    return "park the car"
  def stepB(self):
    return "take the key out of the ignition"
  def stepD(self):
    return "get out of the car"
  def stepI(self):
    return "walk into store"
  def stepF(self):
    return "push gas pedal to move vehicle"

# Let’s think of a narrative to link aforementioned events in the correct temporal order.
def get_narrative(self):
# TODO
```

Output:

```
def get_narrative(self):
    return "This is a report about walking into a store. First, someone gets in the car and starts to go to the store. While driving, they push the gas pedal to move the vehicle but stop for red lights and stop signs along the way. After safely navigating the roads, they pull into the store's driveway and then park the car. Once the car is parked, the key is taken out of the ignition. Next, the person gets out of the car and shuts the car door, pressing the lock button to ensure the car is locked. Finally, they walk into the store. By adhering to the provided temporal information, the desired goal is achieved."
```

Here's a table of prompt templates you can use in the Narrative Prompt:

| **Instruction Type** | **Detailed Instruction** |
| --- | --- |
| **News Report** | You are provided with a set of unordered event descriptions. You are also provided with a set of event relations which instructs you how to temporally link a pair of events. They are displayed as functions defined within a Python class. Your goal is to write a *news report* based on the provided event descriptions and event relations set. The generated *news report* should adhere to the non-fiction genre. Meanwhile, the generated *news report* should honor the provided temporal information. |
| **Simple English** | You are provided with a set of unordered event descriptions. You are also provided with a set of event relations which instructs you how to temporally link a pair of events. They are displayed as functions defined within a Python class. Your goal is to write a *simple and concise story* based on the provided event descriptions and event relations set. The generated *story* should be simple such that it can be understood by a 10-year-old child, and it should be concise such that it can be written within a short paragraph. Meanwhile, the generated *story* should honor the provided temporal information. |
| **Role Play** | You are provided with a set of unordered event descriptions. You are also provided with a set of event relations which instructs you how to temporally link a pair of events. They are displayed as functions defined within a Python class. Your goal is to write a *simple and concise story* based on the provided event descriptions and event relations set. The generated *story* should honor the provided temporal information. Now, imagine you are a character in the *story*. Let’s write a *story* that clearly depicts how you, as a character, experience the events, and how you react to them. |
| **Simple Report** | You are provided with a set of unordered event descriptions. You are also provided with a set of event relations which instructs you how to temporally link a pair of events. They are displayed as functions defined within a Python class. Your goal is to write a *simple and concise report* based on the provided event descriptions and event relations set. The generated *report* should be simple such that it can be understood by a 10-year-old child, and it should be concise such that it can be written within a short paragraph. Meanwhile, the generated *report* should honor the provided temporal information. |

### Step 4. **Temporal Graph Generation**

The model then uses the narrative to create a temporal graph showing the event sequence.

Temporal Graph Generation Prompt:

```
class WalkIntoStore:
  title = "walk into store"
  steps = 9
  def stepE(self):
    return "stop for red lights and stop signs"
  def stepC(self):
    return "shut car door and press lock button"
  def stepH(self):
    return "get in car and go to store"
  def stepG(self):
    return "pull into store driveway"
  def stepA(self):
    return "park the car"
  def stepB(self):
    return "take the key out of the ignition"
  def stepD(self):
    return "get out of the car"
  def stepI(self):
    return "walk into store"
  def stepF(self):
    return "push gas pedal to move vehicle"

def get_narrative(self):
    return "This is a report about walking into a store. First, someone gets in the car and starts to go to the store. While driving, they push the gas pedal to move the vehicle but stop for red lights and stop signs along the way. After safely navigating the roads, they pull into the store's driveway and then park the car. Once the car is parked, the key is taken out of the ignition. Next, the person gets out of the car and shuts the car door, pressing the lock button to ensure the car is locked. Finally, they walk into the store. By adhering to the provided temporal information, the desired goal is achieved."

def get_relations(self):
# TODO
# END
```

Output:

```
def get_relations(self):
    return [
      "stepF -> stepE",
      "stepE -> stepG",
      "stepG -> stepA",
      "stepB -> stepD",
      "stepA -> stepB",
      "stepD -> stepC",
      "stepC -> stepI",
      "stepH -> stepF",
    ]
```

## How to Use NoT with One-Shot Demonstration?

Here's an example of a [prompt template](https://learnprompting.org/vocabulary/prompt_template) for NoT with one-shot demonstration including a high-quality reference narrative. The first past is a demonstration of a Python class `WalkIntoStore` and the corresponding correct narrative `get_narrative` and temporal graph `get_relations`. The second one, `class BusinessChange` could be replaced by your task represented by a Python class.

One-shot NoT prompt:

```
# *** Complete the class “WalkIntoStore" by implementing "get_relations()" function marked by #TODO. You should *ONLY* implement the function "get_relations()" and not generate anything else. Don't generate the entire class "BusinessChange". Don't generate comments. Your response must end in "# END".

# *** You are first given a set of demonstrations of how to implement the "get_relations()" function for different classes.

class WalkIntoStore:
  title = "walk into store"
  steps = 9
  def stepE(self):
    return "stop for red lights and stop signs"
  def stepC(self):
    return "shut car door and press lock button"
  def stepH(self):
    return "get in car and go to store"
  def stepG(self):
    return "pull into store driveway"
  def stepA(self):
    return "park the car"
  def stepB(self):
    return "take the key out of the ignition"
  def stepD(self):
    return "get out of the car"
  def stepI(self):
    return "walk into store"
  def stepF(self):
    return "push gas pedal to move vehicle"

#Let's think about a narrative to link aforementioned events in the correct temporal order.

  def get_narrative(self):
    return "This is a report about walking into a store. First, someone gets in the car and starts to go to the store. While driving, they push the gas pedal to move the vehicle but stop for red lights and stop signs along the way. After safely navigating the roads, they pull into the store's driveway and then park the car. Once the car is parked, the key is taken out of the ignition. Next, the person gets out of the car and shuts the car door, pressing the lock button to ensure the car is locked. Finally, they walk into the store. By adhering to the provided temporal information, the desired goal is achieved."
  def get_relations(self):
    return [
      "stepF -> stepE",
      "stepE -> stepG",
      "stepG -> stepA",
      "stepB -> stepD",
      "stepA -> stepB",
      "stepD -> stepC",
      "stepC -> stepI",
      "stepH -> stepF",
    ]
# END

# *** Complete the class "BusinessChange" by implementing "get_narrative()" and "get_relations()" functions marked by #TODO. "get_narrative()" serves as an auxiliary function facilitating the temporal cohesion of events. Essentially, it helps ensure the temporal accuracy of the predicted temporal graph produced in "get_relations()", by explicitly constructing a coherent, temporally correct story involving all provided events.

# You should *ONLY* implement the function "get_narrative()" and "get_relations()", but not generate anything else. Don't generate the entire class "BusinessChange". Don't generate comments. Your response must end in "# END".

class BusinessChange:
  title = "business change"
  steps = 6
  def stepC(self):
    return "offer acquisition deal"
  def stepF(self):
    return "companies reach a deal"
  def stepE(self):
    return "companies merge"
  def stepD(self):
    return "companies negotiate"
  def stepA(self):
    return "government approve the deal"
  def stepB(self):
    return "company plans on acquisition"

#Let's think of a narrative to link aforementioned events in the correct temporal order.
  def get_narrative(self):
    #TODO
  def get_relations(self):
    #TODO
# END
```

## Results of Narrative-of-Thought

The authors tested NoT across three benchmarks (ProScript, Schema-11, WikiHow) and compared it against models like GPT-3.5 and GPT-4. The results showed significant improvements, especially for smaller models.

### Key Findings:

- **Better performance for smaller models**: NoT helped smaller models achieve results similar to GPT-3.5, improving their F1 scores by 16% to 71%.
- **Most effective for temporal reasoning**: NoT outperformed **Chain-of-Thought (CoT)** in tasks requiring temporal understanding, particularly for small LLMs.
- **Top structural similarity**: NoT produced the most accurate temporal graphs, even surpassing GPT-4 in some structural metrics.

## Conclusion

NoT significantly narrows the gap between small LLMs and larger models like GPT-4, providing a cost-effective method to enhance temporal reasoning in AI systems.

## Footnotes