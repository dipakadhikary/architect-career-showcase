# ADR-0018: Selective Spring Boot Actuator Exposure

Interview summary of [`ADR-0018`](../architecture/adr/ADR-0018-actuator-exposure.md).

## Decision

Expose `health`, `info`, `metrics`, and `prometheus`; permit anonymous access only to health/info.

## Benefits

- Standard ops endpoints for monitoring.
- Prometheus scraping is supported at Actuator level.
- Broader Actuator surface remains closed by default config.

## Limitations

- Metrics/prometheus still depend on deployment-time network controls outside the app.
- No full observability stack (Grafana/Jaeger) is packaged in-repo.

## Code References

- `pom.xml` (`spring-boot-starter-actuator`)
- `application.yml` `management` block
- `SecurityConfiguration` health/info permit
