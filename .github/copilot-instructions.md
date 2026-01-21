# OctoCAT Supply Chain Management Application – General Copilot Instructions

These are repository-wide guidelines. Path‑scoped files in `.github/instructions/*.instructions.md` provide focused guidance for specific areas:

| Instruction File | Scope |
|------------------|-------|
| [`api.instructions.md`](instructions/api.instructions.md) | `api/src/**/*.ts`, API routes, Swagger |
| [`database.instructions.md`](instructions/database.instructions.md) | Migrations, seeds, DB layer |
| [`frontend.instructions.md`](instructions/frontend.instructions.md) | React components, Vite config, Tailwind |
| [`infrastructure.instructions.md`](instructions/infrastructure.instructions.md) | Docker, Bicep, CI/CD workflows |

## Available Skills

Skills provide focused expertise on specific topics. Reference these when needed:

| Skill | When to Use |
|-------|------------|
| [`start-demo-app`](skills/start-demo-app/SKILL.md) | Starting the application, troubleshooting startup issues, environment setup |
| [`show-your-work`](skills/show-your-work/SKILL.md) | Explaining reasoning, debugging complex issues, architectural decisions |

## High-Level Architecture
TypeScript monorepo with:
- `api/` — Express REST API (SQLite persistence, repository pattern, Swagger docs)
- `frontend/` — React + Vite + Tailwind UI
- `infra/` — Bicep IaC for Azure Container Apps
- `docs/` — Architecture decisions, build guides, design assets
- `demo/` — Walkthrough scripts and patch sets for demos

Refer to [`docs/architecture.md`](../docs/architecture.md) and [`docs/sqlite-integration.md`](../docs/sqlite-integration.md) for deeper details. Avoid restating them in reviews and link instead.

## General Review Guidance
When generating suggestions:
1. Prefer incremental, minimal diffs; preserve existing style and naming.
2. Surface security, correctness, and data integrity issues before micro-optimizations.
3. Encourage type safety (no `any` unless justified). Suggest adding/refining model or DTO types when gaps appear.
4. Flag duplicate logic that belongs in a shared utility or repository method.
5. Ensure error handling uses existing custom error types where appropriate (e.g., `NotFoundError`, `ValidationError`, `ConflictError`) and propagates consistent HTTP status codes via middleware.
6. Encourage tests: request unit tests for new repository logic and component tests (React Testing Library) for critical UI paths.
7. For performance concerns, highlight N+1 query patterns, unnecessary data loading, or large bundle additions.
8. Prefer environment variable driven configuration; avoid hard‑coded paths/secrets.
9. Ensure accessibility: semantic HTML, keyboard navigation, ARIA labels where needed.

## Naming Conventions
Maintain consistency across the codebase:
- **TypeScript/JavaScript**: `camelCase` for variables/functions, `PascalCase` for classes/components/types
- **SQL columns**: `snake_case` (mapped automatically in repositories)
- **Files**: `kebab-case` for components (`order-list.tsx`), `camelCase` for utilities (`formatCurrency.ts`)
- **Environment variables**: `SCREAMING_SNAKE_CASE`

## Commit & PR Guidelines
- Use conventional commit prefixes: `feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`
- Keep commits atomic—one logical change per commit
- PR titles should summarize the change; descriptions should link related issues
- Include `Closes #<issue>` when resolving an issue

## Monorepo Workflow

### Using VS Code Tasks (Preferred)
When building, running, or applying demo patches, prefer using VS Code tasks over direct terminal commands to avoid conflicts:

**Build Tasks:**
- Use task: `Build All` instead of `npm run build`
- Use task: `Build API` instead of `npm run build --workspace=api`
- Use task: `Build Frontend` instead of `npm run build --workspace=frontend`

**Development Tasks:**
- Use task: `Start All Services` instead of running `npm run dev:api` and `npm run dev:frontend` separately
- Use task: `Start API` for API-only development
- Use task: `Start Frontend` for frontend-only development

**Demo Patch Tasks:**
- Use task: `GHAS: Inject Secrets` instead of running `./demo/resources/apply_patch_set.sh secret-scanning ...`
- Use task: `GHAS: Inject Dependabot Vulnerable Action` instead of manually applying Dependabot patches
- Use task: `Copilot: Self-Healing DevOps` for DevOps demo setup
- Use task: `Copilot: Custom Instructions` for custom instructions demo

**When to use terminal commands:**
- Direct npm commands in non-conflicting contexts (e.g., `npm test`, `npm audit`)
- Git operations
- Database operations: `npm run db:init --workspace=api`, `npm run db:migrate --workspace=api`, `npm run db:seed --workspace=api`
- Custom one-off commands not covered by tasks

### Traditional Workflow (when tasks unavailable)
- Build frequently: `npm run build --workspace=api` or `--workspace=frontend` (root build runs both)
- Run tests: `npm test --workspace=api` or `npm test --workspace=frontend`
- Lint all workspaces: `npm run lint` (from root)
- Add dependencies to specific workspace: `npm install <pkg> --workspace=api`
- Keep PRs scoped: code + tests + docs (architecture or build notes) when behavior changes
- Update related instruction files if new folders or architectural slices are introduced

## Dependency Management
- Pin major versions in `package.json`; use `^` for patch/minor updates
- Audit dependencies periodically: `npm audit`
- Avoid adding redundant packages—check if functionality exists in current deps first
- Document any non-obvious dependencies in the relevant instruction file

## Do Not Repeat
Do not inline full API route or component files in review feedback unless absolutely necessary: quote only the lines requiring change. Summarize low‑impact nits.

## Escalation Order for Suggestions
1. Security / data integrity
2. Logical / functional correctness
3. Performance / scalability
4. Maintainability / duplication
5. Readability / consistency
6. Style / minor formatting

## Tone & Feedback Style
Be concise, actionable, and cite a rationale ("because" clause) for non-trivial recommendations. Offer one preferred solution; optionally a lightweight alternative.

---
If new subsystems are added (e.g., `mobile/`, `worker/`), create a new `*.instructions.md` with `applyTo` globs instead of bloating this file.
