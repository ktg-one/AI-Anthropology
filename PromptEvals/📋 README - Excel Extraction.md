---
title: "Excel Extraction - Quick Start"
type: guide
created: 2025-01-20
tags: [excel, extraction, quick-start]
status: "ACTIVE"
priority: "HIGH"
---

# 📋 Excel Extraction - Quick Start

> **No manual work needed** | Automatically extract all prompts from Excel

---

## 🚀 Quick Start (3 Steps)

### Step 1: Install Dependencies
```bash
pip install pandas openpyxl
```

Or use the requirements file:
```bash
pip install -r requirements.txt
```

### Step 2: Preview Your Excel Structure
```bash
python extract_excel.py preview
```

This shows you:
- How many sheets
- Column names
- Sample data

**Use this to adjust the script if needed!**

### Step 3: Run Extraction
```bash
python extract_excel.py
```

That's it! All prompts will be extracted to `01-Prompt-dump/`

---

## 🔧 If Columns Don't Match

### Edit `extract_excel.py`

Find this section (around line 20):
```python
COLUMN_MAPPINGS = {
    'title': ['Title', 'Prompt Name', 'Name', 'Prompt'],
    'content': ['Content', 'Prompt', 'Text', 'Body', 'Description'],
    # ... add your column names here
}
```

**Add your actual Excel column names to the lists!**

---

## ✅ What Gets Created

Each prompt becomes a markdown file with:
- ✅ Frontmatter metadata
- ✅ Proper categorization (framework/component/technique)
- ✅ Version tracking
- ✅ Tags
- ✅ Original content preserved

---

## 🎯 Next Steps After Extraction

1. **Review files** - Check a few generated files
2. **Fix metadata** - Adjust frontmatter if needed  
3. **Organize** - Move to proper folders
4. **Link relationships** - Add parent/component links

---

*No more manual conversion - automate it!*

