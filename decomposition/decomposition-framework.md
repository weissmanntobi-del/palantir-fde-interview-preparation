# Decomposition Framework

Decomposition is the discipline of converting a vague operational problem into a solution that users can adopt, engineers can build and stakeholders can evaluate.

## The FRAME–MODEL–SHIP framework

### 1. FRAME the operational problem

#### F — Frontline user

Who performs the work? Who consumes the result? Who approves or is accountable for the decision?

#### R — Real workflow

What happens today from trigger to outcome? Where are the handoffs, delays and workarounds?

#### A — Action or decision

What should the user do differently with the system's output? Information that produces no decision or action rarely creates operational value.

#### M — Mistake cost

What happens after a false positive, false negative, stale result or unavailable system? Can a human reverse the decision?

#### E — Evidence of success

Define a baseline and target. Combine operational metrics—latency, accuracy, freshness—with outcome metrics such as missed incidents, delivery delay or time saved.

### 2. MODEL the operational domain

Describe:

- **Entities:** persistent objects such as Shipment, Vehicle, Facility or Incident
- **Events:** observations such as LocationReported or DeliveryFailed
- **Relationships:** assignment, containment, dependency and ownership
- **States:** controlled lifecycle stages and permitted transitions
- **Provenance:** source, timestamp, confidence and transformation history
- **Permissions:** who may see, change, approve or execute

Keep observed facts separate from derived conclusions. “Sensor reported 85°C” and “machine is likely failing” have different provenance and uncertainty.

### 3. SHIP a measurable thin slice

#### S — Slice

Select one user, one workflow and one valuable decision. State what is explicitly deferred.

#### H — Handling failure

Address missing and stale data, duplicate events, source conflict, access denial, downstream outage and manual recovery.

#### I — Interfaces and architecture

Only now select ingestion, storage, services and user interface. Derive technology from latency, volume, security, availability and deployment constraints.

#### P — Pilot and proof

Define rollout group, human fallback, monitoring, feedback loop, ownership and a go/no-go metric.

## Worked five-minute opening

Prompt: “Design a system to reduce late deliveries for a logistics company.”

> “Before selecting architecture, I want to define whose decision we are improving. I will assume the primary user is a regional dispatcher who must decide whether to reassign a vehicle, change a route or alert a customer. I would first map the workflow from order creation through dispatch and delivery, then identify where lateness becomes detectable and where intervention is still useful.
>
> I need four clarifications: the baseline late-delivery rate, the decisions dispatchers can actually take, how quickly location and traffic data arrive, and the cost of unnecessary intervention. For now, I will assume 50,000 active shipments, GPS updates every minute, a 30-minute intervention window and human approval for reassignment.
>
> My thin slice would cover one region and identify shipments at high risk of being more than 20 minutes late. The core objects are Shipment, Stop, Vehicle, Driver, RoutePlan and LocationEvent. I would preserve source timestamps and confidence because stale GPS data must not trigger an automatic reassignment.
>
> The system would ingest order, vehicle and traffic events, maintain current operational state, calculate risk, and present the dispatcher with the reason and permitted actions. I would initially recommend rather than automatically execute. Success would require a reduction in avoidable late deliveries without increasing unnecessary reassignments or dispatcher workload. If those assumptions are acceptable, I’ll model the workflow and state transitions before designing the components.”

Why this works: it frames the user and decision, makes assumptions visible, proposes a measurable slice and creates a clean transition into modelling.

## Common decomposition failures

- Beginning with Kafka, Kubernetes or a vector database
- Asking questions without converging on assumptions
- Modelling only database tables rather than operational behaviour
- Ignoring source conflict, timestamp and confidence
- Automating a high-cost action without approval or reversal
- Defining only technical metrics
- Designing the complete enterprise platform instead of a thin slice
