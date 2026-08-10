# ADR-0010: Stateless Spring Security Filter Chain

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

HTTP endpoints require a consistent authentication baseline with a small public surface for auth, docs, and health.

## Decision

Configure Spring Security 6 with CSRF disabled, `SessionCreationPolicy.STATELESS`, JWT filter before `UsernamePasswordAuthenticationFilter`, and permit-all for auth register/login/refresh, SpringDoc paths, and selected Actuator health/info endpoints; all other requests require authentication.

## Consequences

- Default-secure API surface.
- OpenAPI UI and health probes remain reachable without tokens.
- Authorization beyond authentication is primarily ownership checks in services (`@EnableMethodSecurity` is present; method annotations are not the primary authorization mechanism today).

## Code References

- `src/main/java/com/acos/auth/config/SecurityConfiguration.java`
- `src/main/java/com/acos/auth/security/JwtAuthenticationFilter.java`
- `src/main/java/com/acos/auth/security/JsonAuthenticationEntryPoint.java`
- `src/main/java/com/acos/auth/security/JsonAccessDeniedHandler.java`

## Related Modules

- Auth; all protected feature APIs; Actuator; SpringDoc
