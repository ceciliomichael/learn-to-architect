# Module 10 Exercise: Refactoring Monoliths & Architecture

Complete your refactoring solutions inside the **ANSWER HERE** blocks below.

---

### Challenge 1: Splitting a Monolithic File
You inherited a single file `badApp.ts` containing mixed domain logic, database operations, and presentation logs:

```typescript
// badApp.ts
interface User { id: string; name: string; age: number; }

function validateUser(user: User): boolean {
  if (user.age < 18) {
    console.error("Validation failed: User too young");
    return false;
  }
  return true;
}

function saveUserToDatabase(user: User): void {
  console.log(`[DB]: Saving user ${user.id} to storage...`);
}

function handleUserRegistration(id: string, name: string, age: number): void {
  const newUser: User = { id, name, age };
  if (validateUser(newUser)) {
    saveUserToDatabase(newUser);
    console.log("Registration successful!");
  }
}
```

Refactor this codebase into 4 distinct, clean modular files following Separation of Concerns:
1. `types.ts`
2. `validator.ts`
3. `userRepository.ts`
4. `index.ts` (Orchestration entrypoint)

#### ✍️ ANSWER HERE:
```typescript
// --- types.ts ---


// --- validator.ts ---


// --- userRepository.ts ---


// --- index.ts ---


```

---

### Challenge 2: The 300-Line Limit Strategy
Write a brief markdown explanation describing how you would structure a massive 800-line `orderProcessing.ts` service file into smaller, modular components without breaking existing imports.

#### ✍️ ANSWER HERE:
> Strategy & Explanation: 
