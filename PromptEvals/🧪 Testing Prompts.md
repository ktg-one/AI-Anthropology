---
title: "Testing Prompts"
type: view
created: 2025-01-20
tags: [testing, experimental, evaluation]
---

# 🧪 Testing Prompts

> Prompts currently under evaluation and testing

---

## 📋 All Testing Prompts

```dataview
TABLE 
  file.link as "Prompt",
  version as "Version",
  model as "Model",
  created as "Created",
  tags as "Tags"
FROM "01-Prompt-dump"
WHERE status = "TESTING"
SORT created DESC
```

---

## 🔍 Filter Testing Prompts

### By Model
```dataview
TABLE version, created, tags
FROM "01-Prompt-dump"
WHERE status = "TESTING" AND model
SORT model ASC, created DESC
```

### Experimental Features
```dataview
TABLE version, model, created
FROM "01-Prompt-dump"
WHERE status = "TESTING" AND contains(tags, "experimental")
SORT created DESC
```

### Recently Created
```dataview
TABLE version, model, created
FROM "01-Prompt-dump"
WHERE status = "TESTING" AND created >= date(today) - dur(14 days)
SORT created DESC
```

---

## 📊 Statistics

```dataview
TABLE length(rows) as "Count"
FROM "01-Prompt-dump"
WHERE status = "TESTING"
GROUP BY model
SORT length(rows) DESC
```

---

## 🎯 Promotion Checklist

Before moving from TESTING to ACTIVE:
- [ ] Tested with target models
- [ ] Validated outputs
- [ ] Documentation complete
- [ ] Examples provided
- [ ] Version finalized

---

*These prompts are experimental and may change*

