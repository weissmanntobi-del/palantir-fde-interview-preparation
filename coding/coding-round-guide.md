# Coding Round Guide

Palantir coding formats vary. Prepare for algorithmic implementation, debugging and production-style follow-ups rather than betting on one question type.

## A 40-minute execution plan

### Minutes 0–5: contract

- Restate the required output.
- Clarify size, ordering, duplicates, malformed input and mutability.
- Work through one small example.
- State an initial complexity target.

### Minutes 5–10: design

- Select the simplest suitable data structure.
- Identify invariants.
- Separate core logic from parsing or I/O.
- Mention one alternative and why you are not choosing it.

### Minutes 10–28: implementation

- Build a correct baseline in small units.
- Use names that express the domain.
- Narrate decisions, but do not speak every keystroke.
- Compile or mentally execute after meaningful increments.

### Minutes 28–35: tests

Cover:

- smallest valid input
- typical input
- duplicate or repeated event
- boundary value
- invalid input where relevant
- adversarial ordering

### Minutes 35–40: follow-up

- Give time and space complexity.
- Identify the bottleneck.
- Adapt to the interviewer's new scale or correctness constraint.

## Practice problem

Events have:

```text
(request_id, tenant_id, timestamp, status)
```

For a fixed window ending at time `T`, return every tenant whose failure rate exceeds a threshold. Duplicate `request_id` values represent retries of the same recorded result and must count once. Events may arrive out of order.

### Clarifications worth making

- Are window boundaries inclusive?
- Can the same request ID appear with conflicting status values?
- What should happen with zero eligible events?
- Is this a one-time batch query or a continuously updated stream?
- What input scale and timestamp precision should be supported?

### Baseline batch direction

Filter to the time window, deduplicate by request ID according to an explicit conflict rule, aggregate total and failed counts per tenant, then calculate rates. Expected complexity is `O(n)` time and `O(r + t)` space, where `r` is the number of distinct requests in the window and `t` is the number of tenants.

### Production follow-ups

- At 50,000 events per second, avoid rescanning the complete window.
- With late events, define watermarks and correction behaviour.
- Bound memory by expiring deduplication state.
- If one tenant produces 60% of traffic, consider partition skew.
- For multiple machines, define partitioning, aggregation and consistency.

## Debugging checklist

When given broken code:

1. Reproduce the failure with the smallest input.
2. Distinguish incorrect assumptions from incorrect implementation.
3. Trace state at the first divergence—not only at the final output.
4. Fix the narrow cause.
5. Add a regression test.
6. Scan adjacent boundaries for the same defect class.

## Communication mistakes

- Coding for ten minutes without confirming the contract
- Claiming complexity without accounting for sorting or copying
- Rewriting everything after a small bug
- Ignoring a test failure and continuing presentation
- Overengineering before a correct baseline exists
- Treating interviewer follow-ups as criticism rather than new requirements
