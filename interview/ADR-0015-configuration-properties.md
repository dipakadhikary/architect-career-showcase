# ADR-0015: Typed Feature Configuration under `acos.*`

Interview summary of [`ADR-0015`](../architecture/adr/ADR-0015-configuration-properties.md).

## Decision

Bind feature settings with `@ConfigurationProperties` records under `acos.jwt`, `acos.dashboard`, `acos.knowledge`, `acos.learning`, `acos.portfolio`, `acos.career`.

## Benefits

- Type-safe, validated configuration.
- Limits/secrets are environment-tunable.
- Features avoid hardcoded magic numbers.

## Limitations

- Each feature must introduce and maintain its own properties type.
- Misconfigured values fail at startup/validation time and require ops awareness.

## Code References

- `src/main/resources/application.yml` (`acos:` block)
- `JwtProperties`, `KnowledgeProperties`, `LearningProperties`, `PortfolioProperties`, `CareerProperties`, `DashboardProperties`
