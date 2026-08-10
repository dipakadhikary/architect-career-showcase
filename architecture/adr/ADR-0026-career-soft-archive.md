# ADR-0026: Soft Archive for Career Job Applications

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Job applications are historical career records. Physical deletion would destroy audit/history value and break related interview/offer context.

## Decision

Do not physically delete job applications. Soft-archive them using `archived` / `archivedAt`. Normal list/search queries exclude archived records. Dedicated archived listing is supported. Mutations on archived applications are rejected.

## Consequences

- Application history remains recoverable.
- Dashboard and search operate on active applications by default.
- This soft-archive pattern is implemented for career job applications only; other features use hard deletes or status enums, not a shared soft-delete framework.

## Code References

- `src/main/java/com/acos/career/entity/JobApplication.java` (`archive()`, archived fields)
- `src/main/resources/db/migration/V9__enhance_career_tracker.sql`
- `com.acos.career.controller.JobApplicationController` (archive / archived endpoints)
- `com.acos.career.exception.ApplicationArchivedException`

## Related Modules

- Career
