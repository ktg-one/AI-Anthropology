---
title: "Search Hub"
type: search
created: 2025-01-20
tags: [search, discovery, queries]
---

# 🔍 Search Hub

> Advanced search queries for discovering prompts

---

## 🎯 Quick Searches

### Find Prompts by Model
```dataview
TABLE version, status, updated
FROM "01-Prompt-dump"
WHERE contains(model, "Claude") OR contains(tags, "claude")
SORT updated DESC
```

### Find Active Prompts
```dataview
TABLE version, model, updated, tags
FROM "01-Prompt-dump"
WHERE status = "ACTIVE"
SORT updated DESC
```

### Find Latest Versions
```dataview
TABLE version, status, model, updated
FROM "01-Prompt-dump"
WHERE version AND version != null
SORT version DESC
LIMIT 20
```

### Find by Technique
```dataview
TABLE version, status, updated
FROM "01-Prompt-dump"
WHERE contains(tags, "chain-of-thought") OR contains(tags, "self-criticism")
SORT updated DESC
```

---

## 🔎 Advanced Queries

### Prompts Updated This Month
```dataview
TABLE version, status, model
FROM "01-Prompt-dump"
WHERE updated >= date(today) - dur(30 days)
SORT updated DESC
```

### High Version Numbers (Mature Prompts)
```dataview
TABLE version, status, model, updated
FROM "01-Prompt-dump"
WHERE version AND version >= "v20"
SORT version DESC
```

### Multi-Model Compatible
```dataview
TABLE version, status, updated
FROM "01-Prompt-dump"
WHERE contains(tags, "multi-model") OR contains(model, ",")
SORT updated DESC
```

### Production Ready
```dataview
TABLE version, model, updated
FROM "01-Prompt-dump"
WHERE status = "ACTIVE" AND contains(tags, "production")
SORT updated DESC
```

---

## 📊 Search by Metadata

### By Creator
```dataview
TABLE version, status, updated
FROM "01-Prompt-dump"
WHERE creator
SORT creator ASC, updated DESC
```

### By Category
```dataview
TABLE version, status, updated
FROM "01-Prompt-dump"
WHERE category
SORT category ASC, updated DESC
```

### By Complexity
```dataview
TABLE version, status, complexity, updated
FROM "01-Prompt-dump"
WHERE complexity
SORT complexity DESC, updated DESC
```

---

## 🎨 Custom Search Builder

Create your own queries using Dataview syntax:

```dataview
TABLE 
  file.link as "Prompt",
  version,
  status,
  model,
  updated
FROM "01-Prompt-dump"
WHERE 
  status = "ACTIVE" AND
  (contains(tags, "research") OR contains(tags, "analysis")) AND
  updated >= date(today) - dur(60 days)
SORT updated DESC
```

---

## 💡 Search Tips

1. **Use tags**: Most powerful way to filter
2. **Combine filters**: Use AND/OR logic
3. **Sort by date**: Find recent updates
4. **Filter by status**: Focus on active prompts
5. **Search content**: Use Obsidian's built-in search (Ctrl+Shift+F)

---

*Need help? Check [[📖 Documentation|Documentation]] for query syntax*

