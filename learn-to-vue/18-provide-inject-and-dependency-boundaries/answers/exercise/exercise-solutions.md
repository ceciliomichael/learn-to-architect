# Exercise Solution: Provide, Inject, and Dependency Boundaries

```ts
import type { InjectionKey, Ref } from "vue";
export const ThemeKey: InjectionKey<Ref<"light" | "dark">> = Symbol("theme");
```

## Why this works

Provide and inject pass a dependency through a component subtree. Use typed keys, stable service contracts, and an intentional provider boundary. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.