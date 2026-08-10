# ADR-0017: SpringDoc OpenAPI with Bearer JWT Security Scheme

Interview summary of [`ADR-0017`](../architecture/adr/ADR-0017-openapi-springdoc.md).

## Decision

Document APIs with SpringDoc, controller annotations, and a global `bearer-jwt` security scheme.

## Benefits

- Living API docs co-located with controllers.
- Security requirements are visible in Swagger UI.
- Public docs paths are available for developers.

## Limitations

- Docs drift if annotations are not updated with contract changes.
- Actuator is intentionally hidden from Swagger (`show-actuator: false`).

## Code References

- `OpenApiConfiguration`
- `application.yml` `springdoc` section
- Annotated feature controllers
