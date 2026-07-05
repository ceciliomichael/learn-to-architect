# Question 02: Property Plucking and Record Dictionaries

Both `Pick<T, Keys>` and `Omit<T, Keys>` construct new interfaces by slicing existing models. Meanwhile, `Record<K, V>` constructs dictionary objects. This question tests your architectural decision-making when designing domain models.

```typescript
interface EnterpriseEmployee {
  id: string;
  firstName: string;
  lastName: string;
  email: string;
  department: string;
  salary: number;
  socialSecurityNumber: string;
  bankRoutingNumber: string;
  hireDate: Date;
  isExecutive: boolean;
}

type UserRole = "admin" | "editor" | "viewer" | "moderator";
```

## Questions

1. **Pick vs Omit Decision Framework**:
   - Imagine you need a public directory card type containing only `id`, `firstName`, and `lastName`. Should you use `Pick` or `Omit`? Why?
   - Imagine you need to send employee data to an external Slack integration that requires every field *except* `salary`, `socialSecurityNumber`, and `bankRoutingNumber`. Should you use `Pick` or `Omit`? Why?
   - State the golden architectural rule for choosing between `Pick` and `Omit` when refactoring large interfaces.
2. **Record Exhaustiveness Checking**:
   - Explain the structural difference between `type RolePermissions = Record<UserRole, boolean>` and an open-ended index signature `type OpenPermissions = { [key: string]: boolean }`.
   - What happens at compile time if a junior developer adds a new role `"guest"` to the `UserRole` union? Why is `Record` superior for finite key sets in production codebases?

## ANSWER HERE

> **1. Pick vs Omit Decision Framework:**

> **2. Record Exhaustiveness Checking:**
