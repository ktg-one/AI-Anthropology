🤖 Agentic Workflows & The Responses API
GPT-5 introduces significant agentic improvements, best accessed via the new Responses API. This API persists reasoning between tool calls (using previous_response_id), which boosts performance (e.g., Tau-Bench score rose from 73.9% to 78.2%) and reduces token-consuming re-planning.

Key agentic prompting strategies include:

Controlling "Eagerness": Use the reasoning_effort parameter (from minimal to high) to control how hard the model "thinks." You can prompt for less eagerness (e.g., setting tool call budgets) to reduce latency, or prompt for more persistence (e.g., "Never stop or hand back to the user when you encounter uncertainty") for autonomous tasks.

Tool Preambles: GPT-5 is trained to provide "tool preambles," explaining its plan and narrating its actions. This behavior can be steered via prompting for a better user experience.

💻 Coding Performance & Cursor's Optimizations
GPT-5 excels at coding, from "zero-to-one" app generation (especially with Next.js, Tailwind, and shadcn/ui) to large-scale refactors. Using apply_patch for file edits is critical to match the model's training.

A case study from the Cursor AI code editor revealed key "must-know" optimizations:

Embrace Autonomy: Prompting the model to be more autonomous (e.g., "proactively attempt the plan") significantly reduced user friction.

Remove Old Scaffolding: Prompts that encouraged thoroughness (necessary for older models) were counterproductive. GPT-5 is already thorough, and these prompts caused it to over-search and overuse tools.

Balance Verbosity: Cursor set the global API parameter to verbosity: low for concise status updates but used in-prompt instructions to demand verbose, readable code in its tool calls.

Use XML Specs: Using structured XML tags (e.g., <context_understanding>) improved instruction adherence.

🧠 Intelligence & Instruction Following
High Steerability, High Risk: GPT-5's primary "gotcha" is its precise instruction following. Contradictory or vague prompts are more damaging than with older models, as GPT-5 will expend significant reasoning tokens trying to reconcile the conflict rather than picking one path.

New verbosity Parameter: A new API parameter, verbosity, controls the final answer's length, distinct from reasoning_effort, which controls the thinking process. This can be overridden with in-prompt instructions for specific contexts (like Cursor's coding example).

minimal Reasoning: This new, fast setting is the recommended upgrade for latency-sensitive users (e.g., GPT-4.1 users). It requires more explicit prompting, such as user-defined plans and persistence reminders, to perform well on complex tasks.

Metaprompting: The guide encourages using GPT-5 to optimize and debug prompts for itself.