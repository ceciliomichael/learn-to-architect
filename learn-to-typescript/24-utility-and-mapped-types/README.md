# Module 24: Utility and Mapped Types

## Before you start

Complete Modules 01 to 23. You should understand generics, `keyof`, and indexed access types.

## What you will learn

- derive common object variations with built-in utility types
- create selected and omitted property shapes
- model key-value mappings with `Record`
- understand the basic mapped type loop
- decide when an explicit type is clearer than a transformation

## Why this matters

Related operations often need related views of one data model. A create form may omit an id. An update may allow only some fields. Utility types can express those relationships without copying every property.

## 1. Starting model

```typescript
interface Task {
  id: string;
  title: string;
  description?: string;
  isComplete: boolean;
}
```

The utilities in this module produce new static types. They do not copy or transform runtime objects.

## 2. `Partial` and `Required`

```typescript
type TaskUpdate = Partial<Task>;
```

Every property becomes optional. This can suit a patch object, but it also permits changing `id`. A more precise update may omit id first:

```typescript
type TaskUpdate = Partial<Omit<Task, "id">>;
```

`Required<Task>` makes every property required, including `description`.

Neither utility recursively changes nested properties. They are shallow.

## 3. `Readonly`

```typescript
type ReadonlyTask = Readonly<Task>;
```

Every top-level property becomes readonly through that type. Like earlier readonly syntax, this does not deeply freeze runtime data.

## 4. `Pick` and `Omit`

```typescript
type TaskSummary = Pick<Task, "id" | "title">;
type NewTask = Omit<Task, "id">;
```

- `Pick` keeps selected keys.
- `Omit` keeps every key except the selected ones.

The key arguments are checked against `keyof Task`, so misspellings are rejected.

For public types, consider writing a small explicit interface when it communicates intent more clearly than several nested utilities.

## 5. `Record`

```typescript
type Status = "todo" | "doing" | "done";
type StatusLabels = Record<Status, string>;

const labels: StatusLabels = {
  todo: "To do",
  doing: "In progress",
  done: "Complete",
};
```

`Record<Keys, Value>` creates properties for every key in the key union. Missing a status or adding an unrelated key causes an error in a directly checked object literal.

This differs from an open string index signature. A literal-key Record describes a closed required set.

## 6. A mapped type

This is a simplified version of `Readonly`:

```typescript
type ReadonlyCopy<T> = {
  readonly [Key in keyof T]: T[Key];
};
```

Read it in steps:

1. `keyof T` creates the source key union.
2. `Key in keyof T` visits each key.
3. `T[Key]` gets that key's original value type.
4. `readonly` adds the modifier in the new type.

This mapped type exists only for type checking.

## 7. Another mapped type

```typescript
type BooleanFlags<T> = {
  [Key in keyof T]: boolean;
};

type TaskFlags = BooleanFlags<Task>;
```

`TaskFlags` has the same property names as `Task`, but every value is boolean.

This is useful only when those flags have a real meaning. Do not transform types merely because it is possible.

## 8. Utility types compose

```typescript
type EditableTaskFields = Pick<Task, "title" | "description">;
type TaskDraft = Partial<EditableTaskFields>;
```

Keep composition shallow enough that a reader can still understand the final contract. A named intermediate type often helps.

## 9. Runtime work is separate

`Pick<Task, "title">` does not remove properties from an object at runtime. A function that creates a summary must still build the summary value:

```typescript
function toTaskSummary(task: Task): TaskSummary {
  return {
    id: task.id,
    title: task.title,
  };
}
```

## Common mistakes

### Treating utilities as runtime transformations

They create static types only.

### Using `Partial<T>` for every update

It may allow fields that should never be changed.

### Forgetting utilities are shallow

Nested data keeps its original modifiers unless transformed separately.

### Nesting utilities until the type is unreadable

Use a direct named shape when it communicates better.

## Check your understanding

1. What does `Partial<T>` change?
2. How do `Pick` and `Omit` differ?
3. What does `Record<Status, string>` require?
4. What does `[Key in keyof T]` do?
5. Do utility types change runtime objects?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 25](../25-classes-and-composition/README.md) introduces class instances and compares inheritance with object composition.
