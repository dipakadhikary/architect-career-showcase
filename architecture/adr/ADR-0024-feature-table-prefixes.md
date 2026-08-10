# ADR-0024: Feature-Prefixed Physical Table Names in Schema `acos`

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Multiple domains share one PostgreSQL schema and need clear physical naming to avoid collisions and aid operations.

## Decision

Name domain tables with feature-oriented prefixes where applied: `career_*`, `portfolio_*`, `learning_*`, and `knowledge_*` note tables. Auth core tables (`users`, `roles`, `user_roles`, `refresh_tokens`) and some knowledge lookup tables (`categories`, `tags`) use unprefixed names as implemented in Flyway.

## Consequences

- Career/portfolio/learning tables are easy to identify in the shared schema.
- Naming is not perfectly uniform across all domains; auth/knowledge lookup tables remain less prefixed.
- New tables should follow the closest existing domain convention.

## Code References

- Flyway migrations `V2`–`V9`
- Entity `@Table(name = "...", schema = "acos")` declarations

## Related Modules

- Auth; Knowledge; Learning; Portfolio; Career
