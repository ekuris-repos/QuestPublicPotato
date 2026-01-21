---
description: "Guidance for editing and reviewing backend infrastructure code including Docker, Bicep, and deployment configurations."
applyTo: "infra/**, docker-compose.yml, api/Dockerfile, frontend/Dockerfile, .github/workflows/deploy*.yml"
---
# Backend Infrastructure Review Guidance
Focus on security, reliability, cost efficiency, and maintainability for containerized Azure deployments.

## Infrastructure Principles

- Prefer Infrastructure as Code (IaC): all Azure resources defined in Bicep files under `infra/`.
- Keep Dockerfiles minimal: use multi-stage builds, prefer Alpine base images, and avoid unnecessary layers.
- Use environment variables for all configuration; never hardcode secrets, URLs, or resource names.
- Apply principle of least privilege for managed identities and role assignments.
- Ensure idempotency: re-running deployments should produce the same result without failures.

## Bicep Review Checklist
1. **Parameters**: all configurable values exposed as parameters with appropriate defaults and descriptions.
2. **Naming**: use `uniqueString()` for globally unique resource names; follow Azure naming conventions.
3. **Dependencies**: verify `dependsOn` chains are correct; avoid circular references between API and frontend.
4. **Outputs**: expose required outputs (URLs, resource IDs) for workflow consumption.
5. **Security**: use `@secure()` decorator for sensitive parameters; reference secrets from Key Vault when possible.
6. **SKU/Sizing**: validate resource SKUs match environment needs (B1 for dev/staging, scale up for production).
7. **CORS**: configure API CORS origins dynamically using environment variables; ensure `https://` prefix.

## Docker Review Checklist
1. **Multi-stage builds**: separate builder and runtime stages to minimize image size.
2. **Base images**: use specific version tags (e.g., `node:24-alpine`), not `latest`.
3. **Layer caching**: copy `package*.json` and install dependencies before copying source code.
4. **Security**: run as non-root user where possible; avoid installing unnecessary packages.
5. **Health checks**: include `HEALTHCHECK` instructions for production readiness.
6. **Build args vs env vars**: use `ARG` for build-time, `ENV` for runtime configuration.

## Docker Compose Review Checklist
1. **Service dependencies**: use `depends_on` with health conditions for proper startup order.
2. **Environment**: pass environment variables explicitly; use `.env` files for local development only.
3. **Volumes**: mount volumes for persistent data (e.g., SQLite DB files) and development hot-reload.
4. **Networks**: define explicit networks for service isolation when needed.
5. **Port mappings**: avoid port conflicts; document exposed ports clearly.

## Azure Container Apps Specifics
- Target port must match the container's exposed port (3000 for API, 80 for frontend).
- Configure ingress as `external: true` for public-facing services.
- Use `latestRevision: true` with weight 100 for simple deployments.
- Set appropriate CPU/memory limits: start with `0.5` CPU and `1Gi` memory, adjust based on load.
- Store sensitive values in Container Apps secrets, reference via `secretRef`.

## SQLite Persistence in Containers
- Mount a persistent volume for the database file (e.g., `/home/site/data/app.db`).
- Set `DB_FILE` environment variable to the mounted path.
- Enable WAL mode (`DB_ENABLE_WAL=true`) for better concurrency in containerized environments.
- Ensure the data directory exists and is writable before application startup.

## GitHub Actions Deployment Checklist
1. **Secrets**: store Azure credentials, registry passwords in GitHub Secrets; never log them.
2. **Environments**: use GitHub Environments for staging/production with required approvals.
3. **Outputs**: capture and use deployment outputs (URLs) for verification and environment variables.
4. **Rollback**: ensure failed deployments don't leave resources in inconsistent state.
5. **Caching**: cache Docker layers and npm dependencies to speed up builds.

## Security Considerations
- Use Managed Identity for Azure resource authentication; avoid storing credentials in code.
- Restrict CORS to known origins; never use `*` in production.
- Enable HTTPS-only ingress; redirect HTTP to HTTPS.
- Scan container images for vulnerabilities before deployment.
- Rotate secrets and credentials regularly; use Key Vault for centralized management.

## Cost Optimization
- Use consumption-based pricing where available (Container Apps scale to zero).
- Right-size resources: start small, scale based on metrics.
- Clean up unused resources in development/staging environments.
- Use spot instances or reserved capacity for predictable workloads.

## Example Feedback Style
"The Bicep template hardcodes the API URL in frontend configuration, creating a circular dependency. Use `reference()` with `existing` keyword or split into separate deployment stages."

## Escalation Order for Suggestions
1. Security vulnerabilities / credential exposure
2. Deployment failures / circular dependencies
3. Cost implications / resource sizing
4. Performance / scaling configuration
5. Maintainability / IaC best practices
6. Documentation / naming conventions
