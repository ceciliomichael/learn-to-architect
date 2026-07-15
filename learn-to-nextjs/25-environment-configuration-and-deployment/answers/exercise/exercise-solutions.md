# Exercise Solution: Environment Configuration and Deployment

```tsx
import { z } from "zod";
const Environment = z.object({ DATABASE_URL: z.string().url(), SESSION_SECRET: z.string().min(32) });
export const environment = Environment.parse(process.env);
```

## Why this works

Validate environment variables on the server, expose only explicitly public values, build in the deployment target, and document migrations, health checks, and rollback. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.