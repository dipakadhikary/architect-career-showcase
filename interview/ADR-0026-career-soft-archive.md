# ADR-0026: Soft Archive for Career Job Applications

Interview summary of [`ADR-0026`](../architecture/adr/ADR-0026-career-soft-archive.md).

## Decision

Do not physically delete job applications; soft-archive with `archived`/`archivedAt`, exclude from normal queries, and block mutations on archived apps.

## Benefits

- Application history remains recoverable.
- Dashboard/search operate on active applications by default.
- Related interviews/offers/history are not destroyed by delete.

## Limitations

- Pattern is career job-application specific, not a platform soft-delete framework.
- Archived rows still occupy storage and must be considered in reporting queries.

## Code References

- `JobApplication.archive()` / archived fields
- `V9__enhance_career_tracker.sql`
- `JobApplicationController` archive/archived endpoints
- `ApplicationArchivedException`
