# Question 05 Answer: Module Resolution, Path Aliases (`@/*`), and Node.js ESM `.js` Extension

This document provides the exhaustive, deeply technical reference answer for Question 05, explaining TypeScript's module resolution algorithm, compile-time vs. runtime behavior, and native Node.js ES Module rules.

---

### 1. Step-by-Step Compiler Resolution Algorithm for Path Aliases
When the TypeScript compiler (`tsc`) evaluates the import statement `import { UserProfile } from '@models/userProfile'` inside `src/app/server.ts`, it executes a rigorous, multi-step module resolution algorithm:
1. **Identify Non-Relative Import**: The compiler observes that `@models/userProfile` does not start with `./`, `../`, or `/`. It is classified as a non-relative module import.
2. **Consult `baseUrl`**: The compiler checks `compilerOptions.baseUrl` in `tsconfig.json`. Finding `"baseUrl": "."`, it establishes the absolute filesystem path of the project root directory as the starting point for all path alias evaluations.
3. **Scan `paths` Mapping Table**: The compiler iterates through the key-value pairs defined in `compilerOptions.paths`. It attempts to match the import string `@models/userProfile` against pattern keys.
4. **Execute Wildcard Capture and Substitution**: The import string matches the pattern key `@models/*`. The wildcard asterisk (`*`) captures the trailing substring `"userProfile"`. The compiler substitutes this captured string into the corresponding target mapping array: `src/domain/models/*` becomes `src/domain/models/userProfile`.
5. **Perform Filesystem Probe**: Relative to `baseUrl`, the compiler probes the physical filesystem in a specific extension order to locate the target file:
   - Probes for `src/domain/models/userProfile.ts` (Found! Resolves type signatures).
   - If not found, probes for `src/domain/models/userProfile.tsx`.
   - If not found, probes for `src/domain/models/userProfile.d.ts`.
   - If not found, probes for a package/barrel directory: `src/domain/models/userProfile/package.json` or `src/domain/models/userProfile/index.ts`.

---

### 2. Compile-Time vs. Runtime Behavior and Emitted JavaScript

**Why `paths` is Strictly a Compile-Time Feature**: A fundamental rule of TypeScript architecture is that **the TypeScript compiler (`tsc`) does NOT rewrite, transform, or resolve path aliases when emitting runtime JavaScript files by default!** TypeScript uses `paths` strictly to verify type safety during compilation.

**Emitted JavaScript String**: When `tsc` compiles `src/app/server.ts` into JavaScript (`dist/app/server.js`), the literal import string `@models/userProfile` is emitted verbatim without modification:
```javascript
// Emitted JavaScript file (dist/app/server.js):
import { UserProfile } from "@models/userProfile"; // OR: const userProfile_1 = require("@models/userProfile");
```

**Runtime Consequence in Native Node.js**: If you execute this compiled file directly in native Node.js (`node dist/app/server.js`), Node.js will crash immediately with a fatal runtime exception:
```text
Error: Cannot find module '@models/userProfile'
```
**Why Node.js Crashes**: Native Node.js has no knowledge of `tsconfig.json` or your virtual path aliases! When Node.js sees `@models/userProfile`, it assumes `@models` is an npm package inside the `node_modules/` directory. Finding no such package, it throws a module not found error. To run path aliases in production Node.js, you must use a runtime resolver like `tsconfig-paths` (`node -r tsconfig-paths/register dist/app/server.js`) or run a build-time rewriter like `tsc-alias` after running `tsc` to physically rewrite `@models/` into relative paths like `../../domain/models/` in the emitted `.js` files.

---

### 3. Why Native Node.js ES Modules Require Explicit `.js` Extensions
When running modern Node.js using native ES Modules (`"type": "module"` in `package.json`), **you must explicitly include the `.js` file extension in all relative import paths**, even when writing source code inside a `.ts` TypeScript file:
```typescript
// Required syntax in native Node.js ES Modules:
import { calculateTax } from './finance/taxCalculator.js';
```
**The Engineering Reason**: 
1. **Strict ECMAScript Specification Compliance**: In the official ES Module specification adopted by web browsers and Node.js, import specifiers are treated as literal URLs or exact file paths. Unlike legacy CommonJS (`require()`), native ES Module loaders **do not perform automatic extension guessing or directory indexing** (such as trying `.js`, `.json`, or `/index.js`). An import must point to an exact, fully qualified filename on disk.
2. **Why You Write `.js` Instead of `.ts`**: You must write `.js` (rather than `.ts`) in your TypeScript source code because **import paths must reflect the filename that will exist at runtime after compilation!** When TypeScript compiles your project, `taxCalculator.ts` is emitted to disk as `taxCalculator.js`. If you wrote `import ... from './taxCalculator.ts'`, Node.js would attempt to load a `.ts` file at runtime in production and fail! TypeScript intentionally designed its compiler to require `.js` extensions in ESM mode to ensure 100% runtime compatibility with native Node.js.

---

### 4. How Frontend Bundlers Handle Module Resolution Differently
When developing frontend applications using web bundlers such as **Vite**, **Next.js**, **Webpack**, or **Esbuild**, developers can omit file extensions (`import { calc } from './math'`) and use path aliases (`@/components/Button`) without installing runtime tools like `tsconfig-paths`.

**Why Bundlers Work Differently**:
1. **Integrated Build-Time Pipeline**: Unlike native Node.js, which executes emitted JavaScript files directly off the filesystem, modern frontend bundlers execute an integrated compilation and bundling pipeline before code ever reaches the browser.
2. **Automatic `tsconfig.json` Ingestion**: Modern bundlers natively read and parse your project's `tsconfig.json` file during the initialization phase. Their internal module resolution engines automatically ingest your `baseUrl` and `paths` mappings.
3. **Virtual Module Resolution and Bundling**: When Vite or Webpack encounters `import { Button } from '@/components/Button'`, the bundler's internal resolver automatically maps `@/` to `src/`, probes disk for `.ts`, `.tsx`, `.js`, and `/index.ts` extensions automatically, compiles the TypeScript code in memory, and bundles all dependencies into a single, optimized JavaScript payload. Because the bundler resolves all paths during the build process, runtime browser engines never encounter raw path aliases or missing extensions.
