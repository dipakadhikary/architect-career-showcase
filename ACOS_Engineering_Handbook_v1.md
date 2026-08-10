
# ACOS Engineering Handbook
Version: 1.0

## Purpose

This handbook defines the engineering standards for every artifact produced in ACOS.
All contributors (human or AI) must follow these standards.

---

# 1. Engineering Principles

- Architecture First
- API First
- Documentation as Code
- Modular Monolith First
- Feature-Oriented Design
- Clean Architecture
- SOLID
- YAGNI
- KISS
- DRY

---

# 2. Feature Lifecycle

Business Requirement
→ Functional Requirement
→ ADR (if needed)
→ HLD / LLD
→ Database
→ OpenAPI
→ Cursor Prompt
→ Implementation
→ Tests
→ Documentation
→ Interview Notes

---

# 3. Repository Standards

Each feature owns:

- README.md
- requirements.md
- architecture.md
- api.md
- database.md
- cursor-prompt.md
- implementation-notes.md
- interview-notes.md

---

# 4. Java Standards

- Java 21
- Spring Boot 3.x
- Constructor injection only
- Records for immutable DTOs
- Package by feature
- Avoid field injection
- Global exception handling
- Validation using Jakarta Validation
- Flyway for schema changes

---

# 5. React Standards

- TypeScript
- Functional components
- Feature folders
- React Query for server state
- Material UI
- No business logic inside components

---

# 6. Python Standards

- FastAPI
- Pydantic models
- LangChain
- LangGraph
- Ruff formatting
- Pytest

---

# 7. REST API Standards

- /api/v1
- Resource-oriented URLs
- Consistent error model
- Pagination
- Filtering
- Sorting
- OpenAPI-first

---

# 8. Database Standards

- PostgreSQL
- Flyway migrations
- UUID primary keys (where appropriate)
- created_at / updated_at audit fields
- Foreign keys
- Explicit indexes
- Naming conventions

---

# 9. Security Standards

- JWT authentication
- Refresh tokens
- BCrypt password hashing
- RBAC
- HTTPS
- Input validation
- OWASP Top 10 awareness

---

# 10. Observability

- Structured JSON logs
- Micrometer metrics
- OpenTelemetry traces
- Prometheus
- Grafana
- Jaeger

---

# 11. Testing Strategy

Backend
- JUnit 5
- Mockito
- Integration tests

Frontend
- React Testing Library

AI
- Pytest
- Evaluation datasets

---

# 12. Code Review Checklist

- Requirements satisfied?
- Architecture respected?
- Security considered?
- Tests included?
- Documentation updated?
- Naming consistent?
- Performance concerns addressed?

---

# 13. Definition of Ready

A feature is ready when:
- Business requirement exists
- Acceptance criteria defined
- API identified
- Database impact understood
- UI scope defined

---

# 14. Definition of Done

A feature is done when:
- Code merged
- Tests pass
- Documentation updated
- ADR updated (if needed)
- Interview notes written
- Demo completed

---

# 15. AI Collaboration Model

ChatGPT
- Architect
- Reviewer
- Mentor
- Documentation
- Interview Coach

Cursor
- Implementation
- Refactoring
- Test generation
- Boilerplate

Developer
- Design decisions
- Final review
- Learning
- Git ownership

---

# Next Deliverables

1. Domain Model
2. Expanded HLD (C4)
3. Database ERD
4. OpenAPI Specification
5. Backend Skeleton
