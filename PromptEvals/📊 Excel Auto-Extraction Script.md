---
title: "Excel Auto-Extraction Script"
type: tool
created: 2025-01-20
tags: [excel, extraction, automation, script]
status: "ACTIVE"
priority: "HIGH"
---

# 📊 Excel Auto-Extraction Script

> **Automatically extract prompts from Excel** | No manual conversion needed

---

## 🎯 The Problem

- Prompts categorized in Excel via LLM
- Manual conversion would take forever
- Need automated extraction
- Preserve categorization

---

## 🐍 Python Script Solution

### Quick Setup
```python
import pandas as pd
import os
from pathlib import Path

# Configuration
EXCEL_FILE = "LLM-Archive.xlsx"
OUTPUT_DIR = "01-Prompt-dump"
SHEET_NAME = None  # None = all sheets, or specify sheet name

def extract_prompts_from_excel():
    """Extract prompts from Excel and create markdown files"""
    
    # Read Excel file
    if SHEET_NAME:
        df = pd.read_excel(EXCEL_FILE, sheet_name=SHEET_NAME)
    else:
        # Read all sheets
        excel_data = pd.read_excel(EXCEL_FILE, sheet_name=None)
        all_prompts = []
        for sheet_name, df in excel_data.items():
            df['source_sheet'] = sheet_name
            all_prompts.append(df)
        df = pd.concat(all_prompts, ignore_index=True)
    
    # Create output directory
    os.makedirs(OUTPUT_DIR, exist_ok=True)
    
    # Process each row
    for idx, row in df.iterrows():
        create_markdown_file(row, idx)
    
    print(f"Extracted {len(df)} prompts to {OUTPUT_DIR}/")

def create_markdown_file(row, idx):
    """Create markdown file from Excel row"""
    
    # Extract data (adjust column names to match your Excel)
    title = row.get('Title', row.get('Prompt Name', f'Prompt_{idx}'))
    content = row.get('Content', row.get('Prompt', row.get('Text', '')))
    category = row.get('Category', row.get('Type', 'unknown'))
    version = row.get('Version', 'v1.0')
    model = row.get('Model', row.get('Models', 'Multi-model'))
    date = row.get('Date', row.get('Created', ''))
    tags = row.get('Tags', '')
    
    # Determine type based on category
    prompt_type = determine_type(category, title)
    
    # Create frontmatter
    frontmatter = f"""---
title: "{title}"
type: "{prompt_type}"
version: "{version}"
status: "ACTIVE"
model: "{model}"
category: "{category}"
tags: [{format_tags(tags)}]
created: "{format_date(date)}"
updated: "{format_date(date)}"
source: "LLM-Archive.xlsx"
---
"""
    
    # Create filename
    safe_title = sanitize_filename(title)
    filename = f"{OUTPUT_DIR}/{safe_title}.md"
    
    # Write file
    with open(filename, 'w', encoding='utf-8') as f:
        f.write(frontmatter)
        f.write(f"\n# {title}\n\n")
        f.write(str(content))
    
    print(f"Created: {filename}")

def determine_type(category, title):
    """Determine prompt type from category/title"""
    category_lower = str(category).lower()
    title_lower = str(title).lower()
    
    if 'framework' in category_lower or 'ktg' in title_lower or 'directive' in title_lower:
        return 'framework'
    elif 'component' in category_lower or 'router' in title_lower or 'rug' in title_lower:
        return 'component'
    elif 'technique' in category_lower or 'bomb' in title_lower or 'thought' in title_lower:
        return 'technique'
    else:
        return 'prompt'

def format_tags(tags):
    """Format tags for frontmatter"""
    if pd.isna(tags) or tags == '':
        return 'extracted'
    
    # If tags are comma-separated
    if ',' in str(tags):
        tag_list = [t.strip().lower() for t in str(tags).split(',')]
    else:
        tag_list = [str(tags).strip().lower()]
    
    return ', '.join([f'"{tag}"' for tag in tag_list])

def format_date(date):
    """Format date for frontmatter"""
    if pd.isna(date) or date == '':
        return '2025-01-20'
    
    # Try to parse date
    try:
        if isinstance(date, str):
            # Handle various date formats
            return date[:10]  # YYYY-MM-DD
        else:
            return str(date)[:10]
    except:
        return '2025-01-20'

def sanitize_filename(name):
    """Create safe filename"""
    # Remove invalid characters
    invalid_chars = '<>:"/\\|?*'
    for char in invalid_chars:
        name = name.replace(char, '_')
    
    # Limit length
    if len(name) > 100:
        name = name[:100]
    
    return name

if __name__ == "__main__":
    extract_prompts_from_excel()
```

---

## 🚀 Usage

### Step 1: Install Dependencies
```bash
pip install pandas openpyxl
```

### Step 2: Run Script
```bash
python extract_excel.py
```

### Step 3: Review Output
- Check `01-Prompt-dump/` folder
- Review generated markdown files
- Adjust script if needed

---

## 🔧 Customization

### Adjust Column Names
```python
# Update these to match your Excel columns
title = row.get('Your Title Column', '')
content = row.get('Your Content Column', '')
category = row.get('Your Category Column', '')
```

### Custom Type Detection
```python
def determine_type(category, title):
    # Add your own logic
    if 'KTG-DIRECTIVE' in title:
        return 'framework'
    elif 'MR_RUG' in title or 'FCoT' in title:
        return 'component'
    # ... your rules
```

### Handle Multiple Sheets
```python
# If Excel has multiple sheets with different structures
SHEET_CONFIGS = {
    'Frameworks': {'type': 'framework'},
    'Components': {'type': 'component'},
    'Techniques': {'type': 'technique'},
}
```

---

## 📋 Excel Structure Assumptions

The script assumes your Excel has columns like:
- **Title** / **Prompt Name** - Prompt title
- **Content** / **Prompt** / **Text** - Prompt content
- **Category** / **Type** - Categorization
- **Version** - Version number
- **Model** / **Models** - Compatible models
- **Date** / **Created** - Creation date
- **Tags** - Tags (comma-separated)

**Adjust script to match your actual Excel structure!**

---

## 🔍 Preview Excel Structure

### Quick Check Script
```python
import pandas as pd

# Preview Excel structure
excel_file = "LLM-Archive.xlsx"
df = pd.read_excel(excel_file)

print("Columns:", df.columns.tolist())
print("\nFirst few rows:")
print(df.head())
print("\nData types:")
print(df.dtypes)
```

Run this first to see your Excel structure, then adjust the extraction script.

---

## ✅ Post-Extraction Steps

### After Running Script
1. **Review files** - Check a few generated markdown files
2. **Fix metadata** - Adjust frontmatter if needed
3. **Categorize** - Move to appropriate folders
4. **Link relationships** - Add parent/component links
5. **Verify** - Ensure all prompts extracted

### Batch Fix Script
```python
# Fix common issues after extraction
import os
import re

def fix_extracted_files():
    for filename in os.listdir('01-Prompt-dump'):
        if filename.endswith('.md'):
            filepath = f'01-Prompt-dump/{filename}'
            with open(filepath, 'r', encoding='utf-8') as f:
                content = f.read()
            
            # Fix common issues
            # Add your fixes here
            
            with open(filepath, 'w', encoding='utf-8') as f:
                f.write(content)
```

---

## 🎯 Next Steps

1. **Run preview script** - See your Excel structure
2. **Adjust extraction script** - Match your columns
3. **Run extraction** - Generate markdown files
4. **Review & fix** - Clean up as needed
5. **Organize** - Move to proper folders

---

## 💡 Tips

- **Start small** - Test on one sheet first
- **Backup Excel** - Keep original safe
- **Incremental** - Extract in batches if large
- **Validate** - Check a few files before full run

---

*No more manual conversion - automate it!*

