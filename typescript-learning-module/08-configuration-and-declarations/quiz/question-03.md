# Question 03: Script vs Module Mode

What turns a TypeScript file from script mode into module mode?

```typescript
// File A  -  no imports or exports at all:
const greeting = "Hello";

// File B  -  has an import:
import { something } from "./other";
const greeting = "Hello";
```

1. In File A, is `greeting` scoped to this file or available globally across all files? Why?
2. In File B, is `greeting` scoped to this file or available globally? Why?
3. If File A and File C both declare `const greeting`, what happens? What error occurs if any?
4. What is the simplest thing you can add to File A to turn it into a module with isolated scope (without importing anything)?

## ANSWER HERE

> **File A  -  is `greeting` global or file-scoped?**

> **File B  -  is `greeting` global or file-scoped?**

> **What happens if two script files declare the same variable?**

> **Simplest way to make File A a module:**
