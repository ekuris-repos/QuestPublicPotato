---
description: "Scaffold a complete new domain entity across all layers"
---
# Add New Entity

Scaffold all artifacts for a new domain entity in the OctoCAT Supply system.

## Input Required
Provide:
- Entity name (singular, e.g., `Warehouse`)
- Key attributes and types
- Relationships to existing entities (FK references)

## Artifacts to Generate

### 1. Database Migration
Create `api/sql/migrations/NNN_create_<entity>.sql`:
- Use next sequential number
- Define table with `id INTEGER PRIMARY KEY AUTOINCREMENT`
- Add foreign keys with explicit `ON DELETE` behavior
- Create indexes on FK columns and common filter fields
- Use `snake_case` for all column names

### 2. Seed Data
Create `api/sql/seed/NNN_<entity>.sql`:
- Add 3-5 representative rows with explicit IDs
- Ensure referential integrity with existing seeds
- Keep data realistic but minimal

### 3. TypeScript Model
Add interface to `api/src/models/` or extend existing file:
- Use `camelCase` property names
- Include `id` as `number`
- Add JSDoc comments for non-obvious fields

### 4. Repository
Create `api/src/repositories/<entity>Repo.ts`:
- Implement: `findAll`, `findById`, `create`, `update`, `delete`
- Add entity-specific queries (e.g., `findByStatus`, `findByParentId`)
- Use parameterized SQL exclusively
- Map `snake_case` ↔ `camelCase` consistently
- Throw `NotFoundError`, `ValidationError`, `ConflictError` appropriately

### 5. Express Routes
Create `api/src/routes/<entity>.ts`:
- RESTful endpoints: `GET /`, `GET /:id`, `POST /`, `PUT /:id`, `DELETE /:id`
- Add Swagger JSDoc comments at top of file
- Validate request bodies before repository calls
- Register routes in `api/src/index.ts`

### 6. Update Swagger Spec
Modify `api/api-swagger.json`:
- Add path definitions for new endpoints
- Add schema definition for the entity
- Include request/response examples

## Patterns to Follow
Reference these existing implementations:
- `api/sql/migrations/001_initial_schema.sql`
- `api/src/repositories/suppliersRepo.ts`
- `api/src/routes/suppliers.ts`

## Checklist Before Done
- [ ] Migration file numbered sequentially
- [ ] Seed data respects FK order
- [ ] Repository has unit test file
- [ ] Routes registered in main app
- [ ] Swagger spec validates (`npm run swagger:validate` if available)
