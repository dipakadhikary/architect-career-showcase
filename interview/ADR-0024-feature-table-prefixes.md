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
