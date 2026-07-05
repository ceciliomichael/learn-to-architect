# Challenge 02 Solution: Named Exports vs. Default Exports and Renaming

This document provides the verified, production-grade reference solution for Challenge 02. It demonstrates how to implement named and default exports across enterprise modules, apply on-the-fly import renaming, and evaluate the deep architectural trade-offs between export styles.

---

## Section 1: The Exporter Module (`src/finance/taxCalculator.ts`)

This module exports two domain tax calculation functions and a regional constant using **Named Exports**, while exposing an enterprise auditing class as the **Default Export** to satisfy legacy regulatory framework requirements.

```typescript
// ============================================================================
// FILE: src/finance/taxCalculator.ts
// ============================================================================

/**
 * Named Export: Constant representing the default tax jurisdiction.
 */
export const DEFAULT_TAX_REGION: string = "NORTH_AMERICA";

/**
 * Named Export: Computes Value Added Tax (VAT) for a given monetary transaction.
 *
 * @param amount The base monetary amount before tax.
 * @param taxRate The decimal percentage rate (for example, 0.15 for 15% VAT).
 * @returns The calculated tax amount rounded to two decimal places.
 * @throws Error if the amount or tax rate is negative.
 */
export function calculateValueAddedTax(amount: number, taxRate: number): number {
  if (amount < 0 || taxRate < 0) {
    throw new Error("Tax calculations cannot accept negative monetary amounts or rates.");
  }
  
  const rawTax = amount * taxRate;
  return Math.round((rawTax + Number.EPSILON) * 100) / 100;
}

/**
 * Named Export: Computes progressive income tax deduction based on salary and bracket rate.
 *
 * @param annualSalary The employee's gross annual salary.
 * @param taxBracketRate The applicable tax bracket decimal rate (for example, 0.28).
 * @returns The total calculated annual tax deduction.
 * @throws Error if annual salary is less than zero.
 */
export function calculateIncomeTax(annualSalary: number, taxBracketRate: number): number {
  if (annualSalary < 0) {
    throw new Error("Annual salary cannot be negative.");
  }
  
  const rawDeduction = annualSalary * taxBracketRate;
  return Math.round((rawDeduction + Number.EPSILON) * 100) / 100;
}

/**
 * Interface defining the structured result of an enterprise financial audit.
 */
export interface AuditReport {
  auditedCount: number;
  totalVolume: number;
  isCompliant: boolean;
}

/**
 * Default Export: Enterprise auditing engine responsible for verifying transaction
 * volumes and compliance rules across financial ledgers.
 */
export default class TaxAuditEngine {
  private readonly complianceThreshold: number;

  constructor(complianceThreshold: number = 1000000) {
    this.complianceThreshold = complianceThreshold;
  }

  /**
   * Performs an automated audit across an array of transaction records.
   *
   * @param transactionAmounts Array of numerical transaction values.
   * @returns A structured audit report detailing compliance status.
   */
  public performAudit(transactionAmounts: number[]): AuditReport {
    if (!Array.isArray(transactionAmounts) || transactionAmounts.length === 0) {
      return {
        auditedCount: 0,
        totalVolume: 0,
        isCompliant: true
      };
    }

    const totalVolume = transactionAmounts.reduce((accumulator, current) => accumulator + current, 0);
    const roundedVolume = Math.round((totalVolume + Number.EPSILON) * 100) / 100;

    // Compliance rule: Total volume must not exceed established regulatory threshold
    const isCompliant = roundedVolume <= this.complianceThreshold;

    return {
      auditedCount: transactionAmounts.length,
      totalVolume: roundedVolume,
      isCompliant: isCompliant
    };
  }
}
```

---

## Section 2: The Consumer Module (`src/app/financialReportGenerator.ts`)

This consumer module imports our tax utilities. Notice how we use the `as` keyword to rename `calculateValueAddedTax` to `computeVat` on the fly, and how we import the default export without curly braces under our chosen domain name `EnterpriseAuditEngine`.

```typescript
// ============================================================================
// FILE: src/app/financialReportGenerator.ts
// ============================================================================

// 1. Importing Named Exports with on-the-fly renaming using 'as':
import {
  calculateValueAddedTax as computeVat,
  calculateIncomeTax,
  DEFAULT_TAX_REGION
} from "../finance/taxCalculator";

// 2. Importing Default Export under a custom domain-specific class name:
import EnterpriseAuditEngine from "../finance/taxCalculator";

/**
 * Generates an annual executive financial report by computing tax deductions,
 * calculating VAT across corporate purchases, and auditing ledger compliance.
 *
 * @param employeeSalary The executive gross annual salary.
 * @param purchaseTransactions Array of corporate purchase amounts requiring VAT calculation.
 */
export function generateAnnualReport(employeeSalary: number, purchaseTransactions: number[]): void {
  console.log("==================================================================");
  console.log(`STARTING FINANCIAL REPORT GENERATION [REGION: ${DEFAULT_TAX_REGION}]`);
  console.log("==================================================================");

  try {
    // 1. Calculate employee income tax deduction (assuming 28% bracket rate)
    const incomeTaxDeduction = calculateIncomeTax(employeeSalary, 0.28);
    const netSalary = employeeSalary - incomeTaxDeduction;
    
    console.log(`Gross Executive Salary : $${employeeSalary.toLocaleString()}`);
    console.log(`Income Tax Deduction   : $${incomeTaxDeduction.toLocaleString()} (28% rate)`);
    console.log(`Net Executive Salary   : $${netSalary.toLocaleString()}`);
    console.log("------------------------------------------------------------------");

    // 2. Compute total VAT across all purchase transactions using renamed import 'computeVat'
    let totalVatAccrued = 0;
    const vatRate = 0.15; // 15% VAT rate

    for (let index = 0; index < purchaseTransactions.length; index++) {
      const transactionAmount = purchaseTransactions[index];
      const transactionVat = computeVat(transactionAmount, vatRate);
      totalVatAccrued += transactionVat;
      console.log(`Transaction #${index + 1} ($${transactionAmount.toLocaleString()}): VAT Accrued = $${transactionVat.toLocaleString()}`);
    }

    console.log(`Total VAT Accrued      : $${totalVatAccrued.toLocaleString()}`);
    console.log("------------------------------------------------------------------");

    // 3. Perform ledger compliance audit using imported Default Export class
    const auditEngine = new EnterpriseAuditEngine(500000); // Set $500,000 threshold
    const auditReport = auditEngine.performAudit(purchaseTransactions);

    console.log("AUDIT ENGINE COMPLIANCE SUMMARY:");
    console.log(`Total Records Audited  : ${auditReport.auditedCount}`);
    console.log(`Total Transaction Vol  : $${auditReport.totalVolume.toLocaleString()}`);
    console.log(`Regulatory Compliance  : ${auditReport.isCompliant ? "PASSED (COMPLIANT)" : "FAILED (THRESHOLD EXCEEDED)"}`);
    console.log("==================================================================");

  } catch (error: unknown) {
    const errorMessage = error instanceof Error ? error.message : "Unknown error occurred.";
    console.error(`[FATAL REPORT ERROR]: Failed to generate financial report: ${errorMessage}`);
  }
}

// Execute sample report generation for verification
generateAnnualReport(180000, [45000, 120000, 85000, 30000]);
```

---

## Section 3: Architectural Trade-Off Analysis

### Why Enterprise Engineering Teams Prefer Named Exports
In modern software architecture, **Named Exports are universally favored over Default Exports by senior engineering teams and tech giants (such as Google, Microsoft, and Airbnb)**. The reasons root in maintainability, predictability, and governance:
* **Enforced Uniform Naming**: When a file exports `export const calculateIncomeTax`, every consuming file across a 10,000-file codebase must import it using the exact name `calculateIncomeTax`. This establishes an immutable vocabulary across the engineering organization.
* **Explicit Contracts**: Named exports clearly advertise what a module provides. A developer inspecting an import block immediately understands the exact tools being extracted from the dependency.
* **No Cognitive Load**: With default exports, developers must invent a variable name upon every import. In large teams, this leads to unnecessary friction during code reviews and inconsistency across files.

### Impact on IDE Autocompletion, Automated Refactoring, and Symbol Searching
* **IDE Autocompletion and Auto-Importing**: When typing a function name in VS Code or JetBrains IDEs, the language server (tsserver) can instantly suggest auto-imports for **Named Exports** because the symbol name is statically bound to the module export table. With Default Exports, autocompletion is unreliable because the symbol has no canonical external name until the developer manually types an import statement!
* **Automated Workspace Refactoring**: Imagine renaming a core utility function from `calculateIncomeTax` to `computeProgressiveIncomeTax` across an enterprise monorepo containing 5,000 files. With **Named Exports**, an IDE refactoring tool performs an Abstract Syntax Tree (AST) traversal, accurately locating and updating every import and call site in milliseconds with 100% precision. With **Default Exports**, automated renaming fails or introduces bugs because the IDE cannot reliably determine whether `import MyTaxTool from './tax'` is referencing the class you wish to rename!
* **Global Symbol Searching**: When investigating bug reports, engineers frequently perform project-wide symbol searches (using `grep`, `ripgrep`, or IDE search) to find every place a domain class is instantiated. If a class is exported as a Named Export (`export class TaxAuditEngine`), searching for `"TaxAuditEngine"` yields 100% of its usages across the codebase.

### Architectural Risks of Random Naming with Default Exports
The primary architectural failure mode of Default Exports occurs in collaborative monorepos: **Symbol Fragmentation**. 

Because Default Exports allow importing files to assign any arbitrary identifier to the imported symbol without compiler warnings, different teams inevitably adopt divergent naming conventions:
```typescript
// File A (Accounting Service):
import TaxCalc from '../finance/taxCalculator';

// File B (Auditing Service):
import AuditEngine from '../finance/taxCalculator';

// File C (Legacy Billing Controller):
import DefaultTaxTool from '../finance/taxCalculator';
```
In this scenario, three different engineering teams are using the exact same underlying class (`TaxAuditEngine`), yet they refer to it by three completely different names! 
* When a junior developer joins the team and reads File C, they assume `DefaultTaxTool` is a billing-specific utility rather than the global auditing engine.
* If a critical security vulnerability is discovered in `TaxAuditEngine`, security analysts searching the codebase for usages will miss File A, File B, and File C entirely if they search by class name!
* In large codebases, this naming fragmentation breeds technical debt, duplicate implementations, and severe onboarding friction.
