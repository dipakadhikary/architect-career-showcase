# ADR-0029: JPA Specifications for Career Application Search

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Job application search requires dynamic combinations of company, recruiter, status, interview round, date range, salary range, and keyword filters. Combinatorial repository method names do not scale.

## Decision

Implement composable `JobApplicationSpecifications` and execute them through `JobApplicationRepository` extending `JpaSpecificationExecutor`. Expose search via `/api/v1/career/applications/search`.

## Consequences

- Dynamic filtering without repository method explosion.
- Specs can be reused/combined in tests and services.
- Other features still use derived queries/`@Query` (for example knowledge search); Specifications are not platform-wide yet.

## Code References

- `src/main/java/com/acos/career/specification/JobApplicationSpecifications.java`
- `src/main/java/com/acos/career/repository/JobApplicationRepository.java`
- `com.acos.career.service.JobApplicationServiceImpl#search`
- `com.acos.career.controller.JobApplicationController` search endpoint

## Related Modules

- Career
