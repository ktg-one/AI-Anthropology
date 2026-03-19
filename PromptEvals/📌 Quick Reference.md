---
title: "Quick Reference"
type: reference
created: 2025-01-20
tags: [reference, cheat-sheet, quick]
---

# 📌 Quick Reference

> Cheat sheet for the Advanced Prompt Directory

---

## 🎯 Essential Links

| Feature | Link |
|---------|------|
| Main Hub | [[📚 PROMPT DIRECTORY\|PROMPT DIRECTORY]] |
| Registry | [[📋 Prompt Registry\|Prompt Registry]] |
| Tags | [[🏷️ Tag Index\|Tag Index]] |
| Search | [[🔍 Search Hub\|Search Hub]] |
| Templates | [[📦 Prompt Templates\|Prompt Templates]] |
| Analytics | [[📊 Analytics Dashboard\|Analytics Dashboard]] |

---

## 📋 Frontmatter Template

```yaml
---
title: "Prompt Name"
version: "v1.0"
status: "ACTIVE" | "TESTING" | "ARCHIVED" | "DEPRECATED"
model: "Claude, GPT-5.1, Gemini"
tags: [claude, system, research]
created: "YYYY-MM-DD"
updated: "YYYY-MM-DD"
---
```

---

## 🏷️ Essential Tags

### Status
- `#active` - Production ready
- `#testing` - Under evaluation
- `#archived` - Stored for reference
- `#deprecated` - Outdated

### Models
- `#claude` `#gpt` `#gemini` `#perplexity` `#qwen` `#deepseek` `#kimi`

### Types
- `#system` `#instruction` `#template` `#technique` `#framework`

---

## 🔍 Quick Searches

### Active Prompts
```dataview
TABLE version, status FROM "01-Prompt-dump" WHERE status = "ACTIVE"
```

### By Tag
```dataview
TABLE version FROM "01-Prompt-dump" WHERE contains(tags, "claude")
```

### Recent Updates
```dataview
TABLE version, updated FROM "01-Prompt-dump" WHERE updated >= date(today) - dur(7 days)
```

---

## 📝 Naming Convention

Format: `YYYYMMDD-creator-name-v[version].md`

Example: `20250120-ktg-Research-Framework-v1.0.md`

---

## ✅ Checklist

Creating a new prompt:
- [ ] Copy template
- [ ] Fill frontmatter
- [ ] Add tags
- [ ] Set version
- [ ] Set status
- [ ] Name file correctly

---

## 🎨 Obsidian Shortcuts

- `Ctrl+O` - Quick switcher
- `Ctrl+Shift+F` - Search
- `Ctrl+G` - Graph view
- `Ctrl+P` - Command palette

---

*Keep this handy for quick access!*

