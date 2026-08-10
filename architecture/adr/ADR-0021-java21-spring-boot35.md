# ADR-0021: Java 21 and Spring Boot 3.5 Platform Baseline

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

The platform needs a current LTS language level and a coherent Spring Boot generation for Security 6, Spring Data, and Actuator.

## Decision

Standardize on Java 21 and Spring Boot 3.5.x (parent `3.5.16`), enforced by the Maven Enforcer plugin (`[21,22)`).

## Consequences

- Access to modern Java language features and current Spring ecosystem APIs.
- Tooling and dependencies must remain compatible with Java 21.
- Upgrades are coordinated at the platform BOM/parent level.

## Code References

- `pom.xml` (`java.version`, Spring Boot parent, Enforcer rules)

## Related Modules

- Platform-wide
