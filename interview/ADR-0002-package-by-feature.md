# ADR-0002: Package-by-Feature with Internal Layering

Interview summary of [`ADR-0002`](../architecture/adr/ADR-0002-package-by-feature.md).

## Decision

Organize code by feature/bounded context first; use technical layers (`controller`, `service`, `repository`, etc.) inside each feature. Put shared concerns in `common`/`config`.

## Benefits

- Feature code is cohesive and easy to locate.
- New features can be added without reshaping a global layer tree.
- Career-specific packages (`event`, `state`, `specification`) fit naturally.

## Limitations

- Shared utilities must be moved deliberately into `common`/`config` to avoid duplication.
- Cross-feature imports are still possible and rely on convention.

## Code References

- `src/main/java/com/acos/career/`
- `src/main/java/com/acos/auth/`
- `src/main/java/com/acos/knowledge/`
- `src/main/java/com/acos/common/`
- `src/main/java/com/acos/config/`
