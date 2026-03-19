---
title: "Prompt Registry"
type: registry
created: 2025-01-20
tags: [registry, catalog, index]
---

# 📋 Prompt Registry

> Complete catalog of all prompts with metadata, versioning, and status tracking

---

## 🔍 Filter Views

### All Active Prompts
```dataview
TABLE 
  version as "Version",
  status as "Status",
  model as "Model",
  updated as "Updated",
  tags as "Tags"
FROM "01-Prompt-dump"
WHERE status = "ACTIVE"
SORT updated DESC
```

### Latest Versions
```dataview
TABLE 
  version as "Version",
  status as "Status",
  model as "Model",
  created as "Created"
FROM "01-Prompt-dump"
WHERE version
SORT version DESC
LIMIT 20
```

### By Model Compatibility
```dataview
TABLE 
  version,
  status,
  updated
FROM "01-Prompt-dump"
WHERE model
SORT model ASC, updated DESC
```

### Recently Updated
```dataview
TABLE 
  file.link as "Prompt",
  version,
  status,
  updated
FROM "01-Prompt-dump"
WHERE updated
SORT updated DESC
LIMIT 15
```

---

## 📊 Statistics

### Status Breakdown
```dataview
TABLE length(rows) as "Count"
FROM "01-Prompt-dump"
GROUP BY status
SORT length(rows) DESC
```

### Version Distribution
```dataview
TABLE length(rows) as "Count"
FROM "01-Prompt-dump"
WHERE version
GROUP BY version
SORT length(rows) DESC
LIMIT 10
```

### Model Compatibility
```dataview
TABLE length(rows) as "Count"
FROM "01-Prompt-dump"
WHERE model
GROUP BY model
SORT length(rows) DESC
```

---

## 🎯 Quick Actions

- [[📦 Prompt Templates|Create New Prompt]]
- [[🔍 Search Hub|Advanced Search]]
- [[📊 Analytics Dashboard|View Analytics]]

---

*This registry auto-updates as you add prompts with proper frontmatter*

