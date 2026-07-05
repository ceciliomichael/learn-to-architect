# Challenge 01: Configuring Module Resolution and Path Aliases

In large enterprise software systems, codebases often grow to hundreds of folders and thousands of files. When developers rely on old-school relative import paths, moving or refactoring files becomes a nightmare. This challenge tests your ability to configure **Path Aliases** in `tsconfig.json` and refactor fragile relative imports into clean, maintainable absolute imports.

## The Scenario

Imagine you have just joined an engineering team building an enterprise e-commerce platform. You open a controller file located at `src/app/controllers/userController.ts` and see the following messy, error-prone relative imports:

```typescript
// Fragile relative imports in src/app/controllers/userController.ts:
import { UserProfile, UserRole } from '../../../../domain/models/userProfile';
import { AuthenticationService } from '../../../../infrastructure/services/authenticationService';
import { DatabaseConnection } from '../../../../infrastructure/database/connection';
import { formatDate, parseTimestamp } from '../../../../common/utilities/dateFormatters';
```

Every time a developer moves a controller file to a new subfolder, every single `../../../../` relative path breaks! Your chief architect has asked you to configure path aliases in `tsconfig.json` and refactor the controller file to use clean absolute imports.

## Your Task

Write your complete solution directly inside the **ANSWER HERE** block below. Your solution must include three distinct sections:

1. **Section 1: `tsconfig.json` Configuration**
   - Write a complete `tsconfig.json` file that defines `baseUrl` as `"."` (the project root).
   - Configure the `paths` compiler option to map the following clean aliases:
     - `@/*` pointing to `src/*`
     - `@models/*` pointing to `src/domain/models/*`
     - `@services/*` pointing to `src/infrastructure/services/*`
     - `@database/*` pointing to `src/infrastructure/database/*`
     - `@utils/*` pointing to `src/common/utilities/*`

2. **Section 2: Refactored Controller File (`src/app/controllers/userController.ts`)**
   - Rewrite the four import statements shown in the scenario using your newly configured path aliases.
   - Write a complete, production-ready class named `UserController` that utilizes these imported symbols to authenticate a user, fetch their profile from the database, format their registration timestamp, and log the result. Provide exhaustive type annotations and error handling.

3. **Section 3: Deep Technical Explanation**
   - In plain, professional engineering English, explain *why* deep relative import paths (`../../../`) break during automated refactoring and team collaboration.
   - Detail how TypeScript's `baseUrl` and `paths` resolution mechanism operates under the hood during the compilation phase.
   - Explain the critical difference between compile-time path resolution in TypeScript and runtime module resolution in JavaScript engines (such as Node.js or browser bundlers like Vite and Webpack). What tool or configuration is required at runtime to ensure Node.js understands `@models/`?

---

## ANSWER HERE

### Section 1: `tsconfig.json` Configuration

```json
// Write your complete tsconfig.json here:
{
  "compilerOptions": {

  }
}
```

### Section 2: Refactored Controller File (`src/app/controllers/userController.ts`)

```typescript
// Write your clean path alias imports and UserController class here:
```

### Section 3: Deep Technical Explanation

> **Why relative import paths break during refactoring:**
> 

> **How TypeScript's `baseUrl` and `paths` resolution works under the hood:**
> 

> **Compile-time resolution vs. runtime execution in Node.js and bundlers:**
> 
