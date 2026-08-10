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
