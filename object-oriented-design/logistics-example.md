# Logistics OOD Example

## Problem

Design the core domain model for a logistics dispatcher. Shipments contain ordered stops and capacity requirements. Dispatchers assign eligible vehicles, record progress and may reassign a shipment after a breakdown.

## Requirements and invariants

- Stops must be completed in the planned order unless an authorised override exists.
- Cargo requirements must fit vehicle capacity.
- A vehicle cannot hold overlapping assignments.
- Reassignment requires a reason and produces an audit event.
- Repeating the same command must not duplicate transitions or events.
- Completed or cancelled shipments cannot be reassigned.

## Candidate model

### Entities

`Shipment`

- identity, version and lifecycle state
- ordered stops
- cargo requirement
- current assignment
- operations: `assign`, `dispatch`, `completeStop`, `requestReassignment`, `cancel`

`Vehicle`

- identity, capacity and availability state
- active assignment periods
- operations: `reserve`, `release`, `reportUnavailable`

`ReassignmentRequest`

- identity, shipment, old assignment, reason, requester and approval state
- operations: `approve`, `reject`, `expire`

### Value objects

- `Capacity(weightKg, volumeM3)`
- `TimeWindow(start, end)`
- `GeoPoint(latitude, longitude)`
- `CargoRequirement(capacity, constraints)`
- `Assignment(vehicleId, period, assignedAt)`

### Policies and services

- `VehicleEligibilityPolicy` evaluates capacity, time overlap and operational constraints.
- `AssignmentService` coordinates shipment and vehicle transactions.
- `RoutePolicy` validates standard or authorised stop order.

## State model

```text
PLANNED → ASSIGNED → IN_TRANSIT → DELIVERED
   │          │           │
   └──────────┴───────────┴──→ CANCELLED
```

Reassignment is not merely another shipment state. It is a controlled process that may replace an assignment while the shipment remains assigned or in transit.

## Command flow: assign a vehicle

1. Load `Shipment` and `Vehicle` at known versions.
2. Reject a terminal shipment.
3. Ask `VehicleEligibilityPolicy` for a decision with reasons.
4. Reserve the vehicle for the planned period.
5. Assign the shipment.
6. Commit both changes or neither.
7. Publish `VehicleAssigned` through a reliable outbox.
8. Return the new versions and decision evidence.

## Concurrency scenario

Two dispatchers assign the same vehicle concurrently. Both initially observe it as available. Use optimistic versions or a database constraint on overlapping active assignments. One command succeeds; the other receives a conflict and must refresh alternatives. A last-write-wins update would silently create an invalid plan.

## Example interfaces

```java
public interface VehicleEligibilityPolicy {
    EligibilityDecision evaluate(
        Shipment shipment,
        Vehicle vehicle,
        AssignmentContext context
    );
}

public sealed interface EligibilityDecision {
    record Eligible() implements EligibilityDecision {}
    record Ineligible(List<Reason> reasons) implements EligibilityDecision {}
}
```

The decision object explains rejection and supports both user feedback and auditability.

## Follow-up questions

- How would you support split shipments?
- Where should hazardous-material compatibility live?
- What changes if vehicle availability comes from an eventually consistent external system?
- How do you recover when the database commit succeeds but event publication initially fails?
- Which commands require dispatcher versus supervisor permission?

## Evaluation signal

A strong answer connects domain concepts to executable invariants, explicit transitions, concurrency control and user-visible recovery. A large class diagram alone is not sufficient.
