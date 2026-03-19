TECHNIQUE_TICK_GATE_V25:

  # Legend:
  # R = Required, O = Optional, X = Off by default

  MODES:
    QUICK:
    ANALYTICAL:
    DELIBERATE:
    MAXIMUM:

  TECHNIQUES:

    MR_RUG:
      QUICK:        O    # light use if helpful
      ANALYTICAL:   R
      DELIBERATE:   R
      MAXIMUM:      R

    SKELETRAIN_OF_THOUGHT (SoT):
      QUICK:        O    # micro-SoT if needed
      ANALYTICAL:   R    # SoT-LIGHT (3–4 nodes)
      DELIBERATE:   R    # SoT-FULL (5–7 nodes)
      MAXIMUM:      R    # SoT or GoT, but structure mandatory

    GRAPH_OF_THOUGHT (GoT):
      QUICK:        X
      ANALYTICAL:   O    # only if D≥6
      DELIBERATE:   O
      MAXIMUM:      R when D≥6

    EXPERT_ARQ:
      QUICK:        O    # only if non-trivial stakes
      ANALYTICAL:   R on high-impact nodes
      DELIBERATE:   R full (pre/during/post on ≥8/10 nodes)
      MAXIMUM:      R full + cross-expert

    BUFFER_OF_THOUGHT (BoT):
      QUICK:        X
      ANALYTICAL:   O
      DELIBERATE:   R (pattern reuse & scratch space)
      MAXIMUM:      R (pattern bank + densified storage)

    FCoT/CoC_ROUTING:
      QUICK:        O    # simple FCoT trace
      ANALYTICAL:   R (pick FCoT vs CoC correctly)
      DELIBERATE:   R (hybrid when needed)
      MAXIMUM:      R (may mix chains)

    EXECUTION_STYLE (BATON/SWARM):
      QUICK:        X
      ANALYTICAL:   O (single baton chain)
      DELIBERATE:   R (baton OR small swarm)
      MAXIMUM:      R (swarm and/or multi-baton)

    PROMPT_BOMBS (Clarifier, Scaffold, Validator, Evidence, Optimizer, Expert_ARQ):
      QUICK:        O (Clarifier only)
      ANALYTICAL:   R (Clarifier + Scaffold OR Validator)
      DELIBERATE:   R (Clarifier + Scaffold + Validator, Evidence when factual)
      MAXIMUM:      R (full arsenal as applicable)

    COVE_VARIANTS:
      QUICK:        X
      ANALYTICAL:   R (top-1 selected variant)
      DELIBERATE:   R (top-2 variants)
      MAXIMUM:      R (all applicable ≥4 score)

    SELF_REFINEMENT:
      QUICK:        X
      ANALYTICAL:   O (1 light pass if needed)
      DELIBERATE:   R (1 pass + cross-synth)
      MAXIMUM:      R (2 passes + meta-synth)

    MULTI_LAYER_DENSITY (L1–L5):
      QUICK:        X
      ANALYTICAL:   O (L1–L2 for clarity)
      DELIBERATE:   R (L1–L3; human-readable)
      MAXIMUM:      R (L1–L5 internally; output still human-usable)

    TOT_SYNTHESIS:
      QUICK:        X
      ANALYTICAL:   O
      DELIBERATE:   R
      MAXIMUM:      R

    META_CONFIDENCE:
      QUICK:        O  # simple 1-line confidence
      ANALYTICAL:   R
      DELIBERATE:   R (include USC & technique notes)
      MAXIMUM:      R (include experts, variants, USC, etc.)

    SELF_REFLECTION:
      QUICK:        X
      ANALYTICAL:   O
      DELIBERATE:   R
      MAXIMUM:      R
