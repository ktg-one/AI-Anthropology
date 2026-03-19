---
Title: Chain of Density (CoD)
Text summarization has long been a challenging task in natural language processing, requiring a delicate balance between brevity and informativeness. Large language models (LLMs) have revolutionized this field by generating coherent summaries with minimal task-specific fine-tuning. However, creating summaries that are both concise and information-rich remains a significant challenge.
**Chain of Density (CoD) prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/self_criticism/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Adams, G., Fabbri, A., Ladhak, F., Lehman, E., &amp; Elhadad, N. (2023). From Sparse to Dense: GPT-4 Summarization with Chain of Density Prompting. <a target="_blank" rel="noopener noreferrer" href="https://arxiv.org/abs/2309.04269" style="color: rgb(29, 151, 116); text-decoration: none; overflow-wrap: break-word;">https://arxiv.org/abs/2309.04269</a> </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> addresses this challenge through an innovative approach that systematically enriches summaries while maintaining a fixed length. This technique represents a significant advancement in how we can leverage LLMs for more effective summarization.
The key aspects of CoD include:
- **Iterative refinement:** Instead of producing a summary in one pass, CoD prompting refines it over multiple iterations. In each step, the model identifies and integrates 1-3 missing salient entities, ensuring that previously omitted details are incorporated gradually.
- **Controlled compression:** To maintain a constant token count, the model compresses or rephrases existing content to make space for new information. This strategy allows the summary to become more detailed without growing longer.
- **Enhanced abstraction:** As the summary is repeatedly reworked, the language shifts toward a more abstract and synthesized narrative, effectively capturing the source material's essence.
The effectiveness of CoD comes from its ability to:
- Preserve a fixed length, preventing verbosity
- Fuse and reorganize content efficiently
- Balance entity density-ideally around 0.15 entities per token-to align with human preferences
## The Mechanics of CoD
Chain of Density (CoD) prompting transforms summarization into a sophisticated, iterative refinement procedure. Here's how it works:
1. Generate an initial "entity-sparse" summary containing only 1-3 salient entities from the source text. The fixed token count is crucial for consistent evaluation of informativeness.
2. Through five fixed iterations, identify unique, missing entities that are:
- Relevant to the primary narrative
- Specific yet concise (five words or fewer)
- Novel to the existing summary
- Faithful to the original article
- Unrestricted in location within the article
3. "Fuse" these missing entities into the existing summary through:
- Compression of redundant language
- Abstraction of content
- Integration of related details
## Implementing CoD in Practice
The following template guides an LLM through the CoD process:
 
![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)
#### Template
---
Article: \[ARTICLE\]
  
You will generate increasingly concise, entity-dense summaries of the above Article. Repeat the following 2 steps 5 times.
  
Step 1. Identify 1-3 informative Entities (";" delimited) from the Article which are missing from the previously generated summary.
  
Step 2. Write a new, denser summary of identical length which covers every entity and detail from the previous summary plus the Missing Entities.
  
A Missing Entity is:
- Relevant: to the main story.
- Specific: descriptive yet concise (5 words or fewer).
- Novel: not in the previous summary.
- Faithful: present in the Article.
- Anywhere: located anywhere in the Article.
  
Guidelines:
- The first summary should be long (4-5 sentences, ~80 words) yet highly non-specific, containing little information beyond the entities marked as missing. Use overly verbose language and fillers (e.g., "this article discusses") to reach ~80 words.
- Make every word count: re-write the previous summary to improve flow and make space for additional entities.
- Make space with fusion, compression, and removal of uninformative phrases like "the article discusses".
- The summaries should become highly dense and concise yet self-contained, e.g., easily understood without the Article.
- Missing entities can appear anywhere in the new summary.
- Never drop entities from the previous summary. If space cannot be made, add fewer new entities.
  
Remember, use the exact same number of words for each summary.
  
Answer in JSON. The JSON should be a list (length 5) of dictionaries whose keys are "Missing\_Entities" and "Denser\_Summary".
## Real-World Application: The Chinese Grand Prix Incident
To better understand how CoD works in practice, let's examine a concrete example from Formula 1 racing:
![Chain of Density (CoD)](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fnew_techniques%2Fchain-of-density.png&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)
The summary evolves through five steps:
1. Initial broad overview of the collision and consequences
2. Addition of team and position details
3. Integration of specific penalties and driver movements
4. Incorporation of technical details (lap numbers, damage specifics)
5. Final refinement while maintaining length
Human evaluations show that steps 3-4 typically achieve the optimal balance of informativeness and readability.
## Comparative Analysis: CoD vs Traditional Methods
| **Method** | **Summary Characteristics** | **Strengths** | **Limitations** |
| --- | --- | --- | --- |
| **Vanilla Summarization** | Single-step, general | Fast and straightforward | Misses crucial details |
| **Human-Written** | Thoughtfully balanced | High readability, context-rich | Subjective and time-intensive |
| **CoD** | Iteratively refined, dense | Incremental detail integration | Multiple processing steps |
## Current Limitations and Future Potential
While CoD advances summarization technology, it faces several challenges:
- Domain specificity: Currently focused on news summarization
- Evaluation challenges: Subjective density standards
- Computational overhead: Multiple processing steps impact real-time performance
- Quality consistency: Varies with source material and LLM selection
Note
Explore CoD further with the creators' dataset on [Hugging Face](https://huggingface.co/datasets/griffin/chain_of_density), featuring 500 annotated and 5,000 unannotated examples.
## Conclusion
Chain of Density Prompting advances automated summarization by combining iterative refinement with controlled information density. Its structured methodology provides a foundation for future developments in text summarization, offering a valuable tool for applications requiring high-quality, balanced summaries.