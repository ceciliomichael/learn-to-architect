# Module 12 Exercise Solutions

## Exercise 1

```typescript
type TrafficLight = "red" | "yellow" | "green";

let light: TrafficLight = "red";
light = "yellow";
light = "green";
```

`"blue"` is not one of the three literal members, so TypeScript rejects it.

## Exercise 2

```typescript
type OrderId = string | number;

function printOrderId(id: OrderId): void {
  console.log(`Order: ${id}`);
}

printOrderId(104);
printOrderId("WEB-104");
```

Template string insertion works for either member, so no member-specific check is needed here.

## Exercise 3

```typescript
function getDayName(dayNumber: number): string | undefined {
  if (dayNumber === 1) {
    return "Monday";
  }

  if (dayNumber === 2) {
    return "Tuesday";
  }

  if (dayNumber === 3) {
    return "Wednesday";
  }

  return undefined;
}

const dayName = getDayName(2);

if (dayName !== undefined) {
  console.log(dayName);
}
```

The return type makes the missing case visible to the caller.

## Exercise 4

```typescript
type Username = string;
type ShirtSize = "small" | "medium" | "large";
type Selection = string | null;
type Rating = 1 | 2 | 3 | 4 | 5;
```

`Username` documents meaning but does not limit which string is valid. The other aliases model exact choices or intentional absence.

## Exercise 5

```typescript
type ConnectionState = "offline" | "connecting" | "online";
```

The original `Data` type mixed unrelated kinds without saying what the value meant. The replacement has one clear subject and three honest possibilities.
