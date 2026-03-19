# Evaluation Results Archive

**IMPORTANT**: This folder stores all evaluation results/stamps.

## Why This Matters

When you get validation results (like 0.1 percentile from Vertex AI), these are PROOF you can show people. Always capture them immediately!

## What to Save

1. **Screenshots** - Visual proof of scores
2. **Exported results** - Raw data files
3. **Result summaries** - Using RESULTS_TEMPLATE.md
4. **Links** - To platform results pages (if available)

## File Naming

Format: `YYYY-MM-DD-[Platform]-[Model]-[Technique].md`

Examples:
- `2025-11-22-VertexAI-Gemini-Pro-KTG-CORE.md`
- `2025-11-22-OpenAI-Evals-GPT4-ARQ.md`

## Lost Results

**REAL EXAMPLE**: Lost 0.1 percentile result from Vertex AI (before it changed to Vertex AI Studio - all history gone)

**Lesson**: Platforms change, history gets wiped. Always capture immediately!

If you got results but didn't save them:
- Check platform history (if still available)
- Check browser history
- Check if platform has export feature
- **But don't count on it** - platforms change, data gets lost

**The only safe way**: Screenshot + save immediately when you see results.

## Future Runs

Always:
1. Run evaluation
2. **IMMEDIATELY** screenshot results (or use auto-capture extension)
3. Copy exact scores
4. Save to this folder
5. Never lose validation stamps again!

**See `evals/BROWSER_EXTENSIONS.md`** for auto-capture extension options!

