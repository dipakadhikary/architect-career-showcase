# ACOS ADR Interview Guide

Interview-oriented summaries of every accepted Architecture Decision Record.

Each card contains **Decision**, **Benefits**, **Limitations**, and **Code References**.

Source ADRs: [`../architecture/adr`](../architecture/adr).

| ADR | Title |
| --- | --- |
| [ADR-0001](./ADR-0001-modular-monolith.md) | Single Deployable Modular Monolith |
| [ADR-0002](./ADR-0002-package-by-feature.md) | Package-by-Feature with Internal Layering |
| [ADR-0003](./ADR-0003-versioned-rest-api.md) | Versioned REST Base Path `/api/v1` |
| [ADR-0004](./ADR-0004-shared-base-entity.md) | Shared BaseEntity with UUID, Optimistic Locking, and Audit Timestamps |
| [ADR-0005](./ADR-0005-flyway-acos-schema.md) | PostgreSQL Schema `acos` Owned by Flyway; Hibernate Validate-Only |
| [ADR-0006](./ADR-0006-osiv-off-utc.md) | Disable Open Session In View and Persist Timestamps in UTC |
| [ADR-0007](./ADR-0007-api-response-envelope.md) | Uniform ApiResponse Envelope |
| [ADR-0008](./ADR-0008-global-exception-handling.md) | Typed ErrorCode Hierarchy with Global Exception Handling |
| [ADR-0009](./ADR-0009-jwt-refresh-auth.md) | Stateless JWT Access Tokens with Hashed Refresh Tokens |
| [ADR-0010](./ADR-0010-spring-security-filter-chain.md) | Stateless Spring Security Filter Chain |
| [ADR-0011](./ADR-0011-owner-scoped-data.md) | Per-User Ownership Isolation |
| [ADR-0012](./ADR-0012-dto-mapstruct-boundary.md) | DTO Records and MapStruct Mapping at the API Boundary |
| [ADR-0013](./ADR-0013-constructor-injection-services.md) | Constructor Injection, Service Interfaces, and Transactional Services |
| [ADR-0014](./ADR-0014-spring-data-repositories.md) | Spring Data Repositories as Persistence Boundary |
| [ADR-0015](./ADR-0015-configuration-properties.md) | Typed Feature Configuration under `acos.*` |
| [ADR-0016](./ADR-0016-correlation-ids.md) | Request Correlation IDs in Logs and API Responses |
| [ADR-0017](./ADR-0017-openapi-springdoc.md) | SpringDoc OpenAPI with Bearer JWT Security Scheme |
| [ADR-0018](./ADR-0018-actuator-exposure.md) | Selective Spring Boot Actuator Exposure |
| [ADR-0019](./ADR-0019-testcontainers-postgres-fallback.md) | Testcontainers PostgreSQL with Local Fallback |
| [ADR-0020](./ADR-0020-maven-quality-gates.md) | Enforceable Maven Static Analysis and Formatting Gates |
| [ADR-0021](./ADR-0021-java21-spring-boot35.md) | Java 21 and Spring Boot 3.5 Platform Baseline |
| [ADR-0022](./ADR-0022-layered-validation.md) | Bean Validation on DTOs plus Feature Domain Validators |
| [ADR-0023](./ADR-0023-bcrypt-password-hashing.md) | BCrypt Password Hashing with Timing-Safe Login Compare |
| [ADR-0024](./ADR-0024-feature-table-prefixes.md) | Feature-Prefixed Physical Table Names in Schema `acos` |
| [ADR-0025](./ADR-0025-local-test-profiles.md) | Local and Test Spring Profiles with Docker Compose Postgres |
| [ADR-0026](./ADR-0026-career-soft-archive.md) | Soft Archive for Career Job Applications |
| [ADR-0027](./ADR-0027-career-status-state-machine.md) | Career Application Status State Machine and History |
| [ADR-0028](./ADR-0028-career-after-commit-events.md) | Career After-Commit Domain Event Publishing |
| [ADR-0029](./ADR-0029-career-jpa-specifications.md) | JPA Specifications for Career Application Search |
| [ADR-0030](./ADR-0030-career-business-audit-log.md) | Career Business Audit Log for Important Actions |

## Combined file

- [All ADR interview cards](./adr-interview-cards.md)

## How to use in interviews

1. State the **Decision** in one sentence.
2. Give 2–3 **Benefits** tied to ACOS.
3. Volunteer 1–2 honest **Limitations**/trade-offs.
4. Point to concrete **Code References**.
