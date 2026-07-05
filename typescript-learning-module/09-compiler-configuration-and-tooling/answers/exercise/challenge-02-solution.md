# Challenge 02: Solution

**Folder structure:**
```
task-manager/
├── types/
│   └── index.ts            -  Task interface definition
├── repositories/
│   └── taskRepository.ts   -  In-memory data store and raw data access
├── services/
│   └── taskService.ts      -  Business logic: create, complete, getAll (with validation)
└── index.ts                -  Entry point: thin orchestration only
```

**types/index.ts:**
```typescript
export interface Task {
  id: string;
  title: string;
  isCompleted: boolean;
  createdAt: Date;
}
```

**services/taskService.ts:**
```typescript
import { Task } from "../types";

const tasks: Task[] = [];

export function createTask(title: string): Task {
  if (title.trim().length === 0) {
    throw new Error("Task title cannot be empty.");
  }
  const task: Task = {
    id: Date.now().toString(),
    title: title.trim(),
    isCompleted: false,
    createdAt: new Date()
  };
  tasks.push(task);
  return task;
}

export function completeTask(id: string): Task {
  const task = tasks.find((t) => t.id === id);
  if (task === undefined) {
    throw new Error("Task not found: " + id);
  }
  if (task.isCompleted) {
    throw new Error("Task is already completed.");
  }
  task.isCompleted = true;
  return task;
}

export function getAllTasks(): Task[] {
  return tasks;
}
```

**index.ts:**
```typescript
import { createTask, completeTask, getAllTasks } from "./services/taskService";

const task1 = createTask("Learn TypeScript");
const task2 = createTask("Build a project");

console.log("Created:", task1.title);

completeTask(task1.id);
console.log("Completed:", task1.isCompleted); // true

console.log("All tasks:", getAllTasks().length); // 2
```
