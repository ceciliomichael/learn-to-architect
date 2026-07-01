# Question 05: Architectural Boundaries & The Result Pattern

In a system architecture interview, you are asked to design the interface between a REST API controller and a backend database service.

1. Compare standard exception throwing (`try/catch`) against the **Result pattern** (`Promise<Result<T, E>>`). Why is throwing exceptions across layer boundaries considered a architectural anti-pattern in TypeScript? Reference what `catch (e: unknown)` forces the caller to do.
2. According to the Single Responsibility Principle (SRP) and clean separation of concerns, why should a UI component or Express route handler *never* construct raw SQL queries or call external `fetch` URLs directly?
3. What is the **300-line rule** in maintainable software engineering, and how does breaking a file into domain logic, orchestration, and data access prevent codebase decay?

## ANSWER HERE

> **1. Exception throwing vs The Result pattern:**

> **2. Why UI/Transport layers must never perform direct I/O:**

> **3. The 300-line rule and modular architecture:**
