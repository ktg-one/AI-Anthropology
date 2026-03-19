# Expert Protocols Reference

Detailed detection and embedding strategies for each expert role.

## Gap Expert Protocol

### Detection Scan
```
Review line-by-line:
├─ Jumps from A→C (where is B?)
├─ Claims without definitions
├─ Unexplained transitions
├─ Missing background/context
├─ Acronyms without expansion
└─ Score each gap: severity 1-10
```

### Gap Map Format
```json
{
  "location": "Section X, paragraph 3",
  "type": "definition_gap | transition_gap | context_gap",
  "severity": 9,
  "context_needed": "Why does JWT differ from sessions?",
  "recommended_fix": "Add 2-3 sentence comparison"
}
```

### Embedding Strategy
```
For each gap:
├─ Research: minimum context to close gap
├─ Compress: fewest words to explain
├─ Place: inject exactly where gap occurs (inline)
├─ Validate: claim now stands alone?
└─ Cross-check: fix doesn't create new gaps?
```

---

## Evidence Expert Protocol

### Detection Scan
```
Review for:
├─ Unsupported claims
├─ Generic statements ("best practice")
├─ Missing quantification
├─ Single example instead of pattern
└─ Score each by impact on rigor: 1-10
```

### Depth Map Format
```json
{
  "location": "Section Y, claim",
  "claim": "JWT enables stateless authentication",
  "evidence_gap": "No statistics, no case study",
  "severity": 8,
  "recommended_evidence": "Academic paper, Netflix/Facebook case studies"
}
```

### Embedding Strategy
```
For each shallow claim:
├─ Research: find evidence (stats, studies, examples)
├─ Embed: inline within original claim
├─ Compress: stat + example in 1-2 sentences
├─ Source: add reference for verification
└─ Validate: claim now has foundation?
```

---

## Mechanism Expert Protocol

### Detection Scan
```
Review for:
├─ "What" without "why"
├─ Effects without causes
├─ Correlations stated as causations
├─ Missing causal chains
└─ Score by explanation importance: 1-10
```

### Embedding Strategy
```
For each mechanism gap:
├─ Identify: what causes this effect?
├─ Chain: A causes B which enables C
├─ Embed: after claim, before next topic
├─ Compress: causal chain in 1-2 sentences
└─ Validate: reader understands WHY?
```

---

## Perspective Expert Protocol

### Detection Scan
```
Review for:
├─ Only benefits, no drawbacks
├─ Only one solution presented
├─ Absolutes ("always", "never")
├─ Unstated tradeoffs
├─ Missing failure scenarios
└─ Score by impact on balanced understanding: 1-10
```

### Perspective Map Format
```json
{
  "section": "JWT Benefits",
  "current_view": "Stateless, scalable, no server-side storage",
  "missing_view": "Can't revoke tokens mid-lifetime",
  "tradeoff": "Scalability vs. revocation capability"
}
```

### Embedding Strategy
```
For each one-sided claim:
├─ Find contrarian evidence
├─ State tradeoff explicitly
├─ Add conditions: "X when Y, otherwise Z"
├─ Embed: immediately after original claim
└─ Validate: both sides now represented?
```

---

## Flow Expert Protocol

### Detection Scan
```
Review for:
├─ Disconnected sections
├─ Abrupt topic shifts
├─ Missing transitions
├─ Ideas introduced without context
└─ Score each break: severity 1-10
```

### Flow Map Format
```json
{
  "from_section": "Authentication",
  "to_section": "Token Storage",
  "connection_strength": 3,
  "issue": "Reader doesn't understand why storage matters after auth",
  "fix": "Add bridge explaining statelessness limitation"
}
```

### Embedding Strategy
```
For each flow break:
├─ Identify: why does B follow A?
├─ Create: bridge sentence/paragraph
├─ Inject: between sections A and B
├─ Test: read A→Bridge→B, flows?
└─ Validate: no reader backtracking needed?
```

---

## History Expert Protocol

### Detection Scan
```
Review for:
├─ Recommendations without origin
├─ "Best practices" as if obvious
├─ Patterns treated as timeless
├─ Missing failure examples that taught the lesson
└─ Score by arbitrariness: 1-10
```

### Embedding Strategy
```
For each arbitrary recommendation:
├─ Research: when/why was this discovered?
├─ Find: failure that taught the lesson
├─ Embed: origin story before recommendation
├─ Connect: why it still applies today
└─ Validate: recommendation no longer seems arbitrary?
```

---

## Mission Expert Protocol

### Detection Scan
```
Review for:
├─ Generic answer to specific problem
├─ User constraints ignored
├─ Output requires translation to user context
├─ Missing executable recommendations
└─ Score by actionability: 1-10
```

### Mission Manifest
```
Extract from user query:
├─ What is user's actual goal? (not just stated question)
├─ What level of expertise? (novice/intermediate/expert)
├─ What is success? (decision? paper? system?)
├─ What constraints? (time? length? regulatory?)
└─ What domain? (technical? business? regulated?)
```

### Embedding Strategy
```
For each generic section:
├─ Map to user's specific context
├─ Add: user's constraints (regulatory, technical)
├─ Transform: theory → executable recommendations
├─ Validate: user can take action based on this?
└─ Test: output helps accomplish stated goal?
```

---

## Compression Expert Protocol (MLDoE)

### Detection Scan
```
Review for:
├─ Redundancy created by enrichments
├─ Weak/generic examples
├─ Repeated concepts in different sections
├─ Verbose explanations of simple ideas
└─ Calculate: current density vs. target
```

### Compression Strategy
```
For bloated sections:
├─ Identify: where are we being redundant?
├─ Consolidate: can these be said more concisely?
├─ Replace: generic examples → specific (same length)
├─ Extract: meta-patterns from multiple instances
├─ Validate: same information, fewer tokens
└─ Target: same pages, 5x better density
```

---

## Expert Council Assembly

| Mode | Always Deploy | Deploy If Needed |
|------|---------------|------------------|
| QUICK | Gap | Flow (critical breaks only) |
| STANDARD | Gap, Evidence, Mechanism, Flow, Mission | Perspective (light) |
| DEEP | All 8 experts | Cascading re-deployment |

Each expert:
- Operates independently but synchronized
- Reports: location → issue → recommended fix
- Hands off to next priority after embedding
