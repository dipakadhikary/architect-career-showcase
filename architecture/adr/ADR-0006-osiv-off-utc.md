# ADR-0006: Disable Open Session In View and Persist Timestamps in UTC

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Lazy loading outside transactional service boundaries hides N+1 problems and couples the web layer to persistence. Mixed timezones corrupt audit and scheduling data.

## Decision

Set `spring.jpa.open-in-view: false` and configure Hibernate JDBC timezone to UTC (`hibernate.jdbc.time_zone: UTC`).

## Consequences

- Associations must be loaded inside transactions (often via `@EntityGraph` or explicit fetches).
- Timestamps are stored and interpreted consistently in UTC.
- Accidental lazy loads fail loudly instead of silently opening sessions.

## Code References

- `src/main/resources/application.yml` (`spring.jpa.open-in-view`, `hibernate.jdbc.time_zone`)

## Related Modules

- Platform JPA configuration; all feature services/repositories
