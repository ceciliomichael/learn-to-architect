# Final Assessment  -  TypeScript Curriculum

You have completed all 11 modules. This is your final test.

There are no guided hints here. No exercises with blanks to fill in. No answer files to peek at. This is the real thing  -  you read a project brief, you architect it, you build it, you document it, and you ship it.

---

## What This Is

This assessment is a self-directed project. You will choose one of the five projects in the `projects/` folder. Each project is a realistic, modern TypeScript codebase challenge at a junior-to-mid-level engineer standard.

You are not being graded by anyone. But you should grade yourself honestly using the Self-Assessment Checklist at the bottom of this document. The only person you are accountable to is yourself.

---

## How to Pick Your Project

Open the `projects/` folder and read through all five project briefs. Each one tells you
- What you are building
- The core requirements
- The stretch goals
- Which TypeScript concepts it primarily exercises

Pick the one that scares you just the right amount  -  challenging enough that you have to think, but not so unfamiliar that you cannot start.

---

## Non-Negotiable Rules

**You must follow all of these. They are not optional.**

1. You write every line of code yourself. Do not copy solutions from the internet, use AI to generate code for you, or copy-paste from the curriculum exercises.

2. Every file must have exactly one clear responsibility. No mixing of types, business logic, data access, and output in the same file. This was Module 09.

3. No file may exceed 300 lines of logic code. Split proactively, not reactively.

4. `any` is banned. You may not use it anywhere. If you do not know the type, use `unknown` and narrow it.

5. All async operations must have proper error handling. Every `await` must be reachable from a `try/catch` block or from a function that explicitly propagates the error.

6. You must write a `PROJECT.md` documentation file as part of your submission. Requirements for this are at the bottom of this document.

---

## What Each Project Tests

Every project covers all 11 modules to some degree, but each one emphasizes different areas. Here is the rough map
| Project | Primary Focus | Modern Application |
|---|---|---|
| Option 01  -  Task API | Classes, generics, async, error handling | Core backend business logic |
| Option 02  -  Budget Tracker | Discriminated unions, utility types, Result pattern | Fintech domain engines |
| Option 03  -  Event Bus | Advanced generics, mapped types, function signatures | Framework internal messaging |
| Option 04  -  CLI Note Manager | Async Node.js I/O, error wrapping, local storage | Developer CLI tooling |
| Option 05  -  Data Pipeline | Async pipelines, iterator patterns, batch resilience | Data engineering / ETL |
| Option 06  -  Autonomous Agent | Tool calling, mock LLM loops, self-correction | Agentic AI orchestrators |
| Option 07  -  Mini-Git Engine | DAG traversal, content hashing, tree structures | Version control internals |
| Option 08  -  State Machine | FSM transition guards, strict state constraints | UI/Workflow orchestration (XState) |
| Option 09  -  HTTP Router | Method chaining, context enrichment, middleware | Web backend frameworks (Hono/tRPC) |
| Option 10  -  Memory Database | ACID transactions, rollback isolation, TTL timers | In-memory cache engines (Redis) |

---

## The Required Documentation: PROJECT.md

When you finish building your project, you must write a `PROJECT.md` file at the root of your project folder. This is not optional. A working codebase with no documentation is an incomplete submission.

Your `PROJECT.md` must include all of the following sections
### 1. Project Overview
A paragraph explaining what the project does and what problem it solves. Write this as if the reader has never seen the project before.

### 2. Architecture
Describe how you split the code into files and folders. Explain the responsibility of each folder and each major file. If you drew this structure as a tree, include it.

Example
```
src/
├── types/index.ts        -  All shared interfaces
├── services/task.ts      -  Business logic
├── repositories/db.ts    -  Data access layer
└── index.ts              -  Entry point
```

### 3. TypeScript Concepts Used
List the TypeScript features you used and, for each one, give one real example from your own code showing how you used it. Do not describe the concept in general  -  describe your specific usage.

Example format
- **Discriminated unions**: Used in `types/index.ts` to model `TaskState` as three possible states  -  `pending`, `in-progress`, and `done`  -  each with different data.
- **Generic function with constraint**: `getById<T extends { id: string }>(...)` in `services/base.ts` allows reuse across Task, User, and Project lookups.

### 4. Decisions and Trade-offs
Describe at least two architectural decisions you made and why. What alternatives did you consider? Why did you choose what you chose?

Example
- "I chose the Result pattern over `try/catch` in the service layer because the callers of these functions need to handle both the success and failure cases at compile time. Using `try/catch` would have made failure handling optional and easy to forget."

### 5. What You Would Improve
List at least two things you would do differently or add if you had more time. Be specific. This is not a self-criticism section  -  it is a demonstration that you understand the limits of your current implementation.

### 6. Self-Assessment Checklist
Copy this checklist into your `PROJECT.md` and mark each item as complete
```
[ ] Every file has one clear responsibility (SRP)
[ ] No file exceeds 300 lines
[ ] No use of 'any'
[ ] All async code has proper error handling
[ ] Types, services, and data access are separated
[ ] All exported functions have explicit return type annotations
[ ] At least one generic type or function is used
[ ] At least one discriminated union or custom type guard is used
[ ] At least one utility type (Partial, Pick, Omit, Record, etc.) is used
[ ] The README.md / PROJECT.md explains the architecture clearly
```

---

## Setup Instructions

All five projects are standalone TypeScript Node.js applications. To set one up
```bash
mkdir my-project
cd my-project
npm init -y
npm install typescript @types/node --save-dev
npx tsc --init
```

Then configure your `tsconfig.json`. A production-ready config for Node.js looks like this
```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "CommonJS",
    "rootDir": "./src",
    "outDir": "./dist",
    "strict": true,
    "skipLibCheck": true,
    "esModuleInterop": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

To compile
```bash
npx tsc
```

To run
```bash
node dist/index.js
```

---

## One Final Note

If you get stuck, go back to the module that covers the concept you are struggling with. That is what the curriculum is for. The modules are not a one-time read  -  they are your reference material. A real engineer uses documentation every day.

Good luck. Build something you are proud of.
