# Challenge 01: Solution

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "CommonJS",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "skipLibCheck": true,
    "esModuleInterop": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

**Explanation of each option:**

- `target: "ES2020"`  -  Tells TypeScript which version of JavaScript to output. ES2020 supports modern features like optional chaining and nullish coalescing.
- `module: "CommonJS"`  -  Specifies the module system. CommonJS uses `require()` and `module.exports`, which is what Node.js uses.
- `outDir: "./dist"`  -  All compiled `.js` files will be placed in the `dist/` folder, keeping your source and output separate.
- `rootDir: "./src"`  -  TypeScript will only compile `.ts` files inside the `src/` folder.
- `strict: true`  -  Enables a collection of strict checks including `strictNullChecks`, `noImplicitAny`, and others. Highly recommended.
- `skipLibCheck: true`  -  Skips type-checking of `.d.ts` files inside `node_modules`. Speeds up compilation and avoids errors in third-party libraries.
- `esModuleInterop: true`  -  Allows you to import CommonJS modules using standard ES module syntax (`import fs from 'fs'` instead of `import * as fs from 'fs'`).
- `include: ["src/**/*"]`  -  Only files inside the `src/` directory (recursively) are included in compilation.
- `exclude: ["node_modules"]`  -  Prevents TypeScript from trying to compile the packages in `node_modules`.
