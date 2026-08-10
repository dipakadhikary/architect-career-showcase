# ADR-0002: Package-by-Feature with Internal Layering

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

A global technical-layer layout (`controllers/`, `services/` across domains) obscures ownership and encourages cross-feature coupling as features grow.

## Decision

Organize primary packages by feature/bounded context. Inside each feature use technical layers: `controller`, `service`, `repository`, `entity`, `dto`, `mapper`, `validator`, `exception`, `config`, plus feature-specific packages where needed (`event`, `state`, `specification` in career). Shared cross-cutting concerns live in `com.acos.common` and `com.acos.config`.

## Consequences

- Feature code is discoverable and cohesive.
- New features can be added without reshaping a global layer tree.
- Shared utilities must be deliberately placed in `common`/`config` to avoid duplication.
- Cross-feature imports remain possible and must be disciplined by convention.

## Code References

- `src/main/java/com/acos/career/` (includes `event`, `state`, `specification`)
- `src/main/java/com/acos/auth/`
- `src/main/java/com/acos/knowledge/`
- `src/main/java/com/acos/learning/`
- `src/main/java/com/acos/portfolio/`
- `src/main/java/com/acos/common/`
- `src/main/java/com/acos/config/`

## Related Modules

- All feature modules; `common`; `config`
