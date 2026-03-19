# 🚀 Boosted Prompts

This directory contains **boosted/improved versions** of prompts from the reference collection.

## What Are Boosted Prompts?

Boosted prompts are:
- **Improved versions** of reference prompts
- **Enhanced** with better structure, clarity, or techniques
- **Tracked** with source attribution
- **Tested** and validated

## Workflow

1. **Find a reference prompt** you want to improve:
   ```bash
   python scripts/boost_prompt.py --list
   ```

2. **Create a boosted version**:
   ```bash
   python scripts/boost_prompt.py --boost "prompt-name.md"
   ```

3. **Edit the boosted version**:
   - Add your improvements
   - Document what changed
   - Test on multiple models

4. **Validate**:
   ```bash
   prompt-validate content/prompts/boosted/
   ```

## File Structure

Boosted prompts include:
- **Frontmatter** with metadata
- **Original prompt** (for reference)
- **Improvements section** (what you changed)
- **Testing notes** (results and validation)

## Naming Convention

Boosted prompts are named:
```
YYYYMMDD-boosted-{original-name}.md
```

Example: `20250120-boosted-chain-of-thought.md`

## Status

Boosted prompts start as `TESTING` and move to `ACTIVE` after validation.

