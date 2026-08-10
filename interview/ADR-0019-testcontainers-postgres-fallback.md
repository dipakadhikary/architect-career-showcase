# ADR-0019: Testcontainers PostgreSQL with Local Fallback

Interview summary of [`ADR-0019`](../architecture/adr/ADR-0019-testcontainers-postgres-fallback.md).

## Decision

Use Testcontainers Postgres when Docker is available; otherwise fall back to env-configured local Postgres. Split unit (Surefire) and integration (Failsafe) tests.

## Benefits

- Tests exercise real Postgres/Flyway behavior.
- Developers without Docker can still run against local Postgres.
- Unit and integration costs are separated.

## Limitations

- CI/dev must provide Docker or a reachable Postgres.
- Local fallback can hide Docker-only environment differences if misconfigured.

## Code References

- `PostgresTestSupport`
- `AuthApiTestSupport`
- Feature `*IntegrationTest` / repository supports
- `pom.xml` Surefire/Failsafe config
