
# ACOS Framework Architecture
Version: 1.0

## Purpose

The ACOS Framework provides reusable engineering capabilities so that business
modules focus only on business logic.

---

# Layered Architecture

Presentation
↓
Application
↓
Domain
↓
Infrastructure
↓
Framework

Business modules depend on the framework.
The framework never depends on business modules.

---

# Framework Modules

## acos-core

Responsibilities

- BaseEntity
- BaseDTO
- Constants
- Error Codes
- Utility Classes
- UUID Generator
- Time Provider

---

## acos-web

Responsibilities

- Base REST Controller
- API Response Wrapper
- Pagination
- Sorting
- Filtering
- Global Exception Handler
- Request Context
- Correlation ID

---

## acos-security

Responsibilities

- JWT Authentication
- Refresh Token Support
- Authorization
- RBAC
- Permission Evaluator
- Security Filters

---

## acos-data

Responsibilities

- BaseRepository
- Audit Support
- Soft Delete
- Optimistic Locking
- Specification Builder

---

## acos-audit

Responsibilities

- Audit Trail
- Entity Auditing
- Domain Audit Events

---

## acos-events

Responsibilities

- Domain Events
- Integration Events
- Event Publisher
- Event Listener

---

## acos-observability

Responsibilities

- Logging
- Metrics
- Tracing
- OpenTelemetry
- Micrometer

---

## acos-testing

Responsibilities

- Base Test Classes
- Test Utilities
- Mock Authentication
- Testcontainers Support

---

# Business Modules

Each module contains:

controller/
service/
repository/
entity/
dto/
mapper/
validator/
config/
exception/

Modules

- auth
- dashboard
- learning
- knowledge
- interview
- portfolio
- career
- analytics
- administration

---

# Dependency Rules

Allowed

Business Module -> Framework

Business Module -> Shared Kernel

Not Allowed

Business Module -> Another Module Repository

Controller -> Repository

DTO -> Entity

UI -> Database

---

# Cross Cutting Concerns

Provided by Framework

- Logging
- Security
- Validation
- Auditing
- Exception Handling
- Pagination
- API Response
- Metrics

---

# Coding Rules

- Constructor Injection
- Records for DTOs
- Feature-first Packaging
- One Responsibility per Service
- No Business Logic in Controller
- Flyway for Schema
- OpenAPI First

---

# Sprint Plan

Sprint 1.1
- Build Framework Modules

Sprint 1.2
- Authentication

Sprint 1.3
- Dashboard

Sprint 1.4
- Knowledge Module

---

# Interview Talking Points

- Why create an internal framework?
- Why modular monolith instead of microservices?
- Which concerns belong in the framework?
- How would you extract a module into a microservice?
- What benefits does feature-first packaging provide?

---

# Exit Criteria

Framework is complete when:

- Shared libraries compile
- Sample authentication module uses framework
- Common exception handling works
- Security works
- Logging works
- OpenAPI generated
- Flyway integrated
