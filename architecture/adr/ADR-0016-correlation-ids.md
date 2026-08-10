# ADR-0016: Request Correlation IDs in Logs and API Responses

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Operators and clients need to correlate a single HTTP request across logs and response payloads.

## Decision

Propagate an `X-Correlation-Id` (or generate one) via `CorrelationIdFilter` into MDC. Include the value in the logging pattern and in every `ApiResponse`.

## Consequences

- End-to-end request tracing in logs and API responses.
- Clients can echo correlation ids when reporting issues.
- Downstream async consumers are not yet wired to inherit the same id.

## Code References

- `src/main/java/com/acos/common/logging/CorrelationIdFilter.java`
- `src/main/java/com/acos/common/api/ApiResponse.java`
- `src/main/resources/application.yml` (`logging.pattern.console` with `%X{correlationId:-}`)

## Related Modules

- `common.logging`; `common.api`; platform logging
