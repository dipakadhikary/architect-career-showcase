# Deployment

## Supported today: local / demo deployment

1. Build Business: `mvn clean package` (optional) and run jar / `spring-boot:run`  
2. Build Web: `npm run build`; serve `dist/` (or `vite preview`) behind same origin or configured API base  
3. AI: `docker build` + compose, or bare uvicorn with env  
4. Do **not** enable AI in Business until AI health is UP  

## Not supported (document as gap)

Automated deploy to cloud; Kubernetes rollout; blue/green; CDN invalidation runbooks.

## Contracts artifacts

Download Actions artifact `career-ai-sdk-artifacts` or produce via `mvn verify`; vendor into AI; optionally consume Java JAR later.


## Interview Discussion

### Why this approach?

Ship a truthful deploy story for portfolio demos.

### Alternative approaches

Fake Kubernetes diagrams. Avoided.

### Trade-offs

Interviewers may ask for CD — point to roadmap.

### Enterprise adoption

Add GitHub Environments + OIDC to cloud.

### Scaling considerations

Immutable tags; progressive delivery.

### Principal Architect interview questions

**Q1. Web production server in repo?**  
No nginx/Dockerfile — static `dist/` only.

**Q2. AI image healthcheck?**  
curl liveness on 8090.
