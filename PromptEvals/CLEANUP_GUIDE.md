# 🧹 Cleanup Guide - What's Actually Relevant

## 📊 The Numbers

- **Total markdown files**: 4,551
- **Your actual work**: ~200 files (prompts, research, docs)
- **Public collections**: 4,152 files (91.2%) - **NOT YOUR WORK**
- **Backups**: 85 files - can delete after migration

## ✅ KEEP THESE (Essential)

### Navigation Files (7 files)
These are your entry points - **MOVE TO `docs/`**:
- `🚀 START HERE.md`
- `📚 PROMPT DIRECTORY.md`
- `📋 Prompt Registry.md` / `📋 Advanced Prompt Registry.md`
- `🏷️ Tag Index.md`
- `🔍 Search Hub.md`
- `📊 Analytics Dashboard.md`
- `📌 Quick Reference.md`
- `📖 Documentation.md`

### Your Actual Prompts (~71 files)
**MOVE TO `content/prompts/`**:
- Files in `01-Prompt-dump/` (your custom prompts)
- Files in `00-Techniques/` (your technique docs)

### Your Research (~8 files)
**MOVE TO `content/research/`**:
- `🎓 AI Anthropology Methodology.md`
- `📊 Your Repo Analysis.md`
- Files in `03-Research-LTS/`
- Files in `04-LLM-individualism/` (your LLM comparisons)

### Publication Plans (~19 files)
**MOVE TO `content/publications/`**:
- `🎯 CoD Publication Strategy.md`
- `🎯 MLDoE Publication Plan.md`
- `⚡ URGENT - Publish CoD Now.md`
- `📝 Publishing Preparation.md`
- etc.

### Evaluation Files (~30 files)
**MOVE TO `content/evaluations/`**:
- Files in `evals/`
- Files in `02-ktg-test/`
- `🔬 MLDoE 5x Evaluation Setup.md`
- etc.

## 📚 ARCHIVE (Reference Material)

### Public Prompt Collections (4,152 files!)
**Location**: `05-Public-prompts/`

**These are reference/comparison material** - public GitHub repos you use to compare your prompts:
- `awesome-ai-system-prompts-main/`
- `Ultimate_Prompts_Directory-main/`
- `prompts-main/`

**Action**: **Archive to `content/reference/public-prompts/`**
- Keep them for comparison purposes
- But clearly separate from "your work"
- Easy to access when needed

### Backup Files (85 files)
**Location**: `01-Prompt-dump-backup/`

**Can delete after migration** - but wait until you've verified migration worked!

## 🎯 Quick Action Plan

### Step 1: Archive Public Collections (Optional)
```bash
# If you want to keep them
mkdir -p content/publications/public-prompts
mv 05-Public-prompts content/publications/public-prompts/

# OR delete them (they're public repos anyway)
# rm -rf 05-Public-prompts
```

### Step 2: Organize Your Actual Work
```bash
# Run the organization script
python scripts/organize_content.py
```

### Step 3: Move Navigation Files
```bash
# Move navigation/index files to docs/
mv "🚀 START HERE.md" docs/
mv "📚 PROMPT DIRECTORY.md" docs/
mv "📋 Prompt Registry.md" docs/
mv "📋 Advanced Prompt Registry.md" docs/
mv "🏷️ Tag Index.md" docs/
mv "🔍 Search Hub.md" docs/
mv "📊 Analytics Dashboard.md" docs/
mv "📌 Quick Reference.md" docs/
mv "📖 Documentation.md" docs/
```

### Step 4: Clean Up Root
After migration, your root should only have:
- `README.md`
- `ORGANIZATION.md`
- `CLEANUP_GUIDE.md` (this file)
- `pyproject.toml`
- `setup.py`
- `requirements.txt`
- `.gitignore`
- `src/`
- `scripts/`
- `tests/`
- `config/`
- `docs/`
- `content/`

## 💡 The Reality

**You have ~200 relevant files**, not 4,551!

The 4,152 files in `05-Public-prompts/` are from public repos - they're reference material, not your work. You can:
- Keep them archived in `content/publications/public-prompts/`
- Delete them (they're public, you can re-download)
- Keep them but know they're not "your" files

## 🚀 After Cleanup

Your directory will be:
- **Clean** - Only your work + essential docs
- **Organized** - Code in `src/`, content in `content/`, docs in `docs/`
- **Functional** - A working directory, not a file dump

