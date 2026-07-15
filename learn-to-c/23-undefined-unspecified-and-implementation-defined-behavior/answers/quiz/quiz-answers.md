# Quiz Answers: Undefined, Unspecified, and Implementation-Defined Behavior

1. **What result does the standard require after undefined behavior?**

   None. The standard imposes no requirements on that execution.

2. **Must an implementation document an unspecified choice?**

   No. It chooses among permitted possibilities without needing to document a fixed choice.

3. **Must implementation-defined behavior be documented?**

   Yes.

4. **Why is one successful test weak evidence for undefined behavior?**

   The observed result is not guaranteed and can change with compiler, optimization, input, or context.

5. **Name two common sources of undefined behavior.**

   Examples include out-of-bounds access, signed overflow, invalid shifts, use after free, and mismatched printf arguments.

