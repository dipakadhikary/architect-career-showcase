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
