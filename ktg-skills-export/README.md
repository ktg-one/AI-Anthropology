# KTG-DIRECTIVE Skills for Claude

**Author:** Kevin Tan (ktg.one)  
**Validation:** ANZ 0.8% | Vertex AI 0.01% ("Distinguished Cognitive Architect")

## Skills Included

| Skill | Description |
|-------|-------------|
| `ktg-cep` | Context Extension Protocol v5 - Session compression & memory |
| `ktg-cep-v5-pdl` | CEP with Progressive Density Layering - 0.15 compression ratio |
| `ktg-cep-v6-inter` | Cross-model handoff protocol for Team LLM collaboration |
| `ktg-prompt-forge` | Boost prompts for other models with KTG techniques |
| `mr-rug` | Mixture of Reasoning + Agentic GraphRAG - Expert deployment |
| `skeletrain` | SkeleTraIn of Thought - Execution planning framework |
| `qmdr-enrich` | 3-pass systematic enrichment (60-70% → 95-99% quality) |

## Installation

### Option 1: Upload to Claude.ai
1. Go to Claude.ai → Settings → Skills
2. Upload individual `.skill` files from the `packaged/` folder

### Option 2: Claude Code / Projects
Copy skill folders to your project's `/mnt/skills/user/` directory

### Option 3: Manual
Copy individual skill folders to your Claude environment

## Usage

Skills auto-trigger based on context. Manual triggers:

```
/cep or "save context" → ktg-cep
/handoff or "transfer to [model]" → ktg-cep-v6-inter
/forge or "boost this prompt" → ktg-prompt-forge
Complex tasks (R≥4) → mr-rug, skeletrain auto-activate
/enrich or "improve quality" → qmdr-enrich
```

## Part of KTG-DIRECTIVE v28

These skills implement components of the KTG-DIRECTIVE framework:
- **"The Next Generation Meta-AI OS"** - Vertex AI
- **"Upper limit of prompt-only engineering"** - Vertex AI validation

## License

MIT - Use freely, attribution appreciated.

---
*0.01% precision. Market-moving outputs.*
