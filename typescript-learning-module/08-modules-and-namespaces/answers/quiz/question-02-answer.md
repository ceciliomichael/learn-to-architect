# Question 02 Answer: Named vs. Default Exports and Enterprise Refactoring Safety

This document provides the exhaustive, deeply technical reference answer for Question 02, analyzing import syntax, renaming rules, and the engineering justifications for preferring Named Exports over Default Exports in enterprise codebases.

---

### 1. Combined Import Statement
To import multiple named exports alongside a default export from `src/utils/mathUtilities.ts` in a single line of code, place the default import identifier first, followed by a comma and the named imports inside curly braces:

```typescript
// ============================================================================
// FILE: src/main.ts
// ============================================================================
import EnterpriseFinancialEngine, { PI, calculateCircleArea } from "./utils/mathUtilities";
```

---

### 2. Renaming Syntax and Comparison

**Renaming Named Import Syntax**: To rename a named import on the fly, use the `as` keyword inside the curly braces:
```typescript
import { calculateCircleArea as computeArea, PI } from "./utils/mathUtilities";
```

**How Renaming Default Imports Differs**: When importing a Default Export, there is no need for the `as` keyword because **the importing file has complete authority to assign whatever local variable name it desires upon importation**:
```typescript
// With a default export, you choose the name directly without 'as':
import FinancialCalculator from "./utils/mathUtilities";
```
With a named import, the symbol name is statically bound to the exported module's symbol table; therefore, you must explicitly tell the compiler to map that canonical name to a new local alias (`calculateCircleArea as computeArea`). With a default export, the exported module simply marks the symbol as the "default" slot, leaving the naming responsibility entirely up to the consumer.

---

### 3. Engineering Justifications for Preferring Named Exports
Senior engineering teams and tech giants (such as Google, Microsoft, and Airbnb) universally mandate **Named Exports** over Default Exports in large enterprise monorepos for several critical reasons:
1. **Enforced Canonical Vocabulary across Teams**: When a library exports `export function calculateCircleArea`, every single file across a 10,000-file monorepo must import it using the exact identifier `calculateCircleArea`. This ensures uniform nomenclature across all microservices, making code reviews, onboarding, and documentation predictable.
2. **Explicit Dependency Contracts**: Named imports explicitly advertise exactly what symbols a consumer is extracting from a dependency. A developer inspecting `import { PI, calculateCircleArea } from './utils'` instantly sees what is being utilized, whereas `import MathTool from './utils'` obscures what underlying functionality is being consumed.
3. **Prevention of Naming Collisions and Cognitive Load**: Default exports force developers to invent a name every time they import a module. In large teams, this inevitably leads to inconsistent naming across different files, increasing cognitive load when navigating between services.

---

### 4. Impact of Default Exports on IDE Refactoring and Symbol Searching

**Impairment of Automated IDE Refactoring**: Modern IDEs (such as VS Code and JetBrains WebStorm) rely on Abstract Syntax Tree (AST) analysis to perform automated workspace refactoring, such as renaming a class across thousands of files. 
* With **Named Exports**, the AST clearly maps every import site directly to the exported symbol name. When you right-click `EnterpriseFinancialEngine` and select "Rename Symbol", the language server accurately updates 100% of the import statements across the entire monorepo in milliseconds.
* With **Default Exports**, automated renaming degrades or fails completely! Because every importing file assigns an arbitrary local variable name (`import Calc from './math'`, `import Engine from './math'`, `import Tool from './math'`), the AST language server cannot reliably determine whether `Engine` refers to the class you are trying to rename or a completely unrelated domain object! As a result, automated workspace refactoring breaks, forcing developers to perform manual, error-prone text replacements.

**Impairment of Codebase Symbol Searching**: When investigating bug reports or performing security audits, engineers frequently search the codebase (using tools like `ripgrep` or IDE search) to discover every place a specific class or function is utilized.
* If three different teams import `EnterpriseFinancialEngine` under three different random names (`AccountingCalc`, `AuditTool`, and `TaxEngine`), searching the codebase for `"EnterpriseFinancialEngine"` will yield **zero consumer call sites**! 
* To find where the engine is used, engineers are forced to manually trace import paths across hundreds of files. This searchability breakdown is why default exports are considered an enterprise anti-pattern.
