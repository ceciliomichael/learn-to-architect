# Module 31: Advanced Mapped and Template Literal Types

## Before you start

Complete Modules 01 to 30. You should understand mapped types, conditional types, literal unions, and `keyof`.

## What you will learn

- add and remove mapped property modifiers
- rename mapped keys with `as`
- combine string literal types into patterns
- use built-in string manipulation types
- connect event names to property value types
- keep generated APIs small and understandable

## Why this matters

Some APIs repeat a predictable name pattern, such as `nameChanged` for a `name` property. TypeScript can derive these names from one source type and keep callbacks connected to the right values.

## 1. Change mapped modifiers

```typescript
type MutableRequired<T> = {
  -readonly [Key in keyof T]-?: T[Key];
};
```

- `-readonly` removes readonly.
- `-?` removes optional.
- `+readonly` and `+?` add modifiers, although the plus is usually omitted when adding.

These changes are shallow and static.

## 2. Template literal types

```typescript
type Side = "top" | "right" | "bottom" | "left";
type MarginProperty = `margin-${Side}`;
```

`MarginProperty` is a union of four exact strings such as `"margin-top"`.

When placeholders contain unions, TypeScript forms every combination:

```typescript
type Size = "small" | "large";
type Variant = `${Size}-${Side}`;
```

Keep combinations controlled. Large unions multiply quickly.

## 3. String manipulation types

Built-in helpers include:

- `Uppercase<Text>`
- `Lowercase<Text>`
- `Capitalize<Text>`
- `Uncapitalize<Text>`

```typescript
type Field = "name" | "age";
type GetterName = `get${Capitalize<Field>}`;
```

The result is `"getName" | "getAge"`.

## 4. Remap keys with `as`

```typescript
type Getters<T> = {
  [Key in keyof T as `get${Capitalize<Key & string>}`]: () => T[Key];
};
```

The `as` clause computes a new property name. `Key & string` keeps string keys because `Capitalize` works on strings.

For:

```typescript
interface Person {
  name: string;
  age: number;
}
```

`Getters<Person>` has `getName(): string` and `getAge(): number`.

## 5. Filter keys by remapping to never

```typescript
type WithoutId<T> = {
  [Key in keyof T as Key extends "id" ? never : Key]: T[Key];
};
```

A mapped key renamed to `never` is omitted. Built-in `Omit` is clearer for this simple case. Key filtering becomes useful when the rule itself is generic.

## 6. Typed property events

```typescript
type PropertyEvents<T> = {
  on<Key extends string & keyof T>(
    eventName: `${Key}Changed`,
    callback: (newValue: T[Key]) => void,
  ): void;
};
```

For `Person`, `"nameChanged"` connects to a string callback value and `"ageChanged"` connects to a number.

This type describes the API. Runtime code still has to store handlers and send correct events.

## 7. Avoid generating an unreadable language

Generated names are helpful when users already expect the pattern. They are harmful when a reader must decode several type layers to discover ordinary methods.

Prefer explicit names when:

- there are only a few members
- the names carry unique meaning
- compiler errors become hard to understand
- runtime implementation does not naturally follow the same pattern

## Common mistakes

### Forgetting non-string keys

Restrict or extract string keys before applying string manipulation types.

### Creating huge cross-product unions

Keep placeholder unions small or generate runtime strings with validation instead.

### Reimplementing `Pick` or `Omit` for a simple case

Prefer the familiar built-in.

### Assuming generated types create runtime methods

They describe required methods only.

## Check your understanding

1. What do `-readonly` and `-?` do?
2. What union does `` `get${Capitalize<"name" | "age">}` `` produce?
3. What does key remapping with `as` change?
4. How does mapping a key to `never` affect it?
5. Do generated getter types implement getters at runtime?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 32](../32-third-party-types-and-declaration-files/README.md) explains how TypeScript learns the APIs of JavaScript libraries.
