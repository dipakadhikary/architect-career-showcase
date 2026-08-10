# ADR-0015: Typed Feature Configuration under `acos.*`

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Feature limits and secrets must be externalized without scattering magic numbers and stringly-typed config lookups.

## Decision

Bind feature settings with `@ConfigurationProperties` records under the `acos` prefix (`acos.jwt`, `acos.dashboard`, `acos.knowledge`, `acos.learning`, `acos.portfolio`, `acos.career`), enabled via feature `@Configuration` classes.

## Consequences

- Type-safe, validated configuration.
- Feature limits are tunable per environment.
- New features should introduce their own `acos.<feature>` properties rather than hardcoding.

## Code References

- `src/main/resources/application.yml` (`acos:` block)
- `com.acos.auth.config.JwtProperties`
- `com.acos.dashboard.config.DashboardProperties`
- `com.acos.knowledge.config.KnowledgeProperties`
- `com.acos.learning.config.LearningProperties`
- `com.acos.portfolio.config.PortfolioProperties`
- `com.acos.career.config.CareerProperties`

## Related Modules

- Auth; Dashboard; Knowledge; Learning; Portfolio; Career
