# Exercise Solution: Build, Configure, Deploy, and Choose an SSR Boundary

```ts
import { z } from "zod";
const PublicEnvironment = z.object({ VITE_API_BASE_URL: z.string().url() });
export const publicEnvironment = PublicEnvironment.parse(import.meta.env);
```

## Why this works

Build and type-check the production application, validate environment configuration, expose only public client values, test the deployed artifact, and choose SSR only when its server and hydration costs solve a real need. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.