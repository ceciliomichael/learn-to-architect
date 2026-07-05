# Challenge 01 Solution: Configuring Module Resolution and Path Aliases

This document provides the verified, production-grade reference solution for Challenge 01. It includes a complete `tsconfig.json` configuration, a refactored enterprise controller class, and an exhaustive technical explanation of TypeScript's module resolution mechanics.

---

## Section 1: `tsconfig.json` Configuration

To enable absolute path resolution and custom path aliases across an enterprise project, configure the `baseUrl` and `paths` compiler options inside `compilerOptions`.

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "lib": ["ES2022"],
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "outDir": "./dist",
    "rootDir": "./src",
    
    // ========================================================================
    // PATH ALIAS CONFIGURATION
    // ========================================================================
    // baseUrl sets the root directory for non-relative module names.
    // Setting it to "." means all path lookups start at the project root folder.
    "baseUrl": ".",
    
    // paths maps virtual prefix patterns to physical disk locations relative to baseUrl.
    "paths": {
      "@/*": ["src/*"],
      "@models/*": ["src/domain/models/*"],
      "@services/*": ["src/infrastructure/services/*"],
      "@database/*": ["src/infrastructure/database/*"],
      "@utils/*": ["src/common/utilities/*"]
    }
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

### Symbol-by-Symbol Configuration Breakdown
* **`baseUrl: "."`**: Establishes the base directory from which all non-relative imports and path alias mappings are resolved. Without `baseUrl`, TypeScript cannot evaluate `paths` rules.
* **`paths`**: A key-value mapping table where keys represent import aliases (using the wildcard `*` to capture filenames or subfolders) and values represent arrays of relative file paths on disk. If the first path in the array fails to resolve, TypeScript sequentially checks fallback paths in the array.

---

## Section 2: Refactored Controller File (`src/app/controllers/userController.ts`)

By leveraging our configured path aliases, we eliminate all fragile `../../../../` relative chains. Below is the production-ready `UserController` class implementing complete domain logic, strict type safety, and comprehensive error handling.

```typescript
// ============================================================================
// FILE: src/app/controllers/userController.ts
// ============================================================================

// Clean, bulletproof absolute imports using configured path aliases:
import { UserProfile, UserRole } from '@models/userProfile';
import { AuthenticationService } from '@services/authenticationService';
import { DatabaseConnection } from '@database/connection';
import { formatDate, parseTimestamp } from '@utils/dateFormatters';

/**
 * Interface defining the expected HTTP request payload for user authentication.
 */
export interface AuthenticationRequest {
  email: string;
  secretToken: string;
  requestTimestamp: string;
}

/**
 * Interface defining the standardized API response structure.
 */
export interface ControllerResponse<T> {
  success: boolean;
  statusCode: number;
  data?: T;
  errorMessage?: string;
  timestamp: string;
}

/**
 * Enterprise user controller responsible for handling authentication workflows
 * and retrieving formatted user profile records from the database.
 */
export class UserController {
  private readonly authService: AuthenticationService;
  private readonly dbConnection: DatabaseConnection;

  constructor(authService: AuthenticationService, dbConnection: DatabaseConnection) {
    this.authService = authService;
    this.dbConnection = dbConnection;
  }

  /**
   * Authenticates a user request, retrieves their database profile, and returns
   * a formatted API response.
   *
   * @param request The incoming authentication request payload.
   * @returns A promise resolving to a standardized controller response.
   */
  public async authenticateAndFetchProfile(
    request: AuthenticationRequest
  ): Promise<ControllerResponse<UserProfile>> {
    const currentFormattedTime = formatDate(new Date());

    try {
      // 1. Validate incoming request timestamp
      const parsedDate = parseTimestamp(request.requestTimestamp);
      const timeDifferenceMs = Math.abs(Date.now() - parsedDate.getTime());
      
      // Reject requests older than 5 minutes (300,000 milliseconds) to prevent replay attacks
      if (timeDifferenceMs > 300000) {
        return {
          success: false,
          statusCode: 401,
          errorMessage: "Authentication request timestamp expired or invalid.",
          timestamp: currentFormattedTime
        };
      }

      // 2. Perform authentication via domain service
      const isValidUser = await this.authService.verifyCredentials(
        request.email,
        request.secretToken
      );

      if (!isValidUser) {
        return {
          success: false,
          statusCode: 403,
          errorMessage: "Invalid email or secret authentication token.",
          timestamp: currentFormattedTime
        };
      }

      // 3. Query user profile from database connection
      const userProfile = await this.dbConnection.findUserByEmail(request.email);

      if (!userProfile) {
        return {
          success: false,
          statusCode: 404,
          errorMessage: `User profile not found for email: ${request.email}`,
          timestamp: currentFormattedTime
        };
      }

      // 4. Return successful payload
      return {
        success: true,
        statusCode: 200,
        data: userProfile,
        timestamp: currentFormattedTime
      };

    } catch (error: unknown) {
      const exceptionMessage = error instanceof Error ? error.message : "An unexpected system error occurred.";
      
      return {
        success: false,
        statusCode: 500,
        errorMessage: `Internal server error during authentication workflow: ${exceptionMessage}`,
        timestamp: currentFormattedTime
      };
    }
  }
}
```

---

## Section 3: Deep Technical Explanation

### Why Relative Import Paths Break During Refactoring
In deeply nested project structures, relative import paths like `../../../../domain/models/userProfile` represent a mechanical instruction set based on **physical folder traversal** rather than conceptual domain identity. 

When an engineer moves `userController.ts` from `src/app/controllers/` to a specialized subfolder like `src/app/controllers/admin/workflows/`, the relative distance to the root folder changes from 4 levels deep (`../../../../`) to 6 levels deep (`../../../../../../`). As a result, every single import statement in the file immediately breaks and throws a compiler error! Furthermore, when reading a code review or pull request, a developer cannot quickly determine what module is being imported without manually counting directory levels. Path aliases solve this by decoupling the consumer's location from the target module's location.

### How TypeScript's `baseUrl` and `paths` Resolution Works Under the Hood
When the TypeScript compiler (`tsc`) encounters an import statement such as `import { UserProfile } from '@models/userProfile'`, it executes a systematic module resolution algorithm:
1. **Check for Relative/Absolute Syntax**: The compiler observes that `@models/userProfile` does not begin with `./`, `../`, or `/`. It is a non-relative module import.
2. **Consult `baseUrl`**: The compiler looks up `baseUrl` in `tsconfig.json`, establishing the project root (`.`) as the starting point for pattern evaluation.
3. **Evaluate `paths` Pattern Matching**: The compiler scans the `paths` key-value mappings in order. It matches the prefix `@models/` against the pattern `@models/*`.
4. **Wildcard Substitution**: The wildcard `*` captures the string `"userProfile"`. The compiler substitutes this captured string into the target mapping array: `src/domain/models/*` becomes `src/domain/models/userProfile`.
5. **Physical Disk Verification**: The compiler checks the filesystem relative to `baseUrl` for `src/domain/models/userProfile.ts`, `src/domain/models/userProfile.tsx`, `src/domain/models/userProfile.d.ts`, or `src/domain/models/userProfile/index.ts`. Once found, the type definitions are imported and validated.

### Compile-Time Resolution vs. Runtime Execution in Node.js and Bundlers
This is the most critical conceptual trap for intermediate TypeScript developers: **TypeScript's `paths` option is strictly a compile-time type-resolution tool. By default, the TypeScript compiler (`tsc`) DOES NOT rewrite or transform import paths when emitting JavaScript files!**

When `tsc` compiles `userController.ts` into JavaScript (`userController.js`), the emitted code still contains the literal string:
```javascript
// Emitted JavaScript file (userController.js):
const userProfile_1 = require("@models/userProfile"); // OR: import { UserProfile } from '@models/userProfile';
```

If you execute this compiled file directly in native Node.js (`node dist/app/controllers/userController.js`), Node.js will crash immediately with the runtime error:
```text
Error: Cannot find module '@models/userProfile'
```
Why? Because native Node.js has no knowledge of your `tsconfig.json` aliases! To solve this mismatch in production environments, you must implement one of three standard architectural solutions:
1. **Runtime Alias Resolvers (Node.js)**: Use a runtime loader such as `tsconfig-paths` when executing Node.js (`node -r tsconfig-paths/register dist/index.js`). This library intercepts Node's module loading engine and resolves `@models/` to physical disk paths at runtime.
2. **Build-Time Path Rewriters**: Run a post-compilation tool like `tsc-alias` immediately after running `tsc`. This tool scans your emitted `./dist` folder and physically rewrites `@models/userProfile` into relative paths like `../../domain/models/userProfile` in the final `.js` files.
3. **Modern Frontend & Backend Bundlers**: When using build bundlers like **Vite**, **Webpack**, **Esbuild**, or **Next.js**, the bundler's internal plugin system reads `tsconfig.json` directly and resolves path aliases automatically during the bundling process, emitting a single self-contained JavaScript file with correct internal references.
