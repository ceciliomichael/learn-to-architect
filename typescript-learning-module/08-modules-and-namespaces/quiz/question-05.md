# Question 05: Module Resolution, Path Aliases (`@/*`), and Node.js ESM `.js` Extension

Navigating module resolution mechanics and runtime execution differences across Node.js, TypeScript, and modern frontend bundlers is an essential skill for senior engineers.

Consider the following `tsconfig.json` snippet from an enterprise project:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "baseUrl": ".",
    "paths": {
      "@models/*": ["src/domain/models/*"],
      "@utils/*": ["src/common/utilities/*"]
    }
  }
}
```

A developer writes the following import in `src/app/server.ts`:
```typescript
import { UserProfile } from '@models/userProfile';
import { calculateTax } from './finance/taxCalculator';
```

## Your Challenge

Answer the following four architectural questions directly inside the **ANSWER HERE** block below. Do not use em dashes anywhere in your response!

1. Explain the step-by-step resolution algorithm the TypeScript compiler (`tsc`) follows to locate the physical file for `@models/userProfile` on disk using `baseUrl` and `paths`.
2. Why is TypeScript's `paths` option strictly a **compile-time** type resolution feature? When `tsc` compiles `src/app/server.ts` to `dist/app/server.js`, what exact literal string is written for the `@models/userProfile` import in the emitted JavaScript file? What happens if you run `node dist/app/server.js` directly without runtime alias tools?
3. When running modern native Node.js using ES Modules (`"type": "module"` in `package.json`), why must you explicitly include the **`.js` file extension** in relative import paths (for example, `import { calculateTax } from './finance/taxCalculator.js'`) even when writing source code inside a `.ts` TypeScript file?
4. Why do frontend web bundlers (like Vite, Next.js, or Webpack) allow developers to omit `.js` and `.ts` file extensions and resolve path aliases automatically without requiring runtime tools like `tsconfig-paths`?

---

## ANSWER HERE

### 1. Step-by-step compiler resolution algorithm for path aliases:
> 

### 2. Compile-time vs. runtime behavior and emitted JavaScript:
> **Emitted JavaScript string:**
> 

> **Runtime consequence in native Node.js:**
> 

### 3. Why native Node.js ES Modules require explicit `.js` extensions:
> 

### 4. How frontend bundlers handle module resolution differently:
> 
