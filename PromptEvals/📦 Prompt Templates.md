---
title: "Prompt Templates"
type: template
created: 2025-01-20
tags: [templates, creation, new-prompt]
---

# 📦 Prompt Templates

> Templates for creating new prompts with proper metadata and structure

---

## 🎯 Quick Start Template

Copy this template when creating a new prompt:

```markdown
---
title: "[Prompt Name]"
version: "v1.0"
status: "TESTING"
model: "Claude, GPT-5.1, Gemini"
category: "[category]"
tags: [tag1, tag2, tag3]
created: {{date:YYYY-MM-DD}}
updated: {{date:YYYY-MM-DD}}
creator: "ktg"
complexity: "medium"
description: "Brief description of what this prompt does"
---

# [Prompt Name] v1.0

## Purpose
[What this prompt is designed to do]

## Model Compatibility
- Claude ✅
- GPT-5.1 ✅
- Gemini ✅

## Usage
[How to use this prompt]

## Parameters
- `parameter1`: Description
- `parameter2`: Description

## Examples
[Example usage]

## Notes
[Additional notes or considerations]

## Changelog
### v1.0 ({{date:YYYY-MM-DD}})
- Initial version
```

---

## 📋 Template Variants

### System Prompt Template
```markdown
---
title: "[System Prompt Name]"
type: "system"
version: "v1.0"
status: "TESTING"
model: "Claude"
tags: [system, claude, framework]
created: {{date:YYYY-MM-DD}}
---

# [System Prompt Name]

## Identity
[Core identity and role]

## Capabilities
- [Capability 1]
- [Capability 2]

## Instructions
[Core instructions]

## Output Format
[Expected output format]
```

### Instruction Template
```markdown
---
title: "[Instruction Name]"
type: "instruction"
version: "v1.0"
status: "ACTIVE"
tags: [instruction, task]
created: {{date:YYYY-MM-DD}}
---

# [Instruction Name]

## Task
[What to do]

## Steps
1. [Step 1]
2. [Step 2]

## Output
[Expected output]
```

### Technique Template
```markdown
---
title: "[Technique Name]"
type: "technique"
version: "v1.0"
status: "ACTIVE"
tags: [technique, method]
created: {{date:YYYY-MM-DD}}
---

# [Technique Name]

## Overview
[What this technique does]

## When to Use
[When this technique is appropriate]

## How It Works
[Mechanism]

## Examples
[Example applications]
```

---

## 🏷️ Required Metadata Fields

### Essential
- `title`: Prompt name
- `version`: Version number (v1.0, v1.1, etc.)
- `status`: ACTIVE | TESTING | ARCHIVED | DEPRECATED
- `created`: Creation date
- `updated`: Last update date

### Recommended
- `model`: Compatible models
- `tags`: Array of tags
- `category`: Category classification
- `description`: Brief description

### Optional
- `creator`: Author/creator
- `complexity`: low | medium | high
- `usage`: Usage notes
- `dependencies`: Related prompts

---

## 📝 Naming Convention

Format: `YYYYMMDD-creator-[name]-v[version].md`

Examples:
- `20250120-ktg-Research-Framework-v1.0.md`
- `20250120-ktg-Business-Analysis-v2.1.md`

---

## ✅ Checklist

Before saving a new prompt:
- [ ] Frontmatter is complete
- [ ] Version number assigned
- [ ] Status set appropriately
- [ ] Tags added
- [ ] Model compatibility noted
- [ ] Description included
- [ ] File named correctly

---

*Use these templates to maintain consistency across your prompt library*

