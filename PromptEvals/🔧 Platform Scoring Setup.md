---
title: "Platform Scoring Setup"
type: setup
created: 2025-01-20
tags: [setup, scoring, platforms]
status: "ACTIVE"
priority: "HIGH"
---

# 🔧 Platform Scoring Setup

> **Quick setup for scoring frameworks** | Get scores from each platform

---

## 🎯 Quick Reference

### Platform Scoring Options

| Platform | Scoring Method | Setup Time |
|----------|---------------|------------|
| **Vertex AI** | Built-in framework | ✅ Already know |
| **OpenAI** | Evals framework | 10 min |
| **Anthropic** | Self-evaluation | 5 min |
| **Gemini** | Self-evaluation | 5 min |
| **xAI** | Check API docs | Varies |

---

## 🚀 Quick Setup Guides

### 1. Vertex AI (You Know This)

**Access:**
- Go to: https://console.cloud.google.com/vertex-ai/studio
- Look for "Evaluation" or "Scoring" features
- Use built-in framework

**If changed:**
- Use Vertex AI for testing
- Score responses yourself
- Document results

---

### 2. OpenAI Evals (Recommended)

**Install:**
```bash
pip install evals
```

**Use:**
```python
from evals import Evaluator

evaluator = Evaluator()

# Score your CoD prompt
results = evaluator.evaluate(
    prompt="Your Chain of Density prompt...",
    model="gpt-4",
    metrics=["clarity", "effectiveness", "quality"]
)
```

**Benefits:**
- ✅ Open source
- ✅ Well-documented
- ✅ Easy to use
- ✅ Standard framework

---

### 3. Anthropic (Self-Evaluation)

**Setup:**
```python
import anthropic
client = anthropic.Anthropic(api_key="your-key")

def score_prompt(prompt, response):
    message = client.messages.create(
        model="claude-3-opus-20240229",
        messages=[{
            "role": "user",
            "content": f"Score this prompt 1-10: {prompt}\nResponse: {response}"
        }]
    )
    return message.content[0].text
```

**Use Claude to score itself** - Simple and effective.

---

### 4. Gemini (Self-Evaluation)

**Setup:**
```python
import google.generativeai as genai
genai.configure(api_key="your-key")

def score_prompt(prompt, response):
    model = genai.GenerativeModel('gemini-pro')
    result = model.generate_content(
        f"Score this prompt 1-10: {prompt}\nResponse: {response}"
    )
    return result.text
```

**Use Gemini to score itself** - Quick setup.

---

### 5. xAI / Others

**Check their API docs:**
- Look for "evaluation" endpoints
- Or use self-evaluation pattern
- Test and document

---

## 📊 Universal Scoring Script

### One Script for All Platforms

```python
"""
Universal Prompt Scoring Script
Tests Chain of Density across platforms and gets scores
"""

def score_cod_all_platforms():
    """Score Chain of Density on all platforms"""
    
    cod_prompt = "Your Chain of Density prompt here..."
    
    results = {}
    
    # 1. Vertex AI
    try:
        vertex_score = score_vertex_ai(cod_prompt)
        results['vertex_ai'] = vertex_score
    except:
        results['vertex_ai'] = "Not available"
    
    # 2. OpenAI Evals
    try:
        openai_score = score_openai_evals(cod_prompt)
        results['openai'] = openai_score
    except:
        results['openai'] = "Not available"
    
    # 3. Anthropic
    try:
        anthropic_score = score_anthropic(cod_prompt)
        results['anthropic'] = anthropic_score
    except:
        results['anthropic'] = "Not available"
    
    # 4. Gemini
    try:
        gemini_score = score_gemini(cod_prompt)
        results['gemini'] = gemini_score
    except:
        results['gemini'] = "Not available"
    
    # 5. +1 more
    # Add your 5th platform
    
    return results

# Run and save
scores = score_cod_all_platforms()
print(scores)
```

---

## ✅ Action Items

### This Week
- [ ] Set up OpenAI Evals
- [ ] Set up Anthropic self-eval
- [ ] Set up Gemini self-eval
- [ ] Test CoD on all platforms
- [ ] Get scores
- [ ] Document results

### For Paper
- [ ] Include validation section
- [ ] Show platform scores
- [ ] Document compatibility
- [ ] Keep it simple

---

*Get scores from each platform - use whatever works!*

