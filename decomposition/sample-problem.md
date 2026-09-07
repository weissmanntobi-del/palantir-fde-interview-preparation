# Sample Decomposition Problem

## Candidate prompt

A regional hospital network says:

> “We need an AI dashboard that predicts emergency-department crowding.”

Design an initial solution. You have 35 minutes.

## Candidate instructions

Do not read the worked direction until you have delivered at least a five-minute opening. Use the following checkpoints:

1. Identify users and decisions.
2. Map the current workflow.
3. Define failure costs and success criteria.
4. Model the operational domain.
5. Select a thin slice.
6. Design the architecture.
7. Address failure, permissions, rollout and measurement.

## Interviewer follow-ups

Introduce these one at a time during practice:

- Nurses say the dashboard creates more work and ignore it.
- One hospital sends updates every minute; another sends a batch every hour.
- Patient identifiers cannot leave each hospital's security boundary.
- The model predicts crowding accurately, but managers cannot take any additional action.
- A source system replays six hours of duplicated events.
- Executives request a network-wide launch next Friday.

## Worked direction

### Frame

The requested dashboard is not yet a problem definition. Candidate users may include charge nurses, bed managers and regional operations leaders, but their available actions differ. A useful first question is:

> Which decision must become earlier or better when crowding risk increases?

Potential actions include calling additional staff, accelerating discharge coordination, redirecting non-critical arrivals where policy permits, or reallocating beds. If no feasible action exists, prediction alone will not create value.

### Model

Possible objects and events:

| Type | Examples |
|---|---|
| Entities | Facility, Department, Bed, CareTeam, Shift, PatientEncounter |
| Events | PatientArrived, TriageCompleted, BedRequested, BedAssigned, DischargeOrdered |
| Derived state | Current occupancy, queue length, estimated wait, staffing coverage |
| Provenance | Source system, event time, ingestion time, correction status |

PatientEncounter data requires strict access control and purpose limitation. A regional overview may use aggregated capacity data rather than exposing patient-level detail.

### Thin slice

Start with one facility, one charge-nurse workflow and a 60–90 minute forecast. Provide a capacity-risk explanation and a small set of approved actions. Keep a human decision-maker in control.

### Architecture direction

- Connect to admissions, bed-management and staffing sources.
- Validate, deduplicate and timestamp events.
- Maintain an operational state model distinct from raw history.
- Produce crowding-risk estimates with feature and version provenance.
- Present current state, forecast, confidence and action options.
- Record acknowledgements, actions and outcomes for evaluation.

### Failure reasoning

- Display freshness and suppress automation when inputs are stale.
- Make event processing idempotent.
- Reconcile corrected and out-of-order events.
- Degrade to current-state visibility if forecasting is unavailable.
- Preserve the existing clinical workflow as a fallback.
- Audit access and action history.

### Measurement

Model accuracy is necessary but insufficient. Evaluate lead time, alert precision, acknowledgement rate, action rate, staff workload, wait time and the frequency of unsafe or unnecessary interventions.

## Self-review questions

- Did I challenge the assumption that a dashboard or AI model is the solution?
- Did I connect every important data element to a decision or action?
- Did I distinguish event time from ingestion time?
- Did I define a safe fallback?
- Did I state what the MVP excludes?
