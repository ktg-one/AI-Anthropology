---
title: End-to-End DAG-Path (EEDP) Prompting
source: https://learnprompting.org/docs/new_techniques/end_to_end_dag_path_prompting
author:
  - '[["Valeriia Kuka"]]'
published:
created: 2025-09-08
description: Explore End-to-End DAG-Path Prompting, a graph flattening technique for LLMs, improving long-range reasoning in graphs.
tags:
  - clippings
feature: thumbnails/external/7bb85bdb8fb7b25b20a4d8b0a73bf6b6.svg
---
◆ This article is rated [hard](https://learnprompting.org/docs/introduction#header-4)

Reading Time: 3 minutes

Last updated on March 10, 2025

[Valeriia Kuka](https://learnprompting.org/docs/new_techniques/#Valeriia%20Kuka-bio)

Takeaways

- **EEDP Overview**: End-to-End DAG-Path (EEDP) prompting is a graph flattening technique that enhances long-range reasoning in large language models (LLMs) by converting graphs into text focused on key paths.
- **Methodology**: EEDP flattens graphs by identifying backbone paths, converting them into structured text, and creating directed acyclic graphs (DAGs) to improve [LLM](https://learnprompting.org/vocabulary/LLM) processing while reducing prompt length.
- **Performance Gains**: EEDP surpassed traditional graph-flattening methods in connectivity and distance prediction tasks, significantly improving accuracy for long-distance relationships.

![Overview of End-to-End DAG-Path (EEDP) Prompting](https://learnprompting.org/docs/assets/advanced/new_docs_oct3/end_to_end_dag_cover.svg)

Overview of End-to-End DAG-Path (EEDP) Prompting

## What is End-to-End DAG-Path prompting (EEDP)?

**End-to-End DAG-Path prompting (EEDP)**, is a graph flattening technique designed to improve reasoning performance in [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM), particularly in scenarios involving long-range dependencies in graphs.

Graphs are often used to represent relationships in data, such as in social networks or molecular structures, but LLMs cannot handle graphs directly. Graph flattening converts graphs into textual formats so that LLMs can process them.

The challenge with existing methods is that they perform well for short-distance reasoning but struggle with long-distance scenarios. Inspired by how humans reason about complex structures, EEDP optimizes graph flattening by focusing on the most important paths in a graph, improving LLMs' ability to understand long-range relationships without losing performance in short-distance scenarios.

### How EEDP Works

1. **Graph Representation**: EEDP flattens a graph by identifying **main backbone paths** between important nodes (endpoints). It generates a specialized graph format called **DAG-Path** that organizes these key paths.
2. **Textual Conversion**: The backbone paths are converted into a structured text format, which the LLM can interpret. This includes compressing repeated sections to reduce the prompt length while retaining essential information.
3. **Graph Preprocessing**: EEDP creates a directed acyclic graph (DAG) from the original input graph, focusing on nodes with zero in-degree or zero out-degree. The backbone paths are extracted from this DAG to form the final textual representation used by the LLM.

## How this technique differs from existing techniques

Compared to traditional graph-flattening methods like adjacency lists or edge lists, EEDP introduces several innovations:

- **Long-distance reasoning**: Existing methods struggle with long paths in graphs, where relationships are spread across many nodes. EEDP enhances reasoning by focusing on paths that connect key nodes, preserving important structural information.
- **Path-based structure**: EEDP doesn’t rely only on one-hop connections (like adjacency matrices) but instead builds upon complete paths between endpoints. This allows for a more holistic view of the graph structure.
- **Compression of information**: EEDP can compress redundant parts of paths in the graph, making the representation more concise and reducing the number of tokens LLMs need to process.

## Results of the Technique

EEDP was tested on two datasets: **Merged 1000** (from educational knowledge graphs) and **ZINC test 2500** (molecular graphs). The method outperformed traditional graph-flattening approaches on tasks such as **connectivity prediction** (whether two nodes are connected) and **distance prediction** (length of the path between nodes).

| Dataset | Task | Accuracy Improvement (%) |
| --- | --- | --- |
| Merged 1000 | Connectivity Prediction | +7% |
| ZINC test 2500 | Distance Prediction | +10% |

The method showed particular strength in handling long-distance relationships, where previous techniques often struggled, making it highly effective for more complex graph-based tasks.

## Conclusion:

EEDP provides a robust and efficient way to flatten graphs for LLMs, enabling these models to perform well in reasoning tasks that involve both short- and long-distance dependencies in graph structures. By mimicking human cognitive reasoning and optimizing graph descriptions, EEDP enhances the performance of LLMs on complex graph-based tasks.