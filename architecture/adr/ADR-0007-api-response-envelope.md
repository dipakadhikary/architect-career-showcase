# ADR-0007: Uniform ApiResponse Envelope

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Clients and API docs need a single success/failure shape across all features, including correlation metadata.

## Decision

All REST endpoints return `ApiResponse<T>` with fields `success`, `data`, `error`, `correlationId`, and `timestamp`. Success uses `ApiResponse.success(data)`; failures use `ApiResponse.failure(ApiError)`.

## Consequences

- Predictable client parsing and OpenAPI documentation.
- Correlation id is available on every response when MDC is populated.
- Controllers must not return bare domain entities.

## Code References

- `src/main/java/com/acos/common/api/ApiResponse.java`
- `src/main/java/com/acos/common/api/ApiError.java`
- Feature controllers under `com.acos.*.controller` and `com.acos.dashboard.web`

## Related Modules

- `common.api`; all REST-facing modules
