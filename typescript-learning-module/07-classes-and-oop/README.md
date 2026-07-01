# Module 07: Classes and Object-Oriented Programming

A class is a blueprint that combines data (properties) and behavior (methods) into a reusable structure. When you create an object from a class, that object is called an **instance**. This module covers everything you need to write production-quality classes in TypeScript.

---

## 1. What is a Class?

Before classes, if you needed to create ten "user" objects, you would have to write each one by hand. A class solves this by defining the shape and behavior once, and then you use the `new` keyword to create as many instances as you need.

```typescript
class Player {
  name: string;
  score: number;

  constructor(playerName: string, initialScore: number) {
    this.name = playerName;
    this.score = initialScore;
  }

  greet(): void {
    console.log("I am " + this.name + " with a score of " + this.score);
  }
}

const player1 = new Player("Alice", 100);
const player2 = new Player("Bob", 75);

player1.greet(); // "I am Alice with a score of 100"
player2.greet(); // "I am Bob with a score of 75"
```

### The `constructor` Method

The `constructor` is a special method that runs automatically when you create an instance using `new`. It is where you receive initial data and set up the properties of the instance.

### `this`

Inside a class, `this` refers to the current instance. When you write `this.name`, you are saying "the `name` property belonging to this specific instance."

---

## 2. Access Modifiers: `public`, `private`, `protected`

Access modifiers control where a property or method can be read or changed. TypeScript enforces them during compilation.

- **`public`** (the default): The property or method is accessible from anywhere, including outside the class.
- **`private`**: Only accessible from inside the class it is defined in. Not accessible in subclasses.
- **`protected`**: Accessible inside the class it is defined in, and also inside any child class that extends it. Not accessible from outside.

```typescript
class BankAccount {
  public accountOwner: string;
  private balance: number;

  constructor(owner: string, initialBalance: number) {
    this.accountOwner = owner;
    this.balance = initialBalance;
  }

  public deposit(amount: number): void {
    if (amount > 0) {
      this.balance = this.balance + amount;
    }
  }

  public withdraw(amount: number): boolean {
    if (amount > 0 && this.balance >= amount) {
      this.balance = this.balance - amount;
      return true;
    }
    return false;
  }

  public getBalance(): number {
    return this.balance; // Public method lets you read the private balance safely.
  }
}

const account = new BankAccount("Alice", 500);
account.deposit(200);
console.log(account.getBalance()); // 700
console.log(account.accountOwner); // "Alice" (public, accessible)
// console.log(account.balance);   // ERROR! 'balance' is private.
```

### Runtime Reality of Access Modifiers

TypeScript access modifiers only exist at compile time. When the code is compiled to JavaScript, there is no real enforcement at runtime. If someone runs the compiled JavaScript directly, they could access `balance`. If you need true runtime privacy in modern JavaScript, use the `#` prefix instead:

```typescript
class SafeAccount {
  #balance: number; // True private field, protected at runtime too.

  constructor(initial: number) {
    this.#balance = initial;
  }
}
```

---

## 3. The `readonly` Keyword on Class Properties

Just like in interfaces, you can mark a class property as `readonly` to prevent it from being changed after the object is created:

```typescript
class Receipt {
  readonly receiptId: string;
  amount: number;

  constructor(id: string, amount: number) {
    this.receiptId = id;
    this.amount = amount;
  }
}

const r = new Receipt("REC-001", 99.99);
r.amount = 150; // Allowed.
// r.receiptId = "REC-002"; // ERROR! 'receiptId' is read-only.
```

---

## 4. Parameter Property Shorthand

Writing out all the property declarations and then assigning them in the constructor is repetitive. TypeScript offers a shorthand: put the access modifier directly inside the constructor parameters, and TypeScript will automatically declare the property and assign the value for you.

```typescript
// Verbose version:
class Product {
  public name: string;
  private price: number;
  readonly id: string;

  constructor(name: string, price: number, id: string) {
    this.name = name;
    this.price = price;
    this.id = id;
  }
}

// Shorthand version (identical result):
class Product {
  constructor(
    public name: string,
    private price: number,
    readonly id: string
  ) {}
  // TypeScript generates all the declarations and assignments above automatically.
}
```

---

## 5. Inheritance: `extends`

A class can inherit all properties and methods from another class using the `extends` keyword. The inheriting class is called a **child class** or **subclass**. The class being inherited from is called the **parent class** or **superclass**.

```typescript
class Animal {
  constructor(public name: string, public age: number) {}

  describe(): void {
    console.log(this.name + " is " + this.age + " years old.");
  }
}

class Dog extends Animal {
  constructor(name: string, age: number, public breed: string) {
    super(name, age); // 'super' calls the parent constructor. This is required.
  }

  bark(): void {
    console.log(this.name + " says: Woof!"); // 'name' is inherited from Animal.
  }
}

const dog = new Dog("Rex", 3, "Husky");
dog.describe(); // "Rex is 3 years old." (inherited method)
dog.bark();     // "Rex says: Woof!"
```

### `super`

The `super` keyword is used in two ways inside a subclass:
1. `super(...)` calls the parent class constructor. You must call it before using `this` in a subclass constructor.
2. `super.methodName()` calls a parent class method from inside the subclass.

---

## 6. Abstract Classes

An abstract class is a class that is designed only to be a parent. It cannot be instantiated directly. You mark it and its methods with the `abstract` keyword.

Abstract methods have no body (no implementation). They are just declarations that say "any child class MUST provide an implementation for this method." This forces consistency across all subclasses:

```typescript
abstract class Shape {
  abstract getArea(): number; // No implementation here. Child classes must provide one.

  describe(): void {
    console.log("This shape has an area of " + this.getArea());
  }
}

class Circle extends Shape {
  constructor(public radius: number) {
    super();
  }

  getArea(): number {
    return 3.14159 * this.radius * this.radius;
  }
}

class Rectangle extends Shape {
  constructor(public width: number, public height: number) {
    super();
  }

  getArea(): number {
    return this.width * this.height;
  }
}

// const s = new Shape(); // ERROR! Cannot create an instance of an abstract class.
const circle = new Circle(5);
circle.describe(); // "This shape has an area of 78.53975"
```

---

## 7. Implementing Interfaces (`implements`)

A class can promise to satisfy an interface contract by using the `implements` keyword. TypeScript will enforce that the class provides all the required methods and properties defined in the interface.

`implements` is a compile-time check only. It does not inject any logic or default values into the class.

```typescript
interface Logger {
  log(message: string): void;
  warn(message: string): void;
}

class ConsoleLogger implements Logger {
  log(message: string): void {
    console.log("[LOG]: " + message);
  }

  warn(message: string): void {
    console.log("[WARN]: " + message);
  }
}

// If you forget to implement 'warn', TypeScript gives an error:
// Class 'ConsoleLogger' incorrectly implements interface 'Logger'.
// Property 'warn' is missing.
```

A class can implement multiple interfaces at once:

```typescript
interface Printable { print(): void; }
interface Saveable  { save(): void; }

class Document implements Printable, Saveable {
  print(): void { console.log("Printing..."); }
  save(): void  { console.log("Saving..."); }
}
```

---

## 8. Method Overriding

When a child class inherits a method from a parent class but needs different behavior, it can **override** that method by re-declaring it with the same name. The `override` keyword makes this explicit and safe:

```typescript
class Animal {
  makeSound(): string {
    return "...";
  }
}

class Cat extends Animal {
  override makeSound(): string {
    return "Meow";
  }
}

const cat = new Cat();
console.log(cat.makeSound()); // "Meow" (overridden version)
```

Using `override` tells TypeScript: "I intend to override a parent method." If you mistype the method name, TypeScript will catch it.

---

## 9. Static Members (`static`)

Normally, class properties and methods belong to instances of the class created with `new`. Sometimes you want properties or methods that belong to the class itself, not to any individual instance. You define these using the `static` keyword:

```typescript
class MathUtils {
  static PI = 3.14159;

  static calculateCircumference(radius: number): number {
    return 2 * MathUtils.PI * radius;
  }
}

// Access directly on the class without creating an instance:
console.log(MathUtils.PI); // 3.14159
console.log(MathUtils.calculateCircumference(10)); // 62.8318

// const m = new MathUtils();
// m.calculateCircumference(10); // ERROR! Static methods cannot be called on instances.
```

Static properties can also have access modifiers like `private static` or `readonly static`:

```typescript
class DatabaseConnection {
  private static instance: DatabaseConnection | null = null;

  private constructor() {
    // Private constructor prevents calling 'new DatabaseConnection()' externally.
  }

  static getInstance(): DatabaseConnection {
    if (DatabaseConnection.instance === null) {
      DatabaseConnection.instance = new DatabaseConnection();
    }
    return DatabaseConnection.instance;
  }
}
```

This pattern (the Singleton pattern) uses `private static` to ensure only one connection ever exists.

