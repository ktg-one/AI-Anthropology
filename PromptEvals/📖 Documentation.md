---
title: "Documentation"
type: documentation
created: 2025-01-20
tags: [documentation, guide, help]
---

# 📖 Documentation

> Complete guide to using the Advanced Prompt Directory

---

## 🚀 Getting Started

### 1. Understanding the Structure

Your prompt directory is organized into several key components:

- **📚 PROMPT DIRECTORY.md** - Main navigation hub
- **📋 Prompt Registry** - Complete catalog with metadata
- **🏷️ Tag Index** - Tag taxonomy and browsing
- **🔍 Search Hub** - Advanced search queries
- **📦 Prompt Templates** - Create new prompts
- **📊 Analytics Dashboard** - Statistics and insights

### 2. Creating a New Prompt

1. Go to [[📦 Prompt Templates|Prompt Templates]]
2. Copy the appropriate template
3. Fill in the frontmatter metadata
4. Write your prompt content
5. Save with proper naming convention
6. The registry will auto-update!

### 3. Tagging Your Prompts

Always include:
- **Status tag**: `#active`, `#testing`, `#archived`, or `#deprecated`
- **Model tag**: `#claude`, `#gpt`, `#gemini`, etc.
- **Type tag**: `#system`, `#instruction`, `#template`, `#technique`
- **Domain tag**: `#research`, `#business`, `#coding`, etc.

See [[🏷️ Tag Index|Tag Index]] for complete taxonomy.

---

## 📋 Frontmatter Schema

### Required Fields

```yaml
---
title: "Prompt Name"
version: "v1.0"
status: "ACTIVE" | "TESTING" | "ARCHIVED" | "DEPRECATED"
created: "YYYY-MM-DD"
updated: "YYYY-MM-DD"
---
```

### Recommended Fields

```yaml
---
model: "Claude, GPT-5.1, Gemini"
tags: [claude, system, research]
category: "research"
description: "Brief description"
creator: "ktg"
complexity: "low" | "medium" | "high"
---
```

### Optional Fields

```yaml
---
dependencies: ["Related Prompt 1", "Related Prompt 2"]
usage: "Usage instructions"
examples: "Example scenarios"
---
```

---

## 🔍 Using Search

### Dataview Queries

The directory uses Dataview queries for dynamic content. Examples:

**Find active prompts:**
```dataview
TABLE version, status
FROM "01-Prompt-dump"
WHERE status = "ACTIVE"
```

**Find by tag:**
```dataview
TABLE version, status
FROM "01-Prompt-dump"
WHERE contains(tags, "claude")
```

**Find recent updates:**
```dataview
TABLE version, updated
FROM "01-Prompt-dump"
WHERE updated >= date(today) - dur(7 days)
```

### Obsidian Search

Use Obsidian's built-in search (Ctrl+Shift+F) for:
- Full-text search
- Tag search: `tag:#claude`
- File search: `path:01-Prompt-dump`

---

## 🏷️ Tagging Best Practices

1. **Be Consistent**: Use the same tags across similar prompts
2. **Be Specific**: Prefer specific tags over generic ones
3. **Use Multiple**: Combine tags for better filtering
4. **Follow Taxonomy**: Use tags from [[🏷️ Tag Index|Tag Index]]

### Tag Combinations

- System prompts: `#system` + `#claude` + `#framework`
- Research: `#research` + `#analysis` + `#active`
- Testing: `#testing` + `#experimental` + model tag

---

## 📊 Version Management

### Version Numbering

- **Major** (v2.0): Significant structural changes
- **Minor** (v1.1): Feature additions or improvements
- **Patch** (v1.1.1): Bug fixes or small tweaks

### Status Lifecycle

1. **TESTING** - New prompt, under evaluation
2. **ACTIVE** - Production-ready, in use
3. **ARCHIVED** - Stored for reference, not active
4. **DEPRECATED** - Outdated, replaced by newer version

### Updating Prompts

When updating a prompt:
1. Increment version number
2. Update `updated` date
3. Add changelog entry
4. Update status if needed

---

## 🗂️ File Organization

### Naming Convention

Format: `YYYYMMDD-creator-[name]-v[version].md`

Examples:
- `20250120-ktg-Research-Framework-v1.0.md`
- `20250120-ktg-Business-Analysis-v2.1.md`

### Folder Structure

```
📁 01-Prompt-dump/          # Your custom prompts
📁 00-Techniques/           # Prompt engineering techniques
📁 04-LLM-individualism/    # Model-specific prompts
📁 05-Public-prompts/       # Community prompts
📁 07-BATTLE-OF-THE-BOTS/   # Comparative prompts
```

---

## 🔧 Obsidian Features

### Graph View

Use Obsidian's graph view to visualize:
- Prompt relationships
- Tag connections
- Category clusters

### Canvas

Create visual maps using Canvas:
- Link related prompts
- Group by category
- Show workflows

### Dataview Plugin

Required for dynamic queries. Ensure it's enabled in:
Settings → Community Plugins → Dataview

---

## 💡 Tips & Tricks

1. **Use Templates**: Always start from [[📦 Prompt Templates|Templates]]
2. **Update Regularly**: Keep `updated` dates current
3. **Link Related**: Use `[[links]]` to connect prompts
4. **Add Examples**: Include usage examples in prompts
5. **Document Changes**: Maintain changelogs

---

## 🆘 Troubleshooting

### Queries Not Working

- Ensure Dataview plugin is enabled
- Check frontmatter syntax (YAML format)
- Verify field names match exactly

### Tags Not Showing

- Check tag format: `tags: [tag1, tag2]`
- Ensure tags are in frontmatter
- Use Obsidian's tag pane to verify

### Links Broken

- Use `[[filename]]` format
- Check file names match exactly
- Use Ctrl+O to search for files

---

## 📚 Additional Resources

- [[📚 PROMPT DIRECTORY|Main Directory]]
- [[📋 Prompt Registry|Prompt Registry]]
- [[🏷️ Tag Index|Tag Index]]
- [[🔍 Search Hub|Search Hub]]

---

*Need help? Check Obsidian documentation or Dataview plugin docs*

