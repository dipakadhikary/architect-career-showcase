# ADR-0025: Local and Test Spring Profiles with Docker Compose Postgres

Interview summary of [`ADR-0025`](../architecture/adr/ADR-0025-local-test-profiles.md).

## Decision

Default profile `local`; provide `application-local.yml` / `application-test.yml`; supply Postgres/pgAdmin via Docker Compose for local development.

## Benefits

- Predictable local bootstrapping.
- Tests can override datasource/Flyway via dynamic properties.
- DB admin tooling is available locally via pgAdmin.

## Limitations

- Production/cloud profiles are not defined beyond local/test defaults in-repo.
- Developers still need Docker or an external Postgres.

## Code References

- `application.yml` (`spring.profiles.default: local`)
- `application-local.yml`
- `application-test.yml`
- `infrastructure/docker/docker-compose.yml`
