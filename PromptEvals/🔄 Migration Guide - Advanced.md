---
title: "Advanced Migration Guide"
type: guide
created: 2025-01-20
tags: [migration, framework, advanced]
---

# 🔄 Advanced Migration Guide

> **Migrating complex frameworks** | Add metadata to framework-level prompts, components, and versions

---

## 🎯 Understanding Your Prompts

Your prompts fall into these categories:

### 1. Framework-Level Prompts
Complete cognitive OS architectures:
- **KTG-DIRECTIVE** (v20, v21, v22, v23, v25, v25.5)
- **QMDR** (Quantum Master Deep Research)
- **Triplexity** (Multi-model research)
- **Perpromperty Nexus** (Business frameworks)

### 2. Component Prompts
Modular pieces that integrate:
- **MR_RUG** (Mixture of Reasoning Experts)
- **FCoT/CoC Router** (Reasoning selector)
- **Prompt Bombs** (Information densification)
- **Skeletrain of Thought** (Planning framework)

### 3. Technique Prompts
Standalone methodologies:
- Chain of Thought variants
- Self-Criticism methods
- Decomposition strategies

---

## 📋 Migration Strategy

### Step 1: Identify Framework Structure

For **KTG-DIRECTIVE v25.5**:

```yaml
---
title: "KTG-DIRECTIVE"
type: "framework"
version: "v25.5"
status: "ACTIVE"
model: "Claude, GPT-5.1, Gemini, Perplexity, Qwen, DeepSeek, Llama"
category: "framework"
tags: [framework, ktg-directive, system, production, multi-model, expert-routing, anti-lazy]
created: "2025-11-16"
updated: "2025-11-16"
creator: "ktg"
complexity: "high"
description: "Production-grade cognitive OS with expert governance, adaptive reasoning, multi-modal verification"
components: ["MR_RUG", "FCoT/CoC Router", "SoT/GoT", "Prompt Bombs", "Expert ARQ", "CoVE"]
techniques: ["Prompt Bombs", "Skeletrain of Thought", "Graph of Thought", "Expert ARQ", "Chain of Verification", "Buffer of Thought"]
previous: "v25.0"
next: ""
---
```

### Step 2: Add Component Metadata

For **MR_RUG**:

```yaml
---
title: "MR_RUG"
type: "component"
version: "v1.0"
status: "ACTIVE"
parent: "KTG-DIRECTIVE"
phase: "1-3"
purpose: "Mixture of Reasoning Experts initialization framework"
tags: [component, ktg-directive, initialization, expert-assembly]
created: "2025-11-16"
updated: "2025-11-16"
creator: "ktg"
complexity: "medium"
description: "Phases 1-3: Task initialization, expert assembly, RAG synthesis, knowledge graph creation"
---
```

### Step 3: Link Versions

For **KTG-DIRECTIVE v25.0**:

```yaml
---
title: "KTG-DIRECTIVE"
type: "framework"
version: "v25.0"
status: "ARCHIVED"
previous: "v23.0"
next: "v25.5"
changelog: "Added Mr. Rug, FCoT/CoC Router, Multi-Layer Density, BoT Integration"
---
```

---

## 🔍 Extracting Information

### From Filename
- `11162025-KTG-DIRECTIVE-v25.5-routing-anti-lazy-fix.md`
  - Date: `2025-11-16`
  - Name: `KTG-DIRECTIVE`
  - Version: `v25.5`
  - Variant: `routing-anti-lazy-fix`

### From Content
- **Version**: Look for `v25.5`, `v25.0` in title or content
- **Components**: Look for "Phase X" or component names
- **Techniques**: Look for technique mentions (Prompt Bombs, SoT, GoT, etc.)
- **Model**: Check "Compatible:" lines
- **Changes**: Look for changelog sections

### From Structure
- **Framework**: Complete system with multiple phases/components
- **Component**: References parent framework, has phase/step
- **Variant**: Model-specific or specialized version

---

## 📊 Example Migrations

### Example 1: KTG-DIRECTIVE v25.5

**Before:**
```markdown
# KTG-DIRECTIVE v25.1 – CANONICAL COGNITIVE OS
# Compatible: Claude, GPT-5.1, Gemini, Perplexity, Qwen, DeepSeek, Llama
# v25.1 = v25.0 + Anti-Lazy + Quantum Deep Research + Expert Routing + Governance Gate
```

**After:**
```yaml
---
title: "KTG-DIRECTIVE"
type: "framework"
version: "v25.5"
status: "ACTIVE"
model: "Claude, GPT-5.1, Gemini, Perplexity, Qwen, DeepSeek, Llama"
tags: [framework, ktg-directive, production, multi-model, anti-lazy, expert-routing]
created: "2025-11-16"
updated: "2025-11-16"
components: ["MR_RUG", "FCoT/CoC Router", "SoT/GoT", "Prompt Bombs", "Expert ARQ"]
techniques: ["Prompt Bombs", "Skeletrain of Thought", "Graph of Thought", "Expert ARQ"]
previous: "v25.0"
changelog: "v25.0 + Anti-Lazy + Quantum Deep Research + Expert Routing + Governance Gate"
---
# KTG-DIRECTIVE v25.1 – CANONICAL COGNITIVE OS
```

### Example 2: Prompt Bombs Component

**Before:**
```markdown
# Prompt Bombs: Hybrid Strategy - Planned + Emergent
```

**After:**
```yaml
---
title: "Prompt Bombs"
type: "component"
version: "v1.0"
status: "ACTIVE"
parent: "KTG-DIRECTIVE"
purpose: "Strategic information densification nodes"
tags: [component, ktg-directive, technique, information-densification]
created: "2025-10-05"
updated: "2025-10-05"
description: "Hybrid strategy for planned and emergent information injection"
---
# Prompt Bombs: Hybrid Strategy - Planned + Emergent
```

### Example 3: Model Variant

**Before:**
```markdown
# KTG-CLAUDE CASCADE v1.0
```

**After:**
```yaml
---
title: "KTG-DIRECTIVE - Claude Variant"
type: "variant"
version: "v1.0"
status: "ACTIVE"
parent: "KTG-DIRECTIVE"
base: "v25.0"
model: "Claude"
tags: [variant, ktg-directive, claude, optimized]
created: "2025-11-16"
updated: "2025-11-16"
optimizations: ["Claude-specific reasoning patterns", "Cascade architecture"]
---
# KTG-CLAUDE CASCADE v1.0
```

---

## 🎯 Priority Migration Order

1. **High Priority**: Active frameworks (KTG-DIRECTIVE v25.5)
2. **Medium Priority**: Components (MR_RUG, FCoT/CoC, Prompt Bombs)
3. **Low Priority**: Archived versions, experimental prompts

---

## ✅ Migration Checklist

For each prompt:
- [ ] Identify type (framework/component/technique/variant)
- [ ] Extract version number
- [ ] Identify parent framework (if component)
- [ ] List components (if framework)
- [ ] List techniques used
- [ ] Set status (ACTIVE/TESTING/ARCHIVED)
- [ ] Link versions (previous/next)
- [ ] Add tags appropriately
- [ ] Set dates (created/updated)

---

## 💡 Tips

1. **Start with frameworks**: Migrate top-level frameworks first
2. **Then components**: Add components and link to frameworks
3. **Link versions**: Connect version chains
4. **Use consistent naming**: Keep framework names consistent
5. **Document relationships**: Use parent/component fields

---

*This guide handles complex framework architectures, not just simple prompts*

