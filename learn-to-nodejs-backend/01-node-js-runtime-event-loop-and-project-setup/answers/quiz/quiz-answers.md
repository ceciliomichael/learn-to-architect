# Quiz Answers: Node.js Runtime, Event Loop, and TypeScript Project Setup

1. TypeScript checks and compiles the source. `@types/node` describes Node.js APIs. `tsx` transforms and executes TypeScript conveniently during development.
2. Development execution does not replace a complete static check. `tsc --noEmit` reports type errors across the included project without generating output.
3. `rootDir` identifies authored TypeScript source. `outDir` keeps generated JavaScript separate in `dist`.
4. Promise callbacks enter the microtask queue, which is drained after the current stack before the event loop takes the eligible timer callback.
5. Commit source, configuration, `package.json`, and `package-lock.json`. Regenerate `node_modules` with installation and `dist` with the build.
