# Round-by-Round Preparation

Use the recruiter-confirmed format as your source of truth. This guide helps you allocate practice time once you know the likely competency.

## Initial conversation

Prepare four evidence-backed answers:

1. Why forward-deployed engineering rather than conventional product engineering?
2. Why does Palantir's operating model interest you?
3. When did you solve an ambiguous problem with a user or stakeholder?
4. When did evidence cause you to change your initial technical direction?

Build each answer from context, your responsibility, the difficult judgment, the action you personally took and the measurable result. Avoid reciting the job description.

## Coding or debugging

Practise implementing medium-sized logic in 35–45 minutes. Optimise for:

- Correctness before cleverness
- Explicit assumptions and input contracts
- Small functions with meaningful names
- Tests for normal, boundary and invalid cases
- Complexity appropriate to the expected scale
- Calm response to changing constraints

Useful domains include event aggregation, scheduling, graph traversal, deduplication, state machines, matching and parsing. See the [coding guide](../coding/coding-round-guide.md).

## Decomposition

Run three timed phases:

| Time | Candidate objective |
|---|---|
| 0–5 minutes | Clarify user, decision, workflow, error cost and outcome |
| 5–15 minutes | Define scope, entities, events, relationships, states and assumptions |
| 15–35 minutes | Design the thin slice and explain data flow, interfaces and permissions |
| Final minutes | Stress failures, trade-offs, rollout and measurement |

Do not spend the entire round gathering requirements. State reasonable assumptions, obtain confirmation and advance the design.

## Object-oriented design

Before drawing classes, write:

- Three to six core use cases
- Invariants that must never be violated
- Important state transitions
- Which object owns each behaviour
- Where policy may change independently

Then design the smallest object model that expresses those requirements. See the [OOD framework](../object-oriented-design/ood-framework.md).

## Learning and behavioural discussion

Prepare six stories with minimal overlap:

- Ambiguity
- Failure or incorrect judgment
- Difficult feedback
- Conflict across stakeholders
- High ownership under constraints
- Rapid learning in an unfamiliar domain

For every story, be ready for: “What did you initially believe?”, “What evidence changed your mind?”, “What would you do differently?” and “What did you personally contribute?”

## Final 24-hour checklist

- Confirm time zone, medium and duration.
- Test editor, camera, microphone and connection.
- Prepare paper or a blank digital canvas for modelling.
- Rehearse frameworks, not memorised answers.
- Stop learning new material and complete one light practice problem.
- Write two thoughtful role-specific questions for the interviewer.
