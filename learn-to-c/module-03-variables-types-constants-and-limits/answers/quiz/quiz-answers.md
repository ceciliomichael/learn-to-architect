# Quiz Answers: Variables, Types, Constants, and Limits

1. **Why is size_t appropriate for a count of array elements?**

   It is the unsigned type used by C for object sizes and is large enough to describe any object this implementation can create.

2. **Does const create a compile-time constant in every C context?**

   No. It prevents assignment through that name, but C has separate rules for integer constant expressions.

3. **Why include limits.h?**

   It provides the actual range limits for fundamental integer types on the current implementation.

4. **What is wrong with reading an uninitialized local variable?**

   Its value is indeterminate, and reading it can produce undefined behavior.

5. **Why use PRId32?**

   It supplies the correct printf conversion text for int32_t on the current implementation.

