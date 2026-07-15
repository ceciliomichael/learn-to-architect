# Quiz Answers: Pointers, Addresses, and Null

1. **What does &value produce?**

   It produces a pointer to the object named value.

2. **What does *pointer mean in an expression?**

   It accesses the object designated by the pointer.

3. **Is every non-null pointer valid to dereference?**

   No. Lifetime, bounds, alignment, type, and access rules must also hold.

4. **Why can a pointer parameter change a caller's object?**

   The copied pointer value still designates the caller-owned object.

5. **Why is a pointer to a returned local variable invalid?**

   The automatic local object's lifetime ends when its function returns.

