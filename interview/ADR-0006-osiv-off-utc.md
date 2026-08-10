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
