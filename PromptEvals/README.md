# AI Anthropology

> **A working directory for AI prompt engineering research, management, and development**

## 🎯 What This Is

This is a **working directory** - a functional Python project for managing and working with AI prompts, research, and evaluations. It's organized to separate:

- **Executable code** (`src/`, `scripts/`) - Python packages and tools
- **Content** (`content/`) - Prompts, research, publications
- **Reference** (`content/reference/`) - Public prompts you can boost/improve
- **Documentation** (`docs/`) - Guides and documentation

## 🚀 Quick Start

### Installation

```bash
# Install the package in development mode
pip install -e .

# Or install with dev dependencies
pip install -e ".[dev]"
```

### Using the Tools

```bash
# Migrate prompts (add frontmatter, organize)
prompt-migrate

# Search prompts
prompt-search -q "chain of density"
prompt-search --tags ktg-directive --status ACTIVE

# Validate prompt files
prompt-validate content/prompts/

# Extract prompts from Excel
prompt-extract file.xlsx -o output/

# Boost/improve reference prompts
python scripts/boost_prompt.py --list
python scripts/boost_prompt.py --boost "prompt-name.md"
```

## 📁 Project Structure

```
.AI-Anthropology/
├── src/                    # Python package (executable code)
│   └── ai_anthropology/
│       ├── scripts/        # CLI tools
│       └── utils/          # Utility functions
├── scripts/                # Standalone utility scripts
├── tests/                  # Test files
├── config/                 # Configuration files
├── docs/                   # Documentation
├── content/                # Non-executable content
│   ├── prompts/           # Your prompt files
│   │   └── boosted/       # Boosted/improved versions
│   ├── research/          # Research materials
│   ├── publications/       # Publication content
│   ├── techniques/         # Technique docs
│   ├── evaluations/        # Test results
│   └── reference/          # Reference prompts (public repos - boost these!)
└── [legacy folders]        # Original folders (being migrated)
```

**See [ORGANIZATION.md](ORGANIZATION.md) for detailed structure explanation.**

## 🛠️ Available Tools

### `prompt-migrate`
Migrates prompt files by:
- Extracting metadata from filenames
- Adding frontmatter YAML
- Organizing by category
- Creating backups

### `prompt-search`
Search prompts by:
- Content (full-text search)
- Tags
- Model compatibility
- Status (ACTIVE, TESTING, etc.)
- Category
- Filename pattern

### `prompt-validate`
Validates prompt files:
- Checks for required frontmatter
- Validates metadata format
- Reports issues and warnings

### `prompt-extract`
Extracts prompts from Excel files:
- Reads multiple sheets
- Identifies prompt columns
- Generates markdown files with metadata

### `boost_prompt.py`
Boost/improve reference prompts:
- List available reference prompts
- Create improved versions with tracking
- Keep source attribution

## 📦 Development

### Setup

```bash
# Clone the repository
git clone <your-repo-url>
cd .AI-Anthropology

# Install in development mode
pip install -e ".[dev]"

# Run tests
pytest
```

### Code Organization

- **`src/ai_anthropology/`** - Main package
- **`src/ai_anthropology/scripts/`** - CLI entry points
- **`scripts/`** - One-off utility scripts
- **`tests/`** - Test files

### Adding New Tools

1. Create script in `src/ai_anthropology/scripts/`
2. Add entry point to `pyproject.toml`:
   ```toml
   [project.scripts]
   my-tool = "ai_anthropology.scripts.my_tool:main"
   ```
3. Reinstall: `pip install -e .`

## 📚 Content Organization

### Prompts
Save new prompts to `content/prompts/`

### Boosted Prompts
Create improved versions in `content/prompts/boosted/`

### Reference Material
Public prompts for boosting in `content/reference/public-prompts/`

### Research
Research materials go in `content/research/`

### Documentation
Project documentation in `docs/`

## 🔄 Migrating Legacy Content

To organize existing content:

```bash
# Dry run (see what would happen)
python scripts/organize_content.py --dry-run

# Actually migrate
python scripts/organize_content.py

# Archive public prompts (keep for boosting)
python scripts/cleanup_public_prompts.py --archive
```

This will move files from legacy folders (`00-Techniques/`, `01-Prompt-dump/`, etc.) to the new organized structure.

## 📖 Documentation

- **[ORGANIZATION.md](ORGANIZATION.md)** - Directory structure guide
- **[docs/](docs/)** - Additional documentation
- **Legacy docs** - Original markdown files (being migrated to `docs/`)

## 🎯 Key Principles

1. **Code vs Content**: Executable Python → `src/` or `scripts/`. Markdown/docs → `content/` or `docs/`.
2. **Working Directory**: This is a functional project, not just a collection of files.
3. **Separation**: Keep executable code separate from content/documentation.
4. **Boosting**: Reference prompts are source material - boost them into better versions!

## 📝 Requirements

- Python 3.9+
- See `requirements.txt` or `pyproject.toml` for dependencies

## 🤝 Contributing

1. Code goes in `src/`
2. Content goes in `content/`
3. Documentation goes in `docs/`
4. Follow the structure in [ORGANIZATION.md](ORGANIZATION.md)

## 📄 License

MIT License

---

**Note**: This project is transitioning from a collection of markdown files to a working directory. Legacy folders are being migrated to the new structure. See [ORGANIZATION.md](ORGANIZATION.md) for migration status.
