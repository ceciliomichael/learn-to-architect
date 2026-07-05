# Question 05 Answer: Union vs. Intersection - Real-World Analogy and Property Analysis

## 1. Executive Summary and Direct Answers

### Part 1: Union Type Guarantee and Real-World Analogy
- **What it guarantees:** A Union Type (`TypeA | TypeB`) guarantees that a value satisfies **at least one** of the listed type blueprints, but because the compiler cannot know which specific type is present without a runtime check, it restricts un-narrowed property access exclusively to features shared by **all** members of the union.
- **Real-World Analogy:** A union type is like a **sealed mystery package** delivered to your office desk labeled "Contains either a Laptop OR a Desktop Printer." You cannot immediately plug a printer cable into it or type on a keyboard until you open the box and verify which specific machine is inside!

### Part 2: Intersection Type Guarantee and Real-World Analogy
- **What it guarantees:** An Intersection Type (`TypeA & TypeB`) guarantees that a value simultaneously satisfies **all** listed type blueprints, meaning every single property, method, and contract from every constituent type is guaranteed to be present on the object at all times.
- **Real-World Analogy:** An intersection type is like a **multidisciplinary emergency response vehicle** that is built as both a fully equipped Ambulance AND a heavy-duty Fire Engine simultaneously. It carries every medical tool from the ambulance and every water hose from the fire engine on a single chassis, ready to perform either role immediately without checking what kind of truck it is!

### Part 3: Property Access Analysis
Given the declarations:
```typescript
type WithEngine = { horsepower: number; startEngine(): void };
type WithSails  = { sailArea: number;   hoist(): void };

declare const u: WithEngine | WithSails;
declare const i: WithEngine & WithSails;
```
- **Safe to access on `u` (Union) without narrowing:** **NONE.** Zero properties are safe to access. Because `u` might be a sailboat (`WithSails`), accessing `.horsepower` or calling `.startEngine()` could trigger a fatal runtime error. Because `u` might be a motorboat (`WithEngine`), accessing `.sailArea` or calling `.hoist()` is equally forbidden.
- **Safe to access on `i` (Intersection) without narrowing:** **ALL FOUR PROPERTIES.** You can safely access `i.horsepower`, `i.startEngine()`, `i.sailArea`, and `i.hoist()` unconditionally. The intersection synthesizes a hybrid vessel guaranteed to possess both an engine and sails simultaneously!

---

## 2. Complete Property Analysis Table

The following matrix illustrates why TypeScript permits or rejects property access across both type operators:

| Property / Method Name | Originating Type | Safe on Union `u` (`WithEngine \| WithSails`)? | Safe on Intersection `i` (`WithEngine & WithSails`)? | Technical Reason and Compiler Rule |
| :--- | :--- | :--- | :--- | :--- |
| `horsepower` | `WithEngine` | **UNSAFE (Compile Error)** | **SAFE (100% Guaranteed)** | On union `u`, property is absent if `u` is `WithSails`. On intersection `i`, all properties are merged. |
| `startEngine()` | `WithEngine` | **UNSAFE (Compile Error)** | **SAFE (100% Guaranteed)** | On union `u`, method is absent if `u` is `WithSails`. On intersection `i`, method is guaranteed to exist. |
| `sailArea` | `WithSails` | **UNSAFE (Compile Error)** | **SAFE (100% Guaranteed)** | On union `u`, property is absent if `u` is `WithEngine`. On intersection `i`, all properties are merged. |
| `hoist()` | `WithSails` | **UNSAFE (Compile Error)** | **SAFE (100% Guaranteed)** | On union `u`, method is absent if `u` is `WithEngine`. On intersection `i`, method is guaranteed to exist. |

---

## 3. Complete Production-Grade Code Demonstration

Below is a complete, runnable TypeScript demonstration proving how the compiler enforces these access rules and how to properly narrow the union type.

```typescript
type WithEngine = { horsepower: number; startEngine(): void };
type WithSails  = { sailArea: number;   hoist(): void };

/**
 * Demonstrates handling a Union type vessel.
 * Unconditional access is blocked; explicit narrowing via the 'in' operator is required.
 *
 * @param vessel - A vessel that is either powered by an engine or powered by sails.
 */
function operateUnionVessel(vessel: WithEngine | WithSails): void {
  // --- UNSAFE ACCESS (Would trigger fatal compiler errors if uncommented) ---
  // console.log(vessel.horsepower);    // ERROR: Property 'horsepower' does not exist on type 'WithSails'.
  // vessel.startEngine();              // ERROR: Property 'startEngine' does not exist on type 'WithSails'.
  // console.log(vessel.sailArea);      // ERROR: Property 'sailArea' does not exist on type 'WithEngine'.
  // vessel.hoist();                    // ERROR: Property 'hoist' does not exist on type 'WithEngine'.

  // --- SAFE ACCESS VIA NARROWING GATE ---
  // We check for the existence of property "horsepower" to prove the vessel is WithEngine
  if ("horsepower" in vessel) {
    // Control Flow Analysis narrows 'vessel' strictly to WithEngine here!
    console.log(`[Union Engine Vessel] Engine rating: ${vessel.horsepower} HP.`);
    vessel.startEngine();
  } else {
    // In the else block, CFA knows 'vessel' must strictly be WithSails!
    console.log(`[Union Sail Vessel] Total sail area: ${vessel.sailArea} sq meters.`);
    vessel.hoist();
  }
}

/**
 * Demonstrates handling an Intersection type hybrid vessel.
 * All properties and methods from both blueprints are accessible immediately!
 *
 * @param hybridVessel - A vessel possessing both an engine AND sails simultaneously.
 */
function operateIntersectionVessel(hybridVessel: WithEngine & WithSails): void {
  console.log(`[Hybrid Vessel] Dual-powered ship ready! Engine: ${hybridVessel.horsepower} HP | Sails: ${hybridVessel.sailArea} sq m.`);
  
  // Unconditional method execution is 100% safe!
  hybridVessel.startEngine();
  hybridVessel.hoist();
}

// --- Comprehensive Runtime Test Cases ---
const speedboat: WithEngine = { horsepower: 450, startEngine: () => console.log("Vroom! Engine started.") };
const sailboat: WithSails   = { sailArea: 120,   hoist: () => console.log("Sails hoisted to the wind!") };
const motorSailer: WithEngine & WithSails = {
  horsepower: 200,
  startEngine: () => console.log("Hybrid engine humming smoothly."),
  sailArea: 85,
  hoist: () => console.log("Auxiliary sails deployed!")
};

operateUnionVessel(speedboat);
operateUnionVessel(sailboat);
operateIntersectionVessel(motorSailer);
```

---

## 4. Deep Technical Explanation: Set Theory and Property Synthesis

To understand why `u` restricts access while `i` permits everything, we must analyze how TypeScript maps type composition to property availability.

### Why Union Types Restrict Properties ($A \cup B$)
In type theory, a union type represents the logical disjunction (OR) of two type sets.
- Let $E$ be the set of all objects containing `horsepower` and `startEngine()`.
- Let $S$ be the set of all objects containing `sailArea` and `hoist()`.
- The union $E \cup S$ contains objects from $E$, objects from $S$, and objects belonging to both.
- **The Compiler Safety Law:** To prevent runtime crashes, the TypeScript compiler only permits access to the **intersection of property keys** across all union members: $\text{Keys}(E \cup S) = \text{Keys}(E) \cap \text{Keys}(S)$.
- Because $\text{Keys}(E) = \{ \text{"horsepower"}, \text{"startEngine"} \}$ and $\text{Keys}(S) = \{ \text{"sailArea"}, \text{"hoist"} \}$, their intersection is the empty set $\emptyset$! Therefore, zero properties can be accessed on `u` before narrowing!

### Why Intersection Types Merge Properties ($A \cap B$)
An intersection type represents the logical conjunction (AND) of two type sets.
- For an object to reside in the intersection set $E \cap S$, it must satisfy the requirements of blueprint $E$ AND blueprint $S$ simultaneously.
- **The Property Synthesis Law:** The property keys available on an intersection type equal the **union of property keys** from all constituent blueprints: $\text{Keys}(E \cap S) = \text{Keys}(E) \cup \text{Keys}(S)$.
- Therefore, the synthesized type for `i` contains all four property keys: $\{ \text{"horsepower"}, \text{"startEngine"}, \text{"sailArea"}, \text{"hoist"} \}$. The compiler guarantees all four exist, permitting unconditional access!

---

## 5. Concrete Anti-Patterns vs. Best Practices

### Anti-Pattern: Assuming Properties Exist on Unions Without Checking
A frequent error in complex codebases is assuming that because an object was passed into a function, a specific property must be present.
```typescript
// BAD: Causes build failures and runtime TypeError risks!
function badVesselHandler(v: WithEngine | WithSails): void {
  // COMPILER ERROR: Property 'horsepower' does not exist on type 'WithEngine | WithSails'.
  const hp = (v as WithEngine).horsepower; // Forced cast bypasses safety!
  console.log(`HP: ${hp}`);
}
```

### Best Practice: Systematic Type Narrowing via `in` or Discriminators
Always inspect the object at runtime using structured guards before accessing member-specific fields.
```typescript
// GOOD: Safe, verified runtime narrowing!
function goodVesselHandler(v: WithEngine | WithSails): void {
  if ("startEngine" in v) {
    v.startEngine();
  } else {
    v.hoist();
  }
}
```

---

## 6. Architectural Trade-offs

| Type Operator | Pros | Cons | Enterprise Best Use Case |
| :--- | :--- | :--- | :--- |
| **Union Types (`\|`)** | Allows functions to accept polymorphic inputs; models real-world variability (e.g., success vs. error data); prevents over-engineering monolithic interfaces. | Requires mandatory runtime narrowing checks (`in`, `typeof`, `switch`) before accessing specific properties; can become complex without shared discriminator tags. | Modeling REST/GraphQL API responses, UI loading/error/success states, and flexible utility function parameters. |
| **Intersection Types (`&`)** | Enables highly modular, composable type architecture; merges multiple smaller type traits into unified blueprints; allows direct, unconditional property access. | Merging incompatible primitive properties (e.g., `{ id: string } & { id: number }`) silently collapses the property type to `never`; produces verbose tooltips in IDEs. | Composing backend middleware request objects (`Request & Auth & Session`), combining database entity audit timestamps with domain models. |
