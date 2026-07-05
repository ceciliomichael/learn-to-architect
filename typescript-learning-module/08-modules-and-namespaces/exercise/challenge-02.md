# Challenge 02: Named Exports vs. Default Exports and Renaming

When exporting tools from an ES Module, TypeScript gives developers two primary styles: **Named Exports** and **Default Exports**. In enterprise engineering teams, choosing the correct export pattern is critical for codebase maintainability, IDE autocompletion, automated refactoring, and searchability.

This challenge tests your ability to architect modular files using both export styles, apply import renaming (`as`), and articulate the deep engineering trade-offs between named and default exports.

## The Scenario

You are architecting an enterprise financial calculation library for a global banking application. Your internal architecture guidelines mandate strict **Named Exports** for all domain calculation functions and tax rate constants to guarantee uniform naming across hundreds of consuming microservices.

However, you must also export an enterprise auditing engine class. To integrate seamlessly with a legacy third-party regulatory framework that strictly expects a **Default Export**, you must export this auditing class as the default export of the module.

## Your Task

Write your complete solution directly inside the **ANSWER HERE** block below. Your solution must include three distinct sections:

1. **Section 1: The Exporter Module (`src/finance/taxCalculator.ts`)**
   - Write a complete TypeScript module that exports:
     - A named export function `calculateValueAddedTax(amount: number, taxRate: number): number` that validates inputs and computes VAT.
     - A named export function `calculateIncomeTax(annualSalary: number, taxBracketRate: number): number` that computes income tax deductions.
     - A named export constant `DEFAULT_TAX_REGION: string = "NORTH_AMERICA"`.
     - A default export class `TaxAuditEngine` with a public method `performAudit(transactionAmounts: number[]): { auditedCount: number; totalVolume: number; isCompliant: boolean }`.

2. **Section 2: The Consumer Module (`src/app/financialReportGenerator.ts`)**
   - Import `calculateValueAddedTax` from `./finance/taxCalculator` and rename it on the fly using the `as` keyword to `computeVat`.
   - Import `calculateIncomeTax` and `DEFAULT_TAX_REGION` using their exact exported names.
   - Import the default export class without curly braces under the custom domain name `EnterpriseAuditEngine`.
   - Write a complete function `generateAnnualReport(salary: number, transactions: number[])` that instantiates `EnterpriseAuditEngine`, executes all imported tax functions, and prints a comprehensive audit summary to the console.

3. **Section 3: Architectural Trade-Off Analysis**
   - Why do modern enterprise engineering teams and style guides universally prefer **Named Exports** over **Default Exports** for large codebases?
   - How do Named Exports impact IDE autocompletion, automated workspace refactoring (such as renaming a symbol across 1,000 files), and global symbol searching?
   - What architectural risks occur when multiple developers import the same Default Export under completely different random names across separate modules in a monorepo?

---

## ANSWER HERE

### Section 1: The Exporter Module (`src/finance/taxCalculator.ts`)

```typescript
// Write your named and default exports here:
```

### Section 2: The Consumer Module (`src/app/financialReportGenerator.ts`)

```typescript
// Write your import renaming and consumer logic here:
```

### Section 3: Architectural Trade-Off Analysis

> **Why enterprise engineering teams prefer Named Exports:**
> 

> **Impact on IDE autocompletion, automated refactoring, and symbol searching:**
> 

> **Architectural risks of random naming with Default Exports:**
> 
