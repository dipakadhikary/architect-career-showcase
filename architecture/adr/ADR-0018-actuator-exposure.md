# ADR-0018: Selective Spring Boot Actuator Exposure

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Operations need health and metrics without exposing the full Actuator surface publicly.

## Decision

Include Actuator and expose `health`, `info`, `metrics`, and `prometheus` under `/actuator`. Enable health probes. Permit unauthenticated access only to health/info in the security filter chain.

## Consequences

- Standard ops endpoints available for monitoring.
- Prometheus scraping is supported at the Actuator level.
- Broader Actuator endpoints remain unexposed by default configuration.

## Code References

- `pom.xml` (`spring-boot-starter-actuator`)
- `src/main/resources/application.yml` (`management:` block)
- `src/main/java/com/acos/auth/config/SecurityConfiguration.java` (health/info permit)

## Related Modules

- Platform operations; Auth security
