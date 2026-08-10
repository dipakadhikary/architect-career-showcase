# Troubleshooting

| Symptom | Likely cause | Action |
| --- | --- | --- |
| Business cannot migrate / DB errors | Credential mismatch compose vs `application-local` | Set `ACOS_DB_USER/PASSWORD` to match |
| Web API 404/proxy fail | Business down or wrong `VITE_API_PROXY_TARGET` | Check :8080; restart Vite |
| 401 loop on Web | Refresh token revoked/expired | Clear localStorage; re-login |
| AI Feign failures | `ai.platform.enabled` false or AI down | Enable flag; check `/api/v1/system/liveness` |
| Circuit open | Repeated AI errors/timeouts | Check AI logs/metrics; fix dependency; wait CB reset 30s |
| Contracts generate fail | Invalid OpenAPI `$ref` / duplicate operationId | Run validate scripts; fix YAML |
| AI import errors for contracts | Stale `third_party` | Re-sync from generated Python |
| Qdrant/Redis degraded | Containers not running | `docker compose ps` in AI repo |
| OTEL noise / connection errors | Collector hostname without service | Disable `OTEL_ENABLED` or add collector |


## Interview Discussion

### Why this approach?

Encode footguns discovered from real defaults.

### Alternative approaches

Generic 'check the logs'. Less useful.

### Trade-offs

Not exhaustive for every domain bug.

### Enterprise adoption

Link symptoms to runbook IDs in alerts.

### Scaling considerations

Auto-remediation for restart-safe failures.

### Principal Architect interview questions

**Q1. CB wait duration Business AI?**  
30 seconds (config).

**Q2. First check when Web cannot login?**  
Business up + DB migrated + CORS/proxy path.
