
# ACOS - Expanded High-Level Design (C4)
Version: 1.0

# Purpose

Describe the overall architecture of ACOS using the C4 model and define how
major components collaborate.

---

# C1 - System Context

Actors

- Software Engineer
- Solution Architect
- Principal Architect

External Systems

- GitHub
- LLM Provider (OpenAI/Ollama)
- Email Provider (Future)

System

ACOS provides learning, interview preparation, portfolio management,
knowledge management and AI-assisted mentoring.

---

# C2 - Container Diagram

+------------------------+
| React Web Application  |
+------------------------+
            |
            | HTTPS / REST
            v
+------------------------+
| Spring Boot API        |
| Business Modules       |
+------------------------+
      |           |
      | JPA       | REST
      v           v
+-----------+   +----------------+
|PostgreSQL |   | Python AI       |
+-----------+   | FastAPI         |
                +----------------+
                       |
                       v
                  +----------+
                  | Qdrant   |
                  +----------+

Observability

Spring Boot
Python
React
  |
OpenTelemetry
  |
Prometheus
Grafana
Jaeger

---

# C3 - Spring Boot Components

Identity Module
Learning Module
Knowledge Module
Interview Module
Portfolio Module
Career Module
Analytics Module
Shared Kernel

Shared Components

- Security
- Validation
- Exception Handling
- Audit
- Events
- Configuration

---

# Request Lifecycle

Browser
→ React
→ Spring Security
→ Controller
→ Service
→ Repository
→ PostgreSQL
→ Response

AI Request

Browser
→ Spring Boot
→ Python AI
→ Qdrant
→ LLM
→ Spring Boot
→ Browser

---

# Deployment View

Docker Compose

react
springboot
python-ai
postgres
qdrant
prometheus
grafana
jaeger

Future

Ingress
Kubernetes
Horizontal scaling

---

# Scalability Strategy

Current
- Modular Monolith

Growth
- Read replicas
- Redis cache
- Async events

Future
- Split bounded contexts
- API Gateway
- Event streaming

---

# Security

JWT
RBAC
HTTPS
Input Validation
Rate Limiting (future)

---

# Availability

Stateless backend
Persistent PostgreSQL
Health checks
Graceful shutdown

---

# Architectural Constraints

- Feature-first packaging
- No cross-module repository access
- Public communication via service interfaces
- API-first development
- Documentation-first workflow

---

# Mapping

Identity -> auth module
Learning -> roadmap module
Knowledge -> knowledge module
Interview -> interview module
Portfolio -> portfolio module
Career -> career module
AI -> python-ai service

---

# Interview Discussion

Why Modular Monolith first?

How would you migrate to microservices?

Why separate AI service?

Why PostgreSQL?

How would you scale to 100k users?

What are the likely bottlenecks?

---

# Next Deliverables

1. Database ERD
2. OpenAPI Specification
3. ADR-001 to ADR-010
4. Backend Skeleton
