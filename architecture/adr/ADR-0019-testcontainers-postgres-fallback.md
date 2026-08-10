# ADR-0019: Testcontainers PostgreSQL with Local Fallback

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Integration and repository tests must run against real PostgreSQL. Docker is not always available on developer machines.

## Decision

Use `PostgresTestSupport` to start `postgres:17.5-alpine` via Testcontainers when Docker is available; otherwise fall back to environment-configured local PostgreSQL (`ACOS_DB_*`). Split unit tests (Surefire) from integration tests (Failsafe includes `*IntegrationTest`).

## Consequences

- Tests exercise real Postgres/Flyway behavior.
- Developers without Docker can still run tests against local Postgres.
- CI/dev environments must provide either Docker or a reachable Postgres instance.

## Code References

- `src/test/java/com/acos/testsupport/PostgresTestSupport.java`
- `src/test/java/com/acos/testsupport/AuthApiTestSupport.java`
- Feature `*IntegrationTest` and `*RepositoryTestSupport` classes
- `pom.xml` (Surefire excludes / Failsafe includes)
- `src/main/resources/application-test.yml`

## Related Modules

- Test support; Auth; Knowledge; Learning; Portfolio; Career; Dashboard
