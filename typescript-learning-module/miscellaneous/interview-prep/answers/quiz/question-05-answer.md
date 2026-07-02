# Answer  -  Question 05: Architectural Boundaries & The Result Pattern

## 1. Exception Throwing vs. The Result Pattern
Throwing exceptions across architectural layers is an anti-pattern because TypeScript does not type-check thrown errors. A caller inspecting `async function getOrder(id: string): Promise<Order>` cannot tell if the function throws `DatabaseTimeoutError` or `OrderNotFoundError`. Furthermore, inside `catch (e: unknown)`, TypeScript forces verbose `instanceof` checks.

The **Result Pattern** models failures as explicit return values (`Promise<Result<Order, "NOT_FOUND" | "TIMEOUT">>`). This forces the compiler to verify that the caller explicitly handles error states before accessing `.data`.

## 2. Why UI/Transport Layers Must Never Perform Direct I/O
According to the Single Responsibility Principle (SRP), a layer should have only one reason to change. If an Express controller or React UI component executes raw SQL queries or direct `fetch` calls
- Testing UI rendering or route parameter parsing requires spinning up a live database connection or mocking global network sockets.
- If the database schema changes, you must hunt through UI files and route controllers to update query strings.
By isolating data access inside dedicated Repository classes, controllers and UI components become pure consumers of clean domain objects.

## 3. The 300-Line Rule & Modular Architecture
When a single code file grows beyond 300 lines, it almost inevitably mixes multiple architectural concerns (e.g., combining data fetching, input validation, business math, and UI formatting in one place). Enforcing a hard 300-line ceiling forces engineers to decompose code into focused, single-purpose modules (`orderRepo.ts`, `orderService.ts`, `orderValidator.ts`). This prevents spaghetti coupling and makes large codebases maintainable across teams.
