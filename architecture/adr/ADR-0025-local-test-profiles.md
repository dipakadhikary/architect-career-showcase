# ADR-0025: Local and Test Spring Profiles with Docker Compose Postgres

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Developers need a default local runtime and a dedicated test profile without hardcoding machine-specific defaults into production config.

## Decision

Default the Spring profile to `local`. Provide `application-local.yml` and `application-test.yml`. Supply PostgreSQL (and pgAdmin) via `infrastructure/docker/docker-compose.yml` for local development.

## Consequences

- Local bootstrapping is predictable.
- Tests can override datasource/Flyway via dynamic properties.
- Production/cloud profiles are not defined in-repo beyond local/test defaults.

## Code References

- `src/main/resources/application.yml` (`spring.profiles.default: local`)
- `src/main/resources/application-local.yml`
- `src/main/resources/application-test.yml`
- `infrastructure/docker/docker-compose.yml`
- `infrastructure/README.md`

## Related Modules

- Platform configuration; infrastructure
