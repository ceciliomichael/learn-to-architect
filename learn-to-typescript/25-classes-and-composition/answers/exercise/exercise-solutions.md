# Module 25 Exercise Solutions

## Exercise 1

```typescript
class Timer {
  private seconds: number;

  constructor(
    public readonly id: string,
    start = 0,
  ) {
    this.seconds = start;
  }

  tick(): void {
    this.seconds = this.seconds + 1;
  }

  getSeconds(): number {
    return this.seconds;
  }
}
```

Each `new Timer` receives its own seconds state.

## Exercise 2

```typescript
interface Formatter {
  format(text: string): string;
}

class UppercaseFormatter implements Formatter {
  format(text: string): string {
    return text.toUpperCase();
  }
}

class TrimFormatter implements Formatter {
  format(text: string): string {
    return text.trim();
  }
}
```

## Exercise 3

```typescript
class Message {
  constructor(public text: string) {}

  describe(): string {
    return this.text;
  }
}

class TimedMessage extends Message {
  constructor(text: string, public timestamp: Date) {
    super(text);
  }

  override describe(): string {
    return `${this.timestamp.toISOString()}: ${this.text}`;
  }
}
```

## Exercise 4

```typescript
interface Notifier {
  notify(message: string): void;
}

class ConsoleNotifier implements Notifier {
  notify(message: string): void {
    console.log(message);
  }
}

class OrderService {
  constructor(private notifier: Notifier) {}

  completeOrder(id: string): void {
    this.notifier.notify(`Order ${id} complete`);
  }
}
```

The service uses a notifier without inheriting from it.

## Exercise 5

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

function validateUsername(username: string): void {
  if (username.trim().length === 0) {
    throw new ValidationError("Username is required", "username");
  }
}

try {
  validateUsername("  ");
} catch (error: unknown) {
  if (error instanceof ValidationError) {
    console.log(`${error.field}: ${error.message}`);
  }
}
```
