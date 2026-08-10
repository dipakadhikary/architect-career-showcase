# ADR-0022: Bean Validation on DTOs plus Feature Domain Validators

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Structural input constraints and business/limit rules are different concerns; mixing them only in controllers creates duplication and weak messages.

## Decision

Apply Jakarta Bean Validation annotations on DTO records and invoke `@Valid` in controllers. Implement additional domain/limit checks in feature validators (`CareerValidator`, `KnowledgeNoteValidator`, `PortfolioValidator`, learning validators, `PasswordValidator`) backed by `acos.*` properties where relevant.

## Consequences

- Clear separation of structural vs business validation.
- Shared limit configuration via properties.
- Validation failures map through the global exception handler to `ApiResponse` errors.

## Code References

- Feature `dto` packages with Jakarta Validation annotations
- `com.acos.career.validator.CareerValidator`
- `com.acos.knowledge.validator.KnowledgeNoteValidator`
- `com.acos.portfolio.validator.PortfolioValidator`
- `com.acos.auth.validator.PasswordValidator`
- Controllers using `@Valid`

## Related Modules

- Auth; Knowledge; Learning; Portfolio; Career
