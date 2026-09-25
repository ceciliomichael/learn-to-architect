# Exercise Solutions: Module 12

Attempt the work first.

## 1. Trace

Quit carries no extra data, Text carries one String, and Move carries two named i32 fields.

## 2. Repair

Add a branch for the omitted real variant. This keeps each domain state visible instead of hiding it behind _.

## 3. Modify

Add a Paused variant and one explicit match arm. The compiler helps locate other exhaustive matches that also need review.

## 4. Build

Use an enum so impossible simultaneous states cannot be represented. The description function should match each variant and use contained fields only where they exist.

Equivalent designs can be correct when they satisfy the same rules and behavior.
