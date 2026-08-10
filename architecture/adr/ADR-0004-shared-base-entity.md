# ADR-0004: Shared BaseEntity with UUID, Optimistic Locking, and Audit Timestamps

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Every persistent aggregate needs identity, concurrency control, and create/update timestamps. Duplicating these fields per entity risks inconsistent behavior.

## Decision

All JPA entities extend `com.acos.common.persistence.BaseEntity`, which provides UUID primary keys, `@Version` optimistic locking, and `@CreatedDate` / `@LastModifiedDate` timestamps via Spring Data JPA auditing.

## Consequences

- Uniform identity and concurrency model across domains.
- Clients can use `version` for optimistic concurrency where exposed.
- Soft-delete/archive remains feature-specific and is not part of `BaseEntity`.

## Code References

- `src/main/java/com/acos/common/persistence/BaseEntity.java`
- `src/main/java/com/acos/config/JpaAuditingConfiguration.java`
- Example entities: `User`, `JobApplication`, `KnowledgeNote`, `LearningPlan`, `PortfolioProject`

## Related Modules

- `common.persistence`; all feature `entity` packages; `config`
