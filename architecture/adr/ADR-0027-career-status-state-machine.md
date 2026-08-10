# ADR-0027: Career Application Status State Machine and History

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Arbitrary status updates would make analytics and timeline views unreliable and allow illegal lifecycle jumps.

## Decision

Enforce allowed transitions through `ApplicationStateMachine` / `ApplicationStateValidator`. Persist every successful transition in `ApplicationStatusHistory`. Expose transition, history, and timeline APIs. Reject invalid transitions with `BusinessException` / `InvalidApplicationStatusTransitionException`.

## Consequences

- Application lifecycle is deterministic and auditable.
- Timeline visualization has a reliable source of truth.
- Status cannot be set freely via CRUD update payloads.
- Pattern is career-specific today.

## Code References

- `src/main/java/com/acos/career/state/ApplicationStateMachine.java`
- `src/main/java/com/acos/career/state/ApplicationStateValidator.java`
- `src/main/java/com/acos/career/entity/ApplicationStatusHistory.java`
- `com.acos.career.service.JobApplicationServiceImpl` (transition/history/timeline)
- `com.acos.career.controller.JobApplicationController` (`/status`, `/history`, `/timeline`)
- `V9__enhance_career_tracker.sql` (`career_application_status_history`)

## Related Modules

- Career (`state`, `entity`, `service`, `controller`)
