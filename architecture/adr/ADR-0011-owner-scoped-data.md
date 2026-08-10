# ADR-0011: Per-User Ownership Isolation

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

ACOS is a multi-user system. Users must only access their own career, knowledge, learning, and portfolio data.

## Decision

Persist `owner_id` on user-owned entities. Resolve the authenticated user via `@AuthenticationPrincipal AcosUserDetails` and `principal.getId()`. Enforce ownership in repositories (`findByIdAndOwnerId`, owner-scoped queries) and services (`requireOwned*` helpers).

## Consequences

- Application-level multi-tenancy by user.
- Controllers stay thin; ownership is enforced below the web layer.
- Does not provide database row-level security; omitted ownership filters can leak data.
- Cross-user admin access is not implemented as a general pattern.

## Code References

- `src/main/java/com/acos/auth/security/AcosUserDetails.java`
- Owner-scoped repositories and services in knowledge, learning, portfolio, and career
- Controllers passing `principal.getId()`

## Related Modules

- Auth (identity); Knowledge; Learning; Portfolio; Career
