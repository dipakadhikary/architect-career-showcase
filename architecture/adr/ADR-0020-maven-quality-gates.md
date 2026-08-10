# ADR-0020: Enforceable Maven Static Analysis and Formatting Gates

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Style and defect regressions must fail the build before merge, not rely on optional IDE settings.

## Decision

Enforce Spotless (Google Java Format), Checkstyle, PMD (including CPD), SpotBugs, and Maven Enforcer (Java 21 / dependency convergence) during the Maven lifecycle. JaCoCo is configured for reporting/check scaffolding.

## Consequences

- Formatting and common defect classes are build blockers.
- Contributors share one quality baseline.
- Some design-smell PMD rules are explicitly excluded in `pmd-ruleset.xml` where they conflict with established patterns.
- JaCoCo minimum coverage is currently configured at `0.00` (gate present, not yet used as a coverage bar).

## Code References

- `pom.xml` (Spotless, Checkstyle, PMD, SpotBugs, Enforcer, JaCoCo plugins)
- `config/checkstyle/checkstyle.xml`
- `config/pmd/pmd-ruleset.xml`
- `config/spotbugs/spotbugs-exclude.xml`
- `.editorconfig`

## Related Modules

- Build/platform-wide
