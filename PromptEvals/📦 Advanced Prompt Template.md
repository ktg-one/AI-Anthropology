---
title: "Advanced Prompt Template"
type: template
created: 2025-01-20
tags: [template, framework, advanced]
---

# 📦 Advanced Prompt Template

> **Templates for framework-level prompts** | Handle complex architectures, components, and versioning

---

## 🏗️ Framework Template

Use this for complete cognitive OS architectures:

```markdown
---
title: "[Framework Name]"
type: "framework"
version: "v1.0"
status: "ACTIVE" | "TESTING" | "ARCHIVED" | "DEPRECATED"
model: "Claude, GPT-5.1, Gemini, Perplexity"
category: "framework"
tags: [framework, system, production, multi-model]
created: "YYYY-MM-DD"
updated: "YYYY-MM-DD"
creator: "ktg"
complexity: "high"
description: "Complete cognitive OS architecture"
components: ["Component1", "Component2", "Component3"]
techniques: ["Technique1", "Technique2"]
dependencies: []
previous: ""
next: ""
---

# [Framework Name] v1.0

## Framework Identity
[Core identity and purpose]

## Architecture Overview
[High-level architecture description]

## Components
- **Component1**: [Description]
- **Component2**: [Description]
- **Component3**: [Description]

## Techniques Used
- [Technique1]: [How it's used]
- [Technique2]: [How it's used]

## Model Compatibility
- Claude ✅
- GPT-5.1 ✅
- Gemini ✅

## Usage
[How to use this framework]

## Changelog
### v1.0 (YYYY-MM-DD)
- Initial version
```

---

## 🧩 Component Template

Use this for modular components that integrate into frameworks:

```markdown
---
title: "[Component Name]"
type: "component"
version: "v1.0"
status: "ACTIVE"
parent: "[Framework Name]"
phase: "1-3" | "4" | "5" | "N/A"
purpose: "What this component does"
tags: [component, [parent-framework], [technique]]
created: "YYYY-MM-DD"
updated: "YYYY-MM-DD"
creator: "ktg"
complexity: "medium"
description: "Component description"
---

# [Component Name]
**Phase X of [Framework Name] | Context: [Context]**

## Purpose
[What this component does]

## Integration Points
- **With [Other Component]**: [How they work together]
- **With [Technique]**: [Integration details]

## Execution Flow
[Step-by-step execution]

## Token Overhead
[Performance metrics]

## Output to Next Phase
[What this component outputs]
```

---

## 🔄 Version Template

Use this when creating a new version of an existing framework:

```markdown
---
title: "[Framework Name]"
type: "framework"
version: "v2.0"
status: "ACTIVE"
previous: "v1.0"
next: ""
model: "Claude, GPT-5.1, Gemini"
tags: [framework, [framework-name], production]
created: "YYYY-MM-DD"
updated: "YYYY-MM-DD"
creator: "ktg"
changelog: "Key changes from previous version"
---

# [Framework Name] v2.0

## What's New in v2.0
- [Major change 1]
- [Major change 2]
- [Major change 3]

## Migration from v1.0
[How to migrate from previous version]

## Changelog
### v2.0 (YYYY-MM-DD)
- [Change 1]
- [Change 2]

### v1.0 (YYYY-MM-DD)
- [Previous changes]
```

---

## 🎨 Model Variant Template

Use this for model-specific optimizations:

```markdown
---
title: "[Framework Name] - [Model] Variant"
type: "variant"
version: "v1.0"
status: "ACTIVE"
parent: "[Base Framework Name]"
base: "v1.0"
model: "[Model Name]"
tags: [variant, [framework-name], [model], optimized]
created: "YYYY-MM-DD"
updated: "YYYY-MM-DD"
creator: "ktg"
optimizations: ["Optimization1", "Optimization2"]
---

# [Framework Name] - [Model] Variant v1.0
**Optimized for [Model Name]**

## Model-Specific Optimizations
- [Optimization 1]: [Details]
- [Optimization 2]: [Details]

## Differences from Base Framework
[What's different and why]

## Usage
[How to use this variant]
```

---

## 📋 Metadata Fields Guide

### Framework Fields
- `type: "framework"` - Complete system architecture
- `components: []` - List of component names
- `techniques: []` - Techniques used
- `previous: ""` - Previous version
- `next: ""` - Next version

### Component Fields
- `type: "component"` - Modular piece
- `parent: ""` - Parent framework name
- `phase: ""` - Which phase/step (if applicable)
- `purpose: ""` - What it does

### Variant Fields
- `type: "variant"` - Model-specific version
- `parent: ""` - Base framework
- `base: ""` - Base version
- `model: ""` - Target model
- `optimizations: []` - Model-specific changes

---

## ✅ Checklist

### Framework
- [ ] Type set to "framework"
- [ ] Components listed
- [ ] Techniques documented
- [ ] Version number assigned
- [ ] Previous/next versions linked

### Component
- [ ] Type set to "component"
- [ ] Parent framework specified
- [ ] Phase/step identified
- [ ] Integration points documented

### Variant
- [ ] Type set to "variant"
- [ ] Base framework specified
- [ ] Model optimizations listed
- [ ] Differences documented

---

*Use these templates to maintain consistency across complex frameworks*

