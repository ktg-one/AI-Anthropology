# 🛠️ Prompt Management Tools Guide

> **Should you use Obsidian or VS Code extensions?** Here's what works best for prompt management.

## 🎯 Quick Answer

**Use BOTH:**
- **Obsidian** - For browsing, organizing, and managing your prompt collection
- **VS Code + Extensions** - For testing, evaluating, and improving prompts

---

## 📝 Obsidian (Best for Organization)

### Why Obsidian?

✅ **Perfect for your use case:**
- You already have 4,551 markdown files
- Obsidian excels at managing large markdown collections
- Graph view shows relationships between prompts
- Dataview queries for dynamic lists
- Tag system for organization
- Fast search across all files

### Essential Obsidian Plugins for Prompts

#### 1. **Dataview** (You're already using this!)
**What it does:**
- Dynamic queries across your prompts
- Auto-updating lists based on frontmatter
- Your `📋 Prompt Registry.md` uses this

**Setup:**
- Already installed (you have Dataview queries in your files)
- Keep using it for dynamic prompt catalogs

#### 2. **Templater** (Recommended)
**What it does:**
- Create prompt templates
- Auto-fill frontmatter
- Consistent prompt creation

**Install:**
```
Settings → Community Plugins → Browse → Search "Templater"
```

**Use for:**
- Creating new prompts with proper frontmatter
- Boosting prompts with templates

#### 3. **Tag Wrangler** (Helpful)
**What it does:**
- Better tag management
- Rename tags across all files
- Tag autocomplete

**Install:**
```
Settings → Community Plugins → Browse → Search "Tag Wrangler"
```

#### 4. **Advanced Tables** (If you use tables)
**What it does:**
- Better table editing
- Useful for prompt comparison tables

#### 5. **Obsidian ACP** (You have this!)
**What it does:**
- AI assistant in Obsidian
- Can help with prompt editing
- Already in `.obsidian/plugins/obsidian-acp-main/`

### Obsidian Workflow

**For Organization:**
1. Browse prompts in Obsidian
2. Use graph view to see relationships
3. Use Dataview queries to filter
4. Edit prompts directly in Obsidian
5. Use tags for organization

**For Creating:**
1. Use Templater to create from template
2. Fill in frontmatter
3. Write prompt content
4. Tag appropriately
5. Registry auto-updates via Dataview

---

## 💻 VS Code (Best for Testing/Evaluation)

### Why VS Code?

✅ **Better for:**
- Testing prompts with LLMs
- Running evaluation scripts
- Using your Python tools (`prompt-search`, `prompt-validate`, etc.)
- Code editing if prompts include code
- Git integration

### Essential VS Code Extensions

#### 1. **Continue** (Highly Recommended)
**What it does:**
- LLM integration in VS Code
- Test prompts directly
- Get responses from multiple models
- Evaluate outputs

**Install:**
```
Extensions → Search "Continue" → Install
```

**Setup:**
1. Install extension
2. Add API keys (OpenAI, Anthropic, etc.)
3. Use chat interface to test prompts

**Use for:**
- Testing prompts before saving
- Comparing responses across models
- Quick iterations

#### 2. **Markdown All in One** (Essential)
**What it does:**
- Better markdown editing
- Table formatting
- TOC generation
- Preview

**Install:**
```
Extensions → Search "Markdown All in One"
```

#### 3. **Markdown Preview Enhanced** (Nice to have)
**What it does:**
- Better markdown preview
- Math support
- Mermaid diagrams

#### 4. **GitLens** (If using Git)
**What it does:**
- Better Git integration
- See prompt history
- Track changes

#### 5. **Python** (For your scripts)
**What it does:**
- Run your `prompt-search`, `prompt-validate` tools
- Debug scripts
- Run evaluation scripts

### VS Code Workflow

**For Testing:**
1. Open prompt in VS Code
2. Use Continue extension
3. Test prompt with different models
4. Compare responses
5. Iterate and improve

**For Evaluation:**
1. Run `prompt-validate` in terminal
2. Run `prompt-search` to find prompts
3. Use evaluation scripts
4. Check results

---

## 🔄 Recommended Workflow: Both Tools

### Best of Both Worlds

**Use Obsidian for:**
- 📚 Browsing your prompt collection
- 🔍 Finding prompts (graph view, search)
- 📝 Creating new prompts (with templates)
- 🏷️ Organizing with tags
- 📊 Viewing dynamic registries (Dataview)

**Use VS Code for:**
- 🧪 Testing prompts (Continue extension)
- ✅ Validating prompts (`prompt-validate`)
- 🔎 Searching (`prompt-search`)
- 📈 Running evaluations
- 🚀 Boosting prompts (`boost_prompt.py`)

### Typical Workflow

1. **Discover** (Obsidian):
   - Browse prompt registry
   - Find prompts via graph/tags
   - Read documentation

2. **Test** (VS Code):
   - Open prompt in VS Code
   - Test with Continue extension
   - Get LLM responses

3. **Improve** (VS Code):
   - Edit prompt based on test results
   - Use `boost_prompt.py` for reference prompts
   - Validate with `prompt-validate`

4. **Organize** (Obsidian):
   - Update tags/status
   - Add to registry
   - Link related prompts

---

## 🎯 Specific Use Cases

### Creating a New Prompt

**Obsidian:**
1. Use Templater template
2. Fill frontmatter
3. Write content
4. Tag appropriately

**VS Code:**
1. Test with Continue
2. Iterate based on responses
3. Validate with `prompt-validate`

### Boosting a Reference Prompt

**VS Code:**
1. `python scripts/boost_prompt.py --list`
2. `python scripts/boost_prompt.py --boost "prompt-name.md"`
3. Edit boosted version
4. Test with Continue

**Obsidian:**
1. View boosted prompt
2. Add to registry
3. Link to original reference

### Finding Prompts

**Obsidian:**
- Use graph view
- Search (Ctrl+Shift+F)
- Dataview queries
- Tag pane

**VS Code:**
- `prompt-search -q "chain of density"`
- `prompt-search --tags ktg-directive`
- Full-text search

### Evaluating Prompts

**VS Code:**
- Run evaluation scripts
- Use `prompt-validate`
- Test with Continue
- Compare responses

**Obsidian:**
- View evaluation results
- Document findings
- Update status

---

## 📊 Comparison

| Feature | Obsidian | VS Code |
|---------|----------|---------|
| **Browsing prompts** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Graph view** | ⭐⭐⭐⭐⭐ | ❌ |
| **Tag management** | ⭐⭐⭐⭐⭐ | ⭐⭐ |
| **Testing prompts** | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Running scripts** | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Markdown editing** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Search** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Dynamic lists** | ⭐⭐⭐⭐⭐ (Dataview) | ⭐⭐ |

---

## 🚀 Setup Checklist

### Obsidian Setup
- [x] Dataview (already installed)
- [x] Obsidian ACP (already installed)
- [ ] Install Templater
- [ ] Install Tag Wrangler (optional)
- [ ] Configure templates folder

### VS Code Setup
- [ ] Install Continue extension
- [ ] Install Markdown All in One
- [ ] Install Python extension
- [ ] Configure API keys in Continue
- [ ] Install your package: `pip install -e .`

---

## 💡 Pro Tips

1. **Keep Obsidian as your "library"** - Browse, organize, discover
2. **Use VS Code as your "workshop"** - Test, improve, evaluate
3. **Sync both** - They read the same files, just different tools
4. **Use Obsidian for documentation** - Keep guides in Obsidian
5. **Use VS Code for scripts** - Run your Python tools there

---

## 🎯 Recommendation

**For your use case (4,551 prompts, boosting, testing):**

✅ **Use Obsidian** for:
- Daily browsing and organization
- Creating new prompts
- Managing your collection
- Viewing relationships

✅ **Use VS Code** for:
- Testing prompts with LLMs
- Running evaluation scripts
- Boosting reference prompts
- Validating prompts

**Both tools read the same files** - no conflict! Use whichever is better for the task at hand.

