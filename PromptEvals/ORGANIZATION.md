# 📁 Directory Organization Guide

This document explains the structure of the AI Anthropology working directory.

## 🎯 Quick Overview

```
.AI-Anthropology/
├── src/                    # Working Python code (executable)
├── scripts/                # Standalone utility scripts
├── tests/                  # Test files
├── config/                 # Configuration files
├── docs/                   # Documentation (guides, READMEs)
├── content/                # Non-executable content
│   ├── prompts/           # Your prompt files
│   ├── research/          # Research papers and materials
│   ├── publications/      # Publication-ready content
│   ├── techniques/        # Technique documentation
│   ├── evaluations/       # Evaluation results and tests
│   └── reference/         # Reference material (public prompts for comparison)
└── [legacy folders]        # Original folders (being migrated)
```

## 📂 Directory Purposes

### `src/` - Working Code
**Purpose**: All executable Python code
- `src/ai_anthropology/` - Main package
- `src/ai_anthropology/scripts/` - Command-line tools
- `src/ai_anthropology/utils/` - Utility functions

**What goes here**: Python modules, packages, executable code

### `scripts/` - Standalone Scripts
**Purpose**: One-off scripts and utilities
- Migration scripts
- Quick automation scripts
- Temporary utilities

**What goes here**: Scripts that don't need to be part of the main package

### `docs/` - Documentation
**Purpose**: Project documentation and guides
- README files
- Setup guides
- Architecture documentation
- How-to guides

**What goes here**: Markdown files that explain the project

### `content/prompts/` - Prompt Files
**Purpose**: Your prompt collection
- Individual prompt files (.md)
- Prompt templates
- Prompt registries

**What goes here**: All `.md` files containing prompts

### `content/research/` - Research Materials
**Purpose**: Research papers, notes, methodology
- PDF papers
- Research notes
- Methodology documentation

**What goes here**: Research-related content

### `content/publications/` - Publication Content
**Purpose**: Content ready for publication
- Paper drafts
- Publication strategies
- Publication checklists

**What goes here**: Content related to publishing

### `content/techniques/` - Technique Documentation
**Purpose**: Documentation of prompt techniques
- Chain of Density
- Self-Criticism
- Decomposition
- etc.

**What goes here**: Technique-specific documentation

### `content/evaluations/` - Evaluation Results
**Purpose**: Test results and evaluations
- Evaluation test suites
- Results
- Benchmarks

**What goes here**: Testing and evaluation content

### `content/reference/` - Reference Material
**Purpose**: Reference prompts and resources for boosting/improving
- Public prompt collections (from GitHub)
- Used as source material to create improved/boosted versions
- Keep the good ones - you can boost all of them
- Not your original work, but source material for your improvements

**What goes here**: Reference material you use to boost/improve into better prompts

## 🔄 Migration Status

### ✅ Organized (New Structure)
- `src/` - Python code
- `scripts/` - Utility scripts
- `docs/` - Documentation
- `config/` - Configuration

### 📦 To Be Migrated (Legacy Folders)
- `00-Techniques/` → `content/techniques/`
- `01-Prompt-dump/` → `content/prompts/`
- `01-Prompt-dump-backup/` → Keep as backup
- `02-ktg-test/` → `content/evaluations/`
- `03-Research-LTS/` → `content/research/`
- `04-LLM-individualism/` → `content/research/llm-comparisons/`
- `05-Public-prompts/` → `content/reference/public-prompts/` (reference material for comparison)
- `06-Media-Team-LLM/` → `content/publications/media/`
- `07-BATTLE-OF-THE-BOTS/` → `content/evaluations/battle-tests/`
- `evals/` → `content/evaluations/`

### 📄 Root-Level Files
Root-level markdown files (like `🚀 START HERE.md`) should be moved to `docs/` or organized by purpose.

## 🚀 Usage

### Working with Code
```bash
# Install the package
pip install -e .

# Run scripts
prompt-migrate
prompt-search -q "chain of density"
prompt-validate 01-Prompt-dump/
prompt-extract file.xlsx
```

### Working with Content
- Browse prompts: `content/prompts/`
- Read research: `content/research/`
- Check evaluations: `content/evaluations/`

### Working with Documentation
- Start here: `docs/START_HERE.md` (if exists)
- Read guides: `docs/`
- Check README: `README.md`

## 💡 Tips

1. **Code vs Content**: If it's executable Python → `src/` or `scripts/`. If it's markdown/docs → `content/` or `docs/`.

2. **New Prompts**: Save new prompts to `content/prompts/` (not the legacy folders).

3. **Scripts**: Use `src/ai_anthropology/scripts/` for reusable tools, `scripts/` for one-offs.

4. **Documentation**: Project docs → `docs/`, content docs → `content/`.

## 🔧 Migration Script

To help migrate files, you can use:
```bash
python scripts/organize_content.py
```

This will help move files from legacy folders to the new structure.

