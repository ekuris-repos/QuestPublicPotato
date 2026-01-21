# Plan: Comprehensive Unit Test Coverage Enhancement

This plan addresses critical testing gaps across the TypeScript monorepo, targeting ~8% API coverage and 0% frontend unit coverage. We'll prioritize high-impact areas—untested repositories, routes, utilities—and establish frontend component testing infrastructure.

## Steps

1. **Add API repository unit tests** for the 7 untested repositories ([productsRepo.ts](api/src/repositories/productsRepo.ts), [ordersRepo.ts](api/src/repositories/ordersRepo.ts), [branchesRepo.ts](api/src/repositories/branchesRepo.ts), etc.) following the existing [suppliersRepo.test.ts](api/src/repositories/suppliersRepo.test.ts) pattern with mocked database instances

2. **Add API route integration tests** for 8 untested routes ([products.ts](api/src/routes/products.ts), [suppliers.ts](api/src/routes/suppliers.ts), [orders.ts](api/src/routes/orders.ts), etc.) using the in-memory SQLite + Supertest pattern from [branch.test.ts](api/src/routes/branch.test.ts)

3. **Test critical SQL utilities and error handling** in [dbHelpers.ts](api/src/utils/dbHelpers.ts) (`buildWhereClause`, `toCamelCase`, `toSnakeCase`) and [errors.ts](api/src/utils/errors.ts) (custom error classes, `errorHandler` middleware, `handleDatabaseError`) with new unit test files

4. **Establish frontend unit testing infrastructure** by creating `frontend/vitest.config.ts` for jsdom environment, adding `test` script to [frontend/package.json](frontend/package.json), then writing component tests for critical UI ([Products.tsx](frontend/src/components/Products.tsx), [Navigation.tsx](frontend/src/components/Navigation.tsx), [OrderForm.tsx](frontend/src/components/OrderForm.tsx)) using React Testing Library

5. **Create shared test utilities** including entity factory functions for common test data (Product, Order, Supplier), database setup/teardown helpers, and mock data generators to reduce duplication across test files

## Further Considerations

1. **Coverage targets**: Aim for 80% repository/route coverage, 70% utilities, 60% components—enforce via CI thresholds. Should we add coverage gates immediately or after initial tests?

2. **Testing order**: Start with API repositories → routes → utilities → frontend setup → components, or prioritize differently based on risk areas?

3. **Test data strategy**: Use hard-coded fixtures, factory functions (e.g., `faker.js`), or database seed subsets? Current tests mix approaches inconsistently.
