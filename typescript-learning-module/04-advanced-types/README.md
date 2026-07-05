# Module 04: Advanced Types and Narrowing

In early modules, our variables held simple, static types: a string, a number, or a single interface blueprint. But real-world data is dynamic and unpredictable. An API endpoint might return a success object *or* an error message; an HTML input might contain a text string *or* be completely empty (`null`).

To model these flexible scenarios safely, TypeScript provides **Advanced Type Operators** (Unions and Intersections) and **Type Narrowing** techniques. This module teaches you how to combine types, how to safely inspect variables at runtime, how to build custom type guards, and how to use discriminated unions to eliminate bugs in complex state machines.

---

## 1. Union Types (`|`)

### Let's Take a Multi-Currency Cash Register as an Example
Imagine operating a cash register at an international border town shop. When a customer pays for an item, the cashier accepts payment in two different formats: you can hand them **US Dollar bills** (`number`), or you can hand them a prepaid **Store Gift Card code** (`string`). The register is designed to process either payment format seamlessly.

In TypeScript, a **Union Type** (created using the vertical pipe symbol `|`) represents that flexible cash register. It allows a variable or function parameter to hold data that matches *one of several possible types*.

### Combining Multiple Type Options
To declare a Union Type, separate your acceptable type options using the vertical bar `|` (located above the Enter key on most keyboards):

```typescript
// A variable that is permitted to store either a text string OR a numeric value
let customerId: string | number;

customerId = "CUST-8899"; // Valid: matches string
customerId = 405060;      // Valid: matches number

// Attempting to assign a boolean is BLOCKED by the compiler:
// customerId = true; // COMPILER ERROR: Type 'boolean' is not assignable to type 'string | number'.
```

You can combine as many types as you need: `type ApiResponse = SuccessObject | ErrorObject | LoadingState;`.

### Syntax Symbols vs. Type Options
| Word in Example | What It Is | Why It Matters |
| :--- | :--- | :--- |
| `|` (vertical pipe) | **Built-in Union Operator** | Language symbol meaning *"or"*: the data can satisfy any one of the listed types. |
| `customerId` | **Your Custom Variable Label** | The name of the memory container storing the flexible data. |
| `string`, `number` | **Built-in Type Rules** | The specific primitive type options permitted inside the container. |

### Deconstructing Union Syntax
Let's look at `let customerId: string | number;`:

* `let` -> Keyword declaring a mutable memory container.
* `customerId` -> Developer-assigned name for the variable container.
* `:` -> Type annotation anchor.
* `string` -> First acceptable data type option.
* `|` -> The union operator (reads in English as *"OR"*).
* `number` -> Second acceptable data type option.
* `;` -> Statement terminator.

### Why Why This Matters in Real-World Projects
In frontend web development, user interface components frequently experience **transient loading states**. When a user visits a profile page, the app queries the backend API for data. Before the network request finishes, the profile data is `null`. Once the request completes, the profile data is a `UserProfile` object.

By annotating the component state as `let activeProfile: UserProfile | null = null;`, senior developers explicitly force the UI rendering logic to check whether the data has loaded before attempting to render `activeProfile.username` onto the screen!

---

## 2. Intersection Types (`&`)

### Think of a Swiss Army Flashlight
Imagine you are packing gear for a camping trip. You own a standalone **LED Flashlight** (which has a battery and an on/off switch), and you also own a standalone **Pocket Knife** (which has a blade and a can opener). 

For convenience, you purchase a multi-tool: a **Swiss Army Flashlight**. This single physical object is an **Intersection** of both tools! It possesses *every single feature of the flashlight* AND *every single feature of the pocket knife* combined into one unified body.

In TypeScript, an **Intersection Type** (created using the ampersand symbol `&`) is that multi-tool. It merges multiple independent type blueprints together into a single new blueprint that must possess all properties from every constituent type simultaneously.

### Merging Multiple Blueprints Together
While a Union Type (`|`) means *"A **or** B"*, an Intersection Type (`&`) means *"A **and** B"*. You use it to synthesize complex object requirements from modular building blocks:

```typescript
// Blueprint 1: Auditing metadata
type Timestamps = {
  createdAt: Date;
  updatedAt: Date;
};

// Blueprint 2: Core User data
type UserData = {
  username: string;
  email: string;
};

// Merging both blueprints together using the Intersection operator (&)
type AuditedUser = Timestamps & UserData;

// A valid AuditedUser object MUST provide ALL properties from both blueprints!
let newAccount: AuditedUser = {
  createdAt: new Date(),
  updatedAt: new Date(),
  username: "cyber_fox",
  email: "fox@cyber.com"
};
```

If you omit even one property from either `Timestamps` or `UserData`, the compiler rejects the object!

### Keywords vs. Merged Names
| Word in Example | What It Is | Why It Matters |
| :--- | :--- | :--- |
| `&` (ampersand) | **Built-in Intersection Operator** | Language symbol meaning *"and"*: the resulting type must satisfy all listed blueprints simultaneously. |
| `Timestamps`, `UserData` | **Your Custom Type Names** | The individual modular building block blueprints. |
| `AuditedUser` | **Your Custom Merged Type** | The name of the combined, multi-tool blueprint. |

### Deconstructing Intersection Syntax
Let's look at `type AuditedUser = Timestamps & UserData;`:

* `type` -> Keyword registering a new type alias definition.
* `AuditedUser` -> Our custom name for the synthesized multi-tool blueprint.
* `=` -> Binding operator connecting the name to the definition.
* `Timestamps` -> First constituent blueprint requirement.
* `&` -> The intersection operator (reads in English as *"AND"*).
* `UserData` -> Second constituent blueprint requirement.
* `;` -> Statement terminator.

### Building Modular Middleware in Node.js
In backend web servers built with Express or NestJS, HTTP requests pass through a pipeline of middleware functions before reaching your route handler. One middleware might authenticate the user (attaching a `.user` property to the request object), while another middleware logs session data (attaching a `.session` property).

To type the final request object cleanly without rewriting Express's built-in types, architects use Intersection Types: `type AuthenticatedRequest = Express.Request & { user: UserProfile; session: SessionData; };`. This grants full type safety across complex middleware chains!

---

## 3. Type Narrowing: The Core Concept

### Picture a Sorting Maze with Gates
When a variable is typed as a Union (like `string | number`), TypeScript adopts a strict safety posture: **it only allows you to access methods that exist on BOTH types simultaneously!**

For example, you cannot call `.toUpperCase()` on a `string | number` variable because numbers don't have uppercase letters! To use string-specific tools, you must guide the data through a conditional gate that mathematically proves to the compiler which specific type is currently inside the container. This process is called **Type Narrowing**.

```typescript
function processFlexibleData(input: string | number): void {
  // At this point, input is 'string | number'. We cannot call .toUpperCase() yet!
  // console.log(input.toUpperCase()); // COMPILER ERROR!

  // Gate 1: We use typeof to check if the input is a text string
  if (typeof input === "string") {
    // Inside this block, TypeScript narrows the type strictly to 'string'!
    console.log("String uppercase: " + input.toUpperCase());
  } 
  // Gate 2: If it wasn't a string, TypeScript knows it MUST be a number!
  else {
    // Inside this block, TypeScript narrows the type strictly to 'number'!
    console.log("Number doubled: " + (input * 2));
  }
}
```

Let's explore the four primary mechanical tools used to build these narrowing gates.

---

## 4. The Four Narrowing Tools (`typeof`, `instanceof`, `in`, Equality)

### 1. The `typeof` Guard (For Primitives)
As explored in Module 01, `typeof` inspects primitive values at runtime and returns lowercase strings like `"string"`, `"number"`, or `"boolean"`. When used inside an `if` statement, TypeScript narrows the variable's type within that conditional block.

### 2. The `instanceof` Guard (For Classes)
When working with objects instantiated from classes (like `Date`, `Error`, or custom classes), `typeof` is useless because it simply returns the generic string `"object"`. To check whether an object was created from a specific class blueprint, you use the **`instanceof`** operator:

```typescript
function formatTimestamp(timeValue: string | Date): string {
  // We check if timeValue was constructed by the built-in Date class
  if (timeValue instanceof Date) {
    // Inside this block, TypeScript knows timeValue is strictly a Date object!
    return timeValue.toISOString();
  } else {
    // Inside this block, TypeScript knows timeValue is strictly a string!
    return timeValue.toUpperCase();
  }
}
```

### 3. The `in` Operator Guard (For Interfaces and Objects)
Because Interfaces and Type Aliases are completely erased when TypeScript compiles to JavaScript, you cannot use `instanceof UserProfile` at runtime! 
To narrow between plain JavaScript objects or interfaces, you use the **`in` operator** to check whether a specific property key exists inside the object:

```typescript
interface Bird {
  wingspan: number;
  fly(): void;
}

interface Fish {
  finCount: number;
  swim(): void;
}

function moveAnimal(pet: Bird | Fish): void {
  // We check if the unique property key "fly" exists IN the pet object
  if ("fly" in pet) {
    // Inside this block, TypeScript narrows pet strictly to Bird!
    pet.fly();
  } else {
    // Inside this block, TypeScript narrows pet strictly to Fish!
    pet.swim();
  }
}
```

### 4. Equality Narrowing (`===` and `!==`)
TypeScript also narrows types when you perform direct literal equality comparisons:
```typescript
function setDirection(direction: "left" | "right" | "up" | "down"): void {
  if (direction === "left") {
    // TypeScript knows direction is strictly the literal string "left" here!
    console.log("Turning left");
  }
}
```

---

## 5. Discriminated Unions (The Tagged Union Pattern)

### Imagine Standardized Shipping Crates with Barcode Tags
Imagine managing a busy port harbor receiving three different types of standardized shipping crates: **Refrigerated Crates** (carrying fruit), **Hazardous Crates** (carrying chemicals), and **Livestock Crates** (carrying cattle). 

If workers had to pry open every crate with a crowbar just to see what was inside (`"fly" in pet`), work would grind to a halt. Instead, the port authority mandates a brilliant rule: every crate must have a standardized, highly visible **Barcode Tag** bolted to the front door labeled `crateType: "refrigerated"`, `crateType: "hazardous"`, or `crateType: "livestock"`. Workers simply scan the tag to know exactly what rules apply!

In TypeScript, a **Discriminated Union** (also called a **Tagged Union**) is that barcode system. It is the single most powerful architectural pattern for modeling complex state machines cleanly.

### Designing Tagged State Machines
To create a Discriminated Union, you define multiple interfaces where every single interface shares a common, literal **discriminator property** (the tag), but different supporting properties:

```typescript
// State 1: Network request is currently loading
interface LoadingState {
  status: "loading"; // The Barcode Tag!
}

// State 2: Network request succeeded and holds data
interface SuccessState {
  status: "success"; // The Barcode Tag!
  dataPayload: string[];
}

// State 3: Network request failed and holds an error message
interface ErrorState {
  status: "error";   // The Barcode Tag!
  errorMessage: string;
  errorCode: number;
}

// The Discriminated Union!
type NetworkState = LoadingState | SuccessState | ErrorState;
```

Now, when you write a function to handle `NetworkState`, you simply inspect the `status` tag using a `switch` statement or `if` branch. TypeScript automatically narrows the type in each branch with 100% precision:

```typescript
function renderUI(state: NetworkState): void {
  switch (state.status) {
    case "loading":
      // TypeScript knows state is strictly LoadingState here!
      console.log("Showing spinner...");
      break;
      
    case "success":
      // TypeScript knows state is strictly SuccessState here! We can safely access dataPayload!
      console.log(`Rendered ${state.dataPayload.length} items.`);
      break;
      
    case "error":
      // TypeScript knows state is strictly ErrorState here! We can safely access errorCode!
      console.log(`Error ${state.errorCode}: ${state.errorMessage}`);
      break;
  }
}
```

### Why Why This Matters in Real-World Projects
In frontend UI libraries like React or Redux, application state changes continuously. If you model state using optional properties (`{ isLoading?: boolean; data?: string[]; error?: string; }`), you create illegal, impossible states—what does it mean if `isLoading: true` AND `error: "Failed"` are both present at the exact same time?! 

By using Discriminated Unions, senior architects make illegal states mathematically impossible to represent. The application can only ever exist in one clean, verified state at a time.

---

## 6. The `never` Type and Exhaustiveness Checking

### Think of an Impossible Black Hole
In computer science, what happens when a function enters an infinite loop, or violently throws a fatal error that crashes the thread? The function **never returns a value**. 

In TypeScript, the **`never` type** represents an impossible state—a container that can never hold any data whatsoever.

### Building Bulletproof Exhaustiveness Checks
Senior architects use the `never` type to build automated safety alarms called **Exhaustiveness Checks**. 

When handling a Discriminated Union inside a `switch` statement, what happens if a junior developer adds a brand new state (`interface TimeoutState { status: "timeout" }`) to the union, but forgets to add a handling `case` for it in your UI renderer?

To prevent this silent bug, you add a `default` case that assigns the unhandled state to a variable typed as `never`:

```typescript
function renderUIExhaustive(state: NetworkState): void {
  switch (state.status) {
    case "loading": /* ... */ break;
    case "success": /* ... */ break;
    case "error":   /* ... */ break;
    
    // The Safety Alarm!
    default:
      // If every possible status tag was handled above, 'state' is narrowed to 'never' here.
      // But if someone added a new status tag and forgot a case, TypeScript throws a compiler error!
      const exhaustiveCheck: never = state;
      return exhaustiveCheck;
  }
}
```

If a new state is added to `NetworkState`, the compiler immediately screams: `Type 'TimeoutState' is not assignable to type 'never'`. You are forced to fix the bug before the code can be compiled!

---

## 7. Custom Type Guards (`is` Keyword)

### Imagine an Official VIP Security Escort
When a bouncer at a club checks a guest's ID at the door, they don't just nod their head; they stamp the guest's hand with an **Official VIP Stamp**. Once that stamp is applied, every other security guard inside the club immediately recognizes the guest as a verified VIP without needing to inspect their ID card a second time.

In TypeScript, a **Custom Type Guard** is a function that acts as that security escort. It inspects an object and returns a boolean, but it attaches a special **Type Predicate stamp (`parameterName is TypeName`)** to the return signature so the TypeScript compiler remembers the verification across scopes!

### Writing Custom Verification Functions
When narrowing complex object structures across multiple files, writing raw `if ("fly" in animal)` checks repeatedly gets messy. You can extract your check into a dedicated helper function that returns a type predicate using the `is` keyword:

```typescript
interface Cat { meow(): void; livesLeft: number; }
interface Dog { bark(): void; walkSpeed: number; }

// Notice the special return type: 'pet is Cat' instead of just 'boolean'!
function isCat(pet: Cat | Dog): pet is Cat {
  // We cast pet to any/Record just to check if the specific method exists
  return (pet as Cat).meow !== undefined;
}

function interactWithPet(pet: Cat | Dog): void {
  // We call our custom type guard function
  if (isCat(pet)) {
    // Because of 'pet is Cat', TypeScript narrows pet strictly to Cat here!
    pet.meow();
  } else {
    // TypeScript knows it MUST be a Dog here!
    pet.bark();
  }
}
```

---

## 8. Real-World Use Cases and Common Pitfalls

### Summary of Critical Beginner Pitfalls to Remember
1. **The Union Property Access Trap:** When a variable is typed as `string | number`, you cannot immediately access `.length` or `.toFixed()`. TypeScript blocks access to any property that is not shared by *all* members of the union. You must narrow the type first!
2. **The `instanceof` Interface Trap:** Never write `if (data instanceof UserInterface)`. Because Interfaces are erased during JavaScript compilation, `instanceof` only works with physical runtime **Classes** (like `Date` or `Error`). For interfaces, use the `in` operator or Discriminated Unions!
3. **The Non-Null Assertion Abuse (`!`):** TypeScript provides a shortcut symbol called the Non-Null Assertion Operator (e.g., `user!.name`), which tells the compiler: *"Shut up, I promise this variable is not null or undefined."* Avoid using `!` in production code! If you are wrong, your application will crash at runtime. Always use proper `if` statement narrowing instead of bypassing the compiler with `!`.
4. **Forgetting Discriminator Literal Types:** When building Discriminated Unions, ensure your tag property uses a **string literal type** (`status: "loading"`), NOT a general string type (`status: string`)! If you type it as `string`, TypeScript cannot narrow the union branches cleanly.
