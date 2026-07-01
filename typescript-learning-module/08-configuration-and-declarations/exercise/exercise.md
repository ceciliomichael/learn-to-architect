# Module 08 Exercise: tsconfig.json & Declaration Files

Complete your code directly inside the **ANSWER HERE** blocks below.

---

### Challenge 1: Configuring `tsconfig.json`
Write a `tsconfig.json` configuration file that implements the following best practices:
1. Target ES2020 output.
2. Put compiled JS files into `./dist`.
3. Read TS source files from `./src`.
4. Enable all strict type-checking options (`"strict": true`).
5. Skip checking types in `node_modules` for build performance (`"skipLibCheck": true`).

#### ✍️ ANSWER HERE:
```json
// Write your tsconfig.json configuration here:


```

---

### Challenge 2: Writing a Declaration File (`.d.ts`)
Imagine you imported a legacy JavaScript utility script `analytics.js` into your app that doesn't have built-in TypeScript support. It exposes a global object `window.Analytics` with two methods:
1. `init(apiKey: string): void`
2. `trackEvent(eventName: string, metadata?: Record<string, any>): boolean`

Write a declaration file `analytics.d.ts` that defines global type definitions for `window.Analytics`.

#### ✍️ ANSWER HERE:
```typescript
// Write your analytics.d.ts definitions here:


```

---

### Challenge 3: Isolating Module Scope
Create a file called `script.ts` with `const myGlobalVar = "hello";`.
Why does TypeScript throw a duplicate identifier error if another file also declares `const myGlobalVar = "world";`?
Add the exact one-line statement needed at the top of `script.ts` to convert it from a global script into an isolated ES Module.

#### ✍️ ANSWER HERE:
```typescript
// Write the exact one-line statement here:


```
