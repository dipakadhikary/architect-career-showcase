# ADR-0010: Stateless Spring Security Filter Chain

Interview summary of [`ADR-0010`](../architecture/adr/ADR-0010-spring-security-filter-chain.md).

## Decision

Use CSRF-off, STATELESS sessions, JWT filter, and a small permit-all surface for auth/docs/health; authenticate everything else.

## Benefits

- Default-secure API surface.
- Swagger and health probes remain reachable without tokens.
- Auth failures use the same JSON envelope as business APIs.

## Limitations

- Authorization beyond authentication is mainly ownership checks in services.
- `@EnableMethodSecurity` is enabled but method annotations are not the primary authorization mechanism today.

## Code References

- `src/main/java/com/acos/auth/config/SecurityConfiguration.java`
- `JwtAuthenticationFilter`
- `JsonAuthenticationEntryPoint`
- `JsonAccessDeniedHandler`
