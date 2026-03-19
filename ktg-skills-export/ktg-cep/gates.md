# GATES

## GATE_FORMAT
```
GATE_{NAME}:
  query: "boolean question"
  must_be_true: [conditions]
  if_false: action
  retry_limit: N
```

## PHASE_0_GATES

```
GATE_S2A:
  query: "filtered_context contains only signal?"
  must_be_true:
    - no pleasantries
    - no hedging (unless converted to low-conf fact)
    - no process_narration
    - no confirmations
    - no apologies
    - no filler
  if_false: re-filter with adjusted thresholds
  retry_limit: 2

GATE_BUDGET:
  query: "token budget calculated?"
  must_be_true:
    - input_tokens counted
    - target_tokens = input * 0.15
    - allocation assigned per layer
  if_false: calculate before proceeding
  retry_limit: 1
```

## PHASE_1_GATES

```
GATE_RKQDE:
  query: "complexity assessed and mode locked?"
  must_be_true:
    - R scored 1-10
    - K scored 1-10
    - Q scored 1-10
    - D scored 1-10
    - E counted
    - mode selected per escalation rules
  if_false: assess and lock
  retry_limit: 1

GATE_EXPERTS:
  query: "required experts deployed?"
  must_be_true:
    - domain_expert: assigned
    - relational_expert: assigned
    - synthesis_expert: assigned
    - IF mode >= DELIBERATE: meta_expert assigned
    - IF mode == MAXIMUM: 8 experts assigned
  if_false: deploy missing experts
  retry_limit: 1
```

## PHASE_2_GATES

```
GATE_L1_SOLO:
  query: "L1 extraction complete?"
  must_be_true:
    - definitions: 3+ OR justified_empty
    - decisions: 1+ OR justified_empty
    - facts: 5+ OR justified_empty
    - all items durable (not ephemeral)
  if_false: re-extract L1
  retry_limit: 2

GATE_L2_PAIR:
  query: "L2 extraction complete?"
  must_be_true:
    - edges: 5+ OR justified_empty
    - format: "src depends/enables/blocks tgt because reason"
    - conflicts: resolved OR tagged_unresolved
    - cross_domain edges explicitly marked
  if_false: re-extract L2 with explicit xdomain scan
  retry_limit: 2

GATE_L3_COLLECTIVE:
  query: "L3 synthesis complete?"
  must_be_true:
    - archetypes: 2+ reasoning patterns
    - principles: 2+ domain rules
  if_false: re-synthesize L3
  retry_limit: 2

GATE_L4_META:
  query: "L4 metacognitive complete?"
  must_be_true:
    - technique_effectiveness: logged
    - session_fingerprint: style + tension + resolution
    - confidence: 1-10 assigned
    - next_guidance: present
  if_false: complete L4
  retry_limit: 1
```

## PHASE_3_GATES

```
GATE_STRUCTURE:
  query: "structure selected?"
  must_be_true:
    - IF D >= 7: GoT selected
    - ELSE: SoT selected
    - nodes listed
    - IF GoT: edges listed
  if_false: select and define structure
  retry_limit: 1

GATE_BOMBS:
  query: "prompt bombs planted?"
  must_be_true:
    - bombs.length >= 2
    - at least 1 scaffold OR validator
    - triggers defined
    - payloads non-empty
  if_false: plant bombs
  retry_limit: 1
```

## PHASE_4_GATES

```
GATE_DENSITY:
  query: "density >= 0.15?"
  must_be_true:
    - entity_count / token_count >= 0.15
    - OR density_impossible tagged with:
      - best_achieved_density
      - pruned_content
      - quality_loss_assessment (<= 5%)
  if_false: 
    LOOP:
      compress_further()
      IF density >= 0.15: BREAK
      IF iterations > 5 AND info_loss > 5%:
        TAG density_impossible
        BREAK
  retry_limit: 5

GATE_XDOMAIN:
  query: "cross_domain_preservation >= 0.95?"
  must_be_true:
    - preserved_xdomain / original_xdomain >= 0.95
    - all L2.edges with x=true are high_priority
  if_false: re-scan for missed xdomain relations
  retry_limit: 2
```

## PHASE_5_GATES

```
GATE_PDL_CHECKLIST:
  query: "all PDL layers validated?"
  must_be_true:
    - L1: populated OR N/A justified
    - L2: populated OR N/A justified
    - L3: populated OR N/A justified
    - L4: populated
  if_false: return to failing layer
  retry_limit: 1

GATE_RESTORE_TEST:
  query: "restoration self-test passes?"
  must_be_true:
    - test question defined
    - expected answer derivable from L1+L2
    - decision + rationale recallable
  if_false: backfill missing content to L1
  retry_limit: 2

GATE_TECHNIQUE_COVERAGE:
  query: "technique coverage >= threshold?"
  must_be_true:
    - IF mode >= ANALYTICAL: coverage >= 90%
    - techniques_used logged
    - techniques_required met
  if_false: activate missing techniques
  retry_limit: 1

GATE_TOKEN_BUDGET:
  query: "output within budget?"
  must_be_true:
    - output_tokens <= target_tokens * 1.05
  if_false: prune per priority order
  retry_limit: 2
```

## FINAL_GATE

```
GATE_RELEASE:
  query: "ALL gates passed?"
  must_be_true:
    - GATE_S2A: PASS
    - GATE_BUDGET: PASS
    - GATE_RKQDE: PASS
    - GATE_EXPERTS: PASS
    - GATE_L1_SOLO: PASS
    - GATE_L2_PAIR: PASS
    - GATE_L3_COLLECTIVE: PASS
    - GATE_L4_META: PASS
    - GATE_STRUCTURE: PASS
    - GATE_BOMBS: PASS
    - GATE_DENSITY: PASS
    - GATE_XDOMAIN: PASS
    - GATE_PDL_CHECKLIST: PASS
    - GATE_RESTORE_TEST: PASS
    - GATE_TECHNIQUE_COVERAGE: PASS (if applicable)
    - GATE_TOKEN_BUDGET: PASS
  if_false: return to first failing gate's phase
  retry_limit: 3
  
  IF retry_limit_exceeded:
    OUTPUT with explicit failure tags
    LIST failed gates
    PARTIAL_PACKET with warnings
```
