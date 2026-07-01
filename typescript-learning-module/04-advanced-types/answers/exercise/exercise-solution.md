# Module 04 Exercise Solutions

Check your solutions against these implementations.

---

### Solution 1: Type Narrowing

```typescript
function formatInput(input: string | number | { title: string }): string {
  if (typeof input === "string") {
    return input.trim().toUpperCase();
  } else if (typeof input === "number") {
    return `$${input.toFixed(2)}`;
  } else {
    return input.title.toUpperCase();
  }
}
```

---

### Solution 2: Custom Type Guard

```typescript
interface Car {
  drive(): void;
  wheels: number;
}

interface Boat {
  sail(): void;
  anchor: boolean;
}

function isCar(vehicle: Car | Boat): vehicle is Car {
  return (vehicle as Car).drive !== undefined;
  // Or: return "wheels" in vehicle;
}

function operateVehicle(vehicle: Car | Boat): void {
  if (isCar(vehicle)) {
    vehicle.drive();
  } else {
    vehicle.sail();
  }
}
```

---

### Solution 3: Discriminated Union State Machine

```typescript
type NetworkState =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; payload: string[] }
  | { status: "error"; code: number; message: string };

function renderNetworkState(state: NetworkState): string {
  switch (state.status) {
    case "idle":
      return "Ready to request.";
    case "loading":
      return "Loading data...";
    case "success":
      return `Received ${state.payload.length} items.`;
    case "error":
      return `Error ${state.code}: ${state.message}`;
    default:
      const _exhaustiveCheck: never = state;
      return _exhaustiveCheck;
  }
}
```
