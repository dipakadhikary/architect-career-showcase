# ADR-0008: Typed ErrorCode Hierarchy with Global Exception Handling

Interview summary of [`ADR-0008`](../architecture/adr/ADR-0008-global-exception-handling.md).

## Decision

Use `ErrorCode` + `BusinessException` subtypes; translate all failures in `GlobalExceptionHandler` (and security JSON handlers) into `ApiResponse` failures.

## Benefits

- Consistent machine-readable error contract.
- Controllers stay free of HTTP error mapping.
- Feature exceptions remain semantic (`*NotFoundException`, rule violations).

## Limitations

- New error categories require extending `ErrorCode` deliberately.
- Misclassified exceptions can produce the wrong HTTP status if the wrong code is chosen.

## Code References

- `src/main/java/com/acos/common/exception/ErrorCode.java`
- `src/main/java/com/acos/common/exception/BusinessException.java`
- `src/main/java/com/acos/common/handler/GlobalExceptionHandler.java`
- `JsonAuthenticationEntryPoint` / `JsonAccessDeniedHandler`
