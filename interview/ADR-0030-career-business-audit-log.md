# ADR-0030: Career Business Audit Log for Important Actions

Interview summary of [`ADR-0030`](../architecture/adr/ADR-0030-career-business-audit-log.md).

## Decision

Record important career actions in `CareerAuditLog` via `CareerAuditService` (who/when/action/entity), using JPA rather than DB triggers.

## Benefits

- Business actions are queryable beyond technical row timestamps.
- Supports diagnostics and future compliance needs.
- Kept in application code next to the use cases that emit them.

## Limitations

- Career-only; not a platform-wide audit framework.
- Audit completeness depends on every service call site recording the action.

## Code References

- `CareerAuditLog`
- `CareerAuditAction`
- `CareerAuditService`
- `V9__enhance_career_tracker.sql` (`career_audit_logs`)
