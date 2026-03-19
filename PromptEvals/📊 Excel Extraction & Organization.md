---
title: "Excel Extraction & Organization"
type: tool
created: 2025-01-20
tags: [extraction, organization, excel, automation]
status: "ACTIVE"
---

# 📊 Excel Extraction & Organization

> **Extract and categorize prompts from Excel** | Agentic organizing assistance

---

## 🎯 Goal

Extract prompts from `LLM-Archive.xlsx` and:
1. Categorize by type (framework/component/technique)
2. Extract metadata (version, model, date)
3. Organize into directory structure
4. Create markdown files with frontmatter
5. Link relationships

---

## 📋 Extraction Process

### Step 1: Analyze Excel Structure
```python
# Check columns, data types, patterns
# Identify prompt fields
# Map to directory schema
```

### Step 2: Extract Metadata
- **Title**: Prompt name
- **Version**: Extract from title/content
- **Date**: Creation date
- **Model**: Compatible models
- **Type**: Framework/Component/Technique
- **Category**: Research/Business/Coding/etc.

### Step 3: Categorize
- **Framework**: Complete systems (KTG-DIRECTIVE, QMDR)
- **Component**: Modular pieces (MR_RUG, FCoT/CoC)
- **Technique**: Standalone methods
- **Variant**: Model-specific versions

### Step 4: Generate Markdown
- Create frontmatter from extracted data
- Preserve original content
- Add directory metadata
- Link relationships

---

## 🤖 Agentic Organization

### Automated Tasks
1. **Pattern Recognition**: Identify framework families
2. **Version Linking**: Connect version chains
3. **Component Mapping**: Link components to frameworks
4. **Tag Assignment**: Auto-tag based on content
5. **Relationship Detection**: Find dependencies

### Manual Review Needed
- Verify categorizations
- Confirm relationships
- Refine metadata
- Add missing information

---

## 📁 Output Structure

```
01-Prompt-dump/
  ├── Frameworks/
  │   ├── KTG-DIRECTIVE/
  │   │   ├── v25.5/
  │   │   ├── v25.0/
  │   │   └── Components/
  │   └── QMDR/
  ├── Components/
  ├── Techniques/
  └── Variants/
```

---

## 🔧 Tools Needed

### Python Script
- Read Excel file
- Parse prompts
- Extract metadata
- Generate markdown
- Create directory structure

### Manual Review
- Verify extractions
- Refine categorizations
- Add relationships
- Complete metadata

---

## 📝 Extraction Template

For each prompt in Excel:

```yaml
---
title: "[Extracted Title]"
version: "[Extracted Version]"
type: "[Detected Type]"
status: "ACTIVE"
model: "[Extracted Models]"
tags: [auto-generated]
created: "[Excel Date]"
source: "LLM-Archive.xlsx"
---
[Original Content]
```

---

*Ready to extract and organize your Excel vault*

