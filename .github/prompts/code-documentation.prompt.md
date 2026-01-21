---
mode: 'agent'
description: 'Generate and improve code documentation (JSDoc, inline comments, README updates)'
tools: ['changes', 'codebase', 'editFiles', 'findTestFiles', 'problems', 'search', 'usages']
---

# 📚 Code Documentation Generator

## 🎯 Objective
Analyze the codebase and generate comprehensive documentation including JSDoc comments, inline documentation, and type annotations to improve code readability and maintainability.

## 📋 Documentation Scope

### 1. **API Layer** (`api/src/`)

#### Routes (`api/src/routes/*.ts`)
- Add JSDoc comments for each route handler
- Document request parameters, query strings, and body schemas
- Document response types and status codes
- Include usage examples where helpful

```typescript
/**
 * Get all products with optional filtering
 * @route GET /api/products
 * @param {string} [req.query.supplierId] - Filter by supplier ID
 * @returns {Product[]} 200 - Array of products
 * @returns {Error} 500 - Internal server error
 */
```

#### Models (`api/src/models/*.ts`)
- Document all interface properties
- Add descriptions for complex fields
- Include validation constraints

```typescript
/**
 * Represents a product in the supply chain
 */
export interface Product {
  /** Unique identifier for the product */
  productId: number;
  /** Reference to the supplying vendor */
  supplierId: number;
  /** Human-readable product name */
  name: string;
  /** Stock Keeping Unit - must be unique */
  sku: string;
  /** Price in USD (before discount) */
  price: number;
  /** Discount percentage (0.0 to 1.0) */
  discount?: number;
}
```

#### Repositories (`api/src/repositories/*.ts`)
- Document all public methods
- Explain SQL query logic for complex operations
- Document return types and error conditions

#### Utilities (`api/src/utils/*.ts`)
- Document helper functions with input/output examples
- Explain error handling utilities

### 2. **Frontend Layer** (`frontend/src/`)

#### Components (`frontend/src/components/**/*.tsx`)
- Add component-level JSDoc with purpose and usage
- Document props with PropTypes or TypeScript interfaces
- Include example usage in complex components

```tsx
/**
 * ProductCard displays a single product with image, price, and add-to-cart action
 * 
 * @example
 * <ProductCard 
 *   product={productData} 
 *   onAddToCart={(id) => handleAdd(id)} 
 * />
 */
interface ProductCardProps {
  /** Product data to display */
  product: Product;
  /** Callback when user clicks add to cart */
  onAddToCart: (productId: number) => void;
}
```

#### Context (`frontend/src/context/*.tsx`)
- Document context purpose and provided values
- Explain state management patterns
- Document custom hooks

#### API Client (`frontend/src/api/*.ts`)
- Document all API functions
- Include request/response types
- Document error handling

### 3. **Database Layer** (`api/sql/`)

#### Migrations (`api/sql/migrations/*.sql`)
- Add header comments explaining migration purpose
- Document table relationships and constraints
- Explain index strategies

#### Seed Data (`api/sql/seed/*.sql`)
- Document seed data purpose
- Explain data relationships

## ✅ Documentation Standards

### JSDoc Requirements
- Use `@param` for all function parameters
- Use `@returns` for return values
- Use `@throws` for error conditions
- Use `@example` for complex functions
- Use `@see` for related functions/files

### Inline Comments
- Explain "why" not "what" for complex logic
- Document workarounds with issue references
- Mark TODO items with owner and date

### Type Documentation
- All interfaces should have descriptions
- Complex types need property-level docs
- Use union types with documentation

## 🚀 Execution Steps

1. **Scan** the target directory for undocumented code
2. **Analyze** existing patterns and conventions
3. **Generate** appropriate documentation following standards
4. **Validate** documentation completeness
5. **Update** any related README files if needed

## 📁 Priority Order
1. Public API routes (highest user impact)
2. Shared models and types
3. Repository methods
4. React components
5. Utility functions
6. Internal/private code
