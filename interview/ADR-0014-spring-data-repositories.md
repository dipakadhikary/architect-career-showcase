# ADR-0014: Spring Data Repositories as Persistence Boundary

Interview summary of [`ADR-0014`](../architecture/adr/ADR-0014-spring-data-repositories.md).

## Decision

Access persistence only through Spring Data repositories; no `EntityManager` in main source; controllers call services only.

## Benefits

- Persistence access is centralized and testable.
- Query methods stay near the domain.
- Supports both derived/`@Query` and Specifications where needed.

## Limitations

- Complex dynamic search outside career still uses ad-hoc query methods rather than a shared specification framework.
- Developers must remember ownership methods on every owned aggregate.

## Code References

- Feature `repository` packages
- `JobApplicationRepository` (`JpaSpecificationExecutor`)
- Repository tests under `src/test/java/com/acos/**/repository`
