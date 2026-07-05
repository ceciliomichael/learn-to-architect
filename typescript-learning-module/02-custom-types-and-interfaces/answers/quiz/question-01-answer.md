# Question 01 Answer: Interface Declaration Merging

## 1. Core Answer & Explanation

**Correct Answer: C** (Automatically merges them into one combined interface).

When you declare two or more `interface` blocks with the exact same identifier name within the same scope, TypeScript does not throw an error nor overwrite the previous declaration. Instead, the TypeScript compiler performs **Declaration Merging**: it silently combines all property signatures from every matching interface declaration into a single, unified structural contract.

If you attempt to declare two `type` aliases with the exact same identifier name within the same scope, TypeScript immediately halts compilation with a fatal syntax error: `Duplicate identifier 'Name'`. Type aliases are strictly closed and cannot be re-opened or augmented after their initial declaration.

---

## 2. Complete Code Examples & Compiler Behavior

### Interface Declaration Merging (Valid)
```typescript
// First declaration of UserSettings (e.g., defined in a core configuration file)
interface UserSettings {
  theme: "light" | "dark";
  autoSave: boolean;
}

// Second declaration of UserSettings (e.g., defined in a plugin module)
interface UserSettings {
  fontSize: number;
  enableNotifications?: boolean;
}

// The compiler merges both declarations into a single required shape!
// You must provide properties from BOTH blocks:
const mySettings: UserSettings = {
  theme: "dark",
  autoSave: true,
  fontSize: 14,
  enableNotifications: true
};

// Attempting to omit a property from either block causes a compiler error:
// const badSettings: UserSettings = { theme: "light", autoSave: false };
// COMPILER ERROR: Property 'fontSize' is missing in type '{ theme: "light"; autoSave: false; }' but required in type 'UserSettings'.
```

### Type Alias Duplicate Identifier (Invalid)
```typescript
type AccountStatus = {
  isActive: boolean;
};

// Attempting to declare another type alias with the exact same name:
// type AccountStatus = {
//   lastLoginDate: Date;
// };
// COMPILER ERROR: Duplicate identifier 'AccountStatus'.
```

---

## 3. Symbol-by-Symbol Breakdown

Let us examine the tokens involved in declaration merging:

* `interface` -> Built-in keyword instructing the compiler to open or append to a structural blueprint.
* `UserSettings` -> The shared PascalCase identifier. When the compiler encounters this token a second time with the `interface` keyword, it looks up the existing symbol table entry and appends the new signatures.
* `theme: "light" | "dark";` -> Property signature utilizing inline string literal union types.
* `type` -> Built-in keyword creating an immutable binding between an identifier and a type expression.
* `AccountStatus` -> Custom identifier. Once bound via `type`, the compiler locks the symbol table entry against further re-assignment or merging.

---

## 4. Architectural Trade-offs & Real-World Use Cases

### Why Does TypeScript Allow Interface Merging?
Declaration merging is not an accident; it is an intentional architectural feature designed to solve a fundamental problem in JavaScript ecosystem tooling: **extending third-party library types without modifying their source code**.

#### Real-World Case 1: Augmenting the Browser `Window` Object
In frontend web development, third-party analytics scripts (like Google Analytics or custom telemetry tools) often inject global variables directly onto the browser's `window` object (e.g., `window.ga` or `window.myCustomLogger`). Because the default TypeScript DOM library types do not know about your custom scripts, accessing `window.myCustomLogger` throws a compiler error (`Property 'myCustomLogger' does not exist on type 'Window'`).
By leveraging declaration merging, you can declare an interface with the exact same name in your project:
```typescript
// In your global types file (e.g., globals.d.ts)
interface Window {
  myCustomLogger: (message: string) => void;
}
```
TypeScript merges your declaration with the built-in browser `Window` interface, making `window.myCustomLogger` type-safe across your entire application!

#### Real-World Case 2: Augmenting Express.js Request Objects
In backend Node.js development using Express.js, authentication middleware (like Passport or JWT validators) intercepts incoming HTTP requests and attaches an authenticated user object to the request (`req.user`). To inform TypeScript that `req.user` exists on all Express routes, engineers merge into the Express namespace:
```typescript
declare namespace Express {
  export interface Request {
    user?: {
      id: string;
      role: "admin" | "user";
    };
  }
}
```

### The Architectural Hazard: Accidental Internal Merging
While declaration merging is indispensable for library augmentation, **you should avoid relying on declaration merging for your own internal application domain models**.
* **The Danger:** If two engineers on a team accidentally declare `interface Customer` in different files that share a global namespace, TypeScript will merge them silently without throwing a warning. This can cause bizarre compilation bugs where a component suddenly requires properties that were defined by a completely unrelated module.
* **Best Practice:** Keep application domain models strictly modular using ES6 `import` and `export` statements, and use distinct names or explicit inheritance (`interface DetailedCustomer extends BaseCustomer`) when extending internal domain shapes.
