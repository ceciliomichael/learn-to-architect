# Option 01: TypeScript Task API

**Difficulty:** Intermediate
**Primary Concepts:** Classes, generics, discriminated unions, async/await, custom errors, project structure

---

## Project Brief

You are building a typed, in-memory task management API. This is the kind of code that lives behind every project management tool  -  the core engine that creates, updates, and queries tasks before a real database or HTTP layer is added.

Think of this as the business logic layer of a real application. No `express`, no `http`, no framework. Pure TypeScript. The "API" is the public interface your service exposes.

---

## Domain

A **Task** has:
- `id`  -  A unique string identifier (you generate this, not the user).
- `title`  -  A non-empty string.
- `description`  -  An optional string.
- `priority`  -  One of: `"low"`, `"medium"`, `"high"`, `"critical"`.
- `status`  -  One of: `"todo"`, `"in-progress"`, `"done"`, `"cancelled"`.
- `createdAt`  -  A `Date`, set automatically.
- `updatedAt`  -  A `Date`, updated every time the task changes.
- `tags`  -  An optional array of strings.
- `dueDate`  -  An optional `Date`.

A **CreateTaskInput** is what the caller provides to create a task. It should not include `id`, `createdAt`, `updatedAt`, or `status`  -  those are managed internally.

An **UpdateTaskInput** is a partial update payload  -  all fields are optional except that at least one must be provided. The caller cannot update `id`, `createdAt`, or `status` through this input (status changes have their own dedicated methods).

---

## Core Requirements

Build a `TaskService` class with the following public API:

```typescript
// These are the method signatures you must implement.
// Do not change the return types.

createTask(input: CreateTaskInput): Task

getTaskById(id: string): Task
// Throws NotFoundError if the task does not exist.

getAllTasks(filter?: TaskFilter): Task[]
// TaskFilter is an optional object: { status?, priority?, tag? }
// Returns all tasks that match ALL provided filter criteria.

updateTask(id: string, input: UpdateTaskInput): Task
// Throws NotFoundError if task does not exist.
// Throws ValidationError if input is empty (no fields to update).

changeStatus(id: string, newStatus: TaskStatus): Task
// Throws NotFoundError if task does not exist.
// Throws InvalidStatusTransitionError if the transition is not allowed.

deleteTask(id: string): void
// Throws NotFoundError if task does not exist.

getStats(): TaskStats
// Returns a summary object: total count, counts by status, counts by priority.
```

---

## Status Transition Rules

Not every status change is valid. You must enforce these rules in `changeStatus`:

```
todo        --> in-progress   (allowed)
todo        --> cancelled     (allowed)
in-progress --> done          (allowed)
in-progress --> todo          (allowed  -  unstarting a task)
in-progress --> cancelled     (allowed)
done        --> todo          (allowed  -  reopening)
done        --> in-progress   (NOT allowed)
cancelled   --> todo          (allowed  -  restoring)
cancelled   --> in-progress   (NOT allowed)
cancelled   --> done          (NOT allowed)
```

Any transition not listed above is also not allowed. Create an `InvalidStatusTransitionError` custom error class for this.

---

## File Structure You Must Use

```
src/
├── types/
│   └── index.ts            -  All interfaces and type aliases
├── errors/
│   └── index.ts            -  All custom error classes
├── services/
│   └── taskService.ts      -  TaskService class
├── utils/
│   └── id.ts               -  ID generation utility
└── index.ts                -  Entry point: demonstrate all features
```

---

## Stretch Goals

Complete these if you want a harder challenge:

1. **Sorting**: Add an optional `sort` field to `TaskFilter` that accepts `"createdAt-asc"`, `"createdAt-desc"`, `"priority-asc"`, or `"priority-desc"`. For priority sorting, `critical > high > medium > low`.

2. **Pagination**: Add `page` and `pageSize` fields to `TaskFilter`. `getAllTasks` should return a `PaginatedResult<Task>` with `data`, `total`, `page`, and `totalPages` fields.

3. **Generic Repository**: Extract the in-memory data store into a generic `Repository<T extends { id: string }>` class with `findById`, `findAll`, `save`, and `delete` methods. Make `TaskService` use it instead of a plain array.

4. **Async simulation**: Make all `TaskService` methods `async` and simulate a 10ms database delay using a `simulateDbDelay()` utility. Update `index.ts` to `await` all calls properly.

---

## Validation Rules

You must enforce these in `createTask` and `updateTask`. Throw a `ValidationError` with the field name and a clear message for each:

- `title` must not be empty and must be between 3 and 100 characters.
- `priority` must be one of the valid priority values.
- `dueDate` if provided must not be in the past.
- `tags` if provided must not contain empty strings.

---

## What Your Final index.ts Should Demonstrate

Your entry point should exercise every method at least once, including error cases. Structure it as a series of named steps with `console.log` separators, like this:

```typescript
console.log("--- Creating tasks ---");
// ... create 4-5 varied tasks

console.log("--- Filtering by status ---");
// ... filter and log

console.log("--- Status transitions ---");
// ... valid and invalid transitions, show the error message

console.log("--- Stats ---");
// ... log final stats
```

---

## PROJECT.md Is Required

When you are done, write your `PROJECT.md` following the requirements in the main `README.md`.
