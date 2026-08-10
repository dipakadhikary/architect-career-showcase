
# ACOS Repository Blueprint
Version: 1.0

# Purpose

This document defines the information architecture for the Architect Career Operating System (ACOS) repository.

The repository is designed to be both:

1. A production software project
2. A lifelong architecture knowledge base

---

# Top-Level Structure

```text
architect-career-operating-system/
│
├── docs/
├── books/
├── architecture/
├── adr/
├── api/
├── database/
├── frontend/
├── backend/
├── ai-service/
├── infrastructure/
├── prompts/
├── cursor/
├── interview-bank/
├── knowledge-base/
├── templates/
├── portfolio/
└── scripts/
```

---

# docs/

Project artifacts.

```text
00-project-charter.md
01-vision.md
02-prd.md
03-business-requirements.md
04-functional-requirements.md
05-non-functional-requirements.md
06-use-cases.md
07-user-stories.md
08-domain-model.md
09-hld.md
10-lld.md
11-database-design.md
12-api-design.md
13-security.md
14-deployment.md
15-observability.md
16-release-strategy.md
17-test-strategy.md
```

---

# books/

## Book 1
Product & Architecture

## Book 2
Engineering Handbook

## Book 3
Principal Architect Handbook

## Book 4
AI Engineering Handbook

## Book 5
Interview Companion

## Book 6
Implementation Guide

Every chapter follows:

- Concept
- Why
- Design
- Alternatives
- Trade-offs
- Example
- Interview Questions
- Common Mistakes
- References

---

# architecture/

```text
context/
containers/
components/
deployment/
sequence/
class/
state/
activity/
mermaid/
plantuml/
```

---

# adr/

Every architectural decision:

```text
ADR-001-Modular-Monolith.md
ADR-002-React.md
ADR-003-SpringBoot.md
ADR-004-PostgreSQL.md
ADR-005-Python-AI-Service.md
ADR-006-Qdrant.md
```

ADR Template

- Context
- Decision
- Alternatives
- Consequences
- Trade-offs
- Interview Notes

---

# api/

OpenAPI specifications

REST conventions

Error model

Versioning

Examples

---

# database/

ER diagrams

DDL

Indexes

Migration scripts

Data dictionary

Naming standards

---

# frontend/

React application

Feature-first structure

components/

pages/

services/

hooks/

---

# backend/

Spring Boot

Feature modules

auth/

knowledge/

interview/

roadmap/

portfolio/

analytics/

common/

---

# ai-service/

FastAPI

LangChain

LangGraph

RAG

Prompt management

Evaluation

---

# infrastructure/

docker/

kubernetes/

github-actions/

terraform/ (future)

---

# prompts/

Reusable prompts

ChatGPT

Cursor

Code Review

Architecture Review

Documentation

Interview

---

# cursor/

Implementation prompts

One prompt per feature.

---

# knowledge-base/

Java

Spring

Kafka

Redis

System Design

Security

AI

Architecture

Leadership

---

# interview-bank/

Question banks

Architecture

Java

Spring

AI

Behavioral

Leadership

Mock Interviews

---

# templates/

PRD

ADR

API

HLD

LLD

Checklist

Meeting Notes

Review Template

---

# Traceability

Requirement
↓
Architecture
↓
ADR
↓
API
↓
Database
↓
Code
↓
Tests
↓
Documentation
↓
Interview Notes

Every artifact references its parent.

---

# Working Process

1. Define Requirement
2. Create ADR (if needed)
3. Design Architecture
4. Design API
5. Design Database
6. Generate Cursor Prompt
7. Implement
8. Review
9. Test
10. Document
11. Capture Interview Notes
12. Update Knowledge Base

---

# Definition of Quality

Every feature is complete only when:

- Requirements approved
- ADR updated
- Code reviewed
- Tests passing
- Documentation updated
- Interview notes written
- Portfolio entry added

---

# Next Deliverables

1. Repository README
2. CONTRIBUTING Guide
3. Coding Standards
4. Architecture Principles
5. NFR
6. Domain Model
7. Expanded HLD
