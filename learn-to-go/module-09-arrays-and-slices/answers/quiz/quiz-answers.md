# Quiz Answers: Arrays and Slices

1. Yes. `[3]int` and `[4]int` are different types.
2. A consecutive region of an underlying array.
3. Append may return a slice describing newly allocated storage and a new length.
4. No. It copies only the slice descriptor, so both can refer to the same elements.
5. Yes. Append can allocate its first backing array.
