# Incident Response

## Severity (practical)

| SEV | Example |
| --- | --- |
| 1 | Data loss / auth completely broken in shared env |
| 2 | AI outage with Business degraded features |
| 3 | Single feature bug; workaround exists |

## Immediate actions (local/shared demo)

1. **Declare** — who is investigating; freeze deploys  
2. **Stabilize** — set `ai.platform.enabled=false` if AI is the blast radius; keep CRUD up  
3. **Preserve** — capture correlation IDs, Actuator health JSON, AI metrics scrape, recent logs  
4. **Mitigate** — restart unhealthy containers; rotate compromised JWT secret if leak suspected (forces re-login)  
5. **Communicate** — status to stakeholders  
6. **Follow up** — root cause notes → Lessons Learned  

## Gaps

No formal on-call, status page, or SEV SLA in-repo.


## Interview Discussion

### Why this approach?

Feature-flag kill switch for AI is the primary blast-radius control.

### Alternative approaches

Always-on AI without flag. Riskier.

### Trade-offs

Manual process without paging.

### Enterprise adoption

Integrate PagerDuty; blameless postmortems.

### Scaling considerations

Automated rollback on SLI burn.

### Principal Architect interview questions

**Q1. Fastest AI mitigation from Business?**  
Disable `ai.platform.enabled`.

**Q2. What ID stitches logs?**  
`X-Correlation-Id` / MDC `correlationId`.
