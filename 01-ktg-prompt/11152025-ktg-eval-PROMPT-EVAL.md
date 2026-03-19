---
title: "Trillet AI Onboarding Guide - Prompt Evaluation Framework"
type: evaluation
version: "v1.0"
status: "ACTIVE"
created: 2025-01-20
tags: [evaluation, trillet-ai, onboarding, prompt-quality]
model: "Claude, GPT-4, Gemini"
---

# Trillet AI Onboarding Guide - Prompt Evaluation Framework

> **Evaluate prompts related to Trillet AI onboarding** | Quality assessment for AI agent creation guides

---

## Objective

Evaluate and refine prompts related to Trillet AI platform onboarding, agent creation, and prompt writing based on key quality criteria to ensure clarity, precision, depth, and relevance for non-technical users.

---

## Evaluation Criteria

### 1. Clarity (1-5)
**Question:** Does the prompt clearly communicate its intent without ambiguity?

**Scoring Guide:**
- **5 (Excellent)**: Crystal clear instructions, no ambiguity, perfect for non-technical users
- **4 (Very Good)**: Clear with minor areas that could be more explicit
- **3 (Good)**: Generally clear but some technical jargon or assumptions
- **2 (Fair)**: Some confusion possible, needs clarification
- **1 (Poor)**: Unclear, ambiguous, or confusing

**Trillet-Specific Checks:**
- ✅ Uses simple, non-technical language
- ✅ Explains concepts before using them (e.g., "Call Flow", "Prompt")
- ✅ Provides visual references (e.g., "top-right corner", "Sidebar → Flow Studio")
- ✅ Avoids platform-specific jargon without explanation

### 2. Precision (1-5)
**Question:** Is the prompt focused and specific in describing the desired outcome?

**Scoring Guide:**
- **5 (Excellent)**: Highly specific, actionable steps, measurable outcomes
- **4 (Very Good)**: Specific with clear action items
- **3 (Good)**: Somewhat specific but could be more detailed
- **2 (Fair)**: Vague or too general
- **1 (Poor)**: Unclear what needs to be accomplished

**Trillet-Specific Checks:**
- ✅ Provides exact button names and locations
- ✅ Includes specific examples (e.g., "Restaurant Booking Flow")
- ✅ Defines success criteria clearly
- ✅ Specifies required fields and formats

### 3. Depth (1-5)
**Question:** Does the prompt consider nuanced aspects of the request, avoiding superficial details?

**Scoring Guide:**
- **5 (Excellent)**: Comprehensive coverage, anticipates edge cases, includes troubleshooting
- **4 (Very Good)**: Good depth with most scenarios covered
- **3 (Good)**: Adequate depth but missing some nuances
- **2 (Fair)**: Surface-level only, misses important details
- **1 (Poor)**: Too superficial, lacks necessary information

**Trillet-Specific Checks:**
- ✅ Covers all phases: Setup → Configuration → Prompting → Testing → Deployment
- ✅ Includes troubleshooting section
- ✅ Addresses edge cases (e.g., "What if caller interrupts?")
- ✅ Provides best practices and pro tips
- ✅ Includes validation checklist

### 4. Relevance (1-5)
**Question:** Does the prompt align with the intended task or question without deviating?

**Scoring Guide:**
- **5 (Excellent)**: Perfectly aligned, stays on topic, no unnecessary information
- **4 (Very Good)**: Relevant with minor tangents
- **3 (Good)**: Mostly relevant but some off-topic content
- **2 (Fair)**: Somewhat relevant but includes unnecessary sections
- **1 (Poor)**: Off-topic or missing key relevant information

**Trillet-Specific Checks:**
- ✅ Focuses on onboarding and agent creation
- ✅ Stays within Trillet AI platform scope
- ✅ Doesn't include irrelevant platform comparisons
- ✅ Maintains focus on non-technical user needs

### 5. Usability (1-5) - Trillet-Specific
**Question:** Can a non-technical user follow this prompt successfully?

**Scoring Guide:**
- **5 (Excellent)**: Perfect for non-coders, includes all necessary context
- **4 (Very Good)**: Mostly accessible, minor technical assumptions
- **3 (Good)**: Requires some technical knowledge
- **2 (Fair)**: Assumes significant technical background
- **1 (Poor)**: Too technical for target audience

**Trillet-Specific Checks:**
- ✅ No coding knowledge required
- ✅ Step-by-step progression
- ✅ Includes examples and templates
- ✅ Provides testing guidance
- ✅ Offers troubleshooting help

---

## Evaluation Process

### Step 1: Initial Assessment
1. Read the prompt/documentation thoroughly
2. Identify target audience (non-technical Good AI clients)
3. Note any immediate clarity or precision issues

### Step 2: Criterion Scoring
For each criterion (Clarity, Precision, Depth, Relevance, Usability):
- Assign score (1-5)
- Provide brief justification
- Note specific examples from the prompt

### Step 3: Strengths Identification
Highlight what the prompt does well:
- ✅ Clear structure and organization
- ✅ Progressive learning approach
- ✅ Practical examples
- ✅ Visual formatting aids
- ✅ Success criteria defined

### Step 4: Weaknesses Identification
Identify areas for improvement:
- ⚠️ Missing information
- ⚠️ Unclear instructions
- ⚠️ Technical assumptions
- ⚠️ Incomplete examples
- ⚠️ Missing edge cases

### Step 5: Improvement Suggestions
Provide specific, actionable recommendations:
- How to improve clarity
- How to increase precision
- How to add depth
- How to enhance relevance
- How to improve usability

### Step 6: Enhanced Version
Create an improved version incorporating all feedback while maintaining original intent.

---

## Example Evaluation Output

### Prompt Being Evaluated:
*[Insert Trillet AI onboarding prompt or related prompt here]*

### Scores:

**Clarity: 4/5**
- Justification: Clear step-by-step instructions with visual references. Minor improvement: Could explicitly state what happens after each action.

**Precision: 5/5**
- Justification: Highly specific with exact button names, locations, and examples. Includes measurable success criteria.

**Depth: 4/5**
- Justification: Comprehensive coverage of all phases. Could add more edge case scenarios (e.g., what if user has no phone number yet?).

**Relevance: 5/5**
- Justification: Perfectly aligned with Trillet AI onboarding. No irrelevant content.

**Usability: 5/5**
- Justification: Excellent for non-technical users. No coding required, includes templates and examples.

### Strengths:
- ✅ Progressive structure (30 min → 7-day roadmap)
- ✅ Multiple examples throughout
- ✅ Testing checklist included
- ✅ Troubleshooting section
- ✅ Confidence score with verification method

### Weaknesses:
- ⚠️ Could add more "what if" scenarios
- ⚠️ Some sections assume prior knowledge (e.g., "Twilio")
- ⚠️ Could include more visual aids or screenshots references

### Suggested Improvements:
1. **Add Edge Case Section**: Include "What if I don't have a phone number yet?" scenarios
2. **Define Technical Terms**: Add glossary for terms like "Twilio", "SIP Address"
3. **Add Visual References**: Include note about where to find screenshots in documentation
4. **Enhance Testing Section**: Add more specific test scenarios (happy path + edge cases)

### Enhanced Prompt:
*[Provide improved version with all suggestions incorporated]*

---

## Trillet AI-Specific Evaluation Checklist

### Content Completeness
- [ ] Platform overview included
- [ ] Sign-up process explained
- [ ] Interface navigation covered
- [ ] Agent creation steps detailed
- [ ] Prompt writing guidance provided
- [ ] Testing procedures included
- [ ] Phone number setup explained
- [ ] Call management covered
- [ ] Transfer setup included
- [ ] Troubleshooting provided
- [ ] Resources linked

### Non-Technical User Support
- [ ] No coding required
- [ ] Technical terms explained
- [ ] Examples provided for each concept
- [ ] Step-by-step instructions
- [ ] Visual formatting aids (tables, lists)
- [ ] Success criteria defined
- [ ] Common mistakes addressed

### Quality Indicators
- [ ] Confidence score provided
- [ ] Verification method stated
- [ ] Sources cited
- [ ] Logical progression
- [ ] Actionable steps
- [ ] Measurable outcomes

---

## Usage Instructions

### To Evaluate a Trillet AI-Related Prompt:

1. **Copy the prompt** you want to evaluate into the "Prompt Being Evaluated" section
2. **Score each criterion** (1-5) with justification
3. **Identify strengths and weaknesses** specific to Trillet AI onboarding context
4. **Provide improvement suggestions** that maintain non-technical user focus
5. **Create enhanced version** incorporating feedback
6. **Verify against Trillet AI-Specific Checklist**

### To Evaluate the Onboarding Guide Itself:

Use this framework to evaluate the original "Good AI Client Onboarding Guide: Trillet AI Platform" document as a prompt for:
- Training AI assistants
- Creating onboarding content
- Generating Trillet AI guides
- Teaching prompt engineering for voice agents

---

## Success Metrics

A high-quality Trillet AI onboarding prompt should achieve:
- **Clarity Score**: ≥ 4/5
- **Precision Score**: ≥ 4/5
- **Depth Score**: ≥ 4/5
- **Relevance Score**: ≥ 4/5
- **Usability Score**: ≥ 4/5

**Overall Quality Threshold**: ≥ 4.0/5.0 average

---

## Notes

- This evaluation framework is specifically designed for Trillet AI platform content
- Focus is on non-technical users (Good AI clients)
- Emphasizes practical, actionable guidance
- Values clarity over technical sophistication
- Prioritizes user success over comprehensive technical coverage

---

*Use this framework to ensure Trillet AI prompts meet the highest standards for clarity, precision, depth, relevance, and usability.*

