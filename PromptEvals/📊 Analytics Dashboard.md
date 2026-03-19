---
title: "Analytics Dashboard"
type: dashboard
created: 2025-01-20
tags: [analytics, statistics, insights]
---

# 📊 Analytics Dashboard

> Insights and statistics about your prompt library

---

## 📈 Overview Statistics

### Total Prompts
```dataview
TABLE length(rows) as "Total"
FROM "01-Prompt-dump"
```

### By Status
```dataview
TABLE 
  status as "Status",
  length(rows) as "Count",
  round(length(rows) * 100.0 / length(flatten(file.lists)) * 100) / 100 as "%"
FROM "01-Prompt-dump"
GROUP BY status
SORT length(rows) DESC
```

### By Model
```dataview
TABLE 
  model as "Model",
  length(rows) as "Count"
FROM "01-Prompt-dump"
WHERE model
GROUP BY model
SORT length(rows) DESC
```

---

## 📅 Activity Timeline

### Prompts Created This Month
```dataview
TABLE 
  file.link as "Prompt",
  version,
  status
FROM "01-Prompt-dump"
WHERE created >= date(today) - dur(30 days)
SORT created DESC
```

### Recently Updated
```dataview
TABLE 
  file.link as "Prompt",
  version,
  status,
  updated
FROM "01-Prompt-dump"
WHERE updated >= date(today) - dur(7 days)
SORT updated DESC
```

---

## 🏆 Top Categories

### Most Used Tags
```dataview
TABLE length(rows) as "Usage"
FROM "01-Prompt-dump"
FLATTEN tags as tag
GROUP BY tag
SORT length(rows) DESC
LIMIT 15
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

---

## 🎯 Quality Metrics

### Production Ready Prompts
```dataview
TABLE 
  file.link as "Prompt",
  version,
  model
FROM "01-Prompt-dump"
WHERE status = "ACTIVE" AND contains(tags, "production")
SORT version DESC
```

### Testing Phase
```dataview
TABLE 
  file.link as "Prompt",
  version,
  created
FROM "01-Prompt-dump"
WHERE status = "TESTING"
SORT created DESC
```

---

## 📊 Growth Trends

### Creation Rate
```dataview
TABLE 
  dateformat(created, "YYYY-MM") as "Month",
  length(rows) as "Created"
FROM "01-Prompt-dump"
WHERE created
GROUP BY dateformat(created, "YYYY-MM")
SORT dateformat(created, "YYYY-MM") DESC
LIMIT 12
```

### Update Frequency
```dataview
TABLE 
  dateformat(updated, "YYYY-MM") as "Month",
  length(rows) as "Updated"
FROM "01-Prompt-dump"
WHERE updated
GROUP BY dateformat(updated, "YYYY-MM")
SORT dateformat(updated, "YYYY-MM") DESC
LIMIT 12
```

---

## 🔍 Insights

### Most Versatile Prompts (Multi-Model)
```dataview
TABLE 
  file.link as "Prompt",
  version,
  model
FROM "01-Prompt-dump"
WHERE contains(model, ",") OR contains(tags, "multi-model")
SORT version DESC
```

### Mature Prompts (High Version Numbers)
```dataview
TABLE 
  file.link as "Prompt",
  version,
  status,
  updated
FROM "01-Prompt-dump"
WHERE version AND version >= "v20"
SORT version DESC
```

---

*Dashboard updates automatically as you add prompts with metadata*

