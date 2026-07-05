# Module 02: Objects, Interfaces, and Type Aliases

In the previous module, we worked with single primitive values like strings, numbers, and booleans. But real software doesn't deal in isolated primitives. An e-commerce application doesn't just pass around a price or a name; it passes around a complete **Product** or a **User** profile: complex data structures that group multiple pieces of information together.

This module teaches you how to model real-world entities in TypeScript using Objects, Interfaces, and Type Aliases. We will explore how to design custom blueprints, how structural typing works under the hood, and how to choose between Interfaces and Type Aliases in production codebases.

---

## 1. What is an Object?

### Let's Take an ID Badge as an Example
To understand how objects work in programming, imagine looking at an employee's physical ID badge clipped to their shirt. The badge isn't just a single word; it's a structured container holding several related facts about that person:
* **Name:** "Sarah Connor"
* **Department:** "Security"
* **Access Level:** 5
* **Is Active:** true

In TypeScript, an **object** is the digital equivalent of that ID badge. It is a single memory container that groups multiple related pieces of information together into labeled key-value pairs.

### How Objects Organize Data
Instead of creating ten separate variables for a single user's profile, you group those facts inside curly braces `{ ... }`. Each piece of data is assigned a specific label (called a **property** or **key**), followed by a colon and the stored value:

```typescript
// Grouping related data into a single object container
let employeeBadge = {
  name: "Sarah Connor",
  department: "Security",
  accessLevel: 5,
  isActive: true
};

// Accessing individual properties using dot notation
console.log(employeeBadge.name); // Outputs: "Sarah Connor"
console.log(employeeBadge.accessLevel); // Outputs: 5
```

If you don't provide a type annotation, TypeScript inspects the object at creation time and locks down the shape automatically. If you later try to assign the wrong type of data to a property, or try to add a property that didn't exist originally, the compiler stops you:

```typescript
// employeeBadge.accessLevel = "high"; // COMPILER ERROR: Type 'string' is not assignable to type 'number'.
// employeeBadge.location = "Building A"; // COMPILER ERROR: Property 'location' does not exist on type...
```

### Separating Syntax from Your Chosen Names
| Word in Example | What It Is | Why It Matters |
| :--- | :--- | :--- |
| `{ }` (curly braces) | **Built-in Object Syntax** | Punctuation marking the start and end of an object literal in computer memory. |
| `:` (colon), `,` (comma) | **Built-in Separators** | Punctuation separating keys from values, and separating individual properties from one another. |
| `employeeBadge`, `name`, `accessLevel` | **Your Custom Labels** | Arbitrary names chosen by you to represent the domain data. You could rename `accessLevel` to `securityRank` without altering language mechanics. |

### Translating Object Creation Symbol-by-Symbol
Let's take `let employeeBadge = { name: "Sarah" };` and translate it into plain English:

* `let` -> Command to allocate a new variable container in memory.
* `employeeBadge` -> Your custom identifier for this entire object container.
* `=` -> Assignment operator putting the object literal on the right into the container on the left.
* `{` -> Opening curly brace marking the creation of an object structure.
* `name` -> The property key (the label attached to this specific compartment inside the object).
* `:` -> Key-value separator dividing the property name from its stored data.
* `"Sarah"` -> The literal string value stored inside the `name` compartment.
* `}` -> Closing curly brace marking the end of the object structure.
* `;` -> Statement terminator.

### Why Why This Matters in Real-World Projects
In full-stack web applications, frontend components communicate with backend servers by sending and receiving JSON (JavaScript Object Notation) payloads over the network. Whether you are fetching a customer order or submitting a registration form, the data is always formatted as an object. Understanding how to interact with object properties safely is essential for building modern web APIs.

### Watch Out for the Comma vs. Semicolon Trap
When writing object literals inside curly braces `{ ... }`, individual properties must be separated by **commas**, not semicolons!
```typescript
// Correct: properties separated by commas
let serverConfig = { host: "localhost", port: 8080 };

// Incorrect: semicolons inside object literals will cause syntax errors!
// let badConfig = { host: "localhost"; port: 8080; };
```

---

## 2. Type Aliases (`type`)

### Think of a Custom Blueprinted Label
Imagine you are managing an inventory of thousands of books. Instead of verbally explaining to every new employee that *"a book consists of a title string, an author string, and a page count number"* over and over again, you print out a standardized paper checklist titled **BookBlueprint**. Whenever a new shipment arrives, employees simply check each item against the **BookBlueprint** checklist.

In TypeScript, a **Type Alias** (created using the `type` keyword) is that standardized paper checklist. It allows you to invent a custom name for a specific data structure so you can reuse it across your codebase without typing out the full shape repeatedly.

### Creating Reusable Custom Shapes
To create a Type Alias, you use the `type` keyword followed by your custom PascalCase name, an equals sign `=`, and the type definition:

```typescript
// Defining a reusable custom type alias for a User Profile
type UserProfile = {
  username: string;
  email: string;
  accountAgeDays: number;
  isPremiumMember: boolean;
};

// Using our custom UserProfile type to annotate variables
let primaryAccount: UserProfile = {
  username: "code_wizard",
  email: "wizard@code.com",
  accountAgeDays: 365,
  isPremiumMember: true
};

let secondaryAccount: UserProfile = {
  username: "data_ninja",
  email: "ninja@data.com",
  accountAgeDays: 12,
  isPremiumMember: false
};
```

If you forget to include a required property, or if you misspell a key when creating a `UserProfile` object, the compiler immediately flags the error:

```typescript
// COMPILER ERROR: Property 'email' is missing in type '{ username: string; ... }' but required in type 'UserProfile'.
let brokenAccount: UserProfile = {
  username: "incomplete_user",
  accountAgeDays: 5,
  isPremiumMember: false
};
```

### Keywords vs. Type Names
| Word in Example | What It Is | Why It Matters |
| :--- | :--- | :--- |
| `type` | **Built-in Language Command** | A keyword instructing TypeScript to register a new custom type definition in its dictionary. |
| `UserProfile` | **Your Custom Type Name** | The identifier you invented for this blueprint (by convention, custom type names always start with a Capital Letter). |
| `primaryAccount`, `secondaryAccount` | **Your Custom Variable Labels** | The names of the actual memory containers storing physical data. |

### Deconstructing a Type Alias Definition
Let's look at `type UserProfile = { username: string; };`:

* `type` -> Keyword initiating the creation of a custom type alias.
* `UserProfile` -> The name we chose for our new custom type.
* `=` -> The binding operator linking our custom name to the shape definition on the right.
* `{` -> Opening curly brace marking an object type shape.
* `username` -> The required property key name.
* `:` -> Type annotation anchor inside the shape definition.
* `string` -> The primitive type required for the `username` property.
* `;` -> Property separator (inside type definitions, properties are conventionally separated by semicolons!).
* `}` -> Closing curly brace ending the object type shape.
* `;` -> Statement terminator.

### Keeping Codebases DRY (Don't Repeat Yourself)
Imagine building an application with 50 different functions that handle user data: functions to update profile pictures, calculate billing discounts, and send notification emails. If you didn't have Type Aliases, you would have to manually type out `{ username: string; email: string; ... }` in all 50 function headers! If your boss later asked you to add a `phoneNumber` field, you would have to edit 50 different files. 

By defining a single `type UserProfile`, you only ever update the definition in one central file, and all 50 functions instantly inherit the new rule.

### Type Aliases Are Not Just for Objects
While Type Aliases are frequently used for object shapes, they can also be used to create nicknames for primitive unions, tuples, or functions:
```typescript
// Creating a custom nickname for a string or number union
type CustomerId = string | number;

let id1: CustomerId = "CUST-1001";
let id2: CustomerId = 84920;
```

---

## 3. Interfaces (`interface`)

### Picture an Architectural Blueprint
Think of an architect drawing a master blueprint for a new office building. The blueprint specifies the exact structural requirements: *"There must be a main entrance door, four fire exits, and an electrical grid."* The blueprint itself isn't a building you can walk into; it is a binding structural contract. The construction crew must build the physical building to match every specification on that blueprint.

In TypeScript, an **Interface** (created using the `interface` keyword) is that architectural blueprint. It is a formal structural contract that defines the exact property names and data types an object must possess.

### Defining Structural Contracts
To declare an interface, you use the `interface` keyword followed by your custom PascalCase name and an object shape definition wrapped in curly braces `{ ... }` (notice that unlike `type`, there is **no equals sign** after the interface name!):

```typescript
// Defining a structural blueprint for a Server Configuration
interface ServerConfig {
  hostIp: string;
  portNumber: number;
  enableSsl: boolean;
}

// Creating a physical object that adheres to the ServerConfig contract
let productionServer: ServerConfig = {
  hostIp: "192.168.1.10",
  portNumber: 443,
  enableSsl: true
};
```

Just like with Type Aliases, any object annotated with an Interface must provide every required property with the exact specified data type, or the TypeScript compiler will refuse to compile the code.

### Keywords vs. Blueprint Names
| Word in Example | What It Is | Why It Matters |
| :--- | :--- | :--- |
| `interface` | **Built-in Language Command** | A keyword instructing TypeScript to create a new structural blueprint contract. |
| `ServerConfig` | **Your Custom Blueprint Name** | The identifier chosen by you to name the contract (always written in PascalCase). |
| `productionServer` | **Your Custom Variable Label** | The identifier of the physical object in memory adhering to the contract. |

### Deconstructing an Interface Declaration
Let's look at `interface ServerConfig { hostIp: string; }`:

* `interface` -> Keyword initiating a formal structural contract definition.
* `ServerConfig` -> The custom name we assigned to this blueprint.
* `{` -> Opening curly brace marking the beginning of the contractual rules.
* `hostIp` -> The name of the required property key.
* `:` -> Type annotation anchor linking the key to its required data type.
* `string` -> The primitive data type required for `hostIp`.
* `;` -> Property separator terminating this specific rule.
* `}` -> Closing curly brace marking the end of the interface contract.

### Enabling Clean Team Collaboration
In large engineering organizations, different teams build different parts of an application. The frontend UI team building a checkout screen might not know how the backend database team writes their SQL queries. 

To work together seamlessly, both teams agree on an `interface OrderPayload` upfront. Once the interface is defined, the frontend team writes UI code that generates objects matching the blueprint, while the backend team writes API handlers expecting objects matching the blueprint. Both teams can work independently without stepping on each other's toes.

### Don't Add an Equals Sign!
One of the most frequent syntax errors made by developers transitioning from `type` to `interface` is accidentally inserting an equals sign after the interface name:
```typescript
// Incorrect: Interfaces do NOT use equals signs!
// interface BadSyntax = { name: string; };

// Correct: Directly open curly braces after the name
interface GoodSyntax { name: string; }
```

---

## 4. Optional Properties (`?`) and Readonly Properties (`readonly`)

### Picture Hotel Room Amenities and Serial Numbers
When you check into a hotel room, certain features are mandatory (a bed, a bathroom, a door lock), while other amenities are **optional**: some luxury suites come with a balcony or a mini-bar, but standard rooms do not. You wouldn't turn away a guest just because their room lacks a mini-bar.

At the same time, consider the television set in that hotel room. On the back of the TV is a manufacturer serial number printed on a metal tag. You are allowed to read the serial number, but it is **read-only**: you cannot scrape it off and paint on a new serial number.

In TypeScript, you use the question mark `?` to make properties optional, and the `readonly` modifier to prevent properties from being modified after creation.

### Handling Flexible and Permanent Data
By default, every property listed in an Interface or Type Alias is strictly required. You can modify this behavior using two special symbols:

1. **Optional Properties (`?`):** Place a question mark immediately after the property name (before the colon) to signal that the property is optional. If omitted, its value defaults to `undefined`.
2. **Readonly Properties (`readonly`):** Place the keyword `readonly` before the property name to prevent anyone from modifying its value after the object is initially created.

```typescript
interface UserAccount {
  readonly accountId: string; // Permanent: cannot be changed after creation!
  username: string;           // Required: must always be provided
  profileBio?: string;        // Optional: can be a string, or omitted entirely (undefined)
}

let newUser: UserAccount = {
  accountId: "ID-998877",
  username: "elena_codes"
  // Notice we omitted profileBio entirely, and the compiler is perfectly happy!
};

// Reading properties is perfectly fine
console.log(newUser.accountId); // Outputs: "ID-998877"

// Modifying normal properties is allowed
newUser.username = "elena_dev";

// Modifying readonly properties is BLOCKED by the compiler:
// newUser.accountId = "ID-000000"; // COMPILER ERROR: Cannot assign to 'accountId' because it is a read-only property.
```

### Modifiers vs. Property Names
| Word in Example | What It Is | Why It Matters |
| :--- | :--- | :--- |
| `readonly` | **Built-in Modifier Keyword** | Instructs the compiler to freeze the property against future reassignments. |
| `?` (question mark) | **Built-in Modifier Symbol** | Instructs the compiler that the property is optional (`string | undefined`). |
| `accountId`, `profileBio` | **Your Custom Property Labels** | The names of the specific compartments inside the object. |

### Deconstructing Modifiers
Let's look at `readonly accountId?: string;`:

* `readonly` -> Keyword enforcing immutability on this specific property slot.
* `accountId` -> The name of the property compartment.
* `?` -> Optional modifier symbol making this property optional.
* `:` -> Type annotation anchor.
* `string` -> The required data type if the property is present.
* `;` -> Property rule terminator.

### Protecting Database IDs and Handling Missing Profile Data
In full-stack web applications, database records always possess unique primary keys (like UUIDs or database IDs). Once a user account or an order is created in PostgreSQL or MongoDB, its ID must never change! Marking `readonly id: string` prevents bugs where an engineer accidentally overwrites an item's unique database ID in memory.

Similarly, when users build public social profiles, fields like `twitterHandle?`, `linkedInUrl?`, and `avatarImage?` are optional. If TypeScript forced every user to provide a Twitter handle just to sign up, your conversion rate would plummet. Optional properties allow developers to model real-world flexibility safely.

### Why You Should Enable `exactOptionalPropertyTypes`
In standard TypeScript setups, declaring `bio?: string` means the property can either be omitted or explicitly set to `undefined` (`{ bio: undefined }`). In high-reliability production codebases, teams enable the `exactOptionalPropertyTypes` compiler flag in `tsconfig.json`. This strict setting forces a clear distinction between *"the property was omitted entirely"* versus *"the property was explicitly set to undefined"*, preventing subtle bugs in database ORM updates.

---

## 5. Extending Interfaces (`extends`)

### Imagine Parent and Child Blueprints
Imagine an auto manufacturer designing blueprints for commercial vehicles. First, they draw a general master blueprint called **BaseVehicle** that specifies fundamental features shared by all vehicles: *wheels, an engine, and headlights*. 

When they want to design an **Ambulance**, they don't redraw the wheels, engine, and headlights from scratch! Instead, they draw a specialized child blueprint that states: *"Copy all specifications from BaseVehicle, and add a siren, a stretcher, and emergency medical equipment."*

In TypeScript, interface inheritance using the **`extends`** keyword allows you to copy all properties from a parent blueprint into a child blueprint without repeating code.

### Building Hierarchies Without Repetition
Instead of copying and pasting shared properties across multiple interfaces, you use the `extends` keyword followed by the parent interface name:

```typescript
// 1. The Parent Blueprint (shared across all entities)
interface BaseDatabaseRecord {
  readonly id: string;
  createdAt: Date;
  updatedAt: Date;
}

// 2. The Child Blueprint (inherits id, createdAt, and updatedAt automatically!)
interface CustomerRecord extends BaseDatabaseRecord {
  customerName: string;
  accountBalance: number;
  loyaltyTier: string;
}

// Creating a physical object adhering to the extended CustomerRecord contract
let customer: CustomerRecord = {
  id: "REC-101",
  createdAt: new Date(),
  updatedAt: new Date(),
  customerName: "Marcus Vance",
  accountBalance: 5400.00,
  loyaltyTier: "Gold"
};
```

You can even extend **multiple parent interfaces simultaneously** by separating their names with commas (`interface SuperUser extends User, Admin { ... }`).

### Keywords vs. Blueprint Names
| Word in Example | What It Is | Why It Matters |
| :--- | :--- | :--- |
| `extends` | **Built-in Language Command** | Instructs TypeScript to inherit all property definitions from the specified parent blueprint(s). |
| `BaseDatabaseRecord`, `CustomerRecord` | **Your Custom Blueprint Names** | The identifiers representing the parent and child contracts. |

### Deconstructing Inheritance Syntax
Let's look at `interface CustomerRecord extends BaseDatabaseRecord {`:

* `interface` -> Keyword initiating a blueprint contract definition.
* `CustomerRecord` -> The name of our new specialized child blueprint.
* `extends` -> Inheritance keyword instructing the compiler to import all properties from a parent.
* `BaseDatabaseRecord` -> The target parent blueprint being copied.
* `{` -> Opening curly brace to define additional properties specific to the child.

### Designing Scalable Enterprise Domain Models
In enterprise software systems (like Salesforce or SAP), database tables share standardized metadata fields across every single entity: creation timestamps, modification tracking, and tenant IDs. 

By defining a core `interface BaseEntity`, every domain model in your application (such as `Product extends BaseEntity`, `Invoice extends BaseEntity`, and `Employee extends BaseEntity`) automatically inherits these critical auditing fields. If the security team later requires adding a `lastModifiedByUserId` field to every database table, you only add it once to `BaseEntity`, and your entire architecture updates instantly.

### Extending Interfaces vs. Intersecting Type Aliases
While Interfaces use the `extends` keyword, Type Aliases accomplish the exact same inheritance goal using the **Intersection Operator (`&`)**:
```typescript
type BaseRecord = { readonly id: string; };
type CustomerType = BaseRecord & { customerName: string; };
```
Both approaches produce identical object shapes in memory! We will explore the nuanced technical differences between them in Section 8.

---

## 6. Index Signatures (Dynamic Keys)

### Picture a Hotel Front Desk Mailbox Grid
Imagine standing at the front desk of a grand hotel. Behind the concierge is a massive wall of wooden cubbies used for storing guest mail and room keys. The cubbies are labeled by room number: Cubby 101, Cubby 102, Cubby 103, and so on up to Room 999.

When the hotel was built, the architect didn't know the exact names of the thousands of guests who would eventually stay in those rooms over the next fifty years! Instead, the architect established a simple structural rule: *"Every cubby on this wall will be identified by a room number string, and whatever is placed inside that cubby must be a mail item."*

In TypeScript, an **Index Signature** is that mailbox grid rule. It allows you to define object types where you do not know the exact property names in advance, but you know the data type of the keys and values.

### Typing Dynamic Dictionaries and Lookups
Sometimes you need to build objects that act as dictionaries, translation maps, or lookup tables where property names are generated dynamically at runtime. To define an Index Signature, you wrap a placeholder key name and type inside square brackets `[key: string]`, followed by a colon and the value type:

```typescript
// Defining a translation dictionary where ANY text string key maps to a text string value
interface EnglishToSpanishDictionary {
  [word: string]: string;
}

// Creating a dictionary object with arbitrary dynamic word keys
let dictionary: EnglishToSpanishDictionary = {
  "hello": "hola",
  "goodbye": "adiós",
  "water": "agua",
  "computer": "computadora"
};

// Adding new dynamic keys later is perfectly valid!
dictionary["book"] = "libro";

// Attempting to store a non-string value is BLOCKED by the compiler:
// dictionary["pageCount"] = 350; // COMPILER ERROR: Type 'number' is not assignable to type 'string'.
```

You can also create numeric index signatures (`[index: number]: string`), which is how TypeScript internally types arrays and array-like objects!

### Syntax Symbols vs. Placeholder Names
| Word in Example | What It Is | Why It Matters |
| :--- | :--- | :--- |
| `[ ]` (in type definitions) | **Index Signature Syntax** | Brackets inside an interface definition indicating dynamic, open-ended property names. |
| `word`, `key`, `index` | **Your Custom Placeholder Labels** | Arbitrary identifier names used inside the brackets to represent the dynamic key (purely for human readability). |
| `string` | **Built-in Type Rule** | The data type required for the dynamic keys and values. |

### Deconstructing an Index Signature
Let's look at `[word: string]: string;`:

* `[` -> Opening square bracket marking the start of an index signature definition.
* `word` -> Developer-chosen placeholder label describing what the keys represent (helps other developers understand the dictionary's purpose).
* `:` -> Type annotation anchor for the key itself.
* `string` -> Rule requiring all dynamic property names to be text strings.
* `]` -> Closing square bracket ending the key definition.
* `:` -> Type annotation anchor for the stored values.
* `string` -> Rule requiring all data stored inside these dynamic compartments to be text strings.
* `;` -> Rule terminator.

### Caching API Responses and Building Lookup Tables
In frontend web applications, querying a backend server over the network for user profiles is slow. To speed up performance, engineers build **In-Memory Caches**: dictionary objects that store previously downloaded user profiles in memory, keyed by their unique user IDs:

```typescript
interface UserProfile { name: string; email: string; }

// A cache dictionary where dynamic User ID strings map to UserProfile objects
interface UserCache {
  [userId: string]: UserProfile;
}

let activeUsersCache: UserCache = {};

function storeInCache(id: string, profile: UserProfile): void {
  activeUsersCache[id] = profile; // Fast, type-safe dynamic storage!
}
```

### The "All Properties Must Match" Rule
A critical technical constraint of Index Signatures is that once you declare `[key: string]: string`, **every other property in that interface must also conform to that value type**!
```typescript
interface BadDictionary {
  [key: string]: string; // Rule: ALL properties must have string values!
  // pageCount: number; // COMPILER ERROR: Property 'pageCount' of type 'number' is not assignable to 'string' index type.
}
```
If you need an object with both dynamic string properties and specific numeric properties, use a Union type: `[key: string]: string | number;`.

---

## 7. Structural Typing (Duck Typing)

### Imagine a Universal Mechanical Power Plug
Think about plugging an appliance into a standard wall electrical outlet in your home. The wall outlet does not care about the brand name printed on your appliance! It doesn't care if you plug in a Samsung toaster, a Sony television, or a generic desk lamp. 

The wall outlet only enforces one mechanical rule: *"Does this plug physically possess two parallel brass prongs of the exact correct dimensions?"* If the physical prongs fit into the slots, electric power flows.

In TypeScript, this concept is called **Structural Typing** (often referred to in computer science as **Duck Typing**: *"If it walks like a duck and quacks like a duck, treat it like a duck"*). TypeScript does not care about the formal brand names of your types; it only cares whether the physical shapes match!

### How TypeScript Compares Shapes
In nominal programming languages like Java or C++, if you define two classes with identical properties, you cannot pass an instance of Class A into a function expecting Class B unless they explicitly inherit from each other. 

In TypeScript, type compatibility is evaluated strictly by **shape**:

```typescript
// Blueprint 1: A 2D Coordinate Point
interface Point2D {
  x: number;
  y: number;
}

// Blueprint 2: A Vector in space (identical shape, completely different name!)
interface Vector2D {
  x: number;
  y: number;
}

// A function expecting a Point2D blueprint
function printCoordinates(point: Point2D): void {
  console.log(`X: ${point.x}, Y: ${point.y}`);
}

// We create a Vector2D object...
let myVector: Vector2D = { x: 10, y: 25 };

// Perfectly valid! TypeScript checks the shape (x: number, y: number), sees a perfect match, and allows it!
printCoordinates(myVector);
```

#### The "Extra Properties" Rule (Subtyping)
What happens if you pass an object that has **extra properties** beyond what the blueprint asks for?

```typescript
interface ThreeDimensionalPoint {
  x: number;
  y: number;
  z: number; // Extra property not required by Point2D!
}

let my3DPoint: ThreeDimensionalPoint = { x: 5, y: 10, z: 15 };

// Perfectly valid! my3DPoint has x and y, which satisfies Point2D. 
// TypeScript ignores the extra 'z' property when passing a variable reference!
printCoordinates(my3DPoint);
```

As long as an object possesses *at least* all the required properties of the target type, TypeScript considers it compatible.

### Structural Comparison vs. Nominal Comparison
| Concept | How It Works | Which Languages Use It |
| :--- | :--- | :--- |
| **Structural Typing** | Compares the actual physical properties and shapes of the data structures. | **TypeScript**, Go, Rust (traits) |
| **Nominal Typing** | Compares the formal explicit brand names and declaration inheritance trees. | **Java**, C++, C#, Swift |

### Why Why This Matters in Real-World Projects
In modern web development, your codebase relies on dozens of external open-source libraries installed via npm. Suppose you install a charting library that expects a configuration object formatted as `{ width: number; height: number; }`. 

Because TypeScript uses Structural Typing, you do not need to import and explicitly inherit from the charting library's proprietary `ChartSize` class! You simply pass in any plain JavaScript object or custom type from your own domain that happens to possess `width` and `height` numeric properties. This makes integrating third-party libraries effortless and decoupled.

### The Excess Property Checking Trap
If Structural Typing allows extra properties, why does the following code throw a compiler error?
```typescript
interface Point2D { x: number; y: number; }

// COMPILER ERROR: Object literal may only specify known properties, and 'z' does not exist in type 'Point2D'.
let badPoint: Point2D = { x: 5, y: 10, z: 15 };
```

**The Explanation:** When you assign an **object literal directly** to a typed variable or pass it directly into a function as an inline argument, TypeScript activates a special safety check called **Excess Property Checking**. This rule assumes that typing extra properties directly inline is almost certainly a typo! 

To pass extra properties without triggering this error, you must assign the object to an intermediate variable first (`let my3DPoint = ...`), or explicitly include the extra property in your blueprint using an optional modifier or index signature.

---

## 8. Interfaces vs. Type Aliases: When to Use Which

### Imagine an Open City Ledger vs. A Sealed Wax Contract
To understand when to use an Interface versus a Type Alias, imagine two different types of legal documents:
1. **The Open City Ledger (`interface`):** A public registry book kept in the town hall. If the town council passes a new law, they can open the ledger and append new rules to the existing page at any time. The ledger is open to **Declaration Merging**.
2. **The Sealed Wax Contract (`type`):** A private contract written on parchment, rolled up, and stamped with a permanent hot wax seal. Once the wax seal cools, the contract is strictly closed. You can never open it up to add new clauses; you can only create a brand new contract that combines old terms with new ones.

### The Technical Differences
For 90% of everyday object modeling tasks, `interface` and `type` behave identically and can be used interchangeably. However, they possess three distinct technical differences that dictate when senior architects choose one over the other:

#### Difference 1: Declaration Merging (Only Interfaces Can Do This!)
If you declare two Interfaces with the exact same name in the same scope, TypeScript automatically merges their properties together into a single unified blueprint!
```typescript
// First declaration in File A
interface Window {
  title: string;
}

// Second declaration in File B (same name!)
interface Window {
  isMaximized: boolean;
}

// TypeScript automatically merges them! The Window interface now requires BOTH properties:
let myWindow: Window = {
  title: "My App",
  isMaximized: true
};
```
If you attempt to declare two Type Aliases with the same name, TypeScript throws a fatal compiler error (`Duplicate identifier 'Window'`).

#### Difference 2: Primaries, Unions, and Tuples (Only Type Aliases Can Do This!)
An Interface can *only* define object shapes. It cannot create nicknames for primitive values, Union types, or Tuple arrays. If you need to name a Union or primitive, you must use `type`:
```typescript
// Valid: Type alias creating a union nickname
type Status = "pending" | "approved" | "rejected";

// INVALID: Interfaces cannot model unions or primitives!
// interface Status = "pending" | "approved"; // SYNTAX ERROR!
```

#### Difference 3: Error Message Readability
When complex type errors occur in deeply nested objects, TypeScript's compiler tooltips often display Interface names cleanly by their short brand name (e.g., `Type 'UserProfile' is not assignable...`). When Type Aliases involving complex intersections fail, the compiler sometimes expands the entire raw object structure in the error tooltip, making debugging slightly harder for beginners.

### The Senior Engineer's Decision Matrix
In professional enterprise architectures, follow this simple rule of thumb:

| Situation / Requirement | Which to Choose | Why |
| :--- | :--- | :--- |
| **Defining standard Object shapes** (Users, Products, API payloads) | **`interface`** | Provides cleaner compiler error messages, better IDE autocompletion performance, and clean inheritance via `extends`. |
| **Building open-source libraries or SDKs** | **`interface`** | Allows external developers to extend your library's configuration objects using Declaration Merging. |
| **Defining Unions, Primitives, or Tuples** | **`type`** | Interfaces physically cannot model these data structures. |
| **Composing complex functional transformations** | **`type`** | Advanced type manipulation (mapped types, conditional types) requires Type Aliases. |

---

## 9. Real-World Use Cases and Common Pitfalls

### Summary of Critical Beginner Pitfalls to Remember
1. **The Equals Sign Trap:** Never write `interface User = { ... }`. Interfaces never use equals signs! Only `type` aliases use equals signs (`type User = { ... }`).
2. **The Comma vs Semicolon Trap:** When defining blueprint rules inside `interface` or `type`, separate properties with **semicolons** `;`. When writing actual object literals with real data in memory, separate key-value pairs with **commas** `,`.
3. **The Excess Property Literal Trap:** If you pass an object literal directly into a function like `printUser({ name: "Alice", age: 25, extra: true })`, TypeScript will throw an error on `extra` even under Structural Typing! To pass extra properties safely, assign the object to an intermediate variable first or update your interface blueprint.
4. **Over-using `any` in Index Signatures:** When creating dynamic dictionaries like `[key: string]: any`, you destroy type safety for all values stored in that dictionary. Always try to type index signatures as strictly as possible, such as `[key: string]: string` or `[key: string]: unknown`.
