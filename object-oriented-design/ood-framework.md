# Object-Oriented Design Framework

Strong OOD represents behaviour, constraints and change—not just nouns connected by arrows.

## Step 1: State the use cases

Write three to six concrete operations. For a dispatch system:

- Create a shipment plan.
- Assign an eligible vehicle.
- Record a vehicle location.
- Mark a stop complete.
- detect a constraint violation.
- propose and approve reassignment.

Use cases determine which behaviours the model must support.

## Step 2: Identify entities and value objects

- **Entity:** has identity and lifecycle, such as `Shipment` or `Vehicle`.
- **Value object:** defined by its attributes and preferably immutable, such as `GeoPoint`, `TimeWindow` or `Capacity`.
- **Service:** coordinates behaviour that does not naturally belong to one object, such as route optimisation.
- **Repository:** abstracts persistence; it should not contain business decisions.

## Step 3: Define invariants

Examples:

- A delivered shipment cannot return directly to `IN_TRANSIT`.
- Assigned cargo must not exceed vehicle capacity.
- A vehicle cannot have two overlapping active assignments.
- Completing a stop twice must not create duplicate effects.

Place invariant enforcement close to the object that owns the state.

## Step 4: Make transitions explicit

Avoid unrestricted setters such as `setStatus(String)`. Prefer intention-revealing operations:

```java
shipment.dispatch(vehicleId, dispatchedAt);
shipment.recordArrival(stopId, arrivedAt);
shipment.completeStop(stopId, proofOfDelivery);
shipment.cancel(reason, cancelledBy);
```

Each operation validates the current state, required data, permissions and idempotency rule.

## Step 5: Separate changing policy

Eligibility, prioritisation and pricing often change independently of entity lifecycle. Express them behind focused interfaces:

```java
interface AssignmentPolicy {
    AssignmentDecision evaluate(Shipment shipment, Vehicle vehicle, Context context);
}
```

Do not create an interface for every class. Introduce an abstraction where multiple policies are credible or change has a clear boundary.

## Step 6: Address concurrency and failure

State who owns the transaction boundary. Consider:

- optimistic version checks for concurrent updates
- idempotency keys for repeated commands
- an outbox for reliable event publication
- explicit rejection results rather than partially updated objects
- compensation or operator repair for cross-system failure

## Step 7: Test behaviour

Prioritise tests such as:

- rejects assignment above vehicle capacity
- rejects an overlapping active assignment
- accepts repeated completion command idempotently
- permits only defined state transitions
- retains the previous assignment when reassignment publication fails

## Warning signs

- An anemic model with only fields and getters/setters
- One manager class containing every rule
- Inheritance based only on shared fields
- Persistence annotations driving the domain design
- Status represented by arbitrary strings
- Interfaces added without a variation or testing need
- No answer for concurrent commands
