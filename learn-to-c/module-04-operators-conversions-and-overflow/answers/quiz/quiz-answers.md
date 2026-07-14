# Quiz Answers: Operators, Conversions, and Overflow

1. **What does 5 / 2 produce when both operands are int?**

   It produces the int value 2 because integer division discards the fractional part.

2. **Why convert before addition?**

   The operation's result type is chosen from its operands, so widening afterward cannot repair overflow that already happened.

3. **Is signed integer overflow guaranteed to wrap?**

   No. In ISO C it has undefined behavior.

4. **What can -Wconversion reveal?**

   It can warn about implicit conversions that may change a value, sign, or precision.

5. **Does a cast prove that a value fits?**

   No. A cast performs a conversion; the programmer must still establish that the source value is valid for the destination.

