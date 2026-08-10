# ADR-0009: Stateless JWT Access Tokens with Hashed Refresh Tokens

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

The API must authenticate users without server-side session sticky state, while still allowing revocation and rotation for longer-lived refresh credentials.

## Decision

Issue short-lived JWT access tokens validated by `JwtAuthenticationFilter` / `JwtTokenProvider`. Persist refresh tokens as SHA-256 hashes (`RefreshToken`). Refresh rotates tokens by revoking the previous refresh token and issuing a new pair.

## Consequences

- Stateless request authentication for APIs.
- Refresh tokens can be revoked at the database.
- Stolen refresh tokens have limited reuse after rotation.
- Clients must handle access-token expiry and refresh flow.

## Code References

- `src/main/java/com/acos/auth/token/JwtTokenProvider.java`
- `src/main/java/com/acos/auth/security/JwtAuthenticationFilter.java`
- `src/main/java/com/acos/auth/token/TokenServiceImpl.java`
- `src/main/java/com/acos/auth/entity/RefreshToken.java`
- `src/main/resources/db/migration/V3__create_refresh_tokens.sql`
- `src/main/resources/db/migration/V4__alter_refresh_token_hash_to_varchar.sql`

## Related Modules

- Auth (`auth.token`, `auth.security`, `auth.entity`)
