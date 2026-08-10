# ADR-0007: Uniform ApiResponse Envelope

Interview summary of [`ADR-0007`](../architecture/adr/ADR-0007-api-response-envelope.md).

## Decision

All REST endpoints return `ApiResponse<T>` with `success`, `data`, `error`, `correlationId`, and `timestamp`.

## Benefits

- Predictable client parsing across features.
- Correlation id is available on every response when MDC is populated.
- OpenAPI can document one envelope shape.

## Limitations

- Adds nesting versus raw payload responses.
- Controllers must not return bare domain objects.

## Code References

- `src/main/java/com/acos/common/api/ApiResponse.java`
- `src/main/java/com/acos/common/api/ApiError.java`
- Feature controllers returning `ResponseEntity<ApiResponse<...>>`
