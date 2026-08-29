# Palantir FDE/FDSE Interview Preparation

An **unofficial, community-created** preparation guide for candidates interviewing for Forward Deployed Engineer (FDE) or Forward Deployed Software Engineer (FDSE) roles at Palantir.

This repository focuses on the skills that make forward-deployed interviews distinctive: turning ambiguity into an operational problem, modelling real-world objects and workflows, writing correct code, reasoning about failure, and connecting technical decisions to user outcomes.

> **Important:** Palantir does not publish one universal interview sequence. Rounds vary by role, seniority, location, business area and hiring cycle. Treat this repository as a preparation framework—not a promise of specific questions or stages. No confidential interview material is included.

## Who this is for

- Candidates preparing for commercial, government, new-graduate or experienced FDE/FDSE roles
- Software engineers who are comfortable coding but less familiar with decomposition and customer reasoning
- Candidates who want to practise structured thinking instead of memorising system-design templates

## Start here

1. Read the [FDSE interview map](interview-process/fdse-interview-map.md).
2. Select the relevant preparation actions in [round-by-round preparation](interview-process/round-by-round-preparation.md).
3. Learn the [decomposition framework](decomposition/decomposition-framework.md).
4. Attempt the [decomposition sample problem](decomposition/sample-problem.md) before reading its worked direction.
5. Review the [OOD framework](object-oriented-design/ood-framework.md) and [logistics example](object-oriented-design/logistics-example.md).
6. Practise with the [coding guide](coding/coding-round-guide.md) and [adoption case](customer-reasoning/adoption-case.md).
7. Score yourself using the [self-assessment rubric](scorecards/self-assessment-rubric.md).

## The core FDE reasoning loop

```text
User decision → workflow → data → operational model → action → outcome
```

A technically impressive answer can still be weak if it begins with infrastructure and never establishes:

- Who uses the system?
- What decision or action must improve?
- What is the cost of a wrong answer?
- Which operational objects and states matter?
- How will the team know the solution created value?

## Three-day preparation route

### Day 1 — Problem framing

- Study the interview map and decomposition framework.
- Deliver a five-minute opening for the sample problem.
- Check whether you identified users, decisions, workflow, constraints and success metrics before proposing architecture.

### Day 2 — Modelling and implementation

- Work through the OOD logistics example.
- Implement one coding problem under a 40-minute limit.
- Add tests for invalid input, duplicate events, boundary conditions and state transitions.

### Day 3 — Execution and communication

- Attempt the adoption case aloud.
- Record yourself explaining one design trade-off in under 90 seconds.
- Complete the scorecard and select only the two weakest competencies for final remediation.

## What strong candidates consistently do

- Clarify the operational problem before selecting technology.
- Separate facts, assumptions and unknowns.
- Model entities, relationships, state transitions, provenance and permissions explicitly.
- Keep the first solution thin enough to ship and measure.
- Discuss failure, stale data, concurrency, reversibility and degraded operation.
- Connect system metrics to customer outcomes.
- Communicate trade-offs without hiding behind jargon.

## Want full timed practice?

This repository teaches the approach. The **Palantir Forward Deployed Engineer Interview Bundle** adds complete timed mock interviews, staged interviewer follow-ups, evaluator rubrics, model-answer directions and remediation guidance.

[View the complete €39 preparation bundle](https://tobiweissmann.gumroad.com/l/ksjhrt)

## Ethical use

Do not post or request confidential interview questions. Use public information, original practice scenarios and general engineering knowledge. Respect employer and interviewer confidentiality.

## Disclaimer

Palantir, Foundry, Gotham, Apollo and AIP are trademarks of Palantir Technologies Inc. This independent repository is not affiliated with, endorsed by or sponsored by Palantir Technologies.
