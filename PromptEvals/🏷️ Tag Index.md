---
title: "Tag Index"
type: taxonomy
created: 2025-01-20
tags: [tags, taxonomy, categories]
---

# 🏷️ Tag Index

> Comprehensive tag taxonomy for prompt organization and discovery

---

## 📚 Tag Categories

### Model Tags
- `#claude` - Claude-specific prompts
- `#gpt` - GPT/OpenAI prompts
- `#gemini` - Google Gemini prompts
- `#perplexity` - Perplexity prompts
- `#qwen` - Qwen prompts
- `#deepseek` - DeepSeek prompts
- `#kimi` - Kimi prompts
- `#multi-model` - Works with multiple models

### Status Tags
- `#active` - Currently in use
- `#testing` - Under evaluation
- `#archived` - Stored for reference
- `#deprecated` - Outdated, replaced

### Type Tags
- `#system` - System prompts
- `#instruction` - Instruction prompts
- `#template` - Reusable templates
- `#technique` - Prompt engineering techniques
- `#framework` - Complete frameworks
- `#meta` - Meta-prompts (prompts about prompts)

### Domain Tags
- `#research` - Research prompts
- `#business` - Business applications
- `#coding` - Programming/development
- `#writing` - Writing/editing
- `#analysis` - Data analysis
- `#strategy` - Strategic planning
- `#education` - Educational content

### Technique Tags
- `#chain-of-thought` - CoT reasoning
- `#few-shot` - Few-shot examples
- `#zero-shot` - Zero-shot prompts
- `#self-criticism` - Self-critique techniques
- `#decomposition` - Problem decomposition
- `#ensembling` - Ensemble methods
- `#graph-of-thought` - GoT techniques

### Quality Tags
- `#production` - Production-ready
- `#experimental` - Experimental/novel
- `#optimized` - Performance optimized
- `#validated` - Tested and validated

---

## 🔍 Browse by Tag

### Model Tags
```dataview
TABLE version, status, updated
FROM "01-Prompt-dump"
WHERE contains(tags, "claude")
SORT updated DESC
LIMIT 10
```

### Status Tags
```dataview
TABLE version, model, updated
FROM "01-Prompt-dump"
WHERE contains(tags, "active")
SORT updated DESC
LIMIT 10
```

### Type Tags
```dataview
TABLE version, status, updated
FROM "01-Prompt-dump"
WHERE contains(tags, "system")
SORT updated DESC
LIMIT 10
```

---

## 📊 Tag Statistics

```dataview
TABLE length(rows) as "Count"
FROM "01-Prompt-dump"
FLATTEN tags as tag
GROUP BY tag
SORT length(rows) DESC
LIMIT 20
```

---

## 🎯 Tagging Guidelines

1. **Always include**: Status tag (`#active`, `#testing`, etc.)
2. **Include model**: At least one model tag
3. **Add domain**: Relevant domain tags
4. **Use techniques**: Tag applicable techniques
5. **Be specific**: Use precise tags, avoid generic ones

---

*Tags enable powerful search and discovery. Use them consistently!*

