# ADR-0020: Enforceable Maven Static Analysis and Formatting Gates

Interview summary of [`ADR-0020`](../architecture/adr/ADR-0020-maven-quality-gates.md).

## Decision

Fail the build on Spotless, Checkstyle, PMD(+CPD), SpotBugs, and Enforcer violations; keep JaCoCo scaffolding.

## Benefits

- Formatting and common defect classes are build blockers.
- Contributors share one quality baseline.
- Java/Maven policy is enforced centrally.

## Limitations

- Some PMD design-smell rules are excluded where they conflict with established patterns.
- JaCoCo minimum coverage is currently `0.00`, so coverage is not yet a real gate.

## Code References

- `pom.xml` quality plugins
- `config/checkstyle/checkstyle.xml`
- `config/pmd/pmd-ruleset.xml`
- `config/spotbugs/spotbugs-exclude.xml`
