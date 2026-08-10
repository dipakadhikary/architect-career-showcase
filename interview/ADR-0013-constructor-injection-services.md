# ADR-0013: Constructor Injection, Service Interfaces, and Transactional Services

Interview summary of [`ADR-0013`](../architecture/adr/ADR-0013-constructor-injection-services.md).

## Decision

Inject dependencies via constructors; controllers depend on service interfaces; put `@Transactional` on service implementations.

## Benefits

- Dependencies are explicit and easy to mock.
- Unit of work lives in the application service layer.
- Controllers remain thin HTTP adapters.

## Limitations

- Interface + `*Impl` pairs increase type count.
- Incorrect transaction boundaries still possible if work leaks outside services.

## Code References

- Feature controllers with constructor injection
- `AuthService` / `AuthServiceImpl`
- `JobApplicationService` / `JobApplicationServiceImpl`
