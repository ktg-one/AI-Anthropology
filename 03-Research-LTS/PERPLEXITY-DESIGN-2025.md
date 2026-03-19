Core Architecture: A Multi-Model MoE
Perplexity's design is a Mixture-of-Experts (MoE) system that runs 20+ AI models simultaneously on H100 GPU pods. This architecture includes:

Dynamic Routing: Classifier models analyze user intent and route tasks to the most appropriate specialist models.

Hidden Specialists: The user's model selection (e.g., Sonar, GPT-4) acts as the "primary expert," but many hidden models handle subtasks like intent classification, retrieval, and generating related questions.

Parallel Subtasks: When a query is complex, the system uses a parallel, swarm-like model to spawn ephemeral subtasks (temporary research units). This is not a persistent Supervisor-Sub-Agent architecture.

Labs, Knowledge, and Memory
Perplexity Labs: Labs tasks are user-initiated and prompt-directed, not autonomous. The runtime is dynamic, not fixed; complex, multi-component projects (like reports or dashboards) can take 30+ minutes to run. Planning is implicit and emergent from the initial prompt decomposition, not a formal, scheduled phase.

Knowledge (Spaces): While users cannot upload documents to extend the AI's core capabilities (e.g., "learn" React), Perplexity Spaces do prioritize uploaded files. Spaces function as a "centralized knowledge hub" or "core brain," where the AI synthesizes insights primarily from those materials.

Memory (Contextual): System memory is contextual and session-bound. It does not use procedural "memory injection". Chain of Density (CoD) is a prompting technique that users can apply to compress information, not a built-in protocol.

Prompting Implications
This web-aware, multi-model design means traditional, closed-model LLM techniques, vague instructions ("make this better"), or generic zero-shot role-playing are ineffective.