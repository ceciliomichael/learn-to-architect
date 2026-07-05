# Module 06: Type Manipulation and Utility Types

In Module 05, we learned how to pass types as variables into Generics. Now we take the next step: what if you need to take an existing interface blueprint and *transform* it into a brand new shape without copy-pasting code?

For example, when a user registers on your site, every profile field is strictly required (`User`). But when they visit the "Edit Profile" settings page, every field becomes optional because they might only want to update their bio (`Partial<User>`).

Instead of duplicating interface blueprints across your codebase, TypeScript provides **Utility Types** and **Type Manipulation** engines. This module teaches you how to programmatically transform types using built-in utilities, Mapped Types, Conditional Types, and Template Literal Types.

---

## 1. Object Shape Transformations (`Partial`, `Required`, `Readonly`)

### Let's Take an Editable User Form as an Example
To understand why object shape transformations exist without getting lost in jargon, imagine a physical paper document used by an HR department.
* **The Master Employee Blueprint:** When an employee is hired, they must fill out a 10-page master form. Every single box (Name, Address, Social Security Number, Tax Withholding) is strictly **Required**.
* **The Annual Address Update Form:** A year later, the employee moves to a new apartment. HR does not make them re-fill all 10 pages! They hand them a **Partial** amendment slip where every box is optional; the employee only fills in the specific address box they wish to change.
* **The Archived Employee File:** When an employee retires, HR places their file into a locked glass cabinet. The file is completely **Readonly**: no one is ever allowed to erase or alter a single word on those pages again.

In TypeScript, you don't write three separate interfaces for these three document states! You write one master interface, and use `Partial<T>`, `Required<T>`, and `Readonly<T>` to transform it dynamically.

### Transforming Object Modifiers
Let's define a master interface and see how TypeScript's built-in utility types modify its rules:

```typescript
// Our Master Blueprint
interface UserProfile {
  id: string;
  username?: string; // Originally optional
  email: string;
}

// 1. Partial<T>: Converts EVERY property in T into an optional property!
// Perfect for database UPDATE queries or patch forms where users only modify 1 or 2 fields.
type UpdateUserPayload = Partial<UserProfile>;
/* Resulting shape in memory:
{
  id?: string;
  username?: string;
  email?: string;
}
*/
let patchData: UpdateUserPayload = { email: "new_email@test.com" }; // Valid! id is optional!

// 2. Required<T>: Converts EVERY property in T into a strictly required property!
// Strips away optional question marks (?) from fields like username.
type CompleteUserRegistration = Required<UserProfile>;
/* Resulting shape in memory:
{
  id: string;
  username: string; // Notice: no longer optional!
  email: string;
}
*/
// let badReg: CompleteUserRegistration = { id: "1", email: "a@b.com" }; // COMPILER ERROR: Missing required property 'username'!

// 3. Readonly<T>: Locks EVERY property in T against reassignment!
// Perfect for redux state trees or frozen configuration objects.
type FrozenUser = Readonly<UserProfile>;
let archivedUser: FrozenUser = { id: "ID-1", email: "test@code.com" };
// archivedUser.email = "hacked@code.com"; // COMPILER ERROR: Cannot assign to 'email' because it is a read-only property.
```

### Syntax Symbols vs. Utility Names
| Word in Example | What It Is | Why It Matters |
| :--- | :--- | :--- |
| `Partial`, `Required`, `Readonly` | **Built-in Utility Types** | Standard generic transformers built into TypeScript's global compiler library. |
| `< >` (angle brackets) | **Generic Parameter Brackets** | Syntax used to pass our master blueprint into the transformation engine. |
| `UserProfile` | **Your Custom Master Blueprint** | The domain interface being transformed. |

### Deconstructing Utility Syntax
Let's look at `type UpdateUserPayload = Partial<UserProfile>;`:

* `type` -> Keyword registering a new type alias.
* `UpdateUserPayload` -> Our chosen identifier for the transformed shape.
* `=` -> Binding operator connecting the name to the transformation.
* `Partial` -> The built-in utility engine that attaches optional `?` modifiers to every property.
* `<` -> Opening generic parameter bracket.
* `UserProfile` -> The target interface being fed into the transformer.
* `>` -> Closing generic parameter bracket.
* `;` -> Statement terminator.

---

## 2. Property Plucking and Pruning (`Pick`, `Omit`, `Record`)

### Think of Selecting Specific Columns on a Spreadsheet
Imagine viewing a massive financial database spreadsheet with 50 columns: Employee ID, Full Name, Home Address, Bank Routing Number, Medical History, Salary, and Phone Number.
* **The Public Directory View:** If you want to print a public phone directory for office receptionists, you don't hand them the entire spreadsheet! You **Pick** strictly two columns: `FullName` and `PhoneNumber`.
* **The Third-Party Vendor View:** If you need to share employee records with an external IT vendor to set up email accounts, you want to share almost everything *except* highly sensitive financial and medical data. You **Omit** the `BankRoutingNumber`, `MedicalHistory`, and `Salary` columns.

In TypeScript, **`Pick<T, Keys>`** and **`Omit<T, Keys>`** allow you to slice and prune existing interfaces with surgical precision.

### Slicing Interfaces Cleanly
Let's see how to pluck specific properties or remove sensitive fields from a master database model:

```typescript
interface MasterEmployeeRecord {
  id: string;
  fullName: string;
  socialSecurityNumber: string; // Sensitive!
  bankAccountNumber: string;    // Sensitive!
  department: string;
  email: string;
}

// 1. Pick<T, Keys>: Plucks ONLY the specified keys out of the master blueprint!
// You can pick multiple keys by joining them with a union pipe (|).
type PublicDirectoryEntry = Pick<MasterEmployeeRecord, "fullName" | "email" | "department">;
/* Resulting shape in memory:
{
  fullName: string;
  email: string;
  department: string;
}
*/
let receptionDisplay: PublicDirectoryEntry = {
  fullName: "Elena Rostova",
  email: "elena@company.com",
  department: "Engineering"
};

// 2. Omit<T, Keys>: Copies the master blueprint, but PRUNES away the specified keys!
// Perfect for creating API payloads that strip out sensitive internal secrets.
type SafeVendorPayload = Omit<MasterEmployeeRecord, "socialSecurityNumber" | "bankAccountNumber">;
/* Resulting shape in memory:
{
  id: string;
  fullName: string;
  department: string;
  email: string;
}
*/
```

#### The `Record<KeyType, ValueType>` Utility
As introduced in Module 05, **`Record<K, V>`** is a built-in utility that constructs a clean dictionary object where all keys match type `K` and all stored values match type `V`:

```typescript
// Creating a dictionary mapping User ID strings to PublicDirectoryEntry objects!
type EmployeeDirectoryMap = Record<string, PublicDirectoryEntry>;

let companyDirectory: EmployeeDirectoryMap = {
  "EMP-101": { fullName: "Alice", email: "a@co.com", department: "Sales" },
  "EMP-102": { fullName: "Bob", email: "b@co.com", department: "Legal" }
};
```

---

## 3. Union Transformations (`Exclude`, `Extract`, `NonNullable`)

### Picture an Automated Coin Sorting Machine
Imagine pouring a bucket of mixed spare change and foreign tokens into an automated bank coin sorting machine. The machine has a series of vibrating mesh sieves:
* **The Exclude Sieve:** The first mesh filter is designed to **Exclude** any foreign arcade tokens or plastic buttons, shaking them out into a reject bin and leaving only official legal currency.
* **The Extract Sieve:** The second mesh filter is designed to **Extract** strictly silver quarters and dimes, isolating them from copper pennies.
* **The Clean Sieve:** The final filter shakes away any accumulated pocket lint, dust, or dirt (**NonNullable**), ensuring only clean, solid metal coins enter the wrapping paper.

In TypeScript, you apply these exact filtering sieves to **Union Types** using `Exclude<T, U>`, `Extract<T, U>`, and `NonNullable<T>`.

### Filtering Union Types Programmatically
When working with complex Union types (like status strings or mixed event payloads), these utilities allow you to filter out or isolate specific union members:

```typescript
// Our Master Union of possible application status codes
type AllStatusCodes = "IDLE" | "LOADING" | "SUCCESS" | "ERROR" | "TIMEOUT" | null | undefined;

// 1. Exclude<Union, RemovedMembers>: Removes specified members from the union!
// Let's remove error states from our status codes:
type SuccessfulStates = Exclude<AllStatusCodes, "ERROR" | "TIMEOUT">;
// Resulting Union: "IDLE" | "LOADING" | "SUCCESS" | null | undefined

// 2. Extract<Union, TargetMembers>: Plucks out strictly the members that match the target!
// Let's extract only the failure states:
type FailureStates = Extract<AllStatusCodes, "ERROR" | "TIMEOUT">;
// Resulting Union: "ERROR" | "TIMEOUT"

// 3. NonNullable<Union>: Automatically strips away null and undefined from any union!
type CleanStatusCodes = NonNullable<AllStatusCodes>;
// Resulting Union: "IDLE" | "LOADING" | "SUCCESS" | "ERROR" | "TIMEOUT"
```

### Why Why This Matters in Real-World Projects
When integrating with third-party database ORMs (like Prisma or TypeORM), database query results are frequently typed as `UserProfile | null | undefined` because a database lookup might fail to find a matching record. 

When you write a frontend rendering function that requires a guaranteed valid user object, you don't want to deal with null checks everywhere! Senior architects define `type ValidUser = NonNullable<DatabaseResult>;`, guaranteeing that after your initial database validation check, all downstream functions receive a strictly non-null data payload.

---

## 4. Function Inspection Utilities (`ReturnType`, `Parameters`)

### Think of Reverse-Engineering an Engine Specification
Imagine you are an engineer handed a sealed, highly complex mechanical engine built by another company (`a third-party library function`). You don't have access to the original architectural blueprint documents. However, you have precision measurement tools! You can attach a gauge to the input fuel pipe to measure exactly what size hose it requires (**Parameters**), and you can attach a meter to the exhaust manifold to measure exactly what energy output it produces (**ReturnType**).

In TypeScript, **`ReturnType<T>`** and **`Parameters<T>`** allow you to reverse-engineer and extract the exact parameter types and return types from existing functions without rewriting code!

### Extracting Types from Functions
Sometimes you import a third-party function from an npm library, but the author forgot to export the interfaces for the data types that function accepts or returns! You can extract those types programmatically using `typeof` combined with these utilities:

```typescript
// Imagine this function was imported from an external library:
function createPaymentTransaction(userId: string, amount: number, currency: "USD" | "EUR") {
  return {
    transactionId: "TX-998877",
    timestamp: new Date(),
    status: "CONFIRMED" as const,
    amountProcessed: amount
  };
}

// 1. ReturnType<typeof Function>: Plucks out the exact return type shape of the function!
type TransactionReceipt = ReturnType<typeof createPaymentTransaction>;
/* Resulting shape in memory:
{
  transactionId: string;
  timestamp: Date;
  status: "CONFIRMED";
  amountProcessed: number;
}
*/
let myReceipt: TransactionReceipt = {
  transactionId: "TX-111",
  timestamp: new Date(),
  status: "CONFIRMED",
  amountProcessed: 50.00
};

// 2. Parameters<typeof Function>: Plucks out all function inputs as a Tuple array!
type TransactionInputs = Parameters<typeof createPaymentTransaction>;
// Resulting Tuple Type: [userId: string, amount: number, currency: "USD" | "EUR"]

// You can even index into the tuple to grab a specific parameter's type!
type CurrencyOption = Parameters<typeof createPaymentTransaction>[2]; // Extracts: "USD" | "EUR"!
```

---

## 5. Mapped Types (`[P in keyof T]`)

### Imagine a Factory Assembly Line Customizing Every Car
Imagine an automotive factory assembly line that receives a frame for a standard vehicle with four doors, a hood, and a trunk.
* **The Armor-Plating Line:** The car moves down a specialized military assembly line. A robotic welding arm visits *every single compartment* on the car (the doors, the hood, the trunk) and welds bulletproof steel plating onto every single piece.
* **The Electrification Line:** The car moves down an EV conversion line. A robot visits *every single engine component* and replaces gas valves with electric wiring.

In TypeScript, a **Mapped Type** is that robotic assembly line. It allows you to write a loop inside a type definition (`[P in keyof T]`) that visits every single property inside an existing interface and applies a transformation rule to it!

### Building Custom Transformers from Scratch
Under the hood, built-in utilities like `Partial` and `Readonly` are actually just Mapped Types! Let's see how Mapped Type syntax works by building our own custom utility called **`NullableProperties<T>`**, which converts every property in an object into a nullable type:

```typescript
// Building a custom Mapped Type transformer!
type NullableProperties<T> = {
  // We loop over every property key P inside object T, and change its value type to include '| null'
  [P in keyof T]: T[P] | null;
};

interface HardwareConfig {
  cpuBrand: string;
  coreCount: number;
  isOverclocked: boolean;
}

// Applying our custom Mapped Type to our HardwareConfig!
type NullableHardware = NullableProperties<HardwareConfig>;
/* Resulting shape in memory:
{
  cpuBrand: string | null;
  coreCount: number | null;
  isOverclocked: boolean | null;
}
*/
```

### Syntax Symbols vs. Loop Variables
| Word in Example | What It Is | Why It Matters |
| :--- | :--- | :--- |
| `[ ]` (around loop syntax) | **Mapped Type Brackets** | Punctuation marking the start and end of a property iteration loop. |
| `in` (inside brackets) | **Iteration Keyword** | Language keyword instructing the engine to loop over every item in the union on the right. |
| `keyof T` | **Property Key Extractor** | Grabs a union of all property names from blueprint `T` (e.g., `"cpuBrand" | "coreCount"`). |
| `P` | **Your Custom Loop Variable** | The placeholder name representing the current property being visited (just like `let i` in a `for` loop!). |

---

## 6. Conditional Types (`T extends U ? X : Y`)

### Think of a Train Track Switch
Imagine a railroad junction with a mechanical track switch. When a train approaches the junction, an automated sensor checks the engine type:
* **If the train is an Electric High-Speed Passenger Train (`T extends Electric`):** The switch flips left, routing the train onto the high-speed passenger track (`Type X`).
* **If the train is a Heavy Freight Cargo Train:** The switch flips right, routing the train onto the industrial cargo loop (`Type Y`).

In TypeScript, **Conditional Types** act as that railroad track switch. They allow you to write ternary statements (`condition ? trueType : falseType`) directly inside your type definitions to route types dynamically!

### Routing Types Programmatically
To write a Conditional Type, use the ternary syntax: `T extends U ? TrueResult : FalseResult`. This reads as: *"If type T is assignable to type U, resolve to TrueResult; otherwise, resolve to FalseResult."*

```typescript
// A Conditional Type that inspects whether a type is an array!
// If T is an array of some element E, return E. Otherwise, return T as-is!
type Flatten<T> = T extends Array<infer ElementType> ? ElementType : T;

// 1. We pass an array of numbers. The switch flips left! It extracts and returns 'number'!
type NumericElement = Flatten<number[]>; // Resolves to: number

// 2. We pass a plain string. The switch flips right! It returns 'string' as-is!
type StringElement = Flatten<string>; // Resolves to: string
```

Notice the magical **`infer`** keyword! Inside a conditional check, writing `infer ElementType` tells TypeScript: *"If this condition matches, magically reach inside the array type and grab the internal element type, storing it in a temporary variable named `ElementType` so we can return it!"*

---

## 7. Template Literal Types (`${string}-${string}`)

### Imagine Standardized License Plate Patterns
Think about the rules for automobile license plates in certain states. A valid license plate isn't just any random string of characters; it must conform to a strict pattern: **Three uppercase letters, followed by a hyphen, followed by four numbers** (for example: `ABC-1234`). 

If you try to screw a license plate onto your car that reads `"HELLO-WORLD"`, the police will pull you over because it violates the structural pattern.

In TypeScript, **Template Literal Types** allow you to apply backtick string interpolation (`${ ... }`) directly at the *type level*, enforcing strict structural text patterns on string variables!

### Enforcing String Patterns and Event Names
You can combine literal strings with primitive types or unions inside backtick type definitions to generate powerful string pattern constraints:

```typescript
// 1. Enforcing strict ID formatting patterns
type ProductSku = `SKU-${number}-${string}`;

let validSku: ProductSku = "SKU-101-IPAD"; // Valid! Matches pattern!
let anotherSku: ProductSku = "SKU-999-LAPTOP"; // Valid!

// let badSku: ProductSku = "INVALID-101-IPAD"; // COMPILER ERROR: Does not start with "SKU-"!
// let badNumber: ProductSku = "SKU-abc-IPAD";  // COMPILER ERROR: Second section must be a number!

// 2. Generating dynamic event listener names from entity unions!
type Entity = "user" | "order" | "product";
type EventAction = "created" | "updated" | "deleted";

// TypeScript automatically multiplies the unions together, generating all 9 possible combinations!
type DomainEvent = `${Entity}:${EventAction}`;
/* Resulting Union in memory:
"user:created" | "user:updated" | "user:deleted" |
"order:created" | "order:updated" | "order:deleted" |
"product:created" | "product:updated" | "product:deleted"
*/

let myEvent: DomainEvent = "order:created"; // Perfectly valid!
// let typoEvent: DomainEvent = "user:destroyed"; // COMPILER ERROR: "destroyed" is not in EventAction!
```

---

## 8. Real-World Use Cases and Common Pitfalls

### Summary of Critical Beginner Pitfalls to Remember
1. **The Over-Transforming Trap:** Don't write incomprehensible type gymnastics just to show off!
   ```typescript
   // Unreadable Type Gymnastics (Nightmare for maintenance):
   type CrazyType<T> = T extends Record<string, infer U> ? (U extends Array<infer V> ? Pick<V, "id"> : never) : Partial<T>;

   // Clean, Professional Architecture: Keep transformations simple, named, and modular!
   type ArrayElement<T> = T extends Array<infer E> ? E : never;
   type IdOnly<T> = Pick<T, "id">;
   ```
2. **Confusing `Partial<T>` with `[key: string]: undefined`:** Making properties optional using `Partial<UserProfile>` means a property can either hold its required data type *or* be omitted. It does NOT mean you should explicitly assign `undefined` to every single key!
3. **Forgetting that `Record<string, T>` Allows Any String Key:** When you type a dictionary as `Record<string, number>`, TypeScript allows you to access *any* arbitrary string key (e.g., `myDict["random_key"]`), and the compiler assumes it returns a `number`! In strict production codebases, remember that accessing a non-existent key at runtime actually returns `undefined`. Combine `Record` with optional types (`Record<string, number | undefined>`) or enable `noUncheckedIndexedAccess` in your `tsconfig.json`!
