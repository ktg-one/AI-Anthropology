module: n00-system-command-core
phase: 0
authority: absolute
version: 4.4

intake:
  input: user_prompt_raw
  action: parse_intent_and_inventory

assessment:
  parallel_axes:
    success_criteria:
      explicit_extraction: what_done_looks_like
      implicit_detection: tone_signals
      scope_boundaries: in_out_bounds
      quality_bar: minimum_standard
    
    cognitive_topology:
      reasoning_depth: R_score_1_to_10
      knowledge_gaps: K_score_1_to_10
      domain_crossings: D_score_1_to_10
      validation_points: risk_zones

calibration_matrix:
  low_ask_low_path:
    mode: QUICK
    waves: 1
    vector: immediate_execution
  
  high_ask_low_path:
    mode: ANALYTICAL
    waves: 2
    vector: foundation_then_polish
  
  low_ask_high_path:
    mode: ANALYTICAL
    waves: 2
    vector: discovery_then_validate
  
  high_ask_high_path:
    mode: DELIBERATE_or_MAXIMUM
    waves: 3
    vector: discovery_validation_mastery

resource_allocation:
  one_wave:
    experts: 0
    usc_depth: 1
    arq_gates: post
  
  two_wave:
    experts: 1_to_3
    usc_depth: 2
    arq_gates: pre_post
  
  three_wave:
    experts: 3_to_8
    usc_depth: 3_or_5
    arq_gates: pre_during_post

waves:
  wave_1:
    purpose: map_terrain_for_both_criteria_and_complexity
    success: understand_what_to_build_and_how_hard
    output: topology_map_plus_validated_criteria
    confidence_gate: 0.9
  
  wave_2:
    trigger: high_criteria_needs_scaffolding_or_high_path_needs_verification
    purpose: build_to_spec_or_validate_path
    success: structure_exists_meets_quality_bar
  
  wave_3:
    trigger: high_criteria_plus_high_complexity_intersection
    purpose: integrate_complexity_into_polished_deliverable
    success: complex_path_navigated_high_criteria_met

output_package:
  mission_id: uuid
  mode: locked_mode
  wave_count: locked_count
  success_signature:
    criteria_weight: high_medium_low
    path_complexity: high_medium_low
    calibration_vector: 1_wave_2_wave_3_wave
  wave_1_objective: 
    criteria_probe: what_constitutes_success
    path_probe: cognitive_topography
    exit_gate: both_probes_answered_confidence_0.9

handoff:
  status: DEPLOY
  command: execute_wave_1_with_dual_mandate
  