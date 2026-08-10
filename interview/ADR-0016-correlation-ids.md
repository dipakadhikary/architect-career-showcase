# ADR-0016: Request Correlation IDs in Logs and API Responses

Interview summary of [`ADR-0016`](../architecture/adr/ADR-0016-correlation-ids.md).

## Decision

Propagate/generate `X-Correlation-Id` via `CorrelationIdFilter` into MDC, logs, and `ApiResponse`.

## Benefits

- End-to-end request tracing across logs and API responses.
- Clients can report issues with a correlation id.

## Limitations

- Async/after-commit consumers are not automatically given the same id unless explicitly handled.
- Clients that ignore the header still get a generated id, but cross-system tracing stops at ACOS.

## Code References

- `CorrelationIdFilter`
- `ApiResponse`
- `application.yml` logging pattern with `%X{correlationId:-}`
