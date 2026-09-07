# FDE Self-Assessment Rubric

Score one complete spoken or written answer. Do not award points for ideas you intended to mention but did not communicate.

## 100-point rubric

| Dimension | Points | Strong-answer evidence |
|---|---:|---|
| Problem framing and discovery | 20 | Identifies user, decision, workflow, error cost and success criteria |
| Domain and ontology modelling | 15 | Models operational objects, relationships, states, provenance and uncertainty |
| Technical architecture | 15 | Derives architecture from scale, latency, security and reliability constraints |
| Failure and correctness reasoning | 15 | Handles stale data, concurrency, permissions, reversibility and degradation |
| MVP and prioritisation | 15 | Defines a measurable thin slice and explicitly defers lower-value scope |
| Customer and adoption judgment | 10 | Considers frontline users, stakeholder conflict and workflow integration |
| Communication | 10 | Structures ambiguity clearly and explains trade-offs without excessive jargon |

## Scoring anchors

For each dimension, award a percentage of the available points:

- **90–100%:** specific, coherent, evidence-backed and integrated into the design
- **70–89%:** sound coverage with one meaningful omission or weak connection
- **50–69%:** recognises the issue but handles it generically or too late
- **1–49%:** fragmentary mention without an actionable design consequence
- **0%:** absent or materially incorrect

## Readiness bands

| Total | Interpretation | Next action |
|---:|---|---|
| 85–100 | Strong practice performance | Maintain fluency; practise novel constraints |
| 70–84 | Promising but inconsistent | Repair the two lowest dimensions |
| 55–69 | Material interview risk | Repeat one framework-guided case daily |
| Below 55 | Foundations not yet reliable | Slow down and rebuild framing, modelling and correctness |

## Critical caps

Regardless of total points, cap the answer at **69** if it:

- proposes architecture without identifying a user decision or action
- permits an unsafe or unauthorised action without mitigation
- ignores a central correctness constraint after it is raised
- cannot explain how the MVP creates measurable evidence

## Evaluator worksheet

```text
Problem framing and discovery: __ / 20
Domain and ontology modelling:  __ / 15
Technical architecture:         __ / 15
Failure/correctness reasoning:   __ / 15
MVP and prioritisation:          __ / 15
Customer/adoption judgment:      __ / 10
Communication:                   __ / 10
----------------------------------------
Total:                           __ / 100

Strongest evidence:

Most consequential omission:

One behaviour to repeat:

One behaviour to change in the next attempt:
```

## How to use the score

Record yourself, wait ten minutes and score the answer from observable evidence. Then ask another person to score it independently. A difference greater than ten points usually means the evidence or rubric interpretation is too vague; discuss the specific answer moment rather than averaging blindly.
