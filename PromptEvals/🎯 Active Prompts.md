---
title: "Active Prompts"
type: view
created: 2025-01-20
tags: [active, production, current]
---

# 🎯 Active Prompts

> Currently active, production-ready prompts

---

## 📋 All Active Prompts

```dataview
TABLE 
  file.link as "Prompt",
  version as "Version",
  model as "Model",
  updated as "Updated",
  tags as "Tags"
FROM "01-Prompt-dump"
WHERE status = "ACTIVE"
SORT updated DESC
```

---

## 🔍 Filter Active Prompts

### By Model
```dataview
TABLE version, updated, tags
FROM "01-Prompt-dump"
WHERE status = "ACTIVE" AND contains(model, "Claude")
SORT updated DESC
```

### By Category
```dataview
TABLE version, model, updated
FROM "01-Prompt-dump"
WHERE status = "ACTIVE" AND category
SORT category ASC, updated DESC
```

### Recently Updated
```dataview
TABLE version, model, updated
FROM "01-Prompt-dump"
WHERE status = "ACTIVE" AND updated >= date(today) - dur(30 days)
SORT updated DESC
```

---

## 📊 Statistics

```dataview
TABLE length(rows) as "Count"
FROM "01-Prompt-dump"
WHERE status = "ACTIVE"
GROUP BY model
SORT length(rows) DESC
```

---

*These prompts are production-ready and actively maintained*

