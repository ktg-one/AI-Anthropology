---
title: "Framework Architecture"
type: framework-index
created: 2025-01-20
tags: [framework, architecture, system-prompts]
---

# 🏗️ Framework Architecture

> **Advanced framework tracking for complex system prompts** | Handle version hierarchies, component relationships, and technique dependencies

---

## 🎯 Framework vs Prompt vs Technique

### Framework-Level Prompts
Complete cognitive OS architectures with multiple components:
- **KTG-DIRECTIVE** - Production-grade cognitive OS
- **QMDR** - Quantum Master Deep Research
- **Triplexity** - Multi-model research frameworks
- **Perpromperty Nexus** - Business opportunity frameworks

### Component Prompts
Modular pieces that integrate into frameworks:
- **MR_RUG** - Mixture of Reasoning Experts initialization
- **FCoT/CoC Router** - Reasoning chain selector
- **Prompt Bombs** - Information densification nodes
- **Skeletrain of Thought** - Planning framework

### Technique Prompts
Standalone methodologies:
- **Chain of Thought** variants
- **Self-Criticism** methods
- **Decomposition** strategies
- **Ensembling** approaches

---

## 🔗 Framework Relationships

### KTG-DIRECTIVE Ecosystem

```dataview
TABLE 
  version as "Version",
  status as "Status",
  type as "Type",
  parent as "Parent Framework"
FROM "01-Prompt-dump"
WHERE contains(tags, "ktg-directive") OR contains(title, "KTG-DIRECTIVE")
SORT version DESC
```

### Component Mapping

```dataview
TABLE 
  file.link as "Component",
  parent as "Used In",
  version as "Version"
FROM "01-Prompt-dump"
WHERE type = "component" OR parent
SORT parent ASC, version DESC
```

---

## 📊 Framework Hierarchy View

### Top-Level Frameworks
```dataview
TABLE 
  version as "Version",
  status as "Status",
  components as "Components",
  updated as "Updated"
FROM "01-Prompt-dump"
WHERE type = "framework" AND NOT parent
SORT updated DESC
```

### Framework Components
```dataview
TABLE 
  file.link as "Component",
  parent as "Framework",
  purpose as "Purpose"
FROM "01-Prompt-dump"
WHERE parent
SORT parent ASC
```

---

## 🔄 Version Evolution Tracking

### KTG-DIRECTIVE Evolution
```dataview
TABLE 
  file.link as "Version",
  version as "v#",
  created as "Created",
  changelog as "Key Changes"
FROM "01-Prompt-dump"
WHERE contains(title, "KTG-DIRECTIVE") OR contains(tags, "ktg-directive")
SORT version DESC
```

### Version Comparison
Track what changed between versions:
- v20 → v21: Expert ARQ Meta-Governance
- v21 → v22: Graph of Thoughts
- v22 → v23: Enhanced CoVE Variants
- v23 → v25: Anti-Lazy + Quantum Deep Research + Expert Routing

---

## 🧩 Component Dependencies

### Techniques Used in Frameworks
```dataview
TABLE 
  file.link as "Framework",
  techniques as "Techniques",
  version as "Version"
FROM "01-Prompt-dump"
WHERE type = "framework" AND techniques
SORT version DESC
```

### Component Integration Map
- **KTG-DIRECTIVE v25** includes:
  - MR_RUG (Phases 1-3)
  - FCoT/CoC Router (Phase 4)
  - SoT/GoT (Phase 5)
  - Prompt Bombs (throughout)
  - Expert ARQ (meta-layer)
  - CoVE variants (verification)

---

## 🎨 Model Variants

### Framework Variants by Model
```dataview
TABLE 
  file.link as "Variant",
  parent as "Base Framework",
  model as "Model",
  version as "Version"
FROM "01-Prompt-dump"
WHERE type = "variant" OR contains(tags, "variant")
SORT parent ASC, model ASC
```

### Model-Specific Optimizations
- **Claude Variants**: Optimized for Claude's strengths
- **Perplexity Variants**: Deep research optimizations
- **GPT Variants**: OpenAI-specific adaptations
- **Multi-Model**: Universal compatibility

---

## 📈 Framework Analytics

### Framework Maturity
```dataview
TABLE 
  file.link as "Framework",
  version as "Version",
  status as "Status",
  components as "Components"
FROM "01-Prompt-dump"
WHERE type = "framework"
SORT version DESC
```

### Most Used Components
```dataview
TABLE 
  file.link as "Component",
  length(rows) as "Used In"
FROM "01-Prompt-dump"
WHERE parent
GROUP BY file.link
SORT length(rows) DESC
```

---

## 🔍 Advanced Queries

### Find Frameworks Using Specific Technique
```dataview
TABLE 
  file.link as "Framework",
  version,
  techniques
FROM "01-Prompt-dump"
WHERE type = "framework" AND contains(techniques, "Prompt Bombs")
```

### Find All Components of a Framework
```dataview
TABLE 
  file.link as "Component",
  version,
  purpose
FROM "01-Prompt-dump"
WHERE parent = "KTG-DIRECTIVE"
SORT version DESC
```

### Framework Evolution Timeline
```dataview
TABLE 
  file.link as "Version",
  version as "v#",
  created as "Date",
  changelog as "Changes"
FROM "01-Prompt-dump"
WHERE contains(title, "KTG-DIRECTIVE")
SORT created ASC
```

---

*This system handles complex framework architectures, not just simple prompts*

