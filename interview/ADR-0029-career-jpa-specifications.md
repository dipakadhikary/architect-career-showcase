# ADR-0029: JPA Specifications for Career Application Search

Interview summary of [`ADR-0029`](../architecture/adr/ADR-0029-career-jpa-specifications.md).

## Decision

Compose dynamic job-application filters with `JobApplicationSpecifications` and `JpaSpecificationExecutor` instead of combinatorial repository method names.

## Benefits

- Dynamic multi-filter search without repository method explosion.
- Specs are reusable/composable in services and tests.

## Limitations

- Not platform-wide; other features still use derived/`@Query` search.
- Complex joins (for example interview round filters) must be written carefully to avoid duplicates.

## Code References

- `JobApplicationSpecifications`
- `JobApplicationRepository`
- `JobApplicationServiceImpl#search`
- `JobApplicationController` search endpoint
