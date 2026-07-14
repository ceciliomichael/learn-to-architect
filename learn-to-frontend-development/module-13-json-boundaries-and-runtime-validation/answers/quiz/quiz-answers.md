# Quiz Answers: JSON Boundaries and Runtime Validation

1. **What does JSON parsing prove?**

   Only valid JSON syntax and resulting JavaScript shapes, not application validity.

2. **Why validate before a type assertion?**

   Runtime data does not become trustworthy because TypeScript is told a type.

3. **Why require safe integer money?**

   The domain uses exact integer minor units within reliable JavaScript integer range.

4. **Should blank trimmed names be accepted?**

   No, when the domain requires a meaningful name; check after normalization.

5. **Where should validation occur?**

   At the boundary before untrusted values enter trusted application behavior.

