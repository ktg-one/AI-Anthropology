---
title: "Migration Guide"
type: guide
created: 2025-01-20
tags: [migration, setup, guide]
---

# 🔄 Migration Guide

> How to add metadata to existing prompts for the Advanced Prompt Directory

---

## 🎯 Goal

Add frontmatter metadata to your existing prompts so they appear in the directory system.

---

## 📋 Step-by-Step Process

### 1. Identify Prompts to Migrate

Start with your most important prompts in `01-Prompt-dump/`.

### 2. Add Frontmatter

Add YAML frontmatter at the very top of each prompt file:

```yaml
---
title: "Prompt Name"
version: "v25.5"
status: "ACTIVE"
model: "Claude, GPT-5.1, Gemini, Perplexity, Qwen, DeepSeek, Llama"
tags: [claude, system, framework, production]
created: "2025-11-16"
updated: "2025-11-16"
creator: "ktg"
category: "framework"
description: "Production-grade cognitive OS with expert governance"
---
```

### 3. Extract Information from Existing Prompts

Look for these patterns in your existing prompts:

- **Version**: Look for `v25.5`, `v1.0`, etc. in filename or content
- **Model**: Check compatibility notes (e.g., "Compatible: Claude, GPT-5.1")
- **Creator**: Look for creator credits
- **Date**: Use filename date (e.g., `11162025` = `2025-11-16`)

### 4. Example: Migrating KTG-DIRECTIVE

**Before:**
```markdown
# KTG-DIRECTIVE v25.1 – CANONICAL COGNITIVE OS
# Compatible: Claude, GPT-5.1, Gemini, Perplexity, Qwen, DeepSeek, Llama
# Creator: Kevin Tan (ktg.one)
```

**After:**
```yaml
---
title: "KTG-DIRECTIVE"
version: "v25.5"
status: "ACTIVE"
model: "Claude, GPT-5.1, Gemini, Perplexity, Qwen, DeepSeek, Llama"
tags: [claude, system, framework, production, multi-model]
created: "2025-11-16"
updated: "2025-11-16"
creator: "ktg"
category: "framework"
description: "Production-grade cognitive OS with expert governance, adaptive reasoning, multi-modal verification"
---
# KTG-DIRECTIVE v25.1 – CANONICAL COGNITIVE OS
# Compatible: Claude, GPT-5.1, Gemini, Perplexity, Qwen, DeepSeek, Llama
# Creator: Kevin Tan (ktg.one)
```

---

## 🔍 Finding Information

### Version Numbers
- Check filename: `v25.5`, `v1.0`
- Check content: Look for version mentions
- Default to `v1.0` if unknown

### Model Compatibility
- Look for "Compatible:" lines
- Check model-specific folders
- Default to "Multi-model" if unclear

### Dates
- Filename format: `11162025` = `2025-11-16`
- Use creation date from filename
- Set updated to same if no updates

### Status
- **ACTIVE**: Currently in use, production-ready
- **TESTING**: Experimental, under evaluation
- **ARCHIVED**: Reference only, not active
- **DEPRECATED**: Replaced by newer version

---

## 🏷️ Tagging Strategy

### Extract from Content
- Look for technique mentions: "Chain of Thought", "Self-Criticism"
- Identify domain: Research, Business, Coding
- Determine type: System, Instruction, Template

### Common Tag Combinations

**System Prompts:**
```yaml
tags: [system, framework, claude, production]
```

**Research Prompts:**
```yaml
tags: [research, analysis, multi-model, active]
```

**Technique Prompts:**
```yaml
tags: [technique, method, chain-of-thought, active]
```

---

## ⚡ Quick Migration Script

For bulk migration, you can use this pattern:

1. **Identify pattern** in filename (e.g., `11162025-ktg-*`)
2. **Extract date**: `11162025` → `2025-11-16`
3. **Extract creator**: `ktg` from filename
4. **Extract version**: Look for `v*` in filename or content
5. **Add frontmatter** with extracted info

---

## ✅ Migration Checklist

For each prompt:
- [ ] Frontmatter added at top
- [ ] Version number set
- [ ] Status assigned
- [ ] Model compatibility listed
- [ ] Tags added (at least 3-5)
- [ ] Dates set (created/updated)
- [ ] Description added
- [ ] File saved

---

## 🎯 Priority Order

1. **High Priority**: Active, frequently used prompts
2. **Medium Priority**: Testing prompts, recent creations
3. **Low Priority**: Archived, deprecated prompts

---

## 📊 Progress Tracking

Track your migration progress:

```dataview
TABLE version, status
FROM "01-Prompt-dump"
WHERE version
SORT updated DESC
```

---

## 💡 Tips

1. **Start Small**: Migrate 5-10 prompts first
2. **Use Templates**: Copy frontmatter from [[📦 Prompt Templates|Templates]]
3. **Batch Similar**: Group similar prompts for consistent tagging
4. **Test Queries**: Verify prompts appear in [[📋 Prompt Registry|Registry]]
5. **Update Gradually**: Don't need to migrate everything at once

---

## 🆘 Troubleshooting

### Prompts Not Appearing
- Check frontmatter syntax (YAML format)
- Ensure no extra spaces or characters
- Verify field names match exactly

### Dates Not Parsing
- Use format: `YYYY-MM-DD`
- Check for typos
- Ensure dates are in quotes

### Tags Not Working
- Use array format: `[tag1, tag2]`
- No spaces after commas
- Lowercase recommended

---

*Migrate at your own pace - the system works with partial migration!*

