# ADR-0003: Versioned REST Base Path `/api/v1`

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Clients need a stable HTTP contract. Breaking API changes must be introducible later without silently changing existing paths.

## Decision

Expose all authenticated and public REST APIs under the `/api/v1/...` prefix.

## Consequences

- Clear public contract versioning.
- Future `/api/v2` can coexist.
- Controllers must keep the prefix consistently.

## Code References

- `com.acos.auth.controller.AuthController` (`/api/v1/auth`)
- `com.acos.career.controller.JobApplicationController` (`/api/v1/career/applications`)
- `com.acos.knowledge.controller.KnowledgeController`
- `com.acos.learning.controller.LearningPlanController`
- `com.acos.portfolio.controller.PortfolioProjectController`
- `com.acos.dashboard.web.DashboardController` (`/api/v1/dashboard`)
- `com.acos.career.controller.CareerDashboardController` (`/api/v1/career/dashboard`)

## Related Modules

- Auth, Knowledge, Learning, Portfolio, Career, Dashboard
