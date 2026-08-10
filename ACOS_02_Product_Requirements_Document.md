
# ACOS - Book 1 : Product & Architecture
# 02 - Product Requirements Document (PRD)

Version: 1.0
Status: Draft

---

# 1. Executive Summary

Architect Career Operating System (ACOS) is a production-grade web platform that helps software engineers and architects manage learning, interview preparation, architecture knowledge, portfolio projects, and AI-assisted mentoring from a single application.

The platform itself is also intended to serve as a showcase project demonstrating enterprise architecture, clean engineering practices, and modern AI integration.

---

# 2. Business Problem

Engineers preparing for senior technical roles typically use many disconnected tools.

Problems include:

- Knowledge scattered across multiple applications
- No unified progress tracking
- Repetitive interview preparation
- Difficult portfolio management
- No structured architecture knowledge base

ACOS addresses these issues through a unified platform.

---

# 3. Product Vision

Build the personal operating system for software engineers, solution architects, and GenAI architects.

---

# 4. Goals

Business Goals

- Improve interview readiness
- Centralize career assets
- Increase learning efficiency
- Build a demonstrable portfolio

Technical Goals

- Modular architecture
- API-first
- Cloud-ready
- AI-ready
- Observable
- Secure

---

# 5. Stakeholders

Product Owner
- Dipak

Principal Architect
- ChatGPT

Implementation Partner
- Cursor

End Users
- Software Engineers
- Senior Engineers
- Architects
- Technical Leads

---

# 6. User Personas

1. Junior Developer
2. Mid-Level Developer
3. Senior Developer
4. Solution Architect
5. Principal Architect

Each persona has different roadmaps, interview banks, dashboards and recommendations.

---

# 7. Core Modules

1. Authentication
2. Dashboard
3. Learning Roadmap
4. Knowledge Base
5. Interview Bank
6. Coding Tracker
7. Portfolio
8. Resume Manager
9. Applications Tracker
10. Mock Interview
11. Analytics
12. AI Tutor (Phase 2)

---

# 8. Functional Requirements (High Level)

FR-001 User authentication

FR-002 Manage learning roadmap

FR-003 Create and organize knowledge articles

FR-004 Maintain interview questions

FR-005 Track coding practice

FR-006 Track projects and portfolio

FR-007 Track job applications

FR-008 Dashboard analytics

FR-009 AI-assisted learning

---

# 9. Non Functional Requirements

Availability : 99%

Security :
- JWT
- RBAC
- HTTPS
- BCrypt
- OWASP

Performance
- API < 500 ms (typical)
- UI load < 2 seconds

Maintainability
- Clean Architecture
- SOLID
- Modular Monolith

Observability
- Logs
- Metrics
- Traces

---

# 10. MVP Scope

Authentication

Dashboard

Knowledge Base

Learning Roadmap

Interview Bank

Portfolio

Resume

Applications

Analytics

---

# 11. Out of Scope

Payments

Mobile App

Collaboration

Marketplace

Multi-tenancy

---

# 12. User Journey

Register

↓

Login

↓

Dashboard

↓

Choose Learning Goal

↓

Study

↓

Practice Interview

↓

Update Progress

↓

Portfolio

↓

Job Applications

↓

Interview Success

---

# 13. Acceptance Criteria

A release is acceptable when:

- Features satisfy functional requirements
- Unit and integration tests pass
- Documentation is updated
- ADR exists for major decisions
- Security review completed
- Interview notes added

---

# 14. Risks

Scope creep

Overengineering

Changing AI ecosystem

Time constraints

Mitigation:
- Deliver incrementally
- Prioritize MVP
- Review backlog every sprint

---

# 15. Release Plan

Release 1
Platform Foundation

Release 2
Learning Platform

Release 3
Interview Platform

Release 4
Portfolio

Release 5
AI Tutor

Release 6
RAG + Agentic AI

---

# 16. Success Metrics

Study hours

Learning streak

Knowledge articles

Interview confidence

Projects completed

Applications submitted

Interview conversion rate

---

# 17. Traceability

Every future artifact (HLD, LLD, APIs, database, UI and tests) shall reference the relevant PRD requirement IDs.

---

# 18. Next Documents

03-Business-Requirements.md

04-Functional-Requirements.md

05-NonFunctional-Requirements.md

These documents will decompose every requirement into detailed specifications with use cases, acceptance criteria and interview discussion points.
