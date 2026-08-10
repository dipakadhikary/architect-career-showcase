# ADR-0030: Career Business Audit Log for Important Actions

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

JPA `created_at`/`updated_at` alone do not capture who performed which business action on which entity.

## Decision

Record important career actions in `CareerAuditLog` via `CareerAuditService` (actor, owner, action, entity type/id, details, occurred-at). Persist through JPA—not database triggers.

## Consequences

- Business actions are queryable for diagnostics and future compliance needs.
- Distinct from technical row auditing on `BaseEntity`.
- Implemented for career actions only; not a platform-wide audit framework.

## Code References

- `src/main/java/com/acos/career/entity/CareerAuditLog.java`
- `src/main/java/com/acos/career/entity/CareerAuditAction.java`
- `src/main/java/com/acos/career/service/CareerAuditService.java`
- `src/main/resources/db/migration/V9__enhance_career_tracker.sql` (`career_audit_logs`)

## Related Modules

- Career
