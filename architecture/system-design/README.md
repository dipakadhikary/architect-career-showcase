# ACOS System Design

High-level and low-level design for the **implemented** Architect Career Operating System (ACOS) backend: a modular Spring Boot monolith.

It does not describe unimplemented frontend, AI, or multi-service topologies from product vision documents.

## High Level Design

| Document | Contents |
| --- | --- |
| [01 — System Context](./01-system-context.md) | External actors and system boundary |
| [02 — Component Diagram](./02-component-diagram.md) | Major runtime components inside the monolith |
| [03 — Module Diagram](./03-module-diagram.md) | Package/feature modules and dependencies |
| [04 — Deployment Diagram](./04-deployment-diagram.md) | Local/runtime deployment topology |
| [05 — Technology Stack](./05-technology-stack.md) | Languages, frameworks, and infrastructure |
| [06 — Module Responsibilities](./06-module-responsibilities.md) | What each module owns |

## Low Level Design

| Document | Contents |
| --- | --- |
| [00 — LLD Index](./00-lld-index.md) | LLD overview and constraints |
| [07 — Package Diagram](./07-package-diagram.md) | Feature package structure |
| [08 — Entity Relationships](./08-entity-relationships.md) | JPA/table relationships by domain |
| [09 — Sequence Diagrams](./09-sequence-diagrams.md) | Auth login, application create, status transition |
| [10 — Service Interaction](./10-service-interaction.md) | Service collaborators and orchestration |
| [11 — Controller Flow](./11-controller-flow.md) | Thin controller request path |
| [12 — Repository Flow](./12-repository-flow.md) | Persistence access patterns |

## Related documentation

- Architecture Decision Records: [`../adr`](../adr)
- Architecture Handbook: [`../architecture-handbook`](../architecture-handbook)
