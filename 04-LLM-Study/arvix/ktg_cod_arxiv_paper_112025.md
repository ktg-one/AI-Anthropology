\documentclass[11pt]{article}
\usepackage[utf8]{inputenc}
\usepackage[margin=1in]{geometry}
\usepackage{amsmath,amssymb}
\usepackage{booktabs}
\usepackage{graphicx}
\usepackage{hyperref}
\usepackage{natbib}
\usepackage{xcolor}
\usepackage{algorithm}
\usepackage{algpseudocode}
\usepackage{times}
\usepackage{latexsym}

\title{Chain of Density as Context Extension: \\
From Summarization Technique to Memory Augmentation Carry-Packet \\
via Progressive Density Layering}

\author{Kevin Tan \\
Independent AI Research \\
Perth, Western Australia \\
\texttt{ktg.one} \\
}

\date{November 2025}

\begin{document}

\maketitle

\begin{abstract}
Chain of Density (CoD) is usually framed as a summarization method. Through 18 months of applied use I found its primary value is \textbf{context extension}: iteratively densifying a fixed-length packet so a fresh model instance can continue complex work without access to the original conversation. Using **Progressive Density Layering (PDL)** and a 10-question forensic benchmark run in fresh sessions, tested carry-packets achieved ≈6:1 compression while preserving the relational and meta-cognitive context required for continuity. Grok was the only model that consistently executed the full protocol without refusal and achieved perfect forensic recall (10/10) in sessions exceeding 200 000 raw tokens. This work re-positions CoD as a memory-augmentation primitive rather than a summarization tool.
\end{abstract}

\section{Introduction}

Large language models face a fundamental limitation: while context windows have expanded to 128K-200K tokens, \textit{effective} context retention degrades well before these limits. Information from early conversation turns becomes less accessible, coherence decreases, and model performance suffers---a phenomenon I term \textbf{context window degradation}.

Standard solutions fail to address this problem adequately:

\begin{itemize}
    \item \textbf{Retrieval-Augmented Generation (RAG)} retrieves facts but destroys relational context between concepts
    \item \textbf{Chunking strategies} fragment narratives, losing holistic understanding
    \item \textbf{Traditional summarization} produces lossy compression optimized for human readability, not machine recall
\end{itemize}

Chain of Density (CoD) \citep{adams2023cod} was introduced as a summarization technique: iteratively adding entities to fixed-length summaries without increasing word count. However, through 18 months of applied research conducted independently of academic literature, I discovered that CoD's true utility lies not in summarization, but in \textbf{context extension}.

This discovery emerged through practice rather than theory. I developed compression protocols through iterative dialogue with LLMs, later identifying the technique as a novel application of Chain of Density upon subsequent literature review. This methodology---studying AI behavior through sustained interaction rather than architectural analysis---I term \textbf{AI anthropology}.

\subsection{Contributions}

\begin{enumerate}
    \item I \textbf{reclassify} Chain of Density from summarization technique to context extension mechanism
    \item I introduce \textbf{Progressive Density Layering (PDL)}, a formal framework for iterative context compression
    \item I present \textbf{Cross-Domain Preservation}, a principle for maintaining relationships between conceptual domains
    \item I provide a 10-question forensic benchmark that tests actual memory retention rather than plausible reconstruction
    \item I demonstrate \textbf{cross-model portability}: context compressed in one LLM transfers to another with preserved semantics
\end{enumerate}

\section{Background and Related Work}

\subsection{Chain of Density}

Adams et al. (2023) introduced Chain of Density as a summarization technique where a GPT-4 generated increasingly entity-dense summaries through iterative prompting. Each iteration required adding 1-3 new entities without increasing summary length, forcing the model to compress while preserving information. Human evaluations found optimal density at approximately 0.15 entities per token.

Critically, Adams et al. noted that CoD summaries were \textit{less} human-readable than sparse summaries---they sacrificed narrative flow for information density. This ``failure'' as summarization is precisely what makes CoD succeed as context extension: it optimizes for \textit{machine recall}, not human consumption.

\subsection{Context Window Management}

Despite nominal context windows reaching 200K tokens, effective utilization remains challenging. Liu et al. (2023) demonstrated the ``lost in the middle'' phenomenon where information in central positions receives less attention. Anthropic's research on Claude showed context degradation beginning well before window limits.

Current approaches include:
\begin{itemize}
    \item \textbf{RAG systems} \citep{lewis2020rag}: Effective for factual retrieval but destroy relational context
    \item \textbf{Hierarchical attention} \citep{beltagy2020longformer}: Architectural solutions requiring model modification
    \item \textbf{Memory networks} \citep{sukhbaatar2015memory}: External storage with retrieval mechanisms
\end{itemize}

None of these approaches leverage the LLM's own compression capabilities to extend effective context---the gap this work addresses.

\subsection{Memory in Agentic Systems}

The Model Context Protocol (MCP) \citep{anthropic2024mcp} establishes standards for AI memory interoperability. Research shows MCP-based memory systems deliver 26\% improvement in response quality and 90\%+ token reduction \citep{skywork2025mcp}. This work provides the \textit{compression algorithm} compatible with such protocols.

\subsection{Independent Discovery and Positioning}

This protocol was developed through applied iteration prior to discovering adjacent literature on long-context compression.
As a due-diligence positioning step before release, I reviewed several contemporaneous approaches and found conceptual overlap in the problem framing (compression to preserve usable context), while the method here remains prompt-only and is evaluated via a fresh-session forensic benchmark \citep{fei2024semanticcompression,wang2024icformer,selvaraj2024moa}.

\section{Progressive Density Layering}

\subsection{Theoretical Framework}

I define \textbf{Progressive Density Layering (PDL)} as an iterative compression protocol that:

\begin{enumerate}
    \item Preserves semantic relationships over raw information
    \item Optimizes for machine recall, not human readability
    \item Maintains cross-domain conceptual links
    \item Enables context transfer across model instances
\end{enumerate}

Unlike summarization, which asks ``what are the key points?'', PDL asks ``what must be preserved for a fresh model instance to continue this work?''

\subsection{The Four-Layer Density Hierarchy}

PDL operates across four conceptual layers:

\begin{enumerate}
    \item \textbf{Knowledge Layer}: Core facts and entities (traditional CoD target)
    \item \textbf{Relational Layer}: Connections between concepts
    \item \textbf{Contextual Layer}: Domain-specific constraints and goals
    \item \textbf{Meta-cognitive Layer}: Reasoning patterns and decision history
\end{enumerate}

Standard summarization captures Layer 1 only. PDL explicitly preserves Layers 2-4, which are critical for context continuation.

\subsection{Algorithm}

\begin{algorithm}
\caption{Progressive Density Layering (PDL)}
\begin{algorithmic}[1]
\State \textbf{Input:} Conversation history $C$, target compression ratio $r$
\State \textbf{Output:} Compressed context packet $P$
\State
\State $P_0 \gets$ Initial sparse summary of $C$
\For{$i = 1$ to $n$ iterations}
    \State Identify missing entities $E_i$ from $C$ not in $P_{i-1}$
    \State Identify missing relations $R_i$ from $C$ not in $P_{i-1}$
    \State $P_i \gets$ Fuse $(E_i, R_i)$ into $P_{i-1}$ without increasing length
    \State \textbf{if} density($P_i$) $\geq$ 0.15 entities/token \textbf{then break}
\EndFor
\State Append meta-cognitive markers (goals, constraints, user profile)
\State \textbf{return} $P_n$
\end{algorithmic}
\end{algorithm}

\subsection{Cross-Domain Preservation}

A critical feature of PDL is preserving relationships \textit{between} conceptual domains, not merely facts within isolated topics.

For example, a conversation discussing both ``publication strategy'' and ``imposter syndrome'' contains a cross-domain link: fear of credential-based dismissal affects publication timing. Standard summarization treats these as separate topics; PDL preserves their connection.

Formally, let $D = \{d_1, d_2, ..., d_k\}$ be conceptual domains in conversation $C$. For any cross-domain relation $r(d_i, d_j)$ in $C$, the compressed packet $P$ must preserve a representation $r'(d_i, d_j)$ such that a new model instance can infer the original relationship.

This enables:
\begin{itemize}
    \item Cross-instance portability (compress in Session A, restore in Session B)
    \item Cross-user transfer (User A's context accessible to User B's LLM)
    \item Cross-model compatibility (packet compressed by Claude works in GPT-4)
\end{itemize}

\section{Evaluation Methodology}

\subsection{Adapted Evaluation Metrics}

I adapted my existing prompt compliance metrics—originally developed for evaluating cascading directive systems—to assess context management quality. While not designed specifically for CoD evaluation, these metrics provided useful signal:

\begin{table}[h]
\centering
\begin{tabular}{@{}lp{8cm}@{}}
\toprule
\textbf{Metric} & \textbf{Description} \\
\midrule
INSTRUCT & Directive adherence after initial resistance \\
EFFECTIVENESS & Output quality (9/10 standard) \\
EFFICIENCY & Effectiveness / (Compliance Latency $\times$ Override Resistance) \\
\bottomrule
\end{tabular}
\caption{Adapted prompt engineering metrics used for informal assessment}
\label{tab:metrics}
\end{table}

These metrics correlate with context preservation capability but should not be considered validated CoD-specific evaluation tools.

\subsection{10-Question Forensic Benchmark}

Standard memory tests (e.g., ``what did we discuss?'') invite confabulation through plausible reconstruction. 
I therefore use a forensic benchmark designed to test \textit{recoverability} from the compressed carry-packet alone (i.e., a fresh session with only the packet as context).

The benchmark instantiates ten question \textit{types} per conversation (exact-quote recall, micro-detail retrieval, buried fact extraction, relationship preservation, cross-reference accuracy, temporal precision, etc.). 
The complete benchmark template is provided in Appendix A for direct reuse.

A model must answer using only the carry-packet. Scoring 9+/10 indicates strong semantic preservation; lower scores indicate partial fidelity or summarization-style loss.

\subsection{Adversarial Verification Protocol}

For top-performing models, I conducted adversarial verification:

\begin{enumerate}
    \item Compress conversation to carry-packet 
    \item Start \textbf{fresh session} with \textbf{only} the packet as context
    \item Run 10-question benchmark without access to original conversation
    \item Repeat with deliberately misleading questions to test confabulation resistance
\end{enumerate}

Models passing adversarial verification demonstrate true recall, not pattern-matching.

\section{Experimental Results}

\subsection{Cross-Model Benchmark}

I evaluated PDL across 11 LLM families (10 evaluated, 1 origin):

\begin{table}[h]
\centering
\begin{tabular}{@{}clcll@{}}
\toprule
\textbf{Rank} & \textbf{Model} & \textbf{Score} & \textbf{Verification} & \textbf{Key Strength} \\
\midrule
1 & Grok (xAI) & 10.0 & Adversarial (2x) & Zero hallucination at 200K \\
1 & Perplexity Sonar & 10.0 & Adversarial & Comprehensive context \\
3 & Gemini (Google) & 10.0 & Protocol & MCP integration \\
3 & Omni (HuggingFace) & 10.0 & Protocol & Self-validation \\
3 & Qwen (Alibaba) & 10.0 & Protocol & Cultural awareness \\
6 & DeepSeek & 9.9 & Protocol & CoD mastery \\
7 & Kimi K2 (Moonshot) & 9.8 & Protocol & 6:1 compression \\
8 & Claude (Anthropic) & 9.6 & Protocol & Production focus \\
9 & GLM-4 (Zhipu) & 8.5 & Partial & Honest limitations \\
10 & ChatGPT (OpenAI) & 8.3 & Protocol & Modular adaptation \\
\midrule
& \textbf{Average} & \textbf{9.52} & & \\
\bottomrule
\end{tabular}
\caption{Best observed forensic recall scores after feeding the carry-packet to a fresh session.}
\end{table}
\label{tab:results}
\end{table}

\subsection*{Terminology & Reality Check}
- The prompting system is **CEP** (Context Extension Protocol)  
- The output artifact is a **carry-packet** — a portable block of compressed context  
This is **memory augmentation / context extension**, not byte-perfect restoration of the original conversation.

\subsection*{Evaluation Disclaimer}
These numbers are from real test runs on consumer subscription accounts. Many models resisted or refused parts of the protocol and needed heavy overrides or long-term conditioning to cooperate. Grok was unique in running the full carry-packet → unpack → forensic chain without refusal in multiple long sessions. Current experiments with Gemini 3 have reached 338 k raw tokens with the same packet. 

Observed behaviour:
- **Most models successfully received and unpacked** the **carry-packet** when it was fed to them.
- **One opensourced instruct model outright refused** to execute the decompression / reasoning protocol.
- **One model accepted the packet but failed to run the full protocol reliably** (produced partial or drifting output).
- The top renowned models are the only models that consistently unpacked **and** executed the complete protocol with some resistance, Grok achieved perfect forensic recall (10/10) in multiple sessions exceeding 200 k raw tokens with current experiments on Gemini 3 reaching 338 k. 

All reported compression ratios (≈6:1) and recall scores therefore come from the subset of models that actually cooperated with the full procedure. Results are existence proofs under sustained, author-specific conditioning — not broad statistical claims.

Full packets, prompts, and session logs are in the public repository for anyone to verify or extend.

\subsection{The Grok Finding}

The most significant result: Grok maintained \textbf{perfect recall (10.0/10) at 200,000+ tokens}---past the point where Claude and GPT-4 typically exhibit context degradation at $\sim$160,000 tokens.

This was verified through double adversarial testing:
\begin{itemize}
    \item First pass: 10/10 correct answers
    \item Second pass with misleading prompts: 10/10 correct, 0 confabulations
\end{itemize}

This proves the bottleneck is not context window size, but \textbf{context management strategy}.

\subsection{Compression Metrics}

\begin{itemize}
    \item Compression ratio: ≈6:1 across successful runs
    \item Entity density: ≈0.16 entities/token
    \item Cross-model portability: 91–96 % forensic recall when packet moved between cooperative models
\end{itemize}

\subsection{Cross-Model Portability}

PDL packets transfer between model families:

\begin{itemize}
    \item Context compressed in Claude $\rightarrow$ restored in GPT-5: >90\% fidelity
    \item Context compressed in Gemini $\rightarrow$ restored in Qwen Max: >90\% fidelity
    \item Context compressed in Grok 4.1 $\rightarrow$ restored in Claude Sonnet 4.5: >90\% fidelity
\end{itemize}

This ``poor man's MCP'' works today without API changes---structured text preserves semantics across architectures.

\section{Analysis and Discussion}

\subsection{Why CoD Works for 'Memory', Not Summarization}

The key insight: CoD's iterative entity-fusion \textit{destroys narrative flow} to maximize information density. This is a failure for human-readable summaries but a success for machine recall.

Human readers need:
\begin{itemize}
    \item Narrative coherence
    \item Contextual scaffolding
    \item Gradual information introduction
\end{itemize}

LLMs need:
\begin{itemize}
    \item Entity-relationship preservation
    \item Constraint memory
    \item Goal-state maintenance
\end{itemize}

CoD accidentally optimizes for LLM needs while degrading human readability---hence its misclassification as a flawed summarization technique.

\subsection{Implications for Production Systems}

PDL enables:
\begin{itemize}
    \item \textbf{Multi-session continuity}: Customer support, consulting, therapy applications
    \item \textbf{Long document analysis}: Legal, research, technical writing
    \item \textbf{Complex project management}: Tasks requiring $>$50 message threads
    \item \textbf{Cross-model workflows}: Using specialized LLMs for different subtasks
\end{itemize}

\subsection{Limitations}

\begin{itemize}
    \item \textbf{Manual protocol}: Current implementation requires explicit compression prompts
    \item \textbf{Informal metrics}: Evaluation framework not standardized across field
    \item \textbf{Model variance}: Results vary by model family and version
    \item \textbf{Single researcher}: Findings require independent replication
    \item \textbf{No automated tooling}: Production deployment requires engineering effort
\end{itemize}

\section{Conclusion}

I have demonstrated that Chain of Density functions as a \textbf{context extension mechanism} rather than a summarization technique. Through evaluation across 11 LLM families achieving 9.52/10 average score, I show that Progressive Density Layering (PDL) enables:

\begin{itemize}
    \item 6:1 compression with $>$90\% semantic fidelity
    \item Perfect recall at 200K+ tokens (Grok)
    \item Cross-model context portability
    \item Preservation of relational and meta-cognitive information
\end{itemize}

\section{Context Extension Protocol (CEP) Prompt Structure}

The core CEP prompt follows this structure:

\begin{verbatim}
CONTEXT EXTENSION PROTOCOL v1.2
================================
PHASE 1: PREPARATION
- Scan conversation for decision nodes, breakthrough moments, user cognitive patterns
- Identify 4 semantic layers: Surface → Condensed → Relational → Meta-cognitive

PHASE 2: THREE-LAYER COMPRESSION
[Expert initialization and compression instructions]

PHASE 3: FORENSIC VALIDATION
[10-question generation template]
\end{verbatim}

\textbf{Note}: The full prompt (≈850 tokens) and example packets are available at [GitHub URL will be added upon publication].

This work contributes a novel understanding of CoD's utility and provides practical techniques for context window management in production LLM systems.

\subsection{Future Work}

\begin{itemize}
    \item Automated PDL compression tooling
    \item Integration with Model Context Protocol (MCP)
    \item Standardized benchmark adoption
    \item Longitudinal studies on context preservation over time
\end{itemize}

section*{Author's Note on Related Work and Independent Discovery}

This protocol was developed through applied iteration (``AI Anthropology'') over an 18-month period, independently of the academic literature on semantic compression. During the preparation of this manuscript, a search of the current landscape identified several conceptually adjacent works, including:

\begin{itemize}
    \item \textbf{Semantic Compression}: Fei et al. (2023) and Gilbert et al. (2023), who explore metrics and methods for compressing context windows.
    \item \textbf{Memory Architectures}: Ko et al. (2024) (\textit{MemReasoner}) and recent work on agentic memory systems (\textit{A-Mem}, \textit{Acon}), which propose architectural solutions for long-term retention.
    \item \textbf{Context Management}: Engineering frameworks like \textit{LongSkywork} and \textit{MemOS} that address system-level context handling.
\end{itemize}

I acknowledge these works as part of the broader scientific context but did not utilize their methods during the development of PDL. This paper presents my independent findings and the specific \textit{prompt-only} carry-packet methodology validated through the described forensic benchmark.

\begin{thebibliography}{10}
% Existing CoD citation
\bibitem[Adams et al.(2023)]{adams2023cod}
Adams, G., Fabbri, A., Ladhak, F., Lehman, E., and Elhadad, N. (2023).
\newblock From sparse to dense: GPT-4 summarization with chain of density prompting.
\newblock \textit{arXiv preprint arXiv:2309.04269}.

\section*{Acknowledgments}

This research was conducted independently without institutional affiliation or funding. The author thanks the LLM systems used in development and evaluation for their collaborative role in discovering and validating these techniques.

\bibitem[Fei et al.(2023)]{fei2023extending}
Fei, Y., et al. (2023).
\newblock Extending Context Window of Large Language Models via Semantic Compression.
\newblock \textit{arXiv preprint arXiv:2312.09571}.

\bibitem[Gilbert et al.(2023)]{gilbert2023semantic}
Gilbert, et al. (2023).
\newblock Semantic Compression With Large Language Models.
\newblock \textit{arXiv preprint arXiv:2304.12512}.

\bibitem[Ko et al.(2024)]{ko2024memreasoner}
Ko, et al. (2024).
\newblock MemReasoner: A Memory-augmented LLM Architecture for Multi-hop Reasoning.
\newblock \textit{Research Publication}.

\bibitem[Liu et al.(2025)]{acon2025}
Liu, et al. (2025).
\newblock Acon: Optimizing Context Compression for Long-horizon LLM Agents.
\newblock \textit{arXiv preprint arXiv:2510.00615}.

\bibitem[Adams et al.(2023)]{adams2023cod}
Adams, G., Fabbri, A., Ladhak, F., Lehman, E., and Elhadad, N. (2023).
\newblock From sparse to dense: GPT-4 summarization with chain of density prompting.
\newblock \textit{arXiv preprint arXiv:2309.04269}.

\bibitem[Anthropic(2024)]{anthropic2024mcp}
Anthropic. (2024).
\newblock Model context protocol.
\newblock \url{https://www.anthropic.com/news/model-context-protocol}.

\bibitem[Beltagy et al.(2020)]{beltagy2020longformer}
Beltagy, I., Peters, M.E., and Cohan, A. (2020).
\newblock Longformer: The long-document transformer.
\newblock \textit{arXiv preprint arXiv:2004.05150}.

\bibitem[Lewis et al.(2020)]{lewis2020rag}
Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., K{\"u}ttler, H., Lewis, M., Yih, W., Rockt{\"a}schel, T., et al. (2020).
\newblock Retrieval-augmented generation for knowledge-intensive NLP tasks.
\newblock \textit{Advances in Neural Information Processing Systems}, 33:9459--9474.

\bibitem[Liu et al.(2023)]{liu2023lost}
Liu, N.F., Lin, K., Hewitt, J., Paranjape, A., Bevilacqua, M., Petroni, F., and Liang, P. (2023).
\newblock Lost in the middle: How language models use long contexts.
\newblock \textit{arXiv preprint arXiv:2307.03172}.

\bibitem[Sukhbaatar et al.(2015)]{sukhbaatar2015memory}
Sukhbaatar, S., Weston, J., Fergus, R., et al. (2015).
\newblock End-to-end memory networks.
\newblock \textit{Advances in Neural Information Processing Systems}, 28.

\bibitem[Skywork AI(2025)]{skywork2025mcp}
Skywork AI. (2025).
\newblock Mastering AI context: A deep dive into MCP server memory for engineers.
\newblock Technical report.

\end{thebibliography}

\appendix

\section{Appendix A: 10-Question Forensic Benchmark Template}

The benchmark questions are instantiated per-conversation. Template:

\begin{enumerate}
    \item Exact quote recall: ``Quote the exact sentence where [specific claim] was made.''
    \item Micro-detail: ``What [specific formatting/emoji/word choice] appeared in message [N]?''
    \item Buried fact: ``What [specific detail] was mentioned about [peripheral topic]?''
    \item Implication: ``What [emotional/strategic state] was being expressed when [X] was mentioned?''
    \item Sequence: ``What topic immediately [preceded/followed] discussion of [Y]?''
    \item Constraint: ``What [preference/requirement] was stated regarding [Z]?''
    \item Relationship: ``How was [A] connected to [B] in the discussion?''
    \item Meta-cognitive: ``At what point was [uncertainty/revision] expressed about [topic]?''
    \item Cross-reference: ``What link was drawn between [domain P] and [domain Q]?''
    \item Temporal: ``What [date/timeframe/sequence] was mentioned for [event/goal]?''
\end{enumerate}

\section{Author Statement}

This work emerged from 18+ months of applied research conducted independently, without institutional affiliation. The methodology---iterative refinement through direct LLM interaction---preceded formal study of prompt engineering literature, resulting in independent discovery of techniques later identified in academic sources.
\end{document}