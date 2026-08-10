# Local Setup

## Prerequisites

- Java 21, Maven 3.8+  
- Node 20+  
- Python 3.13 (AI); 3.12 used in Contracts CI  
- Docker (Postgres / Redis / Qdrant)  

## Checklist

1. **Postgres:** `cd architect-career-operating-system/infrastructure/docker && docker compose up -d`  
2. Align `ACOS_DB_*` with compose (`acos`/`acos` vs `postgres`/`postgres` defaults)  
3. **Business:** `./mvnw spring-boot:run` → http://localhost:8080  
4. **Web:** `npm install && npm run dev` → http://localhost:5173  
5. **AI (optional):** compose up redis/qdrant; `pip install -e ".[dev]"`; uvicorn `:8090`  
6. **Enable AI:** `AI_PLATFORM_ENABLED=true`, `AI_PLATFORM_BASE_URL=http://localhost:8090`  
7. **Contracts change:** `mvn clean verify` then AI `python scripts/sync_contracts.py`  

## Verify

| Check | URL / command |
| --- | --- |
| Business health | `/actuator/health` |
| Web | open SPA, register/login |
| AI liveness | `/api/v1/system/liveness` |


## Interview Discussion

### Why this approach?

Ordered checklist prevents the common DB credential mismatch.

### Alternative approaches

One mega-compose. Future improvement.

### Trade-offs

`.env.example` missing on AI confuses new operators.

### Enterprise adoption

Bootstrap script that waits on healthchecks.

### Scaling considerations

Seed data jobs for demos.

### Principal Architect interview questions

**Q1. pgAdmin port default?**  
5050.

**Q2. AI default port?**  
8090.
