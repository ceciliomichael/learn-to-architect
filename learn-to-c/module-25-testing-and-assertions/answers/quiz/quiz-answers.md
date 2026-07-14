# Quiz Answers: Testing and Assertions

1. **When is assert appropriate?**

   For an internal invariant or programmer precondition whose failure means the program is defective.

2. **Why not validate user input only with assert?**

   Assertions may be disabled, while invalid external input needs normal runtime handling.

3. **What happens when NDEBUG is defined?**

   assert conditions are not evaluated.

4. **What makes a function easier to test?**

   Explicit inputs, observable results, and separation from unrelated I/O or global state.

5. **Which cases belong beside ordinary tests?**

   Boundary cases and every failure case in the public contract.

