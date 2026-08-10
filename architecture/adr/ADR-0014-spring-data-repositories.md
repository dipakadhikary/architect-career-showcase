# ADR-0014: Spring Data Repositories as Persistence Boundary

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Direct `EntityManager` usage in web or ad-hoc SQL in controllers would leak persistence concerns upward.

## Decision

Access persistence only through Spring Data JPA repository interfaces (`JpaRepository`, and where needed `JpaSpecificationExecutor`). Controllers call services; services call repositories.

## Consequences

- Persistence access is centralized and testable.
- Query methods and custom `@Query`/`@EntityGraph` stay near the domain.
- Complex dynamic search uses Specifications in career; other features use derived/`@Query` methods.

## Code References

- Feature `repository` packages
- `com.acos.career.repository.JobApplicationRepository` (`JpaSpecificationExecutor`)
- Repository slice tests under `src/test/java/com/acos/**/repository`

## Related Modules

- Auth; Knowledge; Learning; Portfolio; Career
