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
