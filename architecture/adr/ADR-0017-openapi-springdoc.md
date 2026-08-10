# ADR-0017: SpringDoc OpenAPI with Bearer JWT Security Scheme

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

API consumers and developers need interactive, accurate documentation aligned with authentication requirements.

## Decision

Use SpringDoc OpenAPI. Document endpoints with annotations (`@Tag`, `@Operation`, `@SecurityRequirement`). Register a bearer-JWT security scheme in `OpenApiConfiguration`. Expose `/v3/api-docs` and Swagger UI paths configured in `application.yml`.

## Consequences

- Living API documentation co-located with controllers.
- Security requirements are visible in Swagger UI.
- Docs must be maintained when contracts change.

## Code References

- `src/main/java/com/acos/config/OpenApiConfiguration.java`
- `src/main/resources/application.yml` (`springdoc:` block)
- Annotated feature controllers

## Related Modules

- `config`; all REST controllers
