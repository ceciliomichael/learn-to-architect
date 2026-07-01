# Challenge 02: Solution

```typescript
function greetOptional(name: string, title?: string): string {
  if (title !== undefined) {
    return `Hello, ${title} ${name}`;
  }
  return `Hello, ${name}`;
}

function greetDefault(name: string, title: string = "Traveler"): string {
  return `Hello, ${title} ${name}`;
}

// greetOptional calls:
console.log(greetOptional("Alice", "Dr."));  // "Hello, Dr. Alice"
console.log(greetOptional("Alice"));          // "Hello, Alice"

// greetDefault calls:
console.log(greetDefault("Bob", "Captain")); // "Hello, Captain Bob"
console.log(greetDefault("Bob"));            // "Hello, Traveler Bob"
```
