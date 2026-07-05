# Module 07: Classes and Object-Oriented Programming

Up until now, we have used Interfaces to describe the shape of data, and Functions to perform logic. But in large applications, keeping your data and your functions separated can get messy. 

Object-Oriented Programming (OOP) is an architectural style that bundles data (properties) and the logic that operates on that data (methods) together into a single, organized unit called a **Class**. 

This module breaks down how to build professional, production-ready classes in TypeScript using real-world analogies and exact syntax translations.

---

## 1. What is a Class?

### The Real-World Analogy: The Car Factory Blueprint
Imagine you are building a factory that produces cars. 
You wouldn't design every single car from scratch, one by one. Instead, you design a master **Blueprint**. The blueprint states: *"Every car will have a `color` property, a `speed` property, and an `accelerate()` function."*
When the factory turns on, it uses that single blueprint to manufacture thousands of physical cars.

In TypeScript:
* **The Class** is the master blueprint. It exists only once.
* **The Instance** is the physical car manufactured from the blueprint. You can create as many instances as you want!

### The Core Technical Concept
A `class` defines the properties and methods that its instances will have. You use the `new` keyword to manufacture a new instance from the class.

```typescript
// 1. Defining the Blueprint (The Class)
class Player {
  // Properties (Data)
  name: string;
  score: number;

  // The Manufacturing Robot (Constructor)
  constructor(playerName: string, initialScore: number) {
    this.name = playerName;
    this.score = initialScore;
  }

  // Method (Behavior)
  greet(): void {
    console.log(`I am ${this.name} with a score of ${this.score}`);
  }
}

// 2. Manufacturing Physical Instances using 'new'
const player1 = new Player("Alice", 100);
const player2 = new Player("Bob", 75);

// 3. Using the instances
player1.greet(); // Outputs: "I am Alice with a score of 100"
player2.greet(); // Outputs: "I am Bob with a score of 75"
```

### The `constructor` and `this` Keywords
* **`constructor`**: This is a special automatic function. The exact millisecond you type `new Player()`, the `constructor` runs. Its job is to receive the initial setup data and attach it to the new instance.
* **`this`**: Inside a class, `this` is a magic word that means *"the specific physical instance we are currently looking at."* When `player1` calls `greet()`, `this.name` translates to `"Alice"`. When `player2` calls `greet()`, `this.name` translates to `"Bob"`.

### Built-in Keywords vs. Programmer-Invented Labels
| Word in Example | Category | Explanation |
| :--- | :--- | :--- |
| `class`, `constructor`, `this`, `new` | **Built-in Keywords** | Core Object-Oriented keywords built into JavaScript/TypeScript. |
| `Player`, `name`, `greet`, `player1` | **Programmer-Invented Labels** | Custom identifiers. You could rename `Player` to `Gamer`! |

---

## 2. Access Modifiers: `public`, `private`, `protected`

### The Real-World Analogy: The Bank Vault
If you walk into a bank, there is a public lobby (where anyone can walk), a protected teller area (where only employees can walk), and a private steel vault (where only the bank manager can walk). 

### The Core Technical Concept
Access modifiers control who is allowed to read or change the data inside your class. 

* **`public`** (Default): Anyone, anywhere can read or change the property. (The Lobby).
* **`private`**: The property can ONLY be read or changed from inside the exact class it was defined in. (The Vault).
* **`protected`**: Similar to `private`, but also allows Child Subclasses (which we will learn about below) to access it. (The Employee Area).

```typescript
class BankAccount {
  public accountOwner: string; // Anyone can see the owner's name
  private balance: number;     // The vault! Hidden from the outside world

  constructor(owner: string, initialBalance: number) {
    this.accountOwner = owner;
    this.balance = initialBalance;
  }

  // Public method acting as the Teller. 
  // It safely interacts with the private vault on your behalf!
  public deposit(amount: number): void {
    if (amount > 0) {
      this.balance = this.balance + amount;
    }
  }
}

const myAccount = new BankAccount("Alice", 500);

console.log(myAccount.accountOwner); // Valid! It is public.
myAccount.deposit(200);              // Valid! The method is public.

// myAccount.balance = 999999; // COMPILER ERROR: Property 'balance' is private!
```

### Why Senior Developers Require This (Encapsulation)
Without `private`, a junior developer could accidentally write `myAccount.balance = -5000`, completely bypassing the bank's security checks. By making the balance `private` and forcing developers to use the `public deposit()` method, the senior engineer guarantees that the safety logic (`if amount > 0`) can never be skipped! This is called **Encapsulation**.

---

## 3. The `readonly` Keyword on Class Properties

Just like Interfaces, classes support the `readonly` keyword. While `private` hides a property from the outside world, `readonly` allows the outside world to see it, but physically prevents anyone (even the class itself) from changing it after the constructor finishes!

```typescript
class Receipt {
  public readonly receiptId: string; // Visible to everyone, but unchangeable!
  public amount: number;

  constructor(id: string, amount: number) {
    this.receiptId = id;
    this.amount = amount;
  }
}

const r = new Receipt("REC-001", 99.99);
r.amount = 150; // Allowed!
// r.receiptId = "REC-002"; // COMPILER ERROR: Cannot assign to 'receiptId' because it is read-only.
```

---

## 4. Parameter Property Shorthand

### The Core Technical Concept
If you look at the `Receipt` class above, writing the word `receiptId` three different times (the property declaration, the constructor parameter, the `this.` assignment) is extremely repetitive.

TypeScript offers a magic shorthand. If you put an access modifier (`public`, `private`, `protected`, or `readonly`) directly inside the constructor parentheses, TypeScript will automatically declare the property and assign it for you invisibly!

```typescript
// The EXACT same class as above, written using Shorthand:
class ReceiptShorthand {
  constructor(
    public readonly receiptId: string, 
    public amount: number
  ) {
    // Look mom, no 'this.amount = amount' needed! It happens automatically!
  }
}
```

### Why Production Codebases Rely on This
Backend frameworks like NestJS and Angular use this shorthand extensively for Dependency Injection. It keeps controller files small, clean, and highly readable.

---

## 5. Inheritance (`extends`)

### The Real-World Analogy: Parent and Child Blueprints
Imagine a vehicle manufacturing plant. You have a master blueprint called `Vehicle` with properties for `wheels` and `engine`. 
If you want to build a `Motorcycle`, you don't rewrite the entire blueprint from scratch. You create a `Motorcycle` blueprint that says: *"Copy everything from the `Vehicle` blueprint, but add a `kickstand`."*

### The Core Technical Concept
**Inheritance** allows a child class to inherit all properties and methods from a parent class using the `extends` keyword.

```typescript
// The Parent Class
class Animal {
  constructor(public name: string) {}
  
  breathe(): void {
    console.log(`${this.name} is breathing.`);
  }
}

// The Child Class (Inherits from Animal)
class Dog extends Animal {
  constructor(name: string, public breed: string) {
    // The 'super' keyword calls the Parent's constructor! You MUST include this!
    super(name); 
  }

  bark(): void {
    console.log(`Woof! I am a ${this.breed}.`);
  }
}

const myDog = new Dog("Rex", "Husky");
myDog.breathe(); // Inherited from Parent!
myDog.bark();    // Specific to Child!
```

---

## 6. Abstract Classes

### The Real-World Analogy: The Concept Car
Car companies often build "Concept Cars" for auto shows. These cars look cool, but they don't have real engines inside. They are not meant to be driven; they exist purely to inspire the design of *future* cars.

### The Core Technical Concept
An **Abstract Class** is a Concept Car. It is a parent class that is forbidden from being manufactured directly. It exists purely as a baseline for child classes to extend.
You mark the class with the `abstract` keyword. You can also mark methods as `abstract` (which means they have no code body; the child is FORCED to write the code).

```typescript
abstract class Shape {
  // Abstract method: No curly braces! The Child MUST figure out how to calculate this.
  abstract getArea(): number; 

  // Normal method: Shared by all children!
  describe(): void {
    console.log(`My area is ${this.getArea()}`);
  }
}

// const s = new Shape(); // COMPILER ERROR: Cannot create an instance of an abstract class.

class Square extends Shape {
  constructor(public sideLength: number) { super(); }

  // We are FORCED by the compiler to implement this method!
  getArea(): number {
    return this.sideLength * this.sideLength;
  }
}
```

---

## 7. Implementing Interfaces (`implements`)

### The Core Technical Concept
While `extends` copies code from a Parent Class, `implements` forces a class to obey a strict blueprint Interface. 

```typescript
interface Logger {
  logError(msg: string): void;
}

// The class swears a blood oath to implement everything in the Logger interface
class DatabaseLogger implements Logger {
  
  // If we delete this method, the compiler will throw an error!
  logError(msg: string): void {
    console.log(`[DB ERROR]: ${msg}`);
  }
}
```

### Why Senior Developers Require This
In backend enterprise architecture, you might have a `StripePaymentService` class and a `PaypalPaymentService` class. By forcing both of them to `implements PaymentGateway`, the rest of the application doesn't care which service is being used, because both are guaranteed to have the exact same method names!

---

## 8. Method Overriding (`override`)

### The Core Technical Concept
Sometimes a child inherits a method from a parent, but wants to change how it works. This is called **Overriding**. You use the `override` keyword to explicitly tell the compiler: *"I know the parent has this method, but I am replacing it."*

```typescript
class BasicUser {
  getPermissions(): string[] { return ["read"]; }
}

class AdminUser extends BasicUser {
  // Replacing the parent's logic entirely!
  override getPermissions(): string[] { 
    return ["read", "write", "delete"]; 
  }
}
```

---

## 9. Static Members (`static`)

### The Real-World Analogy: The Factory Instruction Manual
When you buy a car, the steering wheel and the engine belong to *your specific physical car* (the instance). But the "Official Manufacturing Guidelines Manual" sits in the factory office. It doesn't belong to any one car; it belongs to the *Factory itself*.

### The Core Technical Concept
By default, properties and methods belong to the instances you create with `new`. But if you use the `static` keyword, the property is bolted onto the Class Blueprint itself!

```typescript
class MathEngine {
  // Static property: Belongs to the MathEngine blueprint!
  static PI: number = 3.14159;

  // Static method
  static calculateCircleArea(radius: number): number {
    return MathEngine.PI * (radius * radius);
  }
}

// Notice we do NOT use the 'new' keyword! We access it directly on the Class name!
console.log(MathEngine.PI); 
console.log(MathEngine.calculateCircleArea(10));
```

---

## 10. Real-World Use Cases and Common Pitfalls

### Summary of Critical Beginner Pitfalls to Remember
1. **Compile-Time vs Runtime Privacy:** TypeScript's `private` keyword is a compile-time illusion. When compiled to JavaScript, the `private` word disappears, and technically a hacker could still read your "private" variables in the browser. If you need true, unbreakable cryptographic privacy in modern JS, use the `#` symbol (e.g. `#balance: number;`), which enforces privacy at the engine level!
2. **Forgetting `super()`:** If you create a Child class with a constructor, you MUST call `super()` inside of it before you try to use `this`. Why? Because `super()` builds the parent's half of the object. You cannot attach child properties to an object that hasn't been built yet!
3. **Overusing Classes in React:** Classes are the gold standard for backend Node.js services (Controllers, Repositories). However, in modern React frontend development, massive Object-Oriented inheritance chains are considered an anti-pattern. React developers prefer plain functions (Hooks) and simple Objects. Know your environment!
