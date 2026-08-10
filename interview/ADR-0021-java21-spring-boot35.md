# ADR-0021: Java 21 and Spring Boot 3.5 Platform Baseline

Interview summary of [`ADR-0021`](../architecture/adr/ADR-0021-java21-spring-boot35.md).

## Decision

Standardize on Java 21 and Spring Boot 3.5.x, enforced by Maven Enforcer (`[21,22)`).

## Benefits

- Modern language features and current Spring Security/Data APIs.
- Aligned dependency management via Boot parent BOM.

## Limitations

- Tooling and libraries must remain Java 21 compatible.
- Upgrades are coordinated at the platform parent level.

## Code References

- `pom.xml` (`java.version`, Spring Boot parent, Enforcer rules)
