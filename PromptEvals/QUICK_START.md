# 🚀 Quick Start - Clean Up Your Directory

## The Problem

You have **4,551 markdown files**, but only **~200 are actually yours**:
- 4,152 files (91%) are from public GitHub repos (`05-Public-prompts/`)
- 71 files are your actual prompts
- Rest are docs, guides, backups, etc.

## The Solution

### Step 1: Analyze What You Have

```bash
# See the breakdown
python scripts/analyze_markdown.py
```

### Step 2: Decide What to Do with Public Prompts

**Option A: Archive them** (keep for comparison - recommended):
```bash
python scripts/cleanup_public_prompts.py --archive
```
This moves them to `content/reference/public-prompts/` - keeps them for comparison but clearly marks them as reference material, not your work.

**Option B: Delete them** (they're public, you can re-download):
```bash
python scripts/cleanup_public_prompts.py --delete
```

**Option C: Analyze first**:
```bash
python scripts/cleanup_public_prompts.py --analyze
```

### Step 3: Organize Your Actual Work

```bash
# Dry run first (see what would happen)
python scripts/organize_content.py --dry-run

# Actually organize
python scripts/organize_content.py
```

### Step 4: Move Navigation Files to docs/

The 7 navigation files (START HERE, PROMPT DIRECTORY, etc.) should go to `docs/`:

```bash
# Windows PowerShell
Move-Item "🚀 START HERE.md" docs/
Move-Item "📚 PROMPT DIRECTORY.md" docs/
Move-Item "📋 Prompt Registry.md" docs/
Move-Item "📋 Advanced Prompt Registry.md" docs/
Move-Item "🏷️ Tag Index.md" docs/
Move-Item "🔍 Search Hub.md" docs/
Move-Item "📊 Analytics Dashboard.md" docs/
Move-Item "📌 Quick Reference.md" docs/
Move-Item "📖 Documentation.md" docs/
```

## After Cleanup

Your directory will have:
- **~200 relevant files** (your work)
- **Organized structure** (code in `src/`, content in `content/`, docs in `docs/`)
- **Clean root** (only essential files)

## What's Actually Relevant?

### ✅ Keep These
- **7 navigation files** → Move to `docs/`
- **71 prompt files** → Move to `content/prompts/`
- **~30 evaluation files** → Move to `content/evaluations/`
- **~19 publication files** → Move to `content/publications/`
- **~8 research files** → Move to `content/research/`

### ⚠️ Archive or Delete
- **4,152 public prompt files** → Archive or delete (not your work)
- **85 backup files** → Delete after migration verified

## Need Help?

- **Analysis**: `python scripts/analyze_markdown.py`
- **Cleanup guide**: See `CLEANUP_GUIDE.md`
- **Organization**: See `ORGANIZATION.md`

