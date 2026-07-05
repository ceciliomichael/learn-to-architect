# Module 07: Classes and Object-Oriented Programming

In earlier modules, we used Interfaces and Type Aliases to model data shapes. But in standard JavaScript and TypeScript, interfaces are completely erased during compilation—they don't exist at runtime! What if you need a self-contained entity that bundles both **state** (data properties) and **behavior** (methods) together into a permanent physical object in computer memory?

This module teaches you **Object-Oriented Programming (OOP)** in TypeScript using **Classes**. We will explore how to construct blueprints that generate runtime objects, how to enforce encapsulation using access modifiers (`public`, `private`, `protected`), how to design inheritance hierarchies, and how to use abstract classes to build robust enterprise architectures.

---

## 1. Classes vs. Interfaces: What is the Difference?

### Let's Take an Architectural Blueprint vs. A Built House as an Example
To understand why we need both Interfaces and Classes without getting confused by technical definitions, imagine constructing a residential neighborhood.
* **The Interface (The Paper Blueprint):** An architect draws a paper blueprint titled `HouseBlueprint`. The blueprint specifies: *"The house must have 4 walls, a roof, and a front door."* You cannot live inside a paper blueprint! You cannot open the door of a drawing. Furthermore, when the city inspectors approve the neighborhood, they shred the paper blueprint—it disappears completely.
* **The Class (The Factory Mold and Builder):** A construction company creates a physical factory mold called `HouseClass`. This mold is not just a drawing; it is an active mechanical builder! When you press the green **Build** button (`new HouseClass()`), the factory pours concrete and erects a real, physical house standing on a plot of land. You can walk inside it, open its doors, and store furniture inside it. Even after construction is finished, the house remains standing in the physical world.

In TypeScript:
* An **Interface** is purely a compile-time paper blueprint. It checks your syntax during development, and then vanishes entirely when compiled to JavaScript.
* A **Class** is both a type blueprint AND a runtime factory! When you compile your code, classes remain intact as real JavaScript constructor structures, allowing you to instantiate physical object instances in memory using the `new` keyword.

---

## 2. Anatomy of a Class and the Constructor

### Think of an Automated Vending Machine Factory
Imagine a factory that manufactures commercial coffee vending machines. When a new vending machine rolls off the assembly line, it isn't completely empty! A technician initializes the machine with a starting inventory: *"Set the initial coffee bean hopper to 500 grams, and set the coin box balance to $0.00."*

In TypeScript, the **`constructor`** is that factory initialization technician. It is a special built-in method that executes automatically the exact moment you create a new object instance using `new`, allowing you to pass in starting values and set up the object's internal memory state.

### Declaring Properties and Initializing State
When defining a class, you declare its internal properties at the top of the body, and initialize them inside the `constructor(...)` method using the **`this`** keyword (which refers strictly to the specific object instance currently being built):

```typescript
// Defining an Object-Oriented Class blueprint for a Bank Account
class BankAccount {
  // 1. Property declarations (the memory slots every instance will possess)
  public accountHolder: string;
  public currentBalance: number;

  // 2. The Constructor: executed automatically when calling 'new BankAccount(...)'
  constructor(holderName: string, initialDeposit: number) {
    this.accountHolder = holderName;
    this.currentBalance = initialDeposit;
  }

  // 3. Methods (the behaviors attached to every instance)
  public deposit(amount: number): void {
    this.currentBalance = this.currentBalance + amount;
    console.log(`Deposited $${amount}. New balance: $${this.currentBalance}`);
  }
}

// Instantiating physical object instances in memory using the 'new' keyword!
const aliceAccount = new BankAccount("Alice Smith", 1000);
const bobAccount = new BankAccount("Bob Jones", 500);

// Executing behaviors on our instances
aliceAccount.deposit(250); // Outputs: "Deposited $250. New balance: $1250"
console.log(bobAccount.accountHolder); // Outputs: "Bob Jones"
```

### Syntax Symbols vs. Class Names
| Word in Example | What It Is | Why It Matters |
| :--- | :--- | :--- |
| `class`, `constructor`, `new`, `this` | **Built-in OOP Keywords** | Reserved language commands directing class registration, object initialization, instantiation, and instance reference binding. |
| `BankAccount` | **Your Custom Class Name** | The identifier chosen by you for the factory blueprint (written in PascalCase by universal convention). |
| `aliceAccount`, `bobAccount` | **Your Custom Instance Labels** | The variable identifiers pointing to the physical object instances in memory. |

### Deconstructing Instantiation Syntax
Let's look at `const aliceAccount = new BankAccount("Alice", 1000);`:

* `const` -> Keyword declaring a permanent variable container reference.
* `aliceAccount` -> Developer-chosen name for our instance container.
* `=` -> Assignment operator.
* `new` -> The instantiation keyword! This tells the JavaScript runtime: *"Allocate fresh memory, execute the class constructor, and return a physical object."*
* `BankAccount` -> The target class factory being invoked.
* `(` -> Opening parenthesis passing initial startup arguments into the constructor.
* `"Alice", 1000` -> The starting data values for holder name and initial balance.
* `)` -> Closing argument parenthesis.
* `;` -> Statement terminator.

---

## 3. Access Modifiers (`public`, `private`, `protected`)

### Picture Bank Vault Security Tiers
Imagine working inside a high-security national bank. Different areas of the building have different security access tiers:
* **The Public Lobby (`public`):** Anyone can walk off the street into the public lobby. Customers can view promotional flyers and speak to tellers freely.
* **The Employee Breakroom (`protected`):** General members of the public cannot enter the breakroom! Only official bank employees (and employees from subsidiary branch offices inheriting from the main bank) are allowed to swipe their badges and enter.
* **The Underground Cash Vault (`private`):** Even standard bank tellers and branch managers cannot enter the underground cash vault! Only the Chief Vault Officer inside that specific main building is permitted to open the safe.

In TypeScript, **Access Modifiers** (`public`, `private`, `protected`) are those security badges. They control exactly which parts of your application are allowed to read or modify a class's internal properties and methods!

### Enforcing Encapsulation in Code
By default, every property and method in a TypeScript class is `public`. To protect sensitive internal state from external tampering, you explicitly attach access modifiers:

1. **`public` (Default):** Accessible from anywhere—inside the class, inside child subclasses, and from external calling code.
2. **`private`:** Accessible **strictly and exclusively inside the defining class itself!** Child subclasses and external code cannot read or modify it.
3. **`protected`:** Accessible inside the defining class AND inside any child subclasses that inherit from it (`extends`), but completely hidden from external calling code.

```typescript
class EnterpriseServer {
  // Public: Anyone can read the server's public name
  public serverName: string;

  // Protected: Hidden from outside, but accessible to child specialized servers
  protected internalIpAddress: string;

  // Private: Strictly confidential! Hidden from EVERYONE except this specific class!
  private rootAdminPasswordHash: string;

  constructor(name: string, ip: string, passwordHash: string) {
    this.serverName = name;
    this.internalIpAddress = ip;
    this.rootAdminPasswordHash = passwordHash;
  }

  public authenticateAdmin(attemptedHash: string): boolean {
    // Inside the class, we can safely access our private property!
    return this.rootAdminPasswordHash === attemptedHash;
  }
}

const mainServer = new EnterpriseServer("Production-01", "10.0.0.1", "hash_8899");

// Public property access is allowed:
console.log(mainServer.serverName); // Outputs: "Production-01"

// Attempting to access protected or private properties from outside is BLOCKED by the compiler:
// console.log(mainServer.internalIpAddress);   // COMPILER ERROR: Property is protected!
// console.log(mainServer.rootAdminPasswordHash); // COMPILER ERROR: Property is private!
```

### Why Why This Matters in Real-World Projects
In banking and e-commerce software, allowing external developers to directly modify an account balance (`account.balance = 999999`) is a catastrophic security vulnerability! 

By marking `private balance: number;`, senior architects enforce **Encapsulation**. Outside code is physically incapable of changing the balance directly; they are forced to call verified public methods like `account.deposit(amount)` or `account.withdraw(amount)`, which execute strict security checks and audit logging before touching the private balance!

---

## 4. Parameter Properties and `readonly`

### Think of a VIP Fast-Track Check-in Desk
When you check into a hotel normally, the receptionist prints out a form, you write down your name and passport number on paper, and then the receptionist manually types those exact same words into the computer database. It is repetitive double-handling.
At a VIP Fast-Track desk, you simply hand the receptionist your digital ID card, and *in a single instant*, the system scans your card, creates your profile, and assigns your room without typing anything twice!

In TypeScript, **Parameter Properties** are that VIP fast-track desk. They provide a shorthand syntax that allows you to declare a class property AND initialize it inside the constructor simultaneously in a single line of code!

### Streamlining Class boilerplate
Instead of declaring properties at the top of the class and manually assigning them inside the constructor (`this.name = name`), you simply prefix constructor parameters with an access modifier (`public`, `private`, or `protected`) or the `readonly` keyword! TypeScript automatically generates and initializes the field for you invisibly:

```typescript
// 1. Old-School Verbose Class (Repetitive boilerplate)
class VerboseProduct {
  private sku: string;
  public name: string;
  public readonly price: number;

  constructor(sku: string, name: string, price: number) {
    this.sku = sku;
    this.name = name;
    this.price = price;
  }
}

// 2. Modern Parameter Properties Shorthand (100% identical in memory, zero repetition!)
class StreamlinedProduct {
  constructor(
    private sku: string,          // Creates a private property and assigns it automatically!
    public name: string,          // Creates a public property and assigns it automatically!
    public readonly price: number // Creates a public permanent property!
  ) {
    // The constructor body can remain completely empty!
  }

  public getSku(): string {
    return this.sku;
  }
}

const laptop = new StreamlinedProduct("SKU-999", "MacBook Pro", 2499.00);
console.log(laptop.name); // Outputs: "MacBook Pro"
// laptop.price = 1999.00; // COMPILER ERROR: Cannot assign to 'price' because it is a read-only property.
```

---

## 5. Getters and Setters (`get`, `set`)

### Imagine an Automated Climate Control Thermostat
Think about setting the temperature on a modern smart home thermostat. You don't take a screwdriver, open up the wall unit, and manually push copper heating wires together! 
You simply press the up/down arrows on the digital screen (`thermostat.temperature = 72`). 

When you press that button, an internal computer intercepts your request, checks a safety rule (*"Is 72 degrees within safe operating limits?"*), and if valid, engages the furnace for you.

In TypeScript, **Getters (`get`)** and **Setters (`set`)** act as that smart thermostat. They allow you to expose private internal state as what looks like a simple public property, while secretly executing custom validation logic or logging whenever someone reads or assigns a value!

### Intercepting Property Access
To create a getter or setter, place the keywords `get` or `set` in front of a method name:

```typescript
class SmartThermostat {
  // We keep the actual raw temperature private!
  private _celsiusTemp: number = 20;

  // Getter: intercepts reading attempts (e.g., console.log(thermostat.temperature))
  public get temperature(): number {
    console.log("[LOG]: Thermostat temperature read.");
    return this._celsiusTemp;
  }

  // Setter: intercepts assignment attempts (e.g., thermostat.temperature = 25)
  public set temperature(newTemp: number) {
    // We execute custom safety validation before modifying internal memory!
    if (newTemp < 10 || newTemp > 35) {
      console.error("[ERROR]: Temperature setting out of safe operating range (10-35°C)!");
      return; // Reject the assignment!
    }
    
    this._celsiusTemp = newTemp;
    console.log(`[LOG]: Temperature successfully adjusted to ${newTemp}°C.`);
  }
}

const homeTemp = new SmartThermostat();

// Reading triggers the 'get' method!
console.log(homeTemp.temperature); // Outputs log, then: 20

// Assigning triggers the 'set' method!
homeTemp.temperature = 24; // Outputs: "[LOG]: Temperature successfully adjusted to 24°C."

// Attempting to assign an illegal temperature is caught by our setter validation!
homeTemp.temperature = 100; // Outputs: "[ERROR]: Temperature setting out of safe operating range..."
console.log(homeTemp.temperature); // Still safely 24!
```

---

## 6. Inheritance (`extends` and `super`)

### Picture Employee Job Roles and Specialized Responsibilities
Imagine a corporate organization chart. At the base of the chart is the general **Employee** role. Every single employee in the company—whether an accountant, an engineer, or a security guard—shares basic attributes: an Employee ID, a Name, and the ability to clock in for work.
* **The Specialized Manager Role:** A **Manager** is an Employee! They inherit every single attribute of a general Employee (they have an ID, a Name, and clock in), but they also add specialized capabilities that standard employees lack: *a dedicated team budget, and the ability to approve expense reports*.

In TypeScript, class inheritance using the **`extends`** keyword allows a child subclass to inherit all properties and methods from a parent class, while using the **`super`** keyword to invoke the parent's constructor and methods!

### Building Class Hierarchies
Let's see how a child class inherits from a parent class and overrides behaviors:

```typescript
// 1. The Parent Class (Base Blueprint)
class BaseEmployee {
  constructor(
    public employeeId: string,
    public fullName: string,
    protected baseSalary: number // Protected: accessible to subclasses!
  ) {}

  public clockIn(): void {
    console.log(`${this.fullName} (ID: ${this.employeeId}) clocked in.`);
  }
}

// 2. The Child Subclass (Inherits from BaseEmployee using 'extends')
class DepartmentManager extends BaseEmployee {
  constructor(
    id: string,
    name: string,
    salary: number,
    public departmentName: string // New specialized property!
  ) {
    // CRITICAL RULE: In a child constructor, you MUST call super(...) before using 'this'!
    super(id, name, salary);
  }

  // Specialized method unique to Managers
  public approveExpense(amount: number): void {
    console.log(`Manager ${this.fullName} approved expense of $${amount} for ${this.departmentName}.`);
  }

  // Overriding a parent method to add custom manager behavior!
  public clockIn(): void {
    super.clockIn(); // Execute the original parent clock-in logic first
    console.log(`[MANAGER LOG]: Reviewing ${this.departmentName} team status.`);
  }
}

const manager = new DepartmentManager("EMP-001", "Sarah Connor", 95000, "Security");

// Inherited behavior from BaseEmployee:
console.log(manager.employeeId); // Outputs: "EMP-001"

// Specialized overridden behavior:
manager.clockIn();
/* Outputs:
"Sarah Connor (ID: EMP-001) clocked in."
"[MANAGER LOG]: Reviewing Security team status."
*/
```

---

## 7. Abstract Classes (`abstract`)

### Imagine a Government Vehicle Regulation Standard
Imagine the Department of Transportation establishing safety rules for commercial vehicles. They publish a regulation master document called **AbstractVehicle**. 
The regulation states: *"We don't manufacture physical AbstractVehicles; you cannot drive a regulation document down the highway! However, any manufacturer who builds a commercial vehicle (like a **Truck** or a **Bus**) MUST strictly implement a physical emergency brake system and a horn."*

In TypeScript, an **Abstract Class** (created using the `abstract` keyword) is that government regulation document. You **cannot instantiate an abstract class directly using `new`**! Instead, it serves as a master base class that defines shared implemented methods, while marking specific methods as `abstract`—forcing child subclasses to provide their own custom implementations!

### Enforcing Subclass Implementation
Let's see how abstract classes guide architectural consistency across different specialized subclasses:

```typescript
// 1. The Abstract Base Class (Cannot be instantiated directly!)
abstract class PaymentGateway {
  constructor(public merchantId: string) {}

  // A standard implemented method shared by ALL payment gateways!
  public logTransaction(amount: number): void {
    console.log(`[GATEWAY LOG]: Processing $${amount} for merchant ${this.merchantId}`);
  }

  // An ABSTRACT method: no body! Forces every child subclass to implement this exact signature!
  public abstract chargeCard(cardNumber: string, amount: number): boolean;
}

// const badGateway = new PaymentGateway("MERCH-1"); // COMPILER ERROR: Cannot create an instance of an abstract class!

// 2. A Concrete Child Subclass implementing Stripe
class StripeGateway extends PaymentGateway {
  // We MUST implement chargeCard, or TypeScript will throw a compiler error!
  public chargeCard(cardNumber: string, amount: number): boolean {
    this.logTransaction(amount); // Call inherited helper
    console.log(`[STRIPE]: Successfully charged card ${cardNumber} via Stripe API.`);
    return true;
  }
}

// 3. A Concrete Child Subclass implementing PayPal
class PayPalGateway extends PaymentGateway {
  public chargeCard(cardNumber: string, amount: number): boolean {
    this.logTransaction(amount);
    console.log(`[PAYPAL]: Successfully processed PayPal token for $${amount}.`);
    return true;
  }
}

const stripe = new StripeGateway("MERCH-STRIPE-99");
stripe.chargeCard("4242-4242-4242-4242", 99.50);
```

---

## 8. Implementing Interfaces (`implements`)

### Picture Signing an Independent Quality Certification Contract
Imagine running an independent electronics factory. Your factory manufactures mobile phones, laptop computers, and smart televisions—three completely different product lines that don't inherit from the same parent class. 

However, to sell your products in Europe, every single product must pass the **CE Safety Certification**. You sign a binding legal contract: *"I promise that regardless of what product I build, it will physically possess a high-voltage fuse and an auto-shutdown switch."*

In TypeScript, when a class uses the **`implements`** keyword followed by an Interface name, it is signing that quality certification contract! The class promises to provide public implementations for every property and method defined on that interface blueprint.

### Bridging Interfaces and OOP Classes
While `extends` inherits from another class, `implements` forces a class to conform to an interface structural contract:

```typescript
// 1. The Certification Contract Interface
interface PrintableReport {
  title: string;
  generatePdf(): void;
}

// 2. Class A implementing the contract
class FinancialAuditReport implements PrintableReport {
  constructor(public title: string, public totalRevenue: number) {}

  // We MUST provide generatePdf(), or the compiler rejects the class!
  public generatePdf(): void {
    console.log(`Generating PDF for Financial Report: ${this.title} ($${this.totalRevenue})`);
  }
}

// 3. Class B implementing the EXACT same contract!
class EmployeePerformanceReview implements PrintableReport {
  constructor(public title: string, public employeeName: string) {}

  public generatePdf(): void {
    console.log(`Generating PDF for Employee Review: ${this.title} (${this.employeeName})`);
  }
}

// Why this is architectural magic: We can treat completely unrelated classes identically!
const reports: PrintableReport[] = [
  new FinancialAuditReport("Q4 Audit", 1500000),
  new EmployeePerformanceReview("Annual Review", "Alice Smith")
];

for (let report of reports) {
  report.generatePdf(); // Safe polymorphic execution!
}
```

---

## 9. Static Members (`static`)

### Imagine a Company-Wide Bulletin Board vs. Personal Employee Desks
Imagine walking into a corporate office building. Every employee has their own personal **Employee Desk** (`an instance property`). What is on Alice's desk belongs strictly to Alice; what is on Bob's desk belongs strictly to Bob. 
However, in the main lobby hangs a single **Company-Wide Bulletin Board** (`a static property`). There aren't 100 different bulletin boards for 100 employees—there is strictly ONE central board shared across the entire organization!

In TypeScript, when you mark a property or method with the **`static`** keyword, you are attaching it strictly to the **Class Factory Blueprint itself**, rather than to individual instantiated object instances!

### Accessing Shared Factory Utilities
You access static members by calling them directly on the class name (`ClassName.staticMethod()`), without ever using `new` to create an object instance:

```typescript
class MathUtilities {
  // Static property: shared central constant across the entire application
  public static readonly PI: number = 3.14159265359;

  // Static method: utility tool callable directly on the class name!
  public static calculateCircleArea(radius: number): number {
    return MathUtilities.PI * radius * radius;
  }
}

// Notice we NEVER called 'new MathUtilities()'! We access static members directly:
console.log(MathUtilities.PI); // Outputs: 3.14159265359
console.log(MathUtilities.calculateCircleArea(10)); // Outputs: 314.159...

// const mathObj = new MathUtilities();
// console.log(mathObj.PI); // COMPILER ERROR: Property 'PI' is a static member of type 'MathUtilities'!
```

In enterprise backends, database connection pools, logger singletons, and configuration factories are almost universally built using static class members.

---

## 10. Real-World Use Cases and Common Pitfalls

### Summary of Critical Beginner Pitfalls to Remember
1. **The `super()` Order Trap:** When writing a constructor inside a child subclass (`extends`), **you must invoke `super(...)` before you attempt to read or write `this.property`!** If you touch `this` before calling `super()`, JavaScript throws a fatal runtime error because the parent memory allocation hasn't completed yet.
2. **Confusing `private` with Runtime Secrecy:** Marking a property as `private secret: string;` in TypeScript prevents *compilation* if another file tries to access it. However, remember that TypeScript compiles to standard JavaScript! When running in a browser or Node.js, `private` TypeScript fields become plain JavaScript properties that can be inspected by anyone using console debugging tools! If you need true cryptographic runtime privacy, use modern JavaScript private fields prefixed with a hash (`#secret: string`).
3. **Over-using Classes for Simple Data:** Don't write Java-style classes for everything! If you simply need to pass around a user profile object over an API, don't write a 50-line class with getters and setters. Just use a clean, lightweight `interface UserProfile` and plain object literals (`{ name: "Alice" }`). Reserve classes for when you genuinely need to bundle mutable state together with complex domain behavior!
