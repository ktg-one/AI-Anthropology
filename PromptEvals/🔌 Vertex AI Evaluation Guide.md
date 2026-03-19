---
title: "Vertex AI Evaluation Guide"
type: guide
created: 2025-01-20
tags: [vertex-ai, evaluation, google-cloud]
status: "ACTIVE"
priority: "HIGH"
---

# 🔌 Vertex AI Evaluation Guide

> **How to use Vertex AI for evaluation** | Updated for current Vertex AI

---

## 🎯 What Changed in Vertex AI

Vertex AI has evolved - here's how to use it now:

### Current Vertex AI Structure
- **Vertex AI Studio** - Web interface for testing
- **Vertex AI Workbench** - Notebook environment
- **Vertex AI API** - Programmatic access
- **Model Garden** - Pre-trained models

---

## 🚀 Quick Setup

### Option 1: Vertex AI Studio (Easiest)

1. **Go to**: https://console.cloud.google.com/vertex-ai/studio
2. **Sign in** with Google account
3. **Select project** (or create new)
4. **Choose model** (Gemini Pro, Claude, etc.)
5. **Start conversation** - Test your prompts
6. **Save conversations** - Use "Save" button or export

**Benefits:**
- ✅ Web interface (no code needed)
- ✅ Saves conversations automatically
- ✅ Easy to use
- ✅ Multiple models available

### Option 2: Vertex AI API (Programmatic)

```python
from google.cloud import aiplatform
from vertexai.preview.generative_models import GenerativeModel

# Initialize
aiplatform.init(project="your-project-id", location="us-central1")

# Load model
model = GenerativeModel("gemini-pro")

# Test prompt
response = model.generate_content("Your prompt here")
print(response.text)
```

### Option 3: Vertex AI Workbench (Notebooks)

1. Go to: https://console.cloud.google.com/vertex-ai/workbench
2. Create notebook instance
3. Use Jupyter/Lab interface
4. Test prompts in notebooks
5. Save results

---

## 📊 Evaluation Setup

### Using Vertex AI for Prompt Evaluation

```python
from google.cloud import aiplatform
from vertexai.preview.generative_models import GenerativeModel
import json

# Initialize
aiplatform.init(project="your-project-id", location="us-central1")

def evaluate_prompt(prompt, model_name="gemini-pro"):
    """Evaluate a prompt using Vertex AI"""
    
    model = GenerativeModel(model_name)
    
    # Add evaluation instructions
    evaluation_prompt = f"""
    Evaluate the following prompt and provide scores:
    
    Prompt: {prompt}
    
    Provide scores for:
    1. Instruction Adherence (1-10)
    2. Confidence Calibration (1-10)
    3. Adaptability (1-10)
    4. Task Completion Quality (1-10)
    5. Performance-to-Cost Ratio (1-10)
    6. Overall Utility Score (1-10)
    
    Format as JSON.
    """
    
    response = model.generate_content(evaluation_prompt)
    return response.text

# Test your prompts
test_prompts = [
    "Your KTG-DIRECTIVE prompt...",
    "Your Chain of Density prompt...",
]

results = []
for prompt in test_prompts:
    evaluation = evaluate_prompt(prompt)
    results.append({
        'prompt': prompt,
        'evaluation': evaluation
    })

# Save results
with open('vertex_ai_evaluations.json', 'w') as f:
    json.dump(results, f, indent=2)
```

---

## 🔍 Finding Evaluation Features

### Current Vertex AI Features

**In Vertex AI Studio:**
1. **Prompt Testing** - Test prompts directly
2. **Conversation History** - Review past tests
3. **Model Comparison** - Compare different models
4. **Export** - Download conversations

**In Vertex AI API:**
1. **Batch Prediction** - Test multiple prompts
2. **Custom Metrics** - Define evaluation metrics
3. **Evaluation Jobs** - Automated evaluation
4. **Results Storage** - Save evaluations

### Evaluation Jobs (If Available)

```python
from google.cloud import aiplatform

# Create evaluation job
evaluation_job = aiplatform.EvaluationJob.create(
    display_name="prompt-evaluation",
    model_name="gemini-pro",
    evaluation_dataset="your-dataset",
    evaluation_metrics=["instruction_adherence", "quality"]
)

# Run evaluation
evaluation_job.run()

# Get results
results = evaluation_job.get_results()
```

---

## 🛠️ Alternative: Use Vertex AI for Testing, External Tools for Eval

### Recommended Approach

**Use Vertex AI for:**
- ✅ Testing prompts
- ✅ Getting responses
- ✅ Model comparison

**Use External Tools for:**
- ✅ Evaluation metrics
- ✅ Scoring
- ✅ Analysis

### Combined Workflow

```python
# 1. Test prompt with Vertex AI
from google.cloud import aiplatform
from vertexai.preview.generative_models import GenerativeModel

aiplatform.init(project="your-project-id", location="us-central1")
model = GenerativeModel("gemini-pro")
response = model.generate_content("Your prompt")

# 2. Evaluate with your own metrics
def evaluate_response(response_text, prompt):
    # Your evaluation logic here
    scores = {
        'instruction_adherence': calculate_score(response_text, prompt),
        'confidence_calibration': assess_confidence(response_text),
        # ... your metrics
    }
    return scores

# 3. Store results
evaluation = evaluate_response(response.text, "Your prompt")
```

---

## 📋 Step-by-Step: Getting Started

### Step 1: Access Vertex AI
1. Go to: https://console.cloud.google.com/
2. Sign in with Google account
3. Create/select project
4. Enable Vertex AI API

### Step 2: Choose Interface
- **Studio** - For quick testing (web)
- **API** - For programmatic access
- **Workbench** - For notebooks

### Step 3: Test Your Prompts
- Enter prompt in Studio
- Or use API to test programmatically
- Save results

### Step 4: Evaluate
- Use Vertex AI responses
- Apply your evaluation metrics
- Document results

---

## 🔧 Troubleshooting

### "Can't find evaluation feature"
- **Solution**: Use Vertex AI for testing, external tools for evaluation
- Vertex AI may have changed evaluation features
- Use API responses + your own evaluation

### "API changed"
- **Solution**: Check latest Vertex AI Python SDK docs
- Use `vertexai` package (newer)
- Or use REST API directly

### "Don't know how to evaluate"
- **Solution**: 
  1. Get responses from Vertex AI
  2. Apply your metrics (renamed)
  3. Score responses
  4. Document results

---

## ✅ Action Items

### This Week
- [ ] Access Vertex AI Studio
- [ ] Test one prompt
- [ ] Get API access (if needed)
- [ ] Set up evaluation workflow
- [ ] Document process

### For Validation
- [ ] Test prompts on Vertex AI
- [ ] Get responses
- [ ] Apply evaluation metrics
- [ ] Compare with other platforms
- [ ] Document results

---

## 💡 Recommended Workflow

1. **Test on Vertex AI** - Get responses
2. **Evaluate locally** - Use your metrics
3. **Compare platforms** - Test on 5+ platforms
4. **Document** - Save all results
5. **Publish** - Include validation in paper

---

*Vertex AI for testing, your metrics for evaluation - best of both worlds!*

