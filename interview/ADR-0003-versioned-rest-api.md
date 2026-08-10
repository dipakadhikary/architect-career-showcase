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
