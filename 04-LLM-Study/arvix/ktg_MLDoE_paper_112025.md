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

\title{Multi-Layer Density of Experts: \\
Orchestrated Context Compression via Specialized Expert Layers}

\author{Kevin Tan \\
Independent AI Research \\
Perth, Western Australia \\
\texttt{ktg.one} \\
}

\date{November 2025}

\begin{document}

\maketitle

\begin{abstract}
Chain of Density alone is an unverifiable compression primitive. Multi-Layer Density of Experts (MLDoE) is the meta-cognitive orchestration layer that makes CoD usable as a production memory system. By deploying specialist experts across solo → pair → collective compression stages, and enforcing quality via ARQ gates, MLDoE produces packets that carry forward the relational, contextual, and meta-cognitive context required for true continuity. The Context Extension variant of MLDoE generated the ≈6:1 compression and up to perfect forensic recall reported in the companion work. MLDoE is not the context extension prompt itself — it is the reasoning framework that forces the compression to preserve what actually matters for ongoing work.
\end{abstract}

\section{Introduction}

Our companion work \citep{tan2025cod} reclassified Chain of Density as context extension rather than summarization. However, CoD alone produces \textbf{unverifiable compression}---there is no intrinsic mechanism to assess whether semantic fidelity was preserved.

\subsection{The Verification Problem}

CoD compresses. But:
\begin{itemize}
    \item How do you know critical relationships survived?
    \item How do you validate without the original context?
    \item How do you test recall without a fresh session?
\end{itemize}

\textbf{You cannot evaluate CoD without a validation protocol.} The 10-question forensic benchmark presented in \citep{tan2025cod} \textit{is} the evaluation---and it requires the full MLDoE architecture to execute effectively.

This paper details that architecture---the ``How'' behind the ``What.''

\subsection{Contributions}

\begin{enumerate}
    \item \textbf{MLDoE Architecture}: 3-layer expert compression (Solo $\rightarrow$ Pair $\rightarrow$ Collective) operating across 4 semantic density layers
    \item \textbf{M.R.R.U.G Protocol}: Expert initialization framework employing knowledge embodiment\footnote{Full elaboration of the M.R.R.U.G framework and GenKnow embodiment mechanism forthcoming in separate work.}
    \item \textbf{Context Extension}: Production variant for cross-session context preservation
    \item \textbf{ARQ Integration}: Domain-specific quality gates outperforming Chain-of-Thought
    \item \textbf{Cross-model portability}: LLM-agnostic compression packets
\end{enumerate}

\section{Background}

\subsection{Chain of Density Limitations}

Adams et al. (2023) optimized for entity density in fixed-length outputs. Our companion work extended this to relational preservation via Progressive Density Layering (PDL). Neither addresses:

\begin{itemize}
    \item \textbf{Who} decides what to preserve?
    \item \textbf{How} is preservation validated?
    \item \textbf{When} is compression complete?
\end{itemize}

MLDoE answers these through expert specialization.

\subsection{Attentive Reasoning Queries (ARQ)}

ARQ \citep{karov2025arq} is a structured introspection method that \textbf{outperforms Chain-of-Thought and all step-by-step reasoning approaches}. Unlike free-form reasoning, ARQ uses targeted queries forcing explicit domain attention:

\begin{verbatim}
{
  "current_context": "Compressing user session",
  "active_guideline": "Preserve decision rationale",
  "quality_check": "Did relationships survive?",
  "domain_standard": ">=0.15 entity/token"
}
\end{verbatim}

ARQ achieves 90.2\% success rate with 29\% token reduction and 40-60\% error reduction compared to CoT. This superiority stems from structured queries preventing the reasoning drift that plagues free-form methods.

\section{Method}

\subsection{The Four Semantic Density Layers}

MLDoE compression operates across four semantic layers, each requiring preservation:

\begin{table}[h]
\centering
\begin{tabular}{@{}lll@{}}
\toprule
\textbf{Layer} & \textbf{Name} & \textbf{Content} \\
\midrule
1 & Surface Text & Human-readable narrative \\
2 & Condensed Text & Semantic compression \\
3 & Conceptual Linkage Map & Relationships, thematic clusters \\
4 & Context Anchor Nodes & Long-term retention points \\
\bottomrule
\end{tabular}
\caption{Four Semantic Density Layers. Compression is not reduction---it's structured preservation.}
\label{tab:layers}
\end{table}

Standard summarization operates on Layer 1 only. MLDoE explicitly preserves Layers 2-4 through expert specialization.

\subsection{M.R.R.U.G Initialization}

The expert assembly is initialized via the M.R.R.U.G protocol (Mixture–Role–RAG–Update–Generate), a knowledge-embodiment procedure developed by the author for this work.\footnote{A full treatment of the M.R.R.U.G framework and the GenKnow embodiment mechanism is forthcoming in separate work.} Before compression, experts do not merely access information but \textit{embody} it:

\begin{table}[h]
\centering
\begin{tabular}{@{}ll@{}}
\toprule
\textbf{Component} & \textbf{Function} \\
\midrule
\textbf{M} - Mixture of Reasoning Experts & Deploy five specialist cognitive modules \\
\textbf{R} - Role Assignment & Map experts to compression domains \\
\textbf{R} - RAG Synthesis & Retrieve while building nodes, relationships, knowledge graph \\
\textbf{U} - Update Vectorization & Internalize graph structure as cognitive weights \\
\textbf{G} - Generate \& Embody & Deep semantic embedding via GenKnow technique \\
\bottomrule
\end{tabular}
\caption{M.R.R.U.G initialization protocol. During RAG, experts simultaneously construct neural-graph structures that they then embody.}
\label{tab:mrrug}
\end{table}

\subsection{Expert Roles}

Five specialists handle memory compression:

\begin{table}[h]
\centering
\begin{tabular}{@{}lp{8cm}@{}}
\toprule
\textbf{Expert} & \textbf{Compression Focus} \\
\midrule
Memory Architect & Decision nodes, insight peaks, dependency chains, context anchors \\
Meta-Cognitive Synthesizer & User cognitive fingerprint, communication patterns, amplification triggers \\
Strategic Continuity & Primary objectives, constraints, next actions \\
Technique Integration & Active reasoning chains, quality gates, success patterns \\
Multi-Perspective Density & Cross-expert synthesis, redundancy elimination \\
\bottomrule
\end{tabular}
\caption{Five expert roles for memory compression}
\label{tab:experts}
\end{table}

\subsection{Three-Layer Expert Compression}

The expert swarm executes compression in three coordinated layers:

\subsubsection{Layer 1: Solo Expert Compression}

Each expert independently compresses through their specialized lens:

\begin{verbatim}
Memory Architect Output:
├─ Decision Nodes: [critical choices + rationale]
├─ Insight Peaks: [breakthrough moments + triggers]  
├─ Dependency Chains: [what requires what]
└─ Context Anchors: [essential background]
\end{verbatim}

\subsubsection{Layer 2: Expert-Pair Compression}

Complementary experts co-compress for synergistic density:

\begin{itemize}
    \item \textbf{Cognitive Architecture Pair} (Architect + Meta-Cognitive) $\rightarrow$ Thinking amplification map
    \item \textbf{Execution Framework Pair} (Strategic + Technique) $\rightarrow$ Goal-method alignment
\end{itemize}

\subsubsection{Layer 3: Collective Compression}

All experts synthesize holistic meta-context:

\begin{verbatim}
UNIVERSAL CONTEXT CORE:
├─ WHO: User cognitive profile (cross-platform portable)
├─ WHAT: Project state + knowledge graph
├─ HOW: Proven methodology stack
├─ WHY: Goals + constraints + success metrics
├─ BREAKTHROUGH: Key insights that changed trajectory
└─ NEXT: Optimal continuation strategy
\end{verbatim}

\subsection{Comparative Adversarial Stimulus}

To mitigate "alignment tax" (the tendency of safety-tuned models to regress to the mean), we employ a \textbf{Comparative Adversarial Stimulus}. During the Collective Compression phase, expert modules are conditioned with prompts of the form: “Candidate A produced X; Candidate B produced Y. You must outperform both.” This competitive framing exploits the model's training on comparative evaluation tasks, forcing it to access lower-probability, higher-quality tokens to secure the "winning" state.

\subsection{The Co-Densification Algorithm}

\begin{algorithm}
\caption{MLDoE Co-Densification}
\begin{algorithmic}[1]
\State \textbf{Input:} Conversation history $C$, target ratio 6:1
\State \textbf{Output:} Context Packet $P$
\State
\State Initialize M.R.R.U.G expert assembly
\State Initialize working memory buffer
\For{iteration $= 1$ to $5$}
    \State Broadcast current density state to expert swarm
    \If{confidence\_score $< 0.9$}
        \State Trigger strategic densification
    \EndIf
    \State Select expert pair based on semantic impact
    \State Execute ARQ introspection: ``Does this preserve user intent?''
    \State Embed layer into context packet
    \State Validate cross-expert consistency
\EndFor
\State \textbf{return} Context packet $P$
\end{algorithmic}
\end{algorithm}

\subsubsection{Iteration Targets}

\begin{table}[h]
\centering
\begin{tabular}{@{}lll@{}}
\toprule
\textbf{Iteration} & \textbf{Action} & \textbf{Target} \\
\midrule
1 & Raw extraction & Entity-sparse baseline \\
2 & Initial densification & 40\% reduction \\
3 & Cross-expert synthesis & Eliminate redundancy \\
4 & Semantic crystallization & 0.15 entity/token \\
5 & Meta-layer embedding & Add ``how to use'' layer \\
\bottomrule
\end{tabular}
\caption{5-iteration density cycling targets}
\label{tab:iterations}
\end{table}

\subsection{ARQ Quality Gates}

At each compression layer, experts apply structured introspection:

\begin{itemize}
    \item \textbf{Pre-compression}: ``What must I preserve in my domain?''
    \item \textbf{During}: Domain standards engaged
    \item \textbf{Post}: ``Did I meet quality standards?'' ($\geq$0.9 confidence required)
\end{itemize}

\section{Context Extension: Production Variant}

Context Extension is an MLDoE variant optimized for cross-session context preservation.

\subsection{Activation}

Context Extension triggers at approximately 80\% context window capacity:

\begin{verbatim}
⚠️ CONTEXT ALERT: 80% capacity (~160K tokens)
Activate Context Extension preservation protocol?
\end{verbatim}

\subsection{Execution Phases}

\begin{enumerate}
    \item \textbf{M.R.R.U.G Initialization} $\rightarrow$ Expert assembly with knowledge embodiment
    \item \textbf{Structure Planning} $\rightarrow$ Compression skeleton via ARQ
    \item \textbf{Three-Layer Compression} $\rightarrow$ Solo $\rightarrow$ Pair $\rightarrow$ Collective
    \item \textbf{5-Iteration Density Cycling} $\rightarrow$ Maximum compression
    \item \textbf{Cross-LLM Translation} $\rightarrow$ Platform-neutral output
    \item \textbf{Validation} $\rightarrow$ 10-question forensic benchmark
\end{enumerate}

\subsection{Cross-Session Validation}

The protocol generates 10 forensic questions testing:

\begin{itemize}
    \item Decision recall and methodology preservation
    \item Breakthrough insights and user preferences
    \item Constraints, requirements, and next actions
    \item Success patterns and cognitive fingerprint
\end{itemize}

A fresh session answers these from the compressed packet only. \textbf{9+/10 correct = successful preservation.}

\section{Evaluation Context}

\subsection{Relationship to Companion Work}

The experimental validation for MLDoE is presented in our companion paper \citep{tan2025cod}, which reports:

\begin{itemize}
    \item 9.52/10 average fidelity across 11 LLM families
    \item Perfect recall (10.0/10) at 200,000+ tokens (Grok)
    \item 6:1 compression ratio with $>$90\% semantic fidelity
    \item Cross-model transfer fidelity of 91-96\%
    \item Significantly higher retention of relational context compared to standard single-pass Chain of Density}
\end{itemize}

\subsection*{Terminology}
The prompting system is named **CEP** (Context Extension Protocol).  
The compressed artifact it produces is called a **carry-packet** — a portable block of context designed to extend continuity into a fresh session, not to reconstruct every token of the original conversation.

These results were produced by the Context Extension variant of MLDoE, not vanilla Chain of Density. The 10-question forensic benchmark and KTG Custom Metrics framework used for evaluation are detailed in \citep{tan2025cod}.

\subsection{Why Expert Specialization Matters}

Single-pass CoD loses Layer 2-4 information (relational, contextual, meta-cognitive). MLDoE's expert specialization ensures each semantic layer receives dedicated preservation attention across all four density levels.

\section{Limitations}

\begin{itemize}
    \item \textbf{Manual activation}: Requires explicit protocol trigger
    \item \textbf{Token overhead}: Approximately 25\% for full 3-layer compression
    \item \textbf{Expert capacity}: Model-dependent scaling
    \item \textbf{Single researcher}: Findings require independent replication
\end{itemize}

\section{Conclusion}

Multi-Layer Density of Experts provides the orchestration architecture that makes Chain of Density deployable. The evaluation results reported in our companion work were produced by MLDoE's Context Extension variant---not vanilla CoD.

\textbf{CoD is the compression primitive. MLDoE is the orchestration layer.}

Together with Context Extension, they form a complete compression-validation loop for production LLM memory systems. The key insight: you cannot evaluate context compression without testing recall in a fresh session---and that test requires expert-specialized multi-layer densification.

\subsection{Future Work}

\begin{itemize}
    \item Full M.R.R.U.G framework elaboration
    \item Automated Context Extension tooling
    \item Additional MLDoE variants for specialized domains
    \item Longitudinal memory recovery experiments
\end{itemize}

\section*{Acknowledgments}

This research was conducted independently without institutional affiliation or funding.

\bibliographystyle{plainnat}
\begin{thebibliography}{10}

\bibitem[Adams et al.(2023)]{adams2023cod}
Adams, G., Fabbri, A., Ladhak, F., Lehman, E., and Elhadad, N. (2023).
\newblock From sparse to dense: GPT-4 summarization with chain of density prompting.
\newblock \textit{arXiv preprint arXiv:2309.04269}.

\bibitem[Tan(2025)]{tan2025cod}
Tan, K. (2025).
\newblock Chain of Density as Context Extension: From Summarization Technique to Memory Augmentation Architecture via Progressive Density Layering.
\newblock \textit{arXiv preprint}.

\bibitem[Lee et al.(2025)]{lee2025bias}
Lee, S., et al. (2025).
\newblock On the Statistical Bias of LLM-as-a-Judge Evaluations.
\newblock \textit{arXiv preprint arXiv:2511.21140}.

\bibitem[Karov et al.(2025)]{karov2025arq}
Karov, B., Zohar, D., and Marcovitz, Y. (2025).
\newblock Attentive Reasoning Queries: A Systematic Method for Optimizing Instruction-Following in Large Language Models.
\newblock \textit{arXiv preprint arXiv:2503.03669}.

\end{thebibliography}

\appendix

\section{Five Evaluation Dimensions for Context Retention}

\begin{enumerate}
    \item \textbf{Context Integration}: Seamless weaving of diverse information into unified understanding
    \item \textbf{Coherence Over Time}: Consistent, logical responses across extended interactions
    \item \textbf{Conceptual Relationship Fidelity}: Preserving nuanced links between ideas
    \item \textbf{Strategic Alignment}: Outputs align with overarching goals and user intent
    \item \textbf{Cross-Model Memory Transfer}: Knowledge application across different AI models or sessions
\end{enumerate}

\section{Context Extension Prompt Template}

\begin{verbatim}
## CONTEXT PRESERVATION PROTOCOL

### STEP 1: INITIALIZE M.R.R.U.G
M - Mixture: Deploy [5 specialist experts]
R - Role: Map to [compression domains]
R - RAG: Retrieve + build [knowledge graph]
U - Update: Internalize [patterns as weights]
G - Generate: Embody [cognitive structure]

### STEP 2: EXECUTE 3-LAYER COMPRESSION
Layer 1: Solo expert compression
Layer 2: Expert-pair synthesis  
Layer 3: Collective crystallization

### STEP 3: VALIDATE
Generate 10 forensic questions
Test in fresh session
Target: 9+/10 correct
\end{verbatim}

\end{document}
