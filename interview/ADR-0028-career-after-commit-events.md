# ADR-0028: Career After-Commit Domain Event Publishing

Interview summary of [`ADR-0028`](../architecture/adr/ADR-0028-career-after-commit-events.md).

## Decision

Publish career domain events through `CareerDomainEventPublisher` only after successful transaction commit (or immediately if no transaction). No listeners are implemented yet.

## Benefits

- Future modules can subscribe without changing publishers.
- Listeners will not observe rolled-back state.
- Transactional services stay decoupled from side effects.

## Limitations

- Publish-only today; no in-process consumers exist.
- Pattern is implemented in career only.
- Downstream reliability (retries/outbox) is not implemented.

## Code References

- `CareerDomainEventPublisher`
- `CareerDomainEvent` and career event records
- Publication call sites in career services
