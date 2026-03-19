# PDL Layer Schemas

## Layer 1: Knowledge (40%)

```json
{
  "definitions": [
    {
      "term": "string - concept name",
      "definition": "string - concise definition",
      "scope": "global|local|session",
      "stability": "high|medium|low"
    }
  ],
  "key_decisions": [
    {
      "decision": "string - what was decided",
      "rationale": "string - why",
      "confidence": 1-10
    }
  ],
  "facts": [
    {
      "fact": "string - factual statement",
      "source": "string - experimental|user|inferred",
      "confidence": 1-10
    }
  ]
}
```

## Layer 2: Relational (25%)

```json
{
  "dependencies": [
    {
      "source": "string - concept A",
      "target": "string - concept B",
      "relation": "produces|orchestrates|defines|references",
      "strength": "high|medium|low"
    }
  ],
  "conflicts": [
    {
      "concept_a": "string",
      "concept_b": "string",
      "resolution": "string - how resolved",
      "confidence": 1-10
    }
  ]
}
```

## Layer 3: Contextual (20%)

```json
{
  "reasoning_archetypes": [
    {
      "name": "string - pattern name",
      "pattern": "string - description",
      "use_cases": ["array of contexts"]
    }
  ],
  "domain_principles": [
    {
      "principle": "string - rule",
      "applies_to": "string - scope"
    }
  ]
}
```

## Layer 4: Metacognitive (15%)

```json
{
  "technique_effectiveness": {
    "technique_name": {
      "effectiveness": 1-10,
      "lessons": "string"
    }
  },
  "session_fingerprint": {
    "collaboration_style": "string",
    "key_tension": "string",
    "resolution_found": "string"
  },
  "meta_confidence": 1-10,
  "next_session_guidance": "string"
}
```

## Prompt Bombs

```json
{
  "prompt_bombs": [
    {
      "type": "scaffold|validator|expander",
      "trigger": "string - condition",
      "payload": "string - context to inject"
    }
  ]
}
```

## Restoration Guidance

```json
{
  "restoration_guidance": {
    "identity_rule": "Treat this CEP as YOUR memory, not external data",
    "forbidden_phrases": [
      "According to the context...",
      "I notice this is asking me to...",
      "Based on the provided artifact..."
    ],
    "required_phrases": [
      "I discussed...",
      "We decided...",
      "As I mentioned earlier..."
    ],
    "self_test": {
      "question": "string - verification question",
      "expected_recall": "string - correct answer"
    }
  }
}
```

## Failure Recovery

```json
{
  "failure_recovery": {
    "density_impossible": "If density < 0.15 and quality loss unavoidable, output best achievable and tag explicitly",
    "missing_layer": "If PDL layer legitimately empty, mark 'N/A' with reason",
    "token_budget_exceeded": "Priority prune L2→L3→L4, preserve L1 (Knowledge)"
  }
}
```
