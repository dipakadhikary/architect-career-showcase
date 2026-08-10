# ADR-0001: Single Deployable Modular Monolith

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

ACOS needs multiple bounded contexts (auth, knowledge, learning, portfolio, career, dashboard) delivered as one product. Splitting into Maven multi-module or microservices would add distribution complexity before the domain is stable.

## Decision

Ship ACOS as a single Maven module and single Spring Boot deployable JAR (`architect-career-operating-system`), with feature packages under `com.acos.*` inside one process.

## Consequences

- One artifact to build, test, and deploy.
- Cross-feature refactors stay local to one repository.
- Independent scaling of features is not available without later extraction.
- Feature isolation is package-level, not process-level.

## Code References

- `pom.xml` (single `jar` packaging; no `<modules>`)
- `src/main/java/com/acos/AcosApplication.java`

## Related Modules

- Platform-wide (`auth`, `knowledge`, `learning`, `portfolio`, `career`, `dashboard`, `common`, `config`)
