# ADR-0013: Constructor Injection, Service Interfaces, and Transactional Services

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Field injection and business logic in controllers reduce testability and blur transaction boundaries.

## Decision

Inject dependencies through constructors only. Controllers depend on service interfaces; implementations use `*ServiceImpl` naming. Place `@Transactional` on service implementations (with `readOnly = true` for queries).

## Consequences

- Dependencies are explicit and easy to mock.
- Unit of work lives in the application service layer.
- Controllers remain thin HTTP adapters.
- Interface proliferation is accepted as the service boundary convention.

## Code References

- Feature controllers (constructor-injected collaborators)
- Service interfaces/impls such as `AuthService`/`AuthServiceImpl`, `JobApplicationService`/`JobApplicationServiceImpl`
- No field `@Autowired` / `EntityManager` usage in `src/main/java`

## Related Modules

- All feature modules; Auth
