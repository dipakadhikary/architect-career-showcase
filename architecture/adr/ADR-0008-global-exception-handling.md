# ADR-0008: Typed ErrorCode Hierarchy with Global Exception Handling

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Ad-hoc HTTP errors and message formats make client handling and operations unreliable.

## Decision

Use `ErrorCode` for machine-readable codes mapped to HTTP statuses. Domain/business failures extend `BusinessException`. `GlobalExceptionHandler` translates business, validation, and infrastructure exceptions into `ApiResponse` failures. Security entry/denied handlers also emit the same envelope.

## Consequences

- Consistent error contract across features.
- Feature exceptions stay semantic while HTTP mapping stays centralized.
- New error categories require extending `ErrorCode` deliberately.

## Code References

- `src/main/java/com/acos/common/exception/ErrorCode.java`
- `src/main/java/com/acos/common/exception/BusinessException.java`
- `src/main/java/com/acos/common/handler/GlobalExceptionHandler.java`
- `src/main/java/com/acos/auth/security/JsonAuthenticationEntryPoint.java`
- `src/main/java/com/acos/auth/security/JsonAccessDeniedHandler.java`
- Feature exceptions under `com.acos.*.exception`

## Related Modules

- `common.exception`; `common.handler`; Auth security; all feature exception packages
