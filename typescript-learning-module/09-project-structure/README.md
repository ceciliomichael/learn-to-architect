# Module 09: Project Structure and Clean Architecture

Knowing TypeScript syntax is one skill. Knowing how to organize a real project so that it stays maintainable as it grows is a completely different skill. This module covers the architecture decisions that separate junior from senior developers.

---

## 1. Why Structure Matters

When a project is small, one file works fine. As soon as you have multiple developers, hundreds of features, and thousands of lines of code, a monolithic single file becomes impossible to navigate, test, or modify without breaking something else.

Good project structure means
- Any developer can find the code for any feature within seconds.
- Changing one part of the system does not unexpectedly break another part.
- Individual pieces can be tested in isolation.
- New features can be added without touching unrelated code.

---

## 2. Standard TypeScript Project Structure

This is the folder layout used in most professional TypeScript projects
```text
my-app/
├── src/
│   ├── index.ts              # Application entry point. Only orchestration goes here.
│   ├── types/
│   │   └── index.ts          # All shared interfaces and type aliases.
│   ├── services/
│   │   └── userService.ts    # Business logic. No database or HTTP code here.
│   ├── repositories/
│   │   └── userRepository.ts # Direct database access only.
│   ├── utils/
│   │   └── formatters.ts     # Pure helper functions with no side effects.
│   └── controllers/
│       └── userController.ts # Handles HTTP request/response. No business logic.
├── dist/                     # Compiled JavaScript output. Never edit these files.
├── tsconfig.json
└── package.json
```

---

## 3. Separation of Concerns

Every file should have exactly one reason to exist. This is called the **Single Responsibility Principle (SRP)**. The most important separations are
### Types: The Shared Contract

All interfaces and type aliases that are used across multiple files belong in a dedicated `types/` file. This prevents circular imports and makes every interface easy to find.

```typescript
// src/types/index.ts
export interface User {
  id: string;
  username: string;
  email: string;
  age: number;
}

export interface CreateUserInput {
  username: string;
  email: string;
  age: number;
}
```

### Repository: Data Access Only

A repository file is responsible for one thing: reading and writing data to a database or storage. It knows nothing about business rules or HTTP requests.

```typescript
// src/repositories/userRepository.ts
import { User } from "../types";

const users: User[] = []; // Simulating a database.

export function findUserById(id: string): User | undefined {
  return users.find((user) => user.id === id);
}

export function insertUser(user: User): void {
  users.push(user);
}
```

### Service: Business Logic Only

A service file contains the rules and decisions of your application. It knows how to validate data and what should happen in different scenarios. It gets data from repositories, applies logic, and returns results.

```typescript
// src/services/userService.ts
import { User, CreateUserInput } from "../types";
import { insertUser, findUserById } from "../repositories/userRepository";

export function registerUser(input: CreateUserInput): User {
  if (input.age < 18) {
    throw new Error("User must be at least 18 years old.");
  }
  if (input.username.length < 3) {
    throw new Error("Username must be at least 3 characters.");
  }

  const newUser: User = {
    id: Math.random().toString(36).slice(2),
    username: input.username,
    email: input.email,
    age: input.age
  };

  insertUser(newUser);
  return newUser;
}
```

### Entry Point: Orchestration Only

The `index.ts` entry point wires everything together. It should not contain business logic or data access. It simply calls the right service with the right data.

```typescript
// src/index.ts
import { registerUser } from "./services/userService";

const result = registerUser({
  username: "nova",
  email: "nova@example.com",
  age: 22
});

console.log("Registered:", result.username);
```

---

## 4. The 300-Line Rule

A logic file that approaches 300 lines is almost always doing too many things at once. It has become a "God Object" that knows too much and controls too much. Before any file reaches 300 lines, stop and identify its distinct responsibilities, then split them into separate files.

This rule does not apply to purely declarative files like type definitions or JSON configuration, which can be longer.

---

## 5. Circular Dependencies and How to Avoid Them

A circular dependency occurs when File A imports from File B, and File B also imports from File A. This creates a loop
```
userService.ts  imports from  userRepository.ts
userRepository.ts  imports from  userService.ts  <-- loop
```

Circular dependencies can cause modules to resolve to `undefined` at runtime, causing hard-to-debug crashes. They also indicate that the separation between files is not clean.

The solution is almost always to extract the shared dependency into a third file (usually `types/index.ts`). Neither the service nor the repository needs to import from each other if they both just import the shared type from `types/`
```text
userService.ts    --> imports from --> types/index.ts
userRepository.ts --> imports from --> types/index.ts
```

No loop.

---

## 6. When to Split a File

These are the signals that tell you a file needs to be split
| Signal | Action |
|---|---|
| File is over 200 lines and growing | Start splitting immediately. |
| You are scrolling to find a specific function | Too many functions in one file. |
| Two unrelated features are in the same file | Each feature gets its own file. |
| You need to mock part of a file in tests | The mocked part should be a separate module. |
| The file name is vague ("utils.ts", "helpers.ts") | Name has no clear responsibility; split by topic. |

---

## 7. Naming Conventions

Consistent naming makes a codebase readable to any developer
| Item | Convention | Example |
|---|---|---|
| Files | `camelCase.ts` or `kebab-case.ts` | `userService.ts` or `user-service.ts` |
| Interfaces | `PascalCase` | `UserProfile`, `ApiResponse` |
| Type aliases | `PascalCase` | `RequestState`, `Direction` |
| Classes | `PascalCase` | `UserRepository`, `AuthService` |
| Functions | `camelCase` | `getUserById`, `formatDate` |
| Constants | `UPPER_SNAKE_CASE` for global constants | `MAX_RETRIES`, `API_BASE_URL` |
| Variables | `camelCase` | `currentUser`, `isLoading` |

---

## 8. Barrel Files (`index.ts` in Folders)

When a folder contains many related files, you can create an `index.ts` inside that folder that re-exports everything. This lets other files import from the folder name instead of individual files
```typescript
// src/utils/index.ts
export { formatDate } from "./formatDate";
export { formatCurrency } from "./formatCurrency";
export { slugify } from "./slugify";
```

Now instead of
```typescript
import { formatDate } from "../utils/formatDate";
import { formatCurrency } from "../utils/formatCurrency";
```

You write
```typescript
import { formatDate, formatCurrency } from "../utils";
```

Use barrel files in folders with more than 3-4 related files.

---

## 9. A Complete Refactoring Example

Here is a monolithic file that violates every rule, followed by the clean, split version
**Before (everything in one file):**
```typescript
// badApp.ts - 80+ lines of mixed concerns
interface Product { id: string; name: string; price: number; stock: number; }
const db: Product[] = [];

function validateProduct(p: Product): boolean {
  return p.price > 0 && p.name.length > 0;
}

function saveProduct(p: Product): void {
  db.push(p);
}

function handleAddProduct(name: string, price: number, stock: number): void {
  const product: Product = { id: Date.now().toString(), name, price, stock };
  if (!validateProduct(product)) {
    console.log("Invalid product.");
    return;
  }
  saveProduct(product);
  console.log("Product saved:", product.name);
}
```

**After (clean, split version):**

```typescript
// src/types/index.ts
export interface Product {
  id: string;
  name: string;
  price: number;
  stock: number;
}
```

```typescript
// src/repositories/productRepository.ts
import { Product } from "../types";
const db: Product[] = [];

export function save(product: Product): void {
  db.push(product);
}

export function findAll(): Product[] {
  return [...db];
}
```

```typescript
// src/services/productService.ts
import { Product } from "../types";
import { save } from "../repositories/productRepository";

function validateProduct(product: Product): boolean {
  return product.price > 0 && product.name.length > 0;
}

export function addProduct(name: string, price: number, stock: number): Product {
  const product: Product = { id: Date.now().toString(), name, price, stock };
  if (!validateProduct(product)) {
    throw new Error("Invalid product data.");
  }
  save(product);
  return product;
}
```

```typescript
// src/index.ts
import { addProduct } from "./services/productService";

const saved = addProduct("Mechanical Keyboard", 89.99, 25);
console.log("Saved product:", saved.name);
```

Each file has a single, clear responsibility. Each can be read, tested, and modified independently.

---

## 10. Real-World Use Cases and Common Pitfalls

### Real-World Use Case 1: Separation of Concerns in Next.js Full-Stack Apps
In modern web applications, keeping domain types (`types/user.ts`), API database calls (`repositories/userRepo.ts`), and UI components (`components/UserProfile.tsx`) strictly separated means that if you switch your database from MongoDB to PostgreSQL, your UI components do not change a single line of code!

### Real-World Use Case 2: Clean Public APIs with Barrel Files (`index.ts`)
Large component libraries (like Material UI or Radix UI) use barrel files inside folder directories (`src/components/index.ts`) so external developers can import multiple items cleanly (`import { Button, Modal, Card } from "my-ui-lib"`) without typing out internal file paths.

### Common Pitfall to Avoid: Circular Dependencies
When File A imports from File B, and File B imports back from File A, Node and web bundlers can get confused and return `undefined` for imported variables at runtime. Always keep your dependency graph flowing in one direction (e.g., UI Components $\rightarrow$ Services $\rightarrow$ Repositories $\rightarrow$ Types). Types should never import from UI components!
