# Question 02 Answer

```typescript
// Only id and name
type WithPick  = Pick<Employee, "id" | "name">;                               // Concise
type WithOmit  = Omit<Employee, "email" | "salary" | "department" | "startDate">; // Verbose

// Everything except salary
type WithPick2 = Pick<Employee, "id" | "name" | "email" | "department" | "startDate">; // Verbose
type WithOmit2 = Omit<Employee, "salary">;                                              // Concise
```

**General rule:**
- Use `Pick` when you want a **small subset** of properties from a large interface. Listing 2 properties is shorter than listing the 4 you want to exclude.
- Use `Omit` when you want to **exclude a small number** of properties from a large interface. Writing `Omit<Employee, "salary">` is shorter than listing all 5 remaining properties manually.

The guiding question is: "Is the list of what I want shorter, or is the list of what I do not want shorter?" Pick the shorter list.
