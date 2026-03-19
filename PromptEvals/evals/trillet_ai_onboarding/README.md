# Trillet AI Onboarding Guide - OpenAI Evals

Evaluation dataset and test cases for the Trillet AI onboarding guide.

## Overview

This evaluation tests how well LLMs can answer questions about Trillet AI platform onboarding based on the "Good AI Client Onboarding Guide: Trillet AI Platform" document.

## Files

- `trillet_onboarding_dataset.yaml` - Test cases with questions and ideal answers
- `trillet_onboarding_eval.py` - Evaluation script
- `README.md` - This file

## Test Cases

The dataset includes 18 test cases covering:
- Platform overview and capabilities
- Sign-up and interface navigation
- Agent creation and configuration
- Prompt writing best practices
- Testing procedures
- Phone number setup
- Call management (single vs batch)
- Transfer setup
- Troubleshooting
- Best practices
- Onboarding roadmap
- Success criteria

## Running the Evaluation

### Prerequisites

```bash
pip install evals openai
```

### Convert YAML to JSONL

```bash
python -c "
import yaml
import json

with open('trillet_onboarding_dataset.yaml', 'r') as f:
    data = yaml.safe_load(f)

with open('trillet_onboarding_dataset.jsonl', 'w') as f:
    for test_case in data['test_cases']:
        f.write(json.dumps(test_case) + '\n')
"
```

### Run Evaluation

```bash
oaieval gpt-4 trillet_onboarding_eval \
  --samples_jsonl trillet_onboarding_dataset.jsonl
```

Or with custom completion function:

```bash
oaieval your-completion-fn trillet_onboarding_eval \
  --samples_jsonl trillet_onboarding_dataset.jsonl \
  --max_samples 10
```

## Evaluation Metrics

- **Accuracy**: Overall correctness of responses
- **Exact Match Rate**: Percentage of responses matching ideal answers exactly
- **Key Points Coverage**: Percentage of responses containing key information points

## Expected Performance

A well-trained model should achieve:
- Accuracy: ≥ 85%
- Exact Match Rate: ≥ 60%
- Key Points Coverage: ≥ 90%

## Notes

- Test cases are designed for non-technical users
- Answers should be clear, actionable, and comprehensive
- Focus on practical, step-by-step guidance
- Includes troubleshooting and best practices

