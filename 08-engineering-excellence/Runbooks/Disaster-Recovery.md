# Disaster Recovery

## Current reality

DR is **local-volume based**, not multi-region:

| Data | Recovery approach |
| --- | --- |
| Postgres | Docker volume `acos_postgres_data`; restore via `pg_dump`/`pg_restore` (operator-driven; no automated backup job in-repo) |
| Qdrant | `qdrant_data` volume — re-index from Business knowledge if lost |
| Redis | Ephemeral cache — safe to flush |
| Refresh tokens | DB-backed — lost with DB |

## RTO/RPO

**Not contractually defined.** For demos, rebuild from compose + Flyway migrations + optional re-index.

## Future Roadmap

Automated Postgres backups; PITR; multi-AZ; documented RTO/RPO; AI vector rebuild pipelines.


## Interview Discussion

### Why this approach?

State clearly that volumes ≠ DR program.

### Alternative approaches

Claim multi-region DR. Dishonest.

### Trade-offs

Interview risk if not framed as portfolio stage.

### Enterprise adoption

Define RPO for career data; test restore quarterly.

### Scaling considerations

Cross-region replicas; immutable backups.

### Principal Architect interview questions

**Q1. Is Redis durable business state?**  
No — cache only.

**Q2. How to rebuild empty DB?**  
Flyway on Business boot against fresh Postgres.
