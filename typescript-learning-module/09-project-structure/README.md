# Module 09: Project Structure and Clean Architecture

Writing correct TypeScript syntax is only 10% of a software engineer's job. The other 90% is knowing how to organize thousands of lines of code so that a team of 50 developers can work on the same application simultaneously without stepping on each other's toes.

If you put all your code in one file, it will work. But it is not *Engineering*. This module covers the architectural decisions, folder structures, and strict boundary rules that separate junior scripters from senior software engineers.

---

## 1. Why Structure Matters

### The Real-World Analogy: The Restaurant Kitchen
Imagine a restaurant kitchen where everyone does everything. The person chopping onions is also taking orders, washing dishes, and baking the cake, all at the same station. It would be chaos. Orders would get lost, cross-contamination would happen, and if one person gets sick, the whole restaurant shuts down.

A professional kitchen uses **Stations**: a Grill Station, a Prep Station, and an Expeditor. 
In software, we use the **Single Responsibility Principle (SRP)**. Every file should have exactly one job, one reason to exist, and one reason to change. 

Good architecture means:
1. When a bug occurs, you know exactly which folder to look in.
2. When you add a new feature, you don't accidentally break old features.
3. You can test the "Grill Station" without having to turn on the "Dishwasher".

---

## 2. Standard TypeScript Project Structure

Here is the industry-standard folder architecture used in almost every professional Node.js and TypeScript project:

```text
my-app/
├── src/                      # Your actual code lives here
│   ├── index.ts              # The Entry Point. (The Expeditor)
│   ├── types/                # Shared Interface Blueprints.
│   │   └── index.ts          
│   ├── services/             # Business Logic and Rules. (The Chefs)
│   │   └── userService.ts    
│   ├── repositories/         # Database access ONLY. (The Pantry Workers)
│   │   └── userRepository.ts 
│   ├── utils/                # Small, pure helper functions. (The Tools)
│   │   └── formatters.ts     
│   └── controllers/          # HTTP request/response handlers. (The Waiters)
│       └── userController.ts 
├── dist/                     # The compiled output. Never touch this!
├── tsconfig.json             # Compiler configuration
└── package.json              # NPM dependencies
```

---

## 3. Separation of Concerns (The 4 Core Layers)

Let's break down exactly what goes in each folder, and what is strictly forbidden.

### Layer 1: `types/` (The Shared Contracts)
This folder holds all your `interface` and `type` definitions. 
**Rule:** No executable logic (`functions`, `classes`) is allowed here! 
Putting types in a central folder prevents messy circular dependency imports.

```typescript
// src/types/index.ts
export interface User {
  id: string;
  email: string;
  age: number;
}
```

### Layer 2: `repositories/` (The Pantry Workers)
This folder is the ONLY place in your app allowed to talk to the database (SQL, MongoDB, or an array acting as a database).
**Rule:** No business logic! A repository should never validate emails or check if a user is old enough. It blindly saves or retrieves whatever data it is given.

```typescript
// src/repositories/userRepository.ts
import { User } from "../types";

const db: User[] = [];

// BLINDLY saves the user. No validation logic allowed here!
export function saveUser(user: User): void {
  db.push(user);
}
```

### Layer 3: `services/` (The Chefs)
This folder holds the actual "Business Logic" of your application.
**Rule:** No database connection code, and no HTTP request code! The Service receives data, validates it against business rules, and then asks the Repository to save it.

```typescript
// src/services/userService.ts
import { User } from "../types";
import { saveUser } from "../repositories/userRepository";

export function registerUser(email: string, age: number): User {
  // 1. Business Logic / Validation
  if (age < 18) {
    throw new Error("Must be 18 to register.");
  }
  
  // 2. Data Formatting
  const newUser: User = { id: "123", email, age };
  
  // 3. Asking the Repository to save it
  saveUser(newUser);
  return newUser;
}
```

### Layer 4: `index.ts` or `controllers/` (The Expeditor/Waiter)
This is the entry point that wires everything together.
**Rule:** No database code, and no business logic! It simply takes input from the outside world (like a terminal command or HTTP request) and hands it to the Service.

```typescript
// src/index.ts
import { registerUser } from "./services/userService";

// Taking input from the outside world and handing it to the Chef
const result = registerUser("alice@email.com", 25);
console.log("Success:", result);
```

---

## 4. The 300-Line Rule

### The Core Technical Concept
If a file containing logic (a Service or Controller) surpasses 300 lines of code, it has almost certainly become a **"God Object"**—a file that knows too much and controls too much.

When a file hits this limit, stop coding. Look at the file, identify its distinct responsibilities, and split it into multiple smaller files. 
*(Note: Files containing pure configuration or massive lists of Type Interfaces are exempt from this rule).*

---

## 5. Circular Dependencies and How to Avoid Them

### The Real-World Analogy: The Infinite Loop
Imagine Alice needs Bob's signature to approve a document. But Bob's rule is that he cannot sign anything until Alice signs it first. They will stand there staring at each other forever.

### The Core Technical Concept
A **Circular Dependency** happens when `File A` imports from `File B`, but `File B` also imports from `File A`. 
When the TypeScript compiler tries to build the project, it gets stuck in an infinite loop, resulting in variables randomly being `undefined` at runtime and crashing the app!

```text
userService.ts      imports     userRepository.ts
userRepository.ts   imports     userService.ts     <-- DANGER! CIRCULAR LOOP!
```

### How to Fix It
If two files rely on each other, they are usually sharing a Type or a Utility function. Extract that shared piece into a third, independent file (like `types/index.ts`). Then both files import from the third file, breaking the loop!

```text
userService.ts      imports     types/index.ts
userRepository.ts   imports     types/index.ts     <-- NO LOOP! SAFE!
```

---

## 6. When to Split a File

Never write code until you think about where it belongs. Use this decision matrix:

| Signal in your Codebase | Action to Take |
| :--- | :--- |
| File is approaching 300 lines. | Split immediately into smaller domains. |
| You are aggressively scrolling to find a specific function. | Split the file! It holds too many unrelated things. |
| You have `formatDate()` inside `userService.ts`. | Extract `formatDate` to a `utils/` folder so other files can use it. |
| The file is named `helpers.ts` or `misc.ts`. | Rename it! "Misc" means "I was too lazy to organize this." Split by exact topic (e.g. `stringUtils.ts`). |

---

## 7. Professional Naming Conventions

Consistent naming makes a codebase readable to any developer instantly. Break these, and your code looks amateur.

| Item Type | Convention Style | Example |
| :--- | :--- | :--- |
| **Files** | `camelCase.ts` or `kebab-case.ts` | `userService.ts` or `user-service.ts` |
| **Interfaces / Types** | `PascalCase` | `UserProfile`, `ApiResponse` |
| **Classes** | `PascalCase` | `DatabaseRepository` |
| **Functions / Variables**| `camelCase` | `getUserById`, `isLoading` |
| **Global Constants** | `UPPER_SNAKE_CASE` | `MAX_RETRIES`, `API_KEY` |

---

## 8. Barrel Files (`index.ts` in Folders)

### The Core Technical Concept
If your `utils/` folder has 10 different files (`math.ts`, `string.ts`, `date.ts`), importing them into other files gets very messy:
```typescript
import { add } from "../utils/math";
import { capitalize } from "../utils/string";
import { format } from "../utils/date";
```

You can create an `index.ts` file inside the `utils/` folder to act as a **Barrel**. The Barrel's only job is to scoop up everything in its folder and re-export it in one clean package:

```typescript
// src/utils/index.ts (The Barrel File)
export * from "./math";
export * from "./string";
export * from "./date";
```

Now, the rest of your application can import everything from the folder itself on a single line!
```typescript
// Beautiful, clean imports!
import { add, capitalize, format } from "../utils";
```

---

## 9. Real-World Use Cases and Common Pitfalls

### Real-World Use Case 1: Switching Databases without Breaking the App
Because we strictly separated the `Service` (Business Logic) from the `Repository` (Database), if your boss tells you to migrate the company from MongoDB to PostgreSQL, you ONLY rewrite the Repository file. The Service file has no idea the database changed, so the business logic remains perfectly safe and intact! This is the ultimate goal of Clean Architecture.

### Real-World Use Case 2: Clean Public APIs with Barrel Files
Large open-source UI libraries (like Material UI or Radix) use Barrel files heavily so that developers can write clean imports like `import { Button, Modal, Card } from "my-ui-lib"` instead of typing out deep paths like `"my-ui-lib/components/buttons/Button"`.

### Common Pitfall to Avoid: The "God Object" File
Junior developers often put Database SQL queries, HTTP Header validation, and Business Rules all inside a single `app.post("/users")` block. This makes the code impossible to write automated tests for. Always keep your dependency graph flowing in ONE direction: `Controllers -> Services -> Repositories`. 
