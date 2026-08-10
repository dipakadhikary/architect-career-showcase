# ADR-0001: Single Deployable Modular Monolith

Interview summary of [`ADR-0001`](../architecture/adr/ADR-0001-modular-monolith.md).

## Decision

Ship ACOS as one Maven module and one Spring Boot JAR, with feature packages under `com.acos.*` in a single process.

## Benefits

- One artifact to build, test, and deploy.
- Cross-feature refactors stay in one repository.
- Lower operational complexity than early microservices.

## Limitations

- Features cannot scale or deploy independently without later extraction.
- Isolation is package-level, not process-level.
- A defect in one feature can affect the whole process.

## Code References

- `pom.xml` (single `jar` packaging; no `<modules>`)
- `src/main/java/com/acos/AcosApplication.java`
