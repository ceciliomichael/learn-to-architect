# Module 25: Classes and Composition

## Before you start

Complete Modules 01 to 24. You should understand objects, interfaces, functions, readonly data, and modules.

## What you will learn

- create instances from a class
- initialize fields in a constructor
- use public, private, protected, and readonly members
- implement an interface
- extend a class and call `super`
- compare inheritance with composition
- create a custom error class now that class syntax is known

## Why this matters

Classes combine data and behavior and create many instances with the same setup. They are common in TypeScript libraries and frameworks. Plain objects and functions remain good choices, so the goal is to understand classes rather than use them everywhere.

## 1. Declare and instantiate a class

```typescript
class Counter {
  value: number;

  constructor(start: number) {
    this.value = start;
  }

  increment(): void {
    this.value = this.value + 1;
  }
}

const firstCounter = new Counter(0);
const secondCounter = new Counter(10);

firstCounter.increment();
console.log(firstCounter.value);
console.log(secondCounter.value);
```

`new Counter(0)` creates an instance. `this` refers to the current instance.

## 2. Parameter properties

TypeScript can declare and initialize a field from a constructor parameter:

```typescript
class Book {
  constructor(
    public title: string,
    public pages: number,
  ) {}
}
```

This is equivalent to declaring fields and assigning them inside the constructor. Use the shorter form when it remains readable.

## 3. Access modifiers

```typescript
class BankAccount {
  private balance: number;

  constructor(initialBalance: number) {
    this.balance = initialBalance;
  }

  deposit(amount: number): void {
    if (amount <= 0) {
      throw new Error("Deposit must be positive");
    }

    this.balance = this.balance + amount;
  }

  getBalance(): number {
    return this.balance;
  }
}
```

- `public` is the default and can be accessed through an instance.
- TypeScript `private` restricts access during type checking.
- `protected` allows access inside the class and subclasses.

TypeScript's `private` keyword is usually erased and is not the same as JavaScript `#privateField`, which has runtime enforcement. Choose based on whether runtime privacy is required.

## 4. Readonly fields

```typescript
class User {
  constructor(
    public readonly id: string,
    public name: string,
  ) {}
}
```

The id can be set during initialization but not assigned later through the class type. It is still a static shallow restriction.

## 5. Implement an interface

```typescript
interface Describable {
  describe(): string;
}

class Product implements Describable {
  constructor(
    public name: string,
    public price: number,
  ) {}

  describe(): string {
    return `${this.name}: ${this.price}`;
  }
}
```

`implements` checks that the class declaration satisfies the interface. It does not copy method code into the class.

Because TypeScript is structurally typed, a class instance can satisfy an interface even without an explicit `implements` clause. The clause is useful feedback at the class declaration.

## 6. Inheritance

```typescript
class Animal {
  constructor(public name: string) {}

  describe(): string {
    return this.name;
  }
}

class Dog extends Animal {
  constructor(name: string, public breed: string) {
    super(name);
  }

  override describe(): string {
    return `${this.name} is a ${this.breed}`;
  }
}
```

`super(name)` initializes the base class. `override` asks TypeScript to confirm that a base member with a compatible name exists.

Inheritance is appropriate for a stable is-a relationship when callers truly use the shared base behavior.

## 7. Composition

Composition builds behavior from separate values:

```typescript
interface Logger {
  log(message: string): void;
}

class ConsoleLogger implements Logger {
  log(message: string): void {
    console.log(message);
  }
}

class TaskService {
  constructor(private logger: Logger) {}

  complete(title: string): void {
    this.logger.log(`Completed: ${title}`);
  }
}
```

`TaskService` has a logger rather than extending a logger. The logger can be replaced with another implementation for testing or another output.

Prefer composition when the relationship is has-a or uses-a, or when inheritance would create an awkward hierarchy.

## 8. A custom error class

Now class syntax can support a meaningful custom error:

```typescript
class ValidationError extends Error {
  constructor(
    message: string,
    public readonly field: string,
  ) {
    super(message);
    this.name = "ValidationError";
  }
}
```

Use a custom class when callers need structured information or need to distinguish this error at runtime:

```typescript
try {
  throw new ValidationError("Title is required", "title");
} catch (error: unknown) {
  if (error instanceof ValidationError) {
    console.log(error.field);
  }
}
```

Do not create a new class for every message. A built-in Error or result union is often enough.

## Common mistakes

### Using classes for plain data only

An interface and object literal may be simpler when no construction rules or behavior are needed.

### Assuming `implements` adds behavior

It checks a contract only.

### Building deep inheritance trees

They couple behavior across levels. Composition often makes dependencies clearer.

### Assuming TypeScript `private` is runtime secrecy

Use JavaScript private fields or another runtime boundary when that guarantee matters.

## Check your understanding

1. What does a constructor do?
2. How do TypeScript `private` and JavaScript `#private` differ?
3. What does `implements` provide?
4. When must a subclass call `super`?
5. How does composition differ from inheritance?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 26](../26-promises-and-asynchronous-work/README.md) introduces values that become available after asynchronous work finishes.
