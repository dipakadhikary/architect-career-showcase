# ADR-0009: Stateless JWT Access Tokens with Hashed Refresh Tokens

Interview summary of [`ADR-0009`](../architecture/adr/ADR-0009-jwt-refresh-auth.md).

## Decision

Issue short-lived JWTs for access; store refresh tokens as SHA-256 hashes and rotate them on refresh.

## Benefits

- API authentication is stateless per request.
- Refresh tokens are revocable in the database.
- Rotation limits reuse of stolen refresh tokens.

## Limitations

- Clients must implement refresh/retry on access-token expiry.
- Access JWTs remain valid until expiry even after logout unless additional denylist logic is added.

## Code References

- `JwtTokenProvider`
- `JwtAuthenticationFilter`
- `TokenServiceImpl`
- `RefreshToken` entity
- `V3__create_refresh_tokens.sql`
- `V4__alter_refresh_token_hash_to_varchar.sql`
