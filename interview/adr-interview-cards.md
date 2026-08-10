# ACOS ADR Interview Cards

One-page interview review of all implemented ADRs.

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

---

# ADR-0002: Package-by-Feature with Internal Layering

Interview summary of [`ADR-0002`](../architecture/adr/ADR-0002-package-by-feature.md).

## Decision

Organize code by feature/bounded context first; use technical layers (`controller`, `service`, `repository`, etc.) inside each feature. Put shared concerns in `common`/`config`.

## Benefits

- Feature code is cohesive and easy to locate.
- New features can be added without reshaping a global layer tree.
- Career-specific packages (`event`, `state`, `specification`) fit naturally.

## Limitations

- Shared utilities must be moved deliberately into `common`/`config` to avoid duplication.
- Cross-feature imports are still possible and rely on convention.

## Code References

- `src/main/java/com/acos/career/`
- `src/main/java/com/acos/auth/`
- `src/main/java/com/acos/knowledge/`
- `src/main/java/com/acos/common/`
- `src/main/java/com/acos/config/`

---

# ADR-0003: Versioned REST Base Path `/api/v1`

Interview summary of [`ADR-0003`](../architecture/adr/ADR-0003-versioned-rest-api.md).

## Decision

Expose all REST APIs under `/api/v1/...`.

## Benefits

- Clear public contract versioning.
- Future `/api/v2` can coexist.
- Undocumented or unversioned endpoints are easy to spot.

## Limitations

- Every controller must keep the prefix consistently.
- Breaking changes still require a migration plan for clients.

## Code References

- `AuthController` (`/api/v1/auth`)
- `JobApplicationController` (`/api/v1/career/applications`)
- Knowledge, learning, portfolio, dashboard controllers

---

# ADR-0004: Shared BaseEntity with UUID, Optimistic Locking, and Audit Timestamps

Interview summary of [`ADR-0004`](../architecture/adr/ADR-0004-shared-base-entity.md).

## Decision

All JPA entities extend `BaseEntity` providing UUID PKs, `@Version`, and audited `createdAt`/`updatedAt`.

## Benefits

- Uniform identity and concurrency model across domains.
- Technical audit timestamps are automatic via JPA auditing.
- Clients can use `version` where exposed for optimistic concurrency.

## Limitations

- Entities cannot choose alternate PK strategies without breaking the shared contract.
- Soft-delete/archive is not part of `BaseEntity` and remains feature-specific.

## Code References

- `src/main/java/com/acos/common/persistence/BaseEntity.java`
- `src/main/java/com/acos/config/JpaAuditingConfiguration.java`
- Feature entities such as `User`, `JobApplication`, `KnowledgeNote`

---

# ADR-0005: PostgreSQL Schema `acos` Owned by Flyway; Hibernate Validate-Only

Interview summary of [`ADR-0005`](../architecture/adr/ADR-0005-flyway-acos-schema.md).

## Decision

Use schema `acos`, manage DDL with Flyway migrations, and set Hibernate `ddl-auto=validate`.

## Benefits

- Schema changes are reviewed, versioned, and repeatable.
- Startup fails fast on entity/schema mismatch.
- Environments stay aligned through migration history.

## Limitations

- Every structural change requires a new Flyway script.
- Editing already-applied migrations causes checksum failures.

## Code References

- `src/main/resources/db/migration/V1__initial_schema.sql` through `V9__enhance_career_tracker.sql`
- `src/main/resources/application.yml`
- `application-local.yml` / `application-test.yml`

---

# ADR-0006: Disable Open Session In View and Persist Timestamps in UTC

Interview summary of [`ADR-0006`](../architecture/adr/ADR-0006-osiv-off-utc.md).

## Decision

Set `spring.jpa.open-in-view=false` and Hibernate JDBC timezone to UTC.

## Benefits

- Lazy loads cannot silently open sessions in the web layer.
- N+1 and missing-fetch issues surface early.
- Timestamps are consistent in UTC.

## Limitations

- Associations must be fetched inside transactions (`@EntityGraph` / explicit queries).
- Controllers cannot rely on lazy initialization during rendering.

## Code References

- `src/main/resources/application.yml` (`open-in-view`, `hibernate.jdbc.time_zone`)
- Repository `@EntityGraph` usages in feature repositories

---

# ADR-0007: Uniform ApiResponse Envelope

Interview summary of [`ADR-0007`](../architecture/adr/ADR-0007-api-response-envelope.md).

## Decision

All REST endpoints return `ApiResponse<T>` with `success`, `data`, `error`, `correlationId`, and `timestamp`.

## Benefits

- Predictable client parsing across features.
- Correlation id is available on every response when MDC is populated.
- OpenAPI can document one envelope shape.

## Limitations

- Adds nesting versus raw payload responses.
- Controllers must not return bare domain objects.

## Code References

- `src/main/java/com/acos/common/api/ApiResponse.java`
- `src/main/java/com/acos/common/api/ApiError.java`
- Feature controllers returning `ResponseEntity<ApiResponse<...>>`

---

# ADR-0008: Typed ErrorCode Hierarchy with Global Exception Handling

Interview summary of [`ADR-0008`](../architecture/adr/ADR-0008-global-exception-handling.md).

## Decision

Use `ErrorCode` + `BusinessException` subtypes; translate all failures in `GlobalExceptionHandler` (and security JSON handlers) into `ApiResponse` failures.

## Benefits

- Consistent machine-readable error contract.
- Controllers stay free of HTTP error mapping.
- Feature exceptions remain semantic (`*NotFoundException`, rule violations).

## Limitations

- New error categories require extending `ErrorCode` deliberately.
- Misclassified exceptions can produce the wrong HTTP status if the wrong code is chosen.

## Code References

- `src/main/java/com/acos/common/exception/ErrorCode.java`
- `src/main/java/com/acos/common/exception/BusinessException.java`
- `src/main/java/com/acos/common/handler/GlobalExceptionHandler.java`
- `JsonAuthenticationEntryPoint` / `JsonAccessDeniedHandler`

---

# ADR-0009: Stateless JWT Access Tokens with Hashed Refresh Tokens

Interview summary of [`ADR-0009`](../architecture/adr/ADR-0009-jwt-refresh-auth.md).

## Decision

Issue short-lived JWTs for access; store refresh tokens as SHA-256 hashes and rotate them on refresh.

## Benefits

- API authentication is stateless per request.
- Refresh tokens are revocable in the database.
- Rotation limits reuse of stolen refresh tokens.

## Limitations

- Clients must implement refresh/retry on access-token expiry.
- Access JWTs remain valid until expiry even after logout unless additional denylist logic is added.

## Code References

- `JwtTokenProvider`
- `JwtAuthenticationFilter`
- `TokenServiceImpl`
- `RefreshToken` entity
- `V3__create_refresh_tokens.sql`
- `V4__alter_refresh_token_hash_to_varchar.sql`

---

# ADR-0010: Stateless Spring Security Filter Chain

Interview summary of [`ADR-0010`](../architecture/adr/ADR-0010-spring-security-filter-chain.md).

## Decision

Use CSRF-off, STATELESS sessions, JWT filter, and a small permit-all surface for auth/docs/health; authenticate everything else.

## Benefits

- Default-secure API surface.
- Swagger and health probes remain reachable without tokens.
- Auth failures use the same JSON envelope as business APIs.

## Limitations

- Authorization beyond authentication is mainly ownership checks in services.
- `@EnableMethodSecurity` is enabled but method annotations are not the primary authorization mechanism today.

## Code References

- `src/main/java/com/acos/auth/config/SecurityConfiguration.java`
- `JwtAuthenticationFilter`
- `JsonAuthenticationEntryPoint`
- `JsonAccessDeniedHandler`

---

# ADR-0011: Per-User Ownership Isolation

Interview summary of [`ADR-0011`](../architecture/adr/ADR-0011-owner-scoped-data.md).

## Decision

Persist `owner_id`, take owner from `AcosUserDetails.getId()`, and enforce access with owner-scoped repository/service checks.

## Benefits

- Application-level multi-tenancy by user.
- Controllers stay thin while ownership is enforced below the web layer.
- Cross-user reads/writes fail closed via not-found/business exceptions.

## Limitations

- Not database RLS; omitted ownership filters can leak data.
- Cross-user admin access is not implemented as a general pattern.

## Code References

- `AcosUserDetails`
- Owner-scoped repositories/services in knowledge, learning, portfolio, career
- Controllers passing `principal.getId()`

---

# ADR-0012: DTO Records and MapStruct Mapping at the API Boundary

Interview summary of [`ADR-0012`](../architecture/adr/ADR-0012-dto-mapstruct-boundary.md).

## Decision

Use Java records for request/response DTOs and MapStruct mappers (`componentModel=spring`, `unmappedTargetPolicy=ERROR`). Do not return entities from controllers.

## Benefits

- Clear API/persistence separation.
- Unmapped fields fail at compile time.
- Entities stay free of API serialization concerns.

## Limitations

- Mapping code must be updated when entities/DTOs evolve.
- Lombok is on the processor path but unused in application source, which can surprise contributors.

## Code References

- `pom.xml` MapStruct compiler args
- `UserMapper`, `CareerMapper`, `KnowledgeNoteMapper`, `LearningMapper`, `PortfolioMapper`
- Feature `dto` packages

---

# ADR-0013: Constructor Injection, Service Interfaces, and Transactional Services

Interview summary of [`ADR-0013`](../architecture/adr/ADR-0013-constructor-injection-services.md).

## Decision

Inject dependencies via constructors; controllers depend on service interfaces; put `@Transactional` on service implementations.

## Benefits

- Dependencies are explicit and easy to mock.
- Unit of work lives in the application service layer.
- Controllers remain thin HTTP adapters.

## Limitations

- Interface + `*Impl` pairs increase type count.
- Incorrect transaction boundaries still possible if work leaks outside services.

## Code References

- Feature controllers with constructor injection
- `AuthService` / `AuthServiceImpl`
- `JobApplicationService` / `JobApplicationServiceImpl`

---

# ADR-0014: Spring Data Repositories as Persistence Boundary

Interview summary of [`ADR-0014`](../architecture/adr/ADR-0014-spring-data-repositories.md).

## Decision

Access persistence only through Spring Data repositories; no `EntityManager` in main source; controllers call services only.

## Benefits

- Persistence access is centralized and testable.
- Query methods stay near the domain.
- Supports both derived/`@Query` and Specifications where needed.

## Limitations

- Complex dynamic search outside career still uses ad-hoc query methods rather than a shared specification framework.
- Developers must remember ownership methods on every owned aggregate.

## Code References

- Feature `repository` packages
- `JobApplicationRepository` (`JpaSpecificationExecutor`)
- Repository tests under `src/test/java/com/acos/**/repository`

---

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

---

# ADR-0016: Request Correlation IDs in Logs and API Responses

Interview summary of [`ADR-0016`](../architecture/adr/ADR-0016-correlation-ids.md).

## Decision

Propagate/generate `X-Correlation-Id` via `CorrelationIdFilter` into MDC, logs, and `ApiResponse`.

## Benefits

- End-to-end request tracing across logs and API responses.
- Clients can report issues with a correlation id.

## Limitations

- Async/after-commit consumers are not automatically given the same id unless explicitly handled.
- Clients that ignore the header still get a generated id, but cross-system tracing stops at ACOS.

## Code References

- `CorrelationIdFilter`
- `ApiResponse`
- `application.yml` logging pattern with `%X{correlationId:-}`

---

# ADR-0017: SpringDoc OpenAPI with Bearer JWT Security Scheme

Interview summary of [`ADR-0017`](../architecture/adr/ADR-0017-openapi-springdoc.md).

## Decision

Document APIs with SpringDoc, controller annotations, and a global `bearer-jwt` security scheme.

## Benefits

- Living API docs co-located with controllers.
- Security requirements are visible in Swagger UI.
- Public docs paths are available for developers.

## Limitations

- Docs drift if annotations are not updated with contract changes.
- Actuator is intentionally hidden from Swagger (`show-actuator: false`).

## Code References

- `OpenApiConfiguration`
- `application.yml` `springdoc` section
- Annotated feature controllers

---

# ADR-0018: Selective Spring Boot Actuator Exposure

Interview summary of [`ADR-0018`](../architecture/adr/ADR-0018-actuator-exposure.md).

## Decision

Expose `health`, `info`, `metrics`, and `prometheus`; permit anonymous access only to health/info.

## Benefits

- Standard ops endpoints for monitoring.
- Prometheus scraping is supported at Actuator level.
- Broader Actuator surface remains closed by default config.

## Limitations

- Metrics/prometheus still depend on deployment-time network controls outside the app.
- No full observability stack (Grafana/Jaeger) is packaged in-repo.

## Code References

- `pom.xml` (`spring-boot-starter-actuator`)
- `application.yml` `management` block
- `SecurityConfiguration` health/info permit

---

# ADR-0019: Testcontainers PostgreSQL with Local Fallback

Interview summary of [`ADR-0019`](../architecture/adr/ADR-0019-testcontainers-postgres-fallback.md).

## Decision

Use Testcontainers Postgres when Docker is available; otherwise fall back to env-configured local Postgres. Split unit (Surefire) and integration (Failsafe) tests.

## Benefits

- Tests exercise real Postgres/Flyway behavior.
- Developers without Docker can still run against local Postgres.
- Unit and integration costs are separated.

## Limitations

- CI/dev must provide Docker or a reachable Postgres.
- Local fallback can hide Docker-only environment differences if misconfigured.

## Code References

- `PostgresTestSupport`
- `AuthApiTestSupport`
- Feature `*IntegrationTest` / repository supports
- `pom.xml` Surefire/Failsafe config

---

# ADR-0020: Enforceable Maven Static Analysis and Formatting Gates

Interview summary of [`ADR-0020`](../architecture/adr/ADR-0020-maven-quality-gates.md).

## Decision

Fail the build on Spotless, Checkstyle, PMD(+CPD), SpotBugs, and Enforcer violations; keep JaCoCo scaffolding.

## Benefits

- Formatting and common defect classes are build blockers.
- Contributors share one quality baseline.
- Java/Maven policy is enforced centrally.

## Limitations

- Some PMD design-smell rules are excluded where they conflict with established patterns.
- JaCoCo minimum coverage is currently `0.00`, so coverage is not yet a real gate.

## Code References

- `pom.xml` quality plugins
- `config/checkstyle/checkstyle.xml`
- `config/pmd/pmd-ruleset.xml`
- `config/spotbugs/spotbugs-exclude.xml`

---

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

---

# ADR-0022: Bean Validation on DTOs plus Feature Domain Validators

Interview summary of [`ADR-0022`](../architecture/adr/ADR-0022-layered-validation.md).

## Decision

Use Jakarta Validation on DTO records at the controller boundary, plus feature validators for business/limit rules backed by `acos.*` properties.

## Benefits

- Structural vs business validation are separated.
- Shared limits come from configuration.
- Failures map through the global handler into `ApiResponse` errors.

## Limitations

- Developers must remember both annotation validation and feature validator calls.
- Duplicate concepts can appear if DTO constraints and validators overlap poorly.

## Code References

- Feature DTO validation annotations
- `CareerValidator`, `KnowledgeNoteValidator`, `PortfolioValidator`, `PasswordValidator`
- Controllers using `@Valid`

---

# ADR-0023: BCrypt Password Hashing with Timing-Safe Login Compare

Interview summary of [`ADR-0023`](../architecture/adr/ADR-0023-bcrypt-password-hashing.md).

## Decision

Hash passwords with BCrypt and always run password matching on login, using a dummy hash when the user is absent.

## Benefits

- Industry-standard password hashing.
- Reduced user-enumeration timing signal on login.

## Limitations

- BCrypt CPU cost must be sized for login throughput.
- Password policy is separate and must stay aligned with validator rules.

## Code References

- `PasswordEncoderConfiguration`
- `AuthServiceImpl` (`DUMMY_PASSWORD_HASH`)

---

# ADR-0024: Feature-Prefixed Physical Table Names in Schema `acos`

Interview summary of [`ADR-0024`](../architecture/adr/ADR-0024-feature-table-prefixes.md).

## Decision

Use feature-oriented table prefixes (`career_*`, `portfolio_*`, `learning_*`, `knowledge_*` note tables) while auth core tables remain unprefixed as implemented.

## Benefits

- Domain tables are easy to identify in one shared schema.
- Reduces accidental name collisions across features.

## Limitations

- Naming is not perfectly uniform (auth and some knowledge lookup tables are unprefixed).
- Contributors must follow the closest existing convention rather than one absolute rule.

## Code References

- Flyway migrations `V2`–`V9`
- Entity `@Table(name=..., schema="acos")` declarations

---

# ADR-0025: Local and Test Spring Profiles with Docker Compose Postgres

Interview summary of [`ADR-0025`](../architecture/adr/ADR-0025-local-test-profiles.md).

## Decision

Default profile `local`; provide `application-local.yml` / `application-test.yml`; supply Postgres/pgAdmin via Docker Compose for local development.

## Benefits

- Predictable local bootstrapping.
- Tests can override datasource/Flyway via dynamic properties.
- DB admin tooling is available locally via pgAdmin.

## Limitations

- Production/cloud profiles are not defined beyond local/test defaults in-repo.
- Developers still need Docker or an external Postgres.

## Code References

- `application.yml` (`spring.profiles.default: local`)
- `application-local.yml`
- `application-test.yml`
- `infrastructure/docker/docker-compose.yml`

---

# ADR-0026: Soft Archive for Career Job Applications

Interview summary of [`ADR-0026`](../architecture/adr/ADR-0026-career-soft-archive.md).

## Decision

Do not physically delete job applications; soft-archive with `archived`/`archivedAt`, exclude from normal queries, and block mutations on archived apps.

## Benefits

- Application history remains recoverable.
- Dashboard/search operate on active applications by default.
- Related interviews/offers/history are not destroyed by delete.

## Limitations

- Pattern is career job-application specific, not a platform soft-delete framework.
- Archived rows still occupy storage and must be considered in reporting queries.

## Code References

- `JobApplication.archive()` / archived fields
- `V9__enhance_career_tracker.sql`
- `JobApplicationController` archive/archived endpoints
- `ApplicationArchivedException`

---

# ADR-0027: Career Application Status State Machine and History

Interview summary of [`ADR-0027`](../architecture/adr/ADR-0027-career-status-state-machine.md).

## Decision

Enforce allowed status transitions via `ApplicationStateMachine`/`ApplicationStateValidator`, persist history, and expose transition/history/timeline APIs.

## Benefits

- Lifecycle is deterministic and auditable.
- Timeline visualization has a reliable source of truth.
- Invalid jumps are rejected as business-rule violations.

## Limitations

- Status cannot be freely edited via CRUD update payloads.
- Pattern is career-specific today.
- Alternate terminal paths require timeline/history consumers to interpret carefully.

## Code References

- `ApplicationStateMachine`
- `ApplicationStateValidator`
- `ApplicationStatusHistory`
- `JobApplicationServiceImpl` transition/history/timeline
- `JobApplicationController` `/status`, `/history`, `/timeline`

---

# ADR-0028: Career After-Commit Domain Event Publishing

Interview summary of [`ADR-0028`](../architecture/adr/ADR-0028-career-after-commit-events.md).

## Decision

Publish career domain events through `CareerDomainEventPublisher` only after successful transaction commit (or immediately if no transaction). No listeners are implemented yet.

## Benefits

- Future modules can subscribe without changing publishers.
- Listeners will not observe rolled-back state.
- Transactional services stay decoupled from side effects.

## Limitations

- Publish-only today; no in-process consumers exist.
- Pattern is implemented in career only.
- Downstream reliability (retries/outbox) is not implemented.

## Code References

- `CareerDomainEventPublisher`
- `CareerDomainEvent` and career event records
- Publication call sites in career services

---

# ADR-0029: JPA Specifications for Career Application Search

Interview summary of [`ADR-0029`](../architecture/adr/ADR-0029-career-jpa-specifications.md).

## Decision

Compose dynamic job-application filters with `JobApplicationSpecifications` and `JpaSpecificationExecutor` instead of combinatorial repository method names.

## Benefits

- Dynamic multi-filter search without repository method explosion.
- Specs are reusable/composable in services and tests.

## Limitations

- Not platform-wide; other features still use derived/`@Query` search.
- Complex joins (for example interview round filters) must be written carefully to avoid duplicates.

## Code References

- `JobApplicationSpecifications`
- `JobApplicationRepository`
- `JobApplicationServiceImpl#search`
- `JobApplicationController` search endpoint

---

# ADR-0030: Career Business Audit Log for Important Actions

Interview summary of [`ADR-0030`](../architecture/adr/ADR-0030-career-business-audit-log.md).

## Decision

Record important career actions in `CareerAuditLog` via `CareerAuditService` (who/when/action/entity), using JPA rather than DB triggers.

## Benefits

- Business actions are queryable beyond technical row timestamps.
- Supports diagnostics and future compliance needs.
- Kept in application code next to the use cases that emit them.

## Limitations

- Career-only; not a platform-wide audit framework.
- Audit completeness depends on every service call site recording the action.

## Code References

- `CareerAuditLog`
- `CareerAuditAction`
- `CareerAuditService`
- `V9__enhance_career_tracker.sql` (`career_audit_logs`)

---
