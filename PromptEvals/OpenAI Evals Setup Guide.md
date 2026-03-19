# OpenAI Evals Setup & Usage Guide

## ✅ Setup Complete

OpenAI Evals has been successfully installed in `openai-evals/` directory.

## How OpenAI Evals Works

### Overview

OpenAI Evals is a framework for evaluating Large Language Models (LLMs) and systems built with LLMs. It provides:

1. **A registry of pre-built evaluations** - Test different dimensions of models
2. **Custom eval creation** - Build evals for your specific use cases
3. **Private evals** - Use your own data without exposing it publicly
4. **Standardized evaluation protocols** - Consistent way to measure model performance

### Core Concepts

#### 1. **Evals** (Evaluations)
- Test suites that measure specific capabilities (e.g., math, reasoning, coding)
- Defined in YAML files in `evals/registry/evals/`
- Can be model-graded (LLM judges the output) or rule-based

#### 2. **Completion Functions**
- Define how to interact with models
- Can use OpenAI API, other providers, or custom implementations
- Located in `evals/completion_fns/`

#### 3. **Data Files**
- Test datasets in JSONL format
- Stored in `evals/registry/data/`
- Each line is a JSON object with inputs and expected outputs

#### 4. **Solvers**
- Advanced evaluation logic for complex tasks
- Can include multi-step reasoning, tool use, etc.
- Located in `evals/solvers/`

### Directory Structure

```
openai-evals/
├── evals/
│   ├── registry/
│   │   ├── evals/          # YAML eval definitions (463 evals)
│   │   ├── data/            # Test datasets (JSONL files)
│   │   ├── completion_fns/ # Model configurations
│   │   └── solvers/         # Advanced solvers
│   ├── completion_fns/     # Completion function implementations
│   ├── solvers/             # Solver implementations
│   └── elsuite/             # Complex evaluation suites
├── docs/                    # Documentation
└── examples/                # Jupyter notebook examples
```

## Running Evals

### Basic Command

```bash
cd openai-evals
python -m evals.cli.oaieval <completion_fn> <eval_name>
```

### Examples

```bash
# Run a simple eval with GPT-4
python -m evals.cli.oaieval gpt-4 evals::test-basic

# Run with custom parameters
python -m evals.cli.oaieval gpt-4 evals::test-basic --max_samples 10

# Run multiple evals
python -m evals.cli.oaieval gpt-4 evals::test-basic,evals::test-math
```

### Common Options

- `--max_samples N` - Limit number of test cases
- `--cache` / `--no-cache` - Enable/disable caching
- `--seed N` - Set random seed for reproducibility
- `--debug` - Enable debug output
- `--dry-run` - Test without running actual evals

## Creating Custom Evals

### Method 1: YAML-Based (No Code Required)

1. **Create a data file** (`evals/registry/data/my_eval.jsonl`):
```jsonl
{"input": "What is 2+2?", "ideal": "4"}
{"input": "What is 3*3?", "ideal": "9"}
```

2. **Create an eval YAML** (`evals/registry/evals/my_eval.yaml`):
```yaml
my_eval:
  id: my_eval.test.v1
  description: Simple math test
  metrics: [accuracy]
  args:
    test_jsonl: my_eval.jsonl
```

3. **Run it**:
```bash
python -m evals.cli.oaieval gpt-4 my_eval
```

### Method 2: Custom Python Eval

For more complex logic, create a Python file:

```python
# evals/registry/evals/my_custom_eval.py
from evals.api import CompletionFn
from evals.eval import Eval

class MyEval(Eval):
    def __init__(self, completion_fn: CompletionFn, **kwargs):
        self.completion_fn = completion_fn
    
    def eval_sample(self, sample):
        # Your evaluation logic here
        result = self.completion_fn(sample["input"])
        return {"accuracy": 1.0 if result == sample["ideal"] else 0.0}
```

## Environment Setup

### Required Environment Variables

```bash
# Required: OpenAI API Key
export OPENAI_API_KEY='your-api-key-here'

# Optional: Snowflake (for logging results)
export SNOWFLAKE_ACCOUNT='your-account'
export SNOWFLAKE_DATABASE='your-database'
export SNOWFLAKE_USERNAME='your-username'
export SNOWFLAKE_PASSWORD='your-password'
```

### Windows PowerShell

```powershell
$env:OPENAI_API_KEY='your-api-key-here'
```

## Key Features

### 1. **Model-Graded Evals**
- Use an LLM to judge another LLM's output
- Defined in `evals/registry/modelgraded/`
- Great for subjective or complex evaluations

### 2. **Completion Function Protocol**
- Standardized way to interact with any model/provider
- Supports OpenAI, Anthropic, custom APIs, etc.
- See `docs/completion-fns.md`

### 3. **Eval Templates**
- Pre-built templates for common eval types
- See `docs/eval-templates.md`
- No coding required for basic evals

### 4. **Caching**
- Results are cached by default
- Speeds up re-runs and saves API costs
- Use `--no-cache` to disable

## Integration with Your Project

Your existing eval work in `evals/` directory can be integrated:

1. **Convert existing evals** to OpenAI Evals format
2. **Use OpenAI Evals** to run standardized tests
3. **Compare results** across different evaluation frameworks

## Next Steps

1. **Set your OpenAI API key**:
   ```powershell
   $env:OPENAI_API_KEY='your-key'
   ```

2. **Try a simple eval**:
   ```bash
   cd openai-evals
   python -m evals.cli.oaieval gpt-4 evals::test-basic --max_samples 5
   ```

3. **Explore existing evals**:
   - Browse `evals/registry/evals/` for available evals
   - Check `docs/run-evals.md` for detailed usage

4. **Create your own**:
   - Follow `docs/build-eval.md` for step-by-step guide
   - Check `examples/` for Jupyter notebook tutorials

## Resources

- **Official Docs**: `openai-evals/docs/`
- **GitHub**: https://github.com/openai/evals
- **OpenAI Dashboard**: https://platform.openai.com/docs/guides/evals
- **Cookbook**: https://cookbook.openai.com/examples/evaluation/getting_started_with_openai_evals

## Troubleshooting

### Git LFS Issues
If data files are missing:
```bash
cd openai-evals
git lfs fetch --all
git lfs pull
```

### PATH Issues
The scripts `oaieval.exe` and `oaievalset.exe` are installed but may not be on PATH. Use:
```bash
python -m evals.cli.oaieval
```
instead of just `oaieval`.

### API Key Not Found
Make sure `OPENAI_API_KEY` is set in your environment.

---

*Setup completed: 2025-01-20*
*Location: `F:\.AI-Anthropology\openai-evals\`*


