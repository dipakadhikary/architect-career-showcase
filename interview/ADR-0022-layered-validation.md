# ADR-0022: Bean Validation on DTOs plus Feature Domain Validators

Interview summary of [`ADR-0022`](../architecture/adr/ADR-0022-layered-validation.md).

## Decision

Use Jakarta Validation on DTO records at the controller boundary, plus feature validators for business/limit rules backed by `acos.*` properties.

## Benefits

- Structural vs business validation are separated.
- Shared limits come from configuration.
- Failures map through the global handler into `ApiResponse` errors.

## Limitations

- Developers must remember both annotation validation and feature validator calls.
- Duplicate concepts can appear if DTO constraints and validators overlap poorly.

## Code References

- Feature DTO validation annotations
- `CareerValidator`, `KnowledgeNoteValidator`, `PortfolioValidator`, `PasswordValidator`
- Controllers using `@Valid`
