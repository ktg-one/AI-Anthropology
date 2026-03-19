---
title: "Advanced Prompt Directory"
type: index
created: 2025-01-20
updated: 2025-01-20
tags: [directory, index, navigation]
---

# 📚 Advanced Prompt Directory

> **Your comprehensive prompt management system** | Fully Obsidian-compatible with advanced search, categorization, and discovery features

---

## 🚀 **NEW TO THIS VAULT?** 
→ **Start here: [[🚀 START HERE|START HERE]]** - Your navigation guide

---

## 🗺️ Navigation Hub

### Core Directories
- [[📋 Advanced Prompt Registry|Advanced Prompt Registry]] - Framework-aware catalog
- [[🏗️ Framework Architecture|Framework Architecture]] - Framework hierarchies & relationships
- [[🏷️ Tag Index|Tag Index]] - Browse by tags and categories
- [[🔍 Search Hub|Search Hub]] - Advanced search queries
- [[📊 Analytics Dashboard|Analytics Dashboard]] - Usage statistics and insights

### Quick Access
- [[🎯 Active Prompts|Active Prompts]] - Currently in use
- [[🧪 Testing Prompts|Testing Prompts]] - Under evaluation
- [[📦 Advanced Prompt Template|Advanced Prompt Templates]] - Create framework prompts
- [[📖 Documentation|Documentation]] - System guide

### For Complex Frameworks
- [[🔄 Migration Guide - Advanced|Advanced Migration Guide]] - Migrate framework prompts
- [[🏗️ Framework Architecture|Framework Architecture]] - Understand relationships

### For Publishing & Research
- [[🛡️ Safe Evaluation Platforms & Tools|Safe Platforms]] - **READ THIS** - Safe evaluation platforms & tools
- [[🔍 Prompt Foundry & Organizing Tools|Prompt Foundry]] - About Prompt Foundry & organizing tools
- [[🎯 MLDoE Publication Plan|MLDoE Plan]] - **FOCUS** - Multi-Layer Density of Experts (public-ready)
- [[🔬 MLDoE 5x Evaluation Setup|MLDoE Evaluation]] - Set up 5-platform evaluation
- [[🚀 Quick Start - First Publication|Quick Start]] - Get ONE paper published
- [[📋 CoD Applications List Template|Applications List]] - List all your discoveries - claim priority
- [[🚀 Quick Install Guide|Quick Install]] - Install IDE tools for evaluation
- [[🛠️ IDE Tools for Prompt Evaluation|IDE Tools]] - Evaluation tools setup
- [[💪 Building Credibility from Zero|Building Credibility]] - **READ THIS** - You don't need followers to publish
- [[🔥 Getting Your Paper Read|Getting Read]] - How to get noticed even with zero presence
- [[🎯 CoD Publication Strategy|CoD Strategy]] - **FOCUS HERE** - Publish CoD, keep rest private
- [[📊 Prompt Scoring Frameworks|Scoring Frameworks]] - Find scoring systems on each platform
- [[🔧 Platform Scoring Setup|Scoring Setup]] - Quick setup for platform scoring
- [[🔬 Multi-Platform Validation Framework|Multi-Platform Validation]] - **VALIDATE FIRST** - Test on 5+ platforms
- [[🔒 Renamed Evaluation Metrics|Renamed Metrics]] - Keep your evals private, use renamed versions
- [[🔌 Vertex AI Evaluation Guide|Vertex AI Eval]] - How to evaluate with current Vertex AI
- [[📋 Validation Checklist|Validation Checklist]] - Pre-publication checklist
- [[🔌 Vertex AI & Evaluation Tools|Vertex AI Setup]] - Connect & validate prompts
- [[📊 Excel Auto-Extraction Script|Excel Extraction]] - Auto-extract from Excel (no manual work!)
- [[🎓 AI Anthropology Methodology|AI Anthropology Methodology]] - Your unique approach
- [[📝 Publishing Preparation|Publishing Guide]] - Research paper preparation
- [[🌐 Online Presence Strategy|Online Presence]] - Build from zero
- [[🔬 Research Paper Templates|Paper Templates]] - Academic writing templates

---

## 📁 Directory Structure

### By Category
- [[00-Techniques/00-Techniques|Techniques]] - Prompt engineering techniques
- [[01-Prompt-dump/10232025-01-Prompt-dump|Prompt Dump]] - Your custom prompts (frameworks, components, techniques)
- [[04-LLM-individualism/04-LLM-individualism|LLM-Specific]] - Model-specific prompts
- [[05-Public-prompts/05-Public-prompts|Public Prompts]] - Community prompts
- [[07-BATTLE-OF-THE-BOTS/|Battle of the Bots]] - Comparative prompts

### Framework Structure
- **Frameworks**: Complete cognitive OS architectures (KTG-DIRECTIVE, QMDR, Triplexity)
- **Components**: Modular pieces (MR_RUG, FCoT/CoC Router, Prompt Bombs)
- **Techniques**: Standalone methodologies (Chain of Thought, Self-Criticism)
- **Variants**: Model-specific optimizations (Claude variants, Perplexity variants)

### By Status
```dataview
TABLE status, version, updated, tags
FROM "01-Prompt-dump"
WHERE status = "ACTIVE"
SORT updated DESC
LIMIT 10
```

### By Version
```dataview
TABLE version, status, created
FROM "01-Prompt-dump"
WHERE version
SORT version DESC
LIMIT 10
```

---

## 🔍 Quick Search

### Find Prompts By...
- **Model**: `#claude` `#gpt` `#gemini` `#perplexity`
- **Type**: `#system` `#instruction` `#template` `#technique`
- **Status**: `#active` `#testing` `#archived` `#deprecated`
- **Domain**: `#research` `#business` `#coding` `#writing`

---

## 📈 Statistics

```dataview
TABLE
  length(rows) as "Total Prompts"
FROM "01-Prompt-dump"
GROUP BY status
```

---

## 🚀 Getting Started

1. **Browse** the [[📋 Prompt Registry|Prompt Registry]] to find prompts
2. **Use** [[📦 Prompt Templates|Prompt Templates]] to create new ones
3. **Tag** your prompts with the [[🏷️ Tag Index|Tag Taxonomy]]
4. **Track** versions and status in frontmatter

---

*Last Updated: {{date:YYYY-MM-DD}}*

