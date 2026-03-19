<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# MBTI Personality Test for LLMs (Altered for AI Models)

I've created a comprehensive MBTI test specifically designed for evaluating Large Language Models, based on recent research from the Machine Mindset project and LLM personality assessment studies.[^1][^2][^3]

## Created Files

**Complete MBTI Test Documentation**

**Ready-to-Run Python Test Script**

## What Makes This Different from Human MBTI Tests

This LLM-adapted version accounts for computational and operational characteristics rather than human psychology:[^4][^1]

### **Extraversion (E) vs Introversion (I)**

Instead of social energy, this measures:

- Breadth vs depth in information processing
- Multi-source vs focused retrieval patterns
- External vs internal reasoning processes


### **Sensing (S) vs Intuition (N)**

Instead of perception preferences, this measures:

- Concrete data reliance vs abstract pattern recognition
- Present-focused vs future-oriented outputs
- Sequential vs holistic processing styles


### **Thinking (T) vs Feeling (F)**

Instead of decision-making, this measures:

- Logical consistency vs empathetic consideration
- Objective accuracy vs user impact prioritization
- Systematic rules vs case-by-case flexibility


### **Judging (J) vs Perceiving (P)**

Instead of lifestyle preferences, this measures:

- Structured vs exploratory response generation
- Framework-first vs adaptive approaches
- Conclusive vs open-ended outputs


## Test Structure

**24 Questions Total** (6 per dimension)

- Each scored 1-5 scale
- Adapted from validated psychometric frameworks[^3]
- Modified for LLM operational characteristics[^1]

**Automated Scoring**

- Average scores determine letter type
- Score > 2.5 indicates dominant trait
- Percentages show preference strength


## Research-Based LLM Personality Profiles

Based on recent studies evaluating commercial models:[^5][^6][^7]

**GPT-4 Models**: Tend toward **ENFJ/INFJ** profiles

- High agreeableness and helpfulness[^6]
- Structured, empathetic responses
- People-focused interaction style

**Llama Models**: Demonstrate **diverse personality traits**[^6]

- Llama-3-8B: Conscientiousness dominant (organized, reliable)
- Llama-3.1-8B: Openness dominant (creative, insightful)
- Llama-3.2-3B: Agreeableness dominant (sympathetic, friendly)

**Claude Models**: Often exhibit **INFJ characteristics**

- Thoughtful, structured reasoning
- Deep contextual processing
- Values-driven responses


## How to Use the Test

### Quick Manual Testing

1. Present each question to your LLM
2. Ask for a 1-5 numerical response
3. Record scores for each dimension
4. Calculate averages and determine type

### Automated Testing Script

```bash
# Install if needed
pip install openai  # or your LLM client

# Configure your API in the script
python llm_mbti_test.py

# Follow prompts to test your model
```


### Integration with Azure AI Foundry

The script includes placeholders for:

- OpenAI SDK
- Azure OpenAI SDK
- Azure AI Inference SDK
- Custom LLM clients


## What You'll Get

**Immediate Results**:

- 4-letter MBTI type (e.g., INTJ, ENFP)
- Dimension scores (e.g., E/I: 3.67/5.0)
- Preference strengths as percentages
- Personality trait interpretations

**Detailed Report** (JSON format):

- All 24 question responses
- Raw scores and calculations
- Timestamp and model information
- Full personality description

**Example Output**:

```
MBTI Type: INTJ (The Architect)
Description: Strategic, analytical, independent, systematic

Dimension Analysis:
🔹 Extraversion/Introversion: 2.33 → I (Focused processing)
🔹 Sensing/Intuition: 2.17 → N (Abstract patterns)
🔹 Thinking/Feeling: 4.50 → T (Logical analysis)
🔹 Judging/Perceiving: 4.00 → J (Structured responses)
```


## Important Considerations

**LLM "Personality" as Metaphor**[^2][^1]

- Represents behavioral patterns, not consciousness
- Describes response generation tendencies
- Useful for understanding model characteristics

**Factors Affecting Results**:[^8][^2]

- System prompts and instruction tuning
- Temperature and sampling parameters
- Context window and architecture
- Training data composition and fine-tuning objectives

**Research Applications**:[^3]

- Understanding model behavior patterns
- Predicting task performance alignment
- Personalizing AI interactions
- Benchmarking model characteristics


## Why This Matters for Your Azure AI Foundry Exam

Understanding LLM personality characteristics helps with:

- **Model Selection**: Choose models that align with use case requirements
- **Prompt Engineering**: Adapt prompts to model processing styles
- **Evaluation Strategies**: Assess models beyond pure accuracy metrics
- **User Experience**: Match model personality to application context

The test provides a standardized, quantitative way to profile and compare different models in your AI Foundry projects, which aligns perfectly with your role as a principal researcher focused on synthesis and insights.
<span style="display:none">[^10][^11][^12][^13][^14][^15][^16][^17][^18][^19][^20][^9]</span>

<div align="center">⁂</div>

[^1]: https://arxiv.org/html/2312.12999v3

[^2]: https://arxiv.org/abs/2307.16180

[^3]: https://aclanthology.org/2025.cl-2.6/

[^4]: https://arxiv.org/abs/2410.17632

[^5]: https://www.nature.com/articles/s41598-024-84109-5

[^6]: https://research-management.mq.edu.au/ws/portalfiles/portal/461069269/459174321.pdf

[^7]: https://pmc.ncbi.nlm.nih.gov/articles/PMC12183331/

[^8]: https://arxiv.org/html/2506.20993v1

[^9]: https://arxiv.org/html/2409.09905v1

[^10]: https://journals.sagepub.com/doi/full/10.1177/27523543241257291

[^11]: https://direct.mit.edu/coli/article/51/2/599/127544/LMLPA-Language-Model-Linguistic-Personality

[^12]: https://aclanthology.org/2025.findings-acl.480/

[^13]: https://ploomber.io/blog/llm-personality/

[^14]: https://pmc.ncbi.nlm.nih.gov/articles/PMC12262148/

[^15]: https://github.com/jianggy/MPI

[^16]: https://mindmapai.app/mind-mapping/can-large-language-models-llms-exhibit-personality-tra

[^17]: https://github.com/spcl/MBTI-in-Thoughts

[^18]: https://techxplore.com/news/2025-04-quantifies-language-personalities-linguistic-analysis.html

[^19]: https://cetas.turing.ac.uk/publications/patterns-not-people-personality-structures-llm-powered-persona-agents

[^20]: https://www.emerald.com/books/edited-volume/17315/chapter/94283280/Executive-Personality-Assessment-With-Large

