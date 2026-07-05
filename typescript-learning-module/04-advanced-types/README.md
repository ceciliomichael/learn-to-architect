# Module 04: Advanced Types and Narrowing

In previous modules, we built static blueprints (interfaces) where every property was strictly known in advance. But real-world data is messy. 

Sometimes an API returns a string ID, and sometimes it returns a numeric ID. Sometimes a server returns a success message, and sometimes it returns a failure error. If your application crashes when data changes shape, it is not production-ready.

This module teaches you how to build flexible, adaptable types, and how to write intelligent logic that safely inspects dynamic data before acting on it.

---

## 1. Union Types: "This or That"

### The Real-World Analogy: The Dual-Port Charger
Imagine buying a modern phone charger for your car. The charger block has two different slots on the front: a rectangular USB-A slot, and a tiny oval USB-C slot. 
Because the charger supports a **Union** of port types, you can plug in a USB-A cable *OR* a USB-C cable, and the charger will function perfectly either way.

### The Core Technical Concept
A **Union Type** says a variable is allowed to hold one of several different data types. You declare it using the vertical pipe symbol `|` (which reads as "OR"):

```typescript
// The 'id' variable accepts EITHER a string OR a number
let currentUserId: string | number;

currentUserId = "user-abc"; // Valid!
currentUserId = 12345;      // Valid!
// currentUserId = true;    // COMPILER ERROR: Type 'boolean' is not assignable to string | number
```

### The Catch: You Cannot Access Unique Features Blindly!
If a box might contain a string OR a number, TypeScript will physically block you from using methods that only belong to one of them. For example, you cannot call `.toUpperCase()` on a union, because if the data turns out to be a number at runtime, the program will crash!

```typescript
function printId(id: string | number): void {
  // id.toUpperCase(); // COMPILER ERROR: Property 'toUpperCase' does not exist on type 'string | number'.
  
  console.log(id); // Perfectly safe, because BOTH strings and numbers can be printed.
}
```

### Built-in Keywords vs. Programmer-Invented Labels
| Word in Example | Category | Explanation |
| :--- | :--- | :--- |
| `string`, `number` | **Built-in Keywords** | Base primitive types. |
| `|` | **Built-in Syntax** | The Union (OR) operator. |
| `currentUserId`, `printId` | **Programmer-Invented Labels** | Custom variable and function identifiers. |

### Why Senior Developers Require This
When building web servers, route parameters from a URL might come in as text (`"104"`), but database queries might require true mathematical numbers (`104`). Instead of writing two entirely separate functions for `getUserByStringId()` and `getUserByNumberId()`, engineers use a union type to accept both flexibly in a single function signature.

---

## 2. Intersection Types: "This and That"

### The Real-World Analogy: The Swiss Army Flashlight
Imagine you take a standard Flashlight (which has a battery and a lightbulb). Then you take a Swiss Army Knife (which has a blade and a screwdriver). You hire a welder to melt them together into a single, ultimate survival tool. 
That new tool is an **Intersection**. It must possess EVERY single feature from BOTH of its original parent blueprints.

### The Core Technical Concept
An **Intersection Type** combines multiple blueprints into one massive blueprint. A variable assigned to an intersection type must satisfy ALL of the combined rules simultaneously. You declare it using the ampersand symbol `&` (which reads as "AND"):

```typescript
// Blueprint 1
type HasName = { name: string };
// Blueprint 2
type HasAge  = { age: number };

// Welded Blueprint (Intersection)
type Person = HasName & HasAge;

// The resulting object MUST contain BOTH properties!
const employee: Person = { 
  name: "Alice", 
  age: 30 
};
```

### Why Production Codebases Rely on This
When saving data to a PostgreSQL or MongoDB database, backend services take the raw user data (like `{ email, password }`) and intersect it with system audit timestamps (like `{ createdAt, updatedAt }`). Intersections allow engineers to combine these shapes cleanly without typing out monolithic 50-property blueprints.

---

## 3. Literal Types: Restricting to Exact Values

### The Real-World Analogy: The Elevator Button Panel
Inside an elevator, you don't have a blank keyboard where you can type any floor name you want (like "Hogwarts"). You have a panel with exactly four hardcoded plastic buttons: `1`, `2`, `3`, and `4`. You can only press those exact literal buttons.

### The Core Technical Concept
Instead of allowing a variable to hold *any* random string in the universe, you can restrict it to a specific set of exact text values. These are called **Literal Types**. 

```typescript
// This variable can only hold one of these four exact strings!
type CompassDirection = "North" | "South" | "East" | "West";

let currentHeading: CompassDirection = "North"; // Valid!
// currentHeading = "Up"; // COMPILER ERROR: Type '"Up"' is not assignable to type 'CompassDirection'.
```

### Why Senior Developers Require This
When building UI design systems (like buttons), you want to restrict other developers from passing invalid colors. If you type a button color as `string`, someone might pass `"banana"`. By typing it as `"primary" | "secondary" | "danger"`, the compiler catches the typo instantly.

---

## 4. Type Narrowing (`typeof` and `in`)

### The Real-World Analogy: The Security Checkpoint
If you have a Union Type (`string | number`), it is like a mixed crowd of VIPs and general admission ticket holders. To let the VIPs into the lounge, the security guard must **narrow** the crowd by asking for ID: *"If your ticket says VIP, walk through this door."*

### The Core Technical Concept
**Type Narrowing** is the process of writing `if` statements that prove to TypeScript what specific data type you are looking at. Once TypeScript is convinced, it unlocks the methods specific to that type.

#### Narrowing with `typeof` (For Primitive Types)
Use `typeof` to narrow primitive unions (like strings vs numbers):

```typescript
function formatValue(value: string | number): void {
  // Checkpoint 1: Are you a string?
  if (typeof value === "string") {
    // Inside this block, TypeScript narrows the type. It KNOWS it is a string!
    console.log(value.toUpperCase());
  } 
  // Checkpoint 2: You must be a number!
  else {
    // Inside this block, TypeScript unlocks number methods!
    console.log(value.toFixed(2));
  }
}
```

#### Narrowing with `in` (For Objects)
If you have a union of custom objects, `typeof` doesn't help because `typeof {}` always just returns `"object"`. To narrow between objects, use the `in` operator to ask: *"Does this specific property key exist inside this object?"*

```typescript
interface Car  { drive(): void; fuelType: string; }
interface Boat { sail(): void;  anchorWeight: number; }

function operateVehicle(vehicle: Car | Boat): void {
  // Checkpoint: Does the 'fuelType' key exist inside the vehicle object?
  if ("fuelType" in vehicle) {
    // TypeScript knows only Cars have fuelTypes! Narrows to Car!
    vehicle.drive();
  } else {
    // TypeScript knows it must be a Boat!
    vehicle.sail();
  }
}
```

### Symbol-by-Symbol Syntax Deconstruction
Let us deconstruct `if ("fuelType" in vehicle) {`:

* `if` -> Conditional control flow keyword.
* `(` -> Opening parenthesis for the condition expression.
* `"fuelType"` -> The literal string name of the property key we are looking for.
* `in` -> The built-in JavaScript operator that checks if a key exists inside an object.
* `vehicle` -> The object variable we are inspecting.
* `)` -> Closing parenthesis.
* `{` -> Opening block where the narrowed type is safely unlocked.

---

## 5. Custom Type Guards (`is`)

### The Core Technical Concept
Sometimes `typeof` and `in` are not powerful enough. You can write your own custom inspection function. 
A **Type Guard** is a function that returns a boolean, but instead of typing the return as `: boolean`, you use the special `: variable is Type` syntax. This explicitly tells the TypeScript compiler: *"If I return true, I guarantee this variable is this specific type."*

```typescript
interface FreeAccount { plan: "free" }
interface ProAccount  { plan: "pro"; features: string[] }

// The return type 'acc is ProAccount' is the magic Type Predicate!
function isProAccount(acc: FreeAccount | ProAccount): acc is ProAccount {
  // We return true if the plan equals "pro"
  return acc.plan === "pro";
}

function renderDashboard(account: FreeAccount | ProAccount): void {
  if (isProAccount(account)) {
    // TypeScript trusts the type guard! It narrows 'account' to ProAccount here!
    console.log("Pro Features: ", account.features);
  }
}
```

Without the `is ProAccount` keyword, TypeScript would just see a boolean return and would not understand that it was safe to unlock the `.features` array!

---

## 6. The `switch` Statement

### The Real-World Analogy: The Train Station Track Switcher
Imagine a train rolling into a station. A mechanical track switcher looks at the train's destination label. If the label says "North", it pulls lever A. If the label says "South", it pulls lever B.

### The Core Technical Concept
When a variable can hold many different literal values, writing a massive chain of `if / else if / else if / else` becomes very ugly. A `switch` statement is a cleaner tool designed specifically to check one variable against multiple exact matches.

```typescript
type UserStatus = "active" | "inactive" | "banned";

function describeStatus(status: UserStatus): string {
  // The Switcher looks at the 'status' variable
  switch (status) {
    case "active":
      return "User is currently online.";
    case "inactive":
      return "User has not logged in recently.";
    case "banned":
      return "User violated terms of service.";
    default:
      return "Unknown status.";
  }
}
```

Each `case` acts as a destination track. When the value matches a case, the code inside that case runs!

---

## 7. Discriminated Unions

### The Real-World Analogy: The Color-Coded ID Badges
Imagine a hospital where Doctors wear Blue badges, Nurses wear Green badges, and Visitors wear Red badges.
A security guard doesn't need to ask for a medical degree to know someone is a Doctor; they just look at the **discriminator** (the color of the badge).

### The Core Technical Concept
A **Discriminated Union** is an advanced architectural pattern. You create a union of multiple object blueprints, but you ensure that *every single blueprint shares one common property* (usually named `type`, `status`, or `kind`). That common property holds a unique Literal Type (the color of the badge).

```typescript
// Blueprint 1 (Blue Badge)
type LoadingState = { status: "loading" };

// Blueprint 2 (Green Badge)
type SuccessState = { status: "success"; data: string[] };

// Blueprint 3 (Red Badge)
type ErrorState   = { status: "error"; errorMessage: string; errorCode: number };

// The Union!
type RequestState = LoadingState | SuccessState | ErrorState;
```

When you pass this union into a `switch` statement, TypeScript is incredibly smart. It reads the shared `status` property and **instantly narrows the object** to the correct blueprint!

```typescript
function renderUI(state: RequestState): string {
  switch (state.status) {
    case "loading":
      return "Loading spinner...";
      
    case "success":
      // TypeScript perfectly knows state is SuccessState! We can access .data!
      return `Loaded ${state.data.length} items!`; 
      
    case "error":
      // TypeScript perfectly knows state is ErrorState! We can access .errorMessage!
      return `Failed (Code ${state.errorCode}): ${state.errorMessage}`;
  }
}
```

### Why Production Codebases Rely on This
This is the single most important pattern in modern UI development (React, Angular). It makes it literally impossible to write buggy code like `if (loading) { show(data) }` because the `data` array physically does not exist on the `LoadingState` blueprint! 

---

## 8. The `never` Type and Exhaustiveness Checking

### The Core Technical Concept
The `never` type represents a state that physically cannot happen. 
We use `never` as a safety net at the bottom of Discriminated Union `switch` statements to guarantee that we didn't forget any tracks. This is called **Exhaustiveness Checking**.

```typescript
function renderUI(state: RequestState): string {
  switch (state.status) {
    case "loading": return "Loading...";
    case "success": return "Success!";
    case "error":   return "Error!";
    default:
      // If the code reaches the default block, it means we forgot a case!
      // By assigning state to a variable typed as 'never', TypeScript will scream
      // at compile time if we ever add a new status (like "retrying") to the union 
      // but forget to add a case for it here!
      const _exhaustiveCheck: never = state;
      return _exhaustiveCheck;
  }
}
```

---

## 9. Type Casting (`as`)

### The Real-World Analogy: The "Trust Me" Override Badge
Sometimes you know more about a situation than the security guard. The guard sees a man in plain clothes, but you hold up a badge and say: *"Trust me, I am the Police Chief. Let him through."*

### The Core Technical Concept
Type Casting uses the `as` keyword to force TypeScript to treat a variable as a specific type, even if the compiler cannot mathematically prove it. **Use this rarely!**

```typescript
let mysteryData: unknown = "Hello World";

// TypeScript blocks this because unknown data is quarantined:
// let len = mysteryData.length;

// We use 'as' to override the compiler: "Trust me, this is definitely a string."
let forcedLength = (mysteryData as string).length; 
```

### Common Pitfalls & Mix-Ups
* **The Danger of `as`:** The `as` keyword does **not** change the actual data at runtime! It only shuts the compiler up. If you write `(mysteryData as string).toUpperCase()` and the data actually turns out to be a number at runtime, your application will crash. Only use `as` when you have 100% absolute architectural certainty.

---

## 10. The Non-Null Assertion Operator (`!`)

### The Core Technical Concept
If TypeScript warns you that a variable might be `null` or `undefined`, you can place an exclamation mark `!` at the very end of the variable name. This tells the compiler: *"I guarantee this is not null. Stop warning me."*

```typescript
function getHeaderElement(): HTMLElement {
  const header = document.getElementById("header-box");
  // document.getElementById returns HTMLElement | null.
  // The ! asserts: "Trust me, I hardcoded this box in the HTML, it exists."
  return header!;
}
```

### Why Senior Developers Reject This
Just like the `as` keyword, the `!` operator disables safety. If the HTML element was accidentally deleted by a junior developer, the `!` operator will cause a massive runtime crash (`TypeError: Cannot read properties of null`). 
**Professional Standard:** Do not use `!`. Write a safe `if` check instead!

```typescript
// The Professional Way:
const header = document.getElementById("header-box");
if (header === null) {
  throw new Error("Critical UI missing: header-box");
}
return header; // TypeScript safely narrows it to HTMLElement!
```

---

## 11. Enums

### The Real-World Analogy: The Labeled Switchboard
Imagine a flight control deck with a switch that can be set to 1, 2, or 3. Instead of forcing pilots to memorize that "1 = Takeoff, 2 = Cruise, 3 = Land", the engineers print a plastic label over the numbers.

### The Core Technical Concept
An **Enum** (Enumeration) creates a named dictionary of constant values. It provides autocompletion so developers don't make spelling mistakes.

```typescript
// String Enum
enum DeliveryStatus {
  Pending = "PENDING",
  Shipped = "SHIPPED",
  Delivered = "DELIVERED"
}

let packageStatus: DeliveryStatus = DeliveryStatus.Shipped;
```

### Common Pitfalls & Mix-Ups
* **Enums vs Literal Unions:** Modern TypeScript teams often prefer Literal Union types (`type Status = "PENDING" | "SHIPPED"`) over Enums. Why? Because Literal Unions are erased completely at compile time (zero performance cost). Enums actually generate real JavaScript objects in the final output, adding slight bundle bloat. Use Enums when you specifically need a real object to iterate over at runtime; otherwise, stick to Literal Unions!

---

## 12. Real-World Use Cases and Common Pitfalls

### Summary of Critical Beginner Pitfalls to Remember
1. **Confusing Union (`|`) with Intersection (`&`):** A Union means the data can be ONE of the choices. An Intersection means the data must combine EVERY property from ALL the choices simultaneously.
2. **The `typeof null` Bug:** Remember that `typeof null` returns `"object"` in JavaScript! If you are narrowing an object union, checking `if (typeof data === "object")` will accidentally let `null` values slip through. Always check `if (data !== null && typeof data === "object")`!
3. **The `is` Keyword Magic:** If you write a custom type guard function returning a boolean, but you forget to write `: data is SpecificType` in the return signature, TypeScript will not narrow the variable inside your `if` statements!
4. **Overusing `as` and `!`:** Beginners love using `as` and `!` because it instantly makes red squiggly compiler errors disappear. Never forget: turning off the smoke detector does not put out the fire. Use proper `if` narrowing instead of forcing the compiler to trust you!
