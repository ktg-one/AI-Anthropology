---
title: "Quick Install Guide"
type: guide
created: 2025-01-20
tags: [install, quick-start, tools]
status: "ACTIVE"
priority: "HIGH"
---

# 🚀 Quick Install Guide

> **Install evaluation tools fast** | Get set up in 10 minutes

---

## ⚡ Priority: Publish CoD First!

**Before installing tools:**
1. ✅ List your CoD applications (TODAY)
2. ✅ Complete paper draft (TOMORROW)
3. ✅ Submit to ArXiv (DAY 3)
4. ✅ Then install tools for future work

**Tools can wait - priority can't!**

---

## 🛠️ VS Code Extensions (5 minutes)

### Step 1: Open VS Code Extensions
- Press `Ctrl+Shift+X`
- Or click Extensions icon

### Step 2: Install These (One by One)

**1. Continue** (Most Important)
- Search: "Continue"
- Install: "Continue - AI Code Completion"
- Configure: Add API keys (OpenAI, Anthropic)

**2. Jupyter**
- Search: "Jupyter"
- Install: "Jupyter" by Microsoft
- Use: Create `.ipynb` files for evaluation

**3. REST Client** (Optional)
- Search: "REST Client"
- Install: "REST Client" by Huachao Mao
- Use: Test LLM APIs

---

## 🐍 Python Packages (5 minutes)

### Install in Terminal

```bash
# Open terminal in VS Code (Ctrl+`)
# Run these commands:

pip install langchain langchain-openai langchain-anthropic
pip install evals
pip install pandas openai anthropic
```

### Verify Installation

```bash
python -c "import langchain; print('LangChain OK')"
python -c "import evals; print('Evals OK')"
```

---

## ✅ Quick Test

### Test Continue Extension

1. Open any `.md` file
2. Select some text
3. Press `Ctrl+L` (or use Continue chat)
4. Ask: "Evaluate this prompt"
5. Should get LLM response

### Test Python Packages

Create `test_eval.py`:
```python
from langchain.evaluation import load_evaluator
print("LangChain installed successfully!")
```

Run: `python test_eval.py`

---

## 🎯 What to Do NOW

### Today (Priority!)
1. ✅ **List all CoD applications** - Use template
2. ✅ **Add to paper** - Applications section
3. ✅ **Complete draft** - Finish paper

### Tomorrow
1. ✅ **Format for ArXiv** - Create PDF
2. ✅ **Submit** - Upload to ArXiv (PRIORITY!)

### Day 3
1. ✅ **Install tools** - Use this guide
2. ✅ **Set up evaluation** - For future work

---

## 📋 Installation Checklist

### VS Code Extensions
- [ ] Continue (LLM integration)
- [ ] Jupyter (notebooks)
- [ ] REST Client (optional)

### Python Packages
- [ ] langchain
- [ ] evals
- [ ] pandas
- [ ] openai
- [ ] anthropic

### Configuration
- [ ] API keys added to Continue
- [ ] Test workflow working

---

## 💡 After Installation

### Use Tools For:
- ✅ Future prompt evaluation
- ✅ Testing new prompts
- ✅ Analyzing responses
- ✅ Documenting results

### But First:
- ✅ **Publish CoD** - Establish priority
- ✅ **Claim applications** - List them all
- ✅ **Get timestamp** - ArXiv submission

---

*Tools help later - priority helps NOW!*

