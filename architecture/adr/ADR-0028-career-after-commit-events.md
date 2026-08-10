# ADR-0028: Career After-Commit Domain Event Publishing

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Side effects (notifications, analytics, AI) must not observe uncommitted career state, and should not be hardwired into transactional services yet.

## Decision

Publish career domain events through `CareerDomainEventPublisher`, which registers a `TransactionSynchronization` and publishes via `ApplicationEventPublisher` only after successful commit (or immediately if no transaction is active). Event types include application submitted/status changed/rejected and interview/offer lifecycle events. No listeners are implemented yet.

## Consequences

- Future modules can subscribe without changing publishers.
- Listeners will not see rolled-back state when using after-commit publication.
- Today this is publish-only; no in-process consumers exist.
- Pattern is implemented in career only.

## Code References

- `src/main/java/com/acos/career/event/CareerDomainEventPublisher.java`
- `src/main/java/com/acos/career/event/CareerDomainEvent.java`
- Event records under `com.acos.career.event` (`ApplicationSubmittedEvent`, `ApplicationStatusChangedEvent`, `InterviewScheduledEvent`, `OfferReceivedEvent`, etc.)
- Publication call sites in career services

## Related Modules

- Career (`event`, services); future Notification/Analytics/AI consumers
