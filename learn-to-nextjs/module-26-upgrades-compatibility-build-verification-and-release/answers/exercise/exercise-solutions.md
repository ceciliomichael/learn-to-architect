# Exercise Solution: Upgrades, Compatibility, Build Verification, and Release

```tsx
// package.json scripts used by the release check
const releaseCommands = ["npm run lint", "npm run typecheck", "npm test", "npm run build"] as const;
```

## Why this works

Upgrade dependencies intentionally, read official migration notes, verify supported runtimes, and run linting, type checks, tests, and a production build before release. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.