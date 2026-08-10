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
