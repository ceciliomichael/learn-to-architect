# Module 31 Exercise Solutions

```typescript
type Editable<T> = {
  -readonly [Key in keyof T]-?: T[Key];
};

type Action = "save" | "load" | "reset";
type Command = `run-${Action}`;

type Setters<T> = {
  [Key in keyof T as `set${Capitalize<Key & string>}`]: (value: T[Key]) => void;
};

type FunctionsOnly<T> = {
  [Key in keyof T as T[Key] extends (...arguments_: never[]) => unknown ? Key : never]: T[Key];
};
```

`Getters<Person>` only requires the methods statically. Runtime code must create every method and return the real property values.
