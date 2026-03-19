---
title: "Long context prompting tips"
source: "https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/long-context-tips"
author:
  - "[[Anthropic]]"
published:
created: 2025-09-08
description:
tags:
  - "clippings"
---
While these tips apply broadly to all Claude models, you can find prompting tips specific to extended thinking models [here](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/extended-thinking-tips).

Claude’s extended context window (200K tokens for Claude 3 models) enables handling complex, data-rich tasks. This guide will help you leverage this power effectively.

## Essential tips for long context prompts

- **Put longform data at the top**: Place your long documents and inputs (~20K+ tokens) near the top of your prompt, above your query, instructions, and examples. This can significantly improve Claude’s performance across all models.
	Queries at the end can improve response quality by up to 30% in tests, especially with complex, multi-document inputs.
- **Structure document content and metadata with XML tags**: When using multiple documents, wrap each document in `<document>` tags with `<document_content>` and `<source>` (and other metadata) subtags for clarity.
- **Ground responses in quotes**: For long document tasks, ask Claude to quote relevant parts of the documents first before carrying out its task. This helps Claude cut through the “noise” of the rest of the document’s contents.

---## [Prompt library](https://docs.anthropic.com/en/resources/prompt-library/library)

[

Get inspired by a curated selection of prompts for various tasks and use cases.

](https://docs.anthropic.com/en/resources/prompt-library/library)GitHub prompting tutorial

An example-filled tutorial that covers the prompt engineering concepts found in our docs.

[View original](https://github.com/anthropics/prompt-eng-interactive-tutorial)Google Sheets prompting tutorial

A lighter weight version of our prompt engineering tutorial via an interactive spreadsheet.

[View original](https://docs.google.com/spreadsheets/d/19jzLgRruG9kjUQNKtCg1ZjdD6l6weA6qRXG5zLIAhC8)