# Challenge 01: Write a tsconfig.json from Scratch

Prove you understand what each `tsconfig.json` option does.

## Your Task

Write a complete `tsconfig.json` for a Node.js TypeScript project. Then, beneath the JSON block, write a comment for each option explaining what it does in plain English.

The config must include:
- `target`: ES2020
- `module`: CommonJS (used by Node.js)
- `outDir`: `./dist` (compiled JS files go here)
- `rootDir`: `./src` (TypeScript source files are here)
- `strict`: true
- `skipLibCheck`: true
- `esModuleInterop`: true
- `include`: only files inside `src/`
- `exclude`: `node_modules/`

## ANSWER HERE

```json
{
  "compilerOptions": {

  },
  "include": [],
  "exclude": []
}
```

---

> **Explanation of each option (write one sentence per option):**
