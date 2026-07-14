# Module 15 Exercise Solutions

## Exercise 1

```typescript
interface LearnerProfile {
  name: string;
  bio?: string;
}

function describeProfile(profile: LearnerProfile): string {
  const bio = profile.bio ?? "No bio";
  return `${profile.name}: ${bio}`;
}
```

## Exercise 2

```typescript
function getVolume(savedVolume: number | undefined): number {
  return savedVolume ?? 50;
}

console.log(getVolume(0));
console.log(getVolume(undefined));
```

The output is `0` and `50`. Nullish coalescing preserves zero.

## Exercise 3

```typescript
interface Course {
  readonly id: string;
  title: string;
  lessonCount: number;
}

const course: Course = {
  id: "ts-v2",
  title: "TypeScript",
  lessonCount: 34,
};

course.title = "TypeScript Step by Step";
```

Assigning a new value to `course.id` is blocked by the type checker.

## Exercise 4

```typescript
interface PriceLookup {
  [itemName: string]: number;
}

const prices: PriceLookup = {
  pen: 12,
  notebook: 45,
};

function printPrice(itemName: string): void {
  const price = prices[itemName];

  if (price === undefined) {
    console.log(`No price found for ${itemName}.`);
    return;
  }

  console.log(`${itemName}: ${price}`);
}
```

## Exercise 5

```typescript
const a: A = {};
const b: B = { note: undefined };
```

`A` allows the key to be absent. `B` requires the key to exist, although its value may be undefined.
