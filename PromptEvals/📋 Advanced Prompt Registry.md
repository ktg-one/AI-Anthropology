---
title: "Advanced Prompt Registry"
type: registry
created: 2025-01-20
tags: [registry, advanced, framework]
---

# 📋 Advanced Prompt Registry

> **Framework-aware catalog** | Handles complex system prompts, version hierarchies, and component relationships

---

## 🎯 Classification System

### By Type
```dataview
TABLE 
  file.link as "Prompt",
  version as "Version",
  status as "Status",
  model as "Model"
FROM "01-Prompt-dump"
WHERE type
GROUP BY type
SORT type ASC
```

### Framework Prompts
```dataview
TABLE 
  file.link as "Framework",
  version as "Version",
  status as "Status",
  components as "Components",
  techniques as "Techniques",
  updated as "Updated"
FROM "01-Prompt-dump"
WHERE type = "framework" OR contains(tags, "framework")
SORT version DESC
```

### Component Prompts
```dataview
TABLE 
  file.link as "Component",
  parent as "Parent Framework",
  version as "Version",
  purpose as "Purpose"
FROM "01-Prompt-dump"
WHERE type = "component" OR parent
SORT parent ASC, version DESC
```

### Technique Prompts
```dataview
TABLE 
  file.link as "Technique",
  version as "Version",
  category as "Category",
  updated as "Updated"
FROM "01-Prompt-dump"
WHERE type = "technique" OR contains(tags, "technique")
SORT updated DESC
```

---

## 🔗 Relationship Mapping

### Framework → Components
```dataview
TABLE 
  parent as "Framework",
  file.link as "Component",
  version as "Version"
FROM "01-Prompt-dump"
WHERE parent
SORT parent ASC, version DESC
```

### Framework → Techniques Used
```dataview
TABLE 
  file.link as "Framework",
  techniques as "Techniques",
  version as "Version"
FROM "01-Prompt-dump"
WHERE type = "framework" AND techniques
SORT version DESC
```

### Version Relationships
```dataview
TABLE 
  file.link as "Version",
  version as "v#",
  previous as "Previous",
  next as "Next",
  created as "Created"
FROM "01-Prompt-dump"
WHERE version AND (previous OR next)
SORT version DESC
```

---

## 📊 KTG-DIRECTIVE Family

### All KTG-DIRECTIVE Versions
```dataview
TABLE 
  file.link as "Version",
  version as "v#",
  status as "Status",
  created as "Created",
  changelog as "Key Changes"
FROM "01-Prompt-dump"
WHERE contains(title, "KTG-DIRECTIVE") OR contains(tags, "ktg-directive")
SORT version DESC
```

### KTG-DIRECTIVE Components
```dataview
TABLE 
  file.link as "Component",
  version as "Version",
  purpose as "Purpose",
  phase as "Phase"
FROM "01-Prompt-dump"
WHERE parent = "KTG-DIRECTIVE" OR contains(parent, "KTG-DIRECTIVE")
SORT phase ASC, version DESC
```

### KTG-DIRECTIVE Model Variants
```dataview
TABLE 
  file.link as "Variant",
  model as "Model",
  version as "Version",
  base as "Base Version"
FROM "01-Prompt-dump"
WHERE contains(title, "KTG") AND (contains(tags, "variant") OR contains(title, "Claude") OR contains(title, "Cascade"))
SORT model ASC, version DESC
```

---

## 🔍 Advanced Filtering

### Production Frameworks
```dataview
TABLE 
  file.link as "Framework",
  version as "Version",
  status as "Status",
  model as "Model"
FROM "01-Prompt-dump"
WHERE type = "framework" AND status = "ACTIVE"
SORT version DESC
```

### Experimental Components
```dataview
TABLE 
  file.link as "Component",
  parent as "Framework",
  status as "Status",
  created as "Created"
FROM "01-Prompt-dump"
WHERE type = "component" AND status = "TESTING"
SORT created DESC
```

### Multi-Model Frameworks
```dataview
TABLE 
  file.link as "Framework",
  version as "Version",
  model as "Model",
  status as "Status"
FROM "01-Prompt-dump"
WHERE type = "framework" AND (contains(model, ",") OR contains(tags, "multi-model"))
SORT version DESC
```

---

## 📈 Statistics

### Framework Distribution
```dataview
TABLE 
  type as "Type",
  length(rows) as "Count"
FROM "01-Prompt-dump"
WHERE type
GROUP BY type
SORT length(rows) DESC
```

### Version Distribution
```dataview
TABLE 
  length(rows) as "Versions"
FROM "01-Prompt-dump"
WHERE version
GROUP BY version
SORT version DESC
LIMIT 10
```

### Component Usage
```dataview
TABLE 
  parent as "Framework",
  length(rows) as "Components"
FROM "01-Prompt-dump"
WHERE parent
GROUP BY parent
SORT length(rows) DESC
```

---

*This registry understands framework hierarchies and relationships*

