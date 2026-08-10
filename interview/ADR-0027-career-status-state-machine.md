# ADR-0027: Career Application Status State Machine and History

Interview summary of [`ADR-0027`](../architecture/adr/ADR-0027-career-status-state-machine.md).

## Decision

Enforce allowed status transitions via `ApplicationStateMachine`/`ApplicationStateValidator`, persist history, and expose transition/history/timeline APIs.

## Benefits

- Lifecycle is deterministic and auditable.
- Timeline visualization has a reliable source of truth.
- Invalid jumps are rejected as business-rule violations.

## Limitations

- Status cannot be freely edited via CRUD update payloads.
- Pattern is career-specific today.
- Alternate terminal paths require timeline/history consumers to interpret carefully.

## Code References

- `ApplicationStateMachine`
- `ApplicationStateValidator`
- `ApplicationStatusHistory`
- `JobApplicationServiceImpl` transition/history/timeline
- `JobApplicationController` `/status`, `/history`, `/timeline`
