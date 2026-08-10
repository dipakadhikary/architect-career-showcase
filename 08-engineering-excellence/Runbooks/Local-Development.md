# Local Development

## Typical loop

```mermaid
flowchart LR
  Code[Edit] --> Test[Unit/IT]
  Test --> Run[Run service]
  Run --> Proxy[Web :5173 → Business :8080]
```

| Workstream | Commands |
| --- | --- |
| Business | `mvn spring-boot:run` / `mvn test` / `mvn verify` |
| Web | `npm run dev` / `npm test` / `npm run lint` |
| AI | `uvicorn app.main:app --port 8090` or compose; `pytest` |
| Contracts | `mvn clean verify`; sync Python to AI `third_party` |

## Hot reload

- Web: Vite HMR  
- AI dev compose: uvicorn reload  
- Business: Spring DevTools not documented as required — restart on many config changes  

## Quality before push

Run the strongest local gate available (`mvn verify`, `npm run build && npm test`, AI ruff/black/pytest) especially where CI is absent.


## Interview Discussion

### Why this approach?

Document the real developer loop, not an idealized monorepo.

### Alternative approaches

Devcontainer single workspace. Nice future DX.

### Trade-offs

Four terminals / toolchains.

### Enterprise adoption

Devcontainers + taskfile wrappers.

### Scaling considerations

Remote dev environments.

### Principal Architect interview questions

**Q1. Web proxy target default?**  
`http://localhost:8080`.

**Q2. Must AI run for CRUD demos?**  
No — AI flag defaults off.
