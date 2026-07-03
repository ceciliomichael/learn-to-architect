# Module 02: Objects, Interfaces, and Type Aliases

In Module 01 we stored single values like a name or a score. In real programs, data is grouped. A user has a username, an email, an age, and a password all at once. TypeScript lets you describe these grouped shapes using objects, interfaces, and type aliases.

---

## 1. What is an Object?

An object is a collection of related data stored together under one variable. Each piece of data is called a **property**, and it has a name (called a key) and a value.

```typescript
const player = {
  username: "shadow_blade",
  level: 42,
  isOnline: true
};

// You access a property using dot notation
console.log(player.username); // Outputs: "shadow_blade"
console.log(player.level);   // Outputs: 42
```

The object above has three properties: `username` (string), `level` (number), and `isOnline` (boolean).

---

## 2. The Problem Without a Blueprint

If you just write an object like the one above and pass it around your program, TypeScript has to guess its structure each time. When you have many objects of the same shape (for example, hundreds of users), you need a reusable contract that describes what every user object must look like. That contract is called an **interface** or a **type alias**.

---

## 3. Interfaces

An interface is a blueprint that describes the exact shape an object must have. Once you define an interface, you can apply it to any variable to enforce that shape
```typescript
interface Player {
  username: string;
  level: number;
  isOnline: boolean;
}

// Applying the blueprint
const playerOne: Player = {
  username: "shadow_blade",
  level: 42,
  isOnline: true
};

// TypeScript will give an error if you miss a property or use the wrong type
// const playerTwo: Player = { username: "nova" }; // ERROR! 'level' and 'isOnline' are missing.
```

### Optional Properties (`?`)

Sometimes a property is not always present. For example, a user may or may not have set an avatar. You mark optional properties with a `?` after the property name
```typescript
interface UserProfile {
  username: string;
  avatarUrl?: string; // The ? means this property can be left out entirely.
}

const userA: UserProfile = { username: "nova" };          // Valid. avatarUrl is absent.
const userB: UserProfile = { username: "blaze", avatarUrl: "https://cdn.site.com/blaze.png" }; // Also valid.
### Readonly Properties

If a property should never be changed after the object is created (like a unique ID that the database assigns), use the `readonly` keyword. Any attempt to overwrite it will cause a TypeScript error
```typescript
interface DatabaseRecord {
  readonly id: string;
  content: string;
}

const record: DatabaseRecord = { id: "rec-001", content: "Hello" };
record.content = "World"; // Allowed.
// record.id = "rec-002"; // ERROR! Cannot assign to 'id' because it is a read-only property.
```

---

## 4. Type Aliases

A `type` alias is another way to define a named shape. For describing object structures, `type` and `interface` look almost identical
```typescript
type Enemy = {
  name: string;
  health: number;
  isBoss: boolean;
};

const goblin: Enemy = {
  name: "Goblin Scout",
  health: 50,
  isBoss: false
};
```

The key distinction between `type` and `interface` is discussed in the next section. For simple object shapes, you can use either one.

---

## 5. `interface` vs `type`: Key Differences

### Extending (Inheriting Properties)

When designing complex applications, many object shapes share common attributes. For example, a video game might have a `Warrior`, a `Mage`, and an `Archer`. Every character needs an `id`, a `name`, and `health`, but each specific class also needs unique fields like `ragePoints` or `manaPool`.

If you wrote out `id`, `name`, and `health` inside every single interface, your codebase would suffer from massive code duplication. If you later decided to change `id` from a `number` to a `string`, you would have to manually edit dozens of interfaces.

To solve this, TypeScript allows interfaces to **inherit** properties from parent blueprints using the `extends` keyword. 

When you declare `interface Child extends Parent`, two things happen automatically:
1. **Property Copying:** All properties defined on the `Parent` interface are automatically included on the `Child` interface.
2. **Type Compatibility:** Any object that satisfies the `Child` interface is structurally guaranteed to also satisfy the `Parent` interface.

Both interfaces and type aliases can achieve property inheritance, but their syntax differs.

With `interface`, you use the explicit `extends` keyword
```typescript
interface Animal {
  name: string;
  age: number;
}

interface Dog extends Animal {
  breed: string; // Dog automatically inherits 'name' and 'age' from Animal, AND adds 'breed'.
}

const myDog: Dog = { name: "Rex", age: 3, breed: "Husky" };
```

With `type`, you combine shapes using the `&` (intersection) operator
```typescript
type Animal = {
  name: string;
  age: number;
};

type Dog = Animal & {
  breed: string;
};
```

Both approaches produce the same result. Most teams prefer `interface` when describing objects because of how it handles merging (see below).

### Declaration Merging (Only `interface` Does This)

If you declare two interfaces with the same name in the same file, TypeScript automatically combines them into one. This is called declaration merging
```typescript
interface UserSettings {
  theme: string;
}

interface UserSettings {
  fontSize: number;
}

// TypeScript silently merges these into: { theme: string; fontSize: number; }
const settings: UserSettings = { theme: "dark", fontSize: 16 };
```

If you try the same thing with `type`, TypeScript throws a "Duplicate identifier" error. You cannot declare the same type alias twice.

---

## 6. Union Types (`|`): A Value Can Be One of Several Types

Sometimes a variable can hold more than one type of data. For example, a function might accept either a `string` or a `number`. You express this with the `|` (pipe) operator, which means "or"
```typescript
let id: string | number;

id = "user-abc"; // Valid.
id = 12345;      // Also valid.
// id = true;    // ERROR! boolean is not part of the union.
```

Unions work with custom types too
```typescript
type SuccessResponse = { status: "success"; data: string };
type ErrorResponse = { status: "error"; message: string };

type ApiResponse = SuccessResponse | ErrorResponse;
```

---

## 7. Index Signatures: Objects with Dynamic Keys

Sometimes you need an object where you do not know the property names in advance, but you know what type the keys and values will be. This is common for dictionaries, lookup tables, or configuration maps.

You define this using an **index signature**
```typescript
interface TranslationDictionary {
  [word: string]: string; // Any string key must hold a string value.
}

const french: TranslationDictionary = {
  hello: "bonjour",
  cat: "chat",
  dog: "chien"
};

// Adding a number value would be an error
// french.count = 3; // ERROR! Type 'number' is not assignable to type 'string'.
```

---

## 8. Structural Typing: TypeScript Checks Shape, Not Name

TypeScript does not care what you named a variable. It only checks whether the variable has the required properties with the correct types. This is called structural typing.

If an object has all the properties that an interface requires, TypeScript accepts it, even if the object has extra properties or was never explicitly typed as that interface
```typescript
interface Point2D {
  x: number;
  y: number;
}

// point3D has extra property 'z', but it still satisfies Point2D because it has x and y
const point3D = { x: 10, y: 20, z: 30 };
const point: Point2D = point3D; // Valid
```

This is why the exercises may show you assigning one object to a differently-typed variable without any errors. TypeScript checks the structure, not the label.

---

## 9. `null` and `undefined`

Two special values exist for "no value" or "not yet set"
- `undefined`: The variable was declared but never assigned a value.
- `null`: The variable was intentionally set to "empty" or "nothing".

With TypeScript's strict mode (which you should always use), you must explicitly say a variable can hold one of these
```typescript
let username: string = "Alice";
// username = null; // ERROR in strict mode
let optionalName: string | null = null; // Explicitly allows null.
optionalName = "Bob"; // Can later be assigned a real value.
```

### Optional Properties (`?`) vs Explicit `undefined`

When designing interfaces, it is important to understand the difference between marking a property as optional (`property?: string`) versus typing it explicitly as a union with `undefined` (`property: string | undefined`):

- **Optional (`property?: string`):** You are allowed to **omit the key entirely** when creating the object (`{}`). If the property is present, its value can be either a string or `undefined`.
- **Explicit Undefined (`property: string | undefined`):** You **must include the property key** when creating the object, even if you set its value to `undefined` (`{ property: undefined }`). If you leave the key out entirely (`{}`), TypeScript will give a compiler error stating that the required property is missing.

Use `?` when a property can be safely left off the object. Use `| undefined` when your application requires every key to be present on the object shape.
