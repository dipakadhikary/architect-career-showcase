# ADR-0005: PostgreSQL Schema `acos` Owned by Flyway; Hibernate Validate-Only

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Schema drift between environments is unacceptable. Hibernate auto-DDL is unsafe for a multi-feature evolving database.

## Decision

Use PostgreSQL schema `acos` as the application schema. Flyway migrations under `src/main/resources/db/migration/` are the source of truth for DDL. Hibernate runs with `ddl-auto: validate` only.

## Consequences

- Repeatable, reviewed schema changes (V1–V9).
- Startup fails fast on entity/schema mismatch.
- Developers must author Flyway scripts for every structural change.

## Code References

- `src/main/resources/db/migration/V1__initial_schema.sql` through `V9__enhance_career_tracker.sql`
- `src/main/resources/application.yml` (`spring.jpa.hibernate.ddl-auto: validate`, Flyway enabled)
- `src/main/resources/application-local.yml`
- `src/main/resources/application-test.yml`

## Related Modules

- Platform persistence; Auth; Knowledge; Learning; Portfolio; Career
