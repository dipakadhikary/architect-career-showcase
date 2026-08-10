# ADR-0012: DTO Records and MapStruct Mapping at the API Boundary

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Exposing JPA entities directly couples clients to persistence and invites lazy-loading and over-exposure problems.

## Decision

Use Java records for request/response DTOs. Map entities to DTOs with MapStruct mappers (`componentModel = spring`, `unmappedTargetPolicy = ERROR`). Controllers return DTOs inside `ApiResponse`. Lombok is on the classpath for annotation processing compatibility but is not used in application source.

## Consequences

- Clear API/persistence separation.
- Unmapped fields fail at compile time.
- Mapping code must be maintained when entities/DTOs evolve.
- Entities remain free of API serialization concerns.

## Code References

- `pom.xml` (MapStruct compiler args)
- `com.acos.auth.mapper.UserMapper`
- `com.acos.career.mapper.CareerMapper`
- `com.acos.knowledge.mapper.KnowledgeNoteMapper`
- `com.acos.learning.mapper.LearningMapper`
- `com.acos.portfolio.mapper.PortfolioMapper`
- Feature `dto` packages

## Related Modules

- Auth; Knowledge; Learning; Portfolio; Career; Dashboard
